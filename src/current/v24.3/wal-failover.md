---
title: WAL Failover
summary: XXX
toc: true
docs_area: deploy
---

[TODO](): add this to the 'resilience' nav section from https://github.com/cockroachdb/docs/pull/18997

[TODO](): UPDATEME with all the things from internal 'WAL failover playbook'

{% include {{ page.version.version }}/wal-failover-intro.md %}

This page has information on:

- How WAL failover works
- How to enable it
- How to test it
- How to monitor it

## Enable WAL failover

To enable WAL failover, you must take one of the following actions:

- Pass [`--wal-failover=among-stores`](#flag-wal-failover) to `cockroach start`, or
- Set the environment variable `COCKROACH_WAL_FAILOVER=among-stores` before starting the node.

[Writing log files to local disk]({% link {{ page.version.version }}/configure-logs.md %}#output-to-files) using the default configuration can lead to cluster instability in the event of a [disk stall]({% link {{ page.version.version }}/cluster-setup-troubleshooting.md %}#disk-stalls). It's not enough to failover your WAL writes to another disk: you must also write your log files in such a way that the forward progress of your cluster is not stalled due to disk unavailability.

Therefore, if you enable WAL failover and log to local disks, you must also update your [logging]({% link {{page.version.version}}/logging-overview.md %}) configuration as follows:

1. Disable [audit logging]({% link {{ page.version.version }}/sql-audit-logging.md %}). File-based audit logging cannot coexist with the WAL failover feature. File-based audit logging provides guarantees that every log message makes it to disk, or CockroachDB must be shut down. For this reason, resuming operations in the face of disk unavailability is not compatible with audit logging.
1. Enable asynchronous buffering of [`file-groups` log sinks]({% link {{ page.version.version }}/configure-logs.md %}#output-to-files) using the `buffering` configuration option. The `buffering` configuration can be applied to [`file-defaults`]({% link {{ page.version.version }}/configure-logs.md %}#configure-logging-defaults) or individual `file-groups` as needed. Note that enabling asynchronous buffering of `file-groups` log sinks is in [preview]({% link {{page.version.version}}/cockroachdb-feature-availability.md %}#features-in-preview).
1. Set `max-staleness: 1s` and `flush-trigger-size: 256KiB`.
1. When `buffering` is enabled, `buffered-writes` must be explicitly disabled as shown in the following example. This is necessary because `buffered-writes` does not provide true asynchronous disk access, but rather a small buffer. If the small buffer fills up, it can cause internal routines performing logging operations to hang. This will in turn cause internal routines doing other important work to hang, potentially affecting cluster stability.
1. The recommended logging configuration for using file-based logging with WAL failover is as follows:

      ~~~
      file-defaults:
        buffered-writes: false
        buffering:
          max-staleness: 1s
          flush-trigger-size: 256KiB
          max-buffer-size: 50MiB
      ~~~

As an alternative to logging to local disks, you can configure [remote log sinks]({% link {{page.version.version}}/logging-use-cases.md %}#network-logging) that are not correlated with the availability of your cluster's local disks. However, this will make troubleshooting using [`cockroach debug zip`]({% link {{ page.version.version}}/cockroach-debug-zip.md %}) more difficult, since the output of that command will not include the (remotely stored) log files.

## Disable WAL failover

To disable WAL failover, you must [restart the node]({% link {{ page.version.version }}/node-shutdown.md %}#stop-and-restart-a-node) and either:

- Pass the [`--wal-failover=disabled`](#flag-wal-failover) flag to `cockroach start`, or
- Set the environment variable `COCKROACH_WAL_FAILOVER=disabled` before restarting the node.

## Monitor WAL failover

You can monitor if WAL failover occurs using the following metrics:

- `storage.wal.failover.secondary.duration`: Cumulative time spent (in nanoseconds) writing to the secondary WAL directory. Only populated when WAL failover is configured.
- `storage.wal.failover.primary.duration`: Cumulative time spent (in nanoseconds) writing to the primary WAL directory. Only populated when WAL failover is configured.
- `storage.wal.failover.switch.count`: Count of the number of times WAL writing has switched from primary to secondary store, and vice versa.

The `storage.wal.failover.secondary.duration` is the primary metric to monitor. You should expect this metric to be `0` unless a WAL failover occurs. If a WAL failover occurs, you probably care about how long it remains non-zero because it provides an indication of the health of the primary store.

You can access these metrics via the following methods:

- The [Custom Chart Debug Page]({% link {{ page.version.version }}/ui-custom-chart-debug-page.md %}) in [DB Console]({% link {{ page.version.version }}/ui-custom-chart-debug-page.md %}).
- By [monitoring CockroachDB with Prometheus]({% link {{ page.version.version }}/monitor-cockroachdb-with-prometheus.md %}).

## See also

+ [Data Resilience]({% link {{ page.version.version }}/data-resilience.md %})
+ [`cockroach start` store flags]({% link {{ page.version.version }}/cockroach-start.md %}#store)
