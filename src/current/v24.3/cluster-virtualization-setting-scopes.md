---
title: Cluster Setting Scopes with Cluster Virtualization enabled
summary: Learn which cluster settings are scoped to the system virtual cluster and to virtual clusters when Cluster Virtualization is enabled.
toc: true
docs_area: deploy
---

{{site.data.alerts.callout_info}}
{% include feature-phases/preview.md %}

Refer to the [Cluster Virtualization Overview]({% link {{ page.version.version }}/cluster-virtualization-overview.md %}#known-limitations) for further detail.
{{site.data.alerts.end}}

When [cluster virtualization]({% link {{ page.version.version }}/cluster-virtualization-overview.md %}) is enabled, each cluster setting has a scope, which may be a virtual cluster or the system virtual cluster. This page categorizes each public cluster setting by scope. For descriptions and details about each public cluster setting, refer to [Cluster Settings]({% link {{ page.version.version }}/cluster-settings.md %}).

- When a cluster setting is scoped to a virtual cluster, it affects only a virtual cluster and not the system virtual cluster. To configure a cluster setting that is scoped to a virtual cluster, you must have the `admin` role on it, and you must connect to it before configuring the setting. The majority of cluster settings are scoped to a virtual cluster and are visible only when connected to it.
- When a cluster setting is scoped to the system virtual cluster, it affects the entire CockroachDB cluster. To configure a cluster setting that is scoped to the system virtual cluster, you must have the `admin` role on the system virtual cluster, and you must connect to the system virtual cluster before configuring the setting. For example, the cluster setting `admission.disk_bandwidth_tokens.elastic.enabled` is scoped to the system virtual cluster.
- When a cluster setting is system-visible, it can be set only from the system virtual cluster but can be queried from any virtual cluster. For example, a virtual cluster can query a system-visible cluster setting's value, such as `storage.max_sync_duration`, to help adapt to the CockroachDB cluster's configuration.

{% comment %}
Src: cockroach gen metrics-list --format=csv against cockroach-v24.3.0-beta.1.darwin-10.9-amd64

Also saved in https://docs.google.com/spreadsheets/d/1HIalzAhwU0CEYzSuG2m1aXSJRpiIyQPJdt8SusHpJ_U/edit?usp=sharing
(shared CRL-internal). Sort by the Class column, then Settings column, and paste into the correct section below.

application: Scoped to a virtual cluster
system-only: Scoped to the system virtual cluster
system-visible: Can be set / modified only from the system virtual cluster, but can be viewed from a VC
{% endcomment %}

## Cluster settings scoped to a virtual cluster

{% comment %}Class=application{% endcomment %}

- `admission.epoch_lifo.enabled`
- `admission.epoch_lifo.epoch_closing_delta_duration`
- `admission.epoch_lifo.epoch_duration`
- `admission.epoch_lifo.queue_delay_threshold_to_switch_to_lifo`
- `admission.sql_kv_response.enabled`
- `admission.sql_sql_response.enabled`
- `bulkio.backup.deprecated_full_backup_with_subdir.enabled`
- `bulkio.backup.file_size`
- `bulkio.backup.read_timeout`
- `bulkio.backup.read_with_priority_after`
- `changefeed.aggregator.flush_jitter`
- `changefeed.backfill.concurrent_scan_requests`
- `changefeed.backfill.scan_request_size`
- `changefeed.batch_reduction_retry.enabled (alias: changefeed.batch_reduction_retry_enabled)`
- `changefeed.default_range_distribution_strategy`
- `changefeed.event_consumer_worker_queue_size`
- `changefeed.event_consumer_workers`
- `changefeed.fast_gzip.enabled`
- `changefeed.frontier_highwater_lag_checkpoint_threshold`
- `changefeed.memory.per_changefeed_limit`
- `changefeed.min_highwater_advance`
- `changefeed.node_throttle_config`
- `changefeed.protect_timestamp.max_age`
- `changefeed.protect_timestamp_interval`
- `changefeed.schema_feed.read_with_priority_after`
- `changefeed.sink_io_workers`
- `cloudstorage.azure.concurrent_upload_buffers`
- `cloudstorage.azure.read.node_burst_limit`
- `cloudstorage.azure.read.node_rate_limit`
- `cloudstorage.azure.write.node_burst_limit`
- `cloudstorage.azure.write.node_rate_limit`
- `cloudstorage.gs.read.node_burst_limit`
- `cloudstorage.gs.read.node_rate_limit`
- `cloudstorage.gs.write.node_burst_limit`
- `cloudstorage.gs.write.node_rate_limit`
- `cloudstorage.http.custom_ca`
- `cloudstorage.http.read.node_burst_limit`
- `cloudstorage.http.read.node_rate_limit`
- `cloudstorage.http.write.node_burst_limit`
- `cloudstorage.http.write.node_rate_limit`
- `cloudstorage.nodelocal.read.node_burst_limit`
- `cloudstorage.nodelocal.read.node_rate_limit`
- `cloudstorage.nodelocal.write.node_burst_limit`
- `cloudstorage.nodelocal.write.node_rate_limit`
- `cloudstorage.nullsink.read.node_burst_limit`
- `cloudstorage.nullsink.read.node_rate_limit`
- `cloudstorage.nullsink.write.node_burst_limit`
- `cloudstorage.nullsink.write.node_rate_limit`
- `cloudstorage.s3.read.node_burst_limit`
- `cloudstorage.s3.read.node_rate_limit`
- `cloudstorage.s3.write.node_burst_limit`
- `cloudstorage.s3.write.node_rate_limit`
- `cloudstorage.timeout`
- `cloudstorage.userfile.read.node_burst_limit`
- `cloudstorage.userfile.read.node_rate_limit`
- `cloudstorage.userfile.write.node_burst_limit`
- `cloudstorage.userfile.write.node_rate_limit`
- `cluster.auto_upgrade.enabled`
- `cluster.preserve_downgrade_option`
- `debug.zip.redact_addresses.enabled`
- `diagnostics.forced_sql_stat_reset.interval`
- `diagnostics.reporting.enabled`
- `diagnostics.reporting.interval`
- `external.graphite.endpoint`
- `external.graphite.interval`
- `feature.backup.enabled`
- `feature.changefeed.enabled`
- `feature.export.enabled`
- `feature.import.enabled`
- `feature.restore.enabled`
- `feature.schema_change.enabled`
- `feature.stats.enabled`
- `jobs.retention_time`
- `kv.dist_sender.circuit_breaker.cancellation.enabled`
- `kv.dist_sender.circuit_breaker.cancellation.write_grace_period`
- `kv.dist_sender.circuit_breaker.probe.interval`
- `kv.dist_sender.circuit_breaker.probe.threshold`
- `kv.dist_sender.circuit_breaker.probe.timeout`
- `kv.dist_sender.circuit_breakers.mode`
- `kv.rangefeed.client.stream_startup_rate`
- `kv.transaction.max_intents_bytes`
- `kv.transaction.max_refresh_spans_bytes`
- `kv.transaction.randomized_anchor_key.enabled`
- `kv.transaction.reject_over_max_intents_budget.enabled`
- `kv.transaction.write_pipelining.locking_reads.enabled`
- `kv.transaction.write_pipelining.ranged_writes.enabled`
- `kv.transaction.write_pipelining.enabled (alias: kv.transaction.write_pipelining_enabled)`
- `kv.transaction.write_pipelining.max_batch_size (alias: kv.transaction.write_pipelining_max_batch_size)`
- `obs.tablemetadata.automatic_updates.enabled`
- `obs.tablemetadata.data_valid_duration`
- `schedules.backup.gc_protection.enabled`
- `security.ocsp.mode`
- `security.ocsp.timeout`
- `server.auth_log.sql_connections.enabled`
- `server.auth_log.sql_sessions.enabled`
- `server.authentication_cache.enabled`
- `server.child_metrics.enabled`
- `server.client_cert_expiration_cache.capacity`
- `server.clock.forward_jump_check.enabled (alias: server.clock.forward_jump_check_enabled)`
- `server.clock.persist_upper_bound_interval`
- `server.eventlog.enabled`
- `server.eventlog.ttl`
- `server.host_based_authentication.configuration`
- `server.hot_ranges_request.node.timeout`
- `server.hsts.enabled`
- `server.http.base_path`
- `server.identity_map.configuration`
- `server.jwt_authentication.audience`
- `server.jwt_authentication.claim`
- `server.jwt_authentication.client.timeout`
- `server.jwt_authentication.enabled`
- `server.jwt_authentication.issuers.configuration (alias: server.jwt_authentication.issuers)`
- `server.jwt_authentication.issuers.custom_ca`
- `server.jwt_authentication.jwks`
- `server.jwt_authentication.jwks_auto_fetch.enabled`
- `server.ldap_authentication.client.tls_certificate`
- `server.ldap_authentication.client.tls_key`
- `server.ldap_authentication.domain.custom_ca`
- `server.log_gc.max_deletions_per_cycle`
- `server.log_gc.period`
- `server.max_connections_per_gateway`
- `server.max_open_transactions_per_gateway`
- `server.oidc_authentication.autologin.enabled (alias: server.oidc_authentication.autologin)`
- `server.oidc_authentication.button_text`
- `server.oidc_authentication.claim_json_key`
- `server.oidc_authentication.client.timeout`
- `server.oidc_authentication.client_id`
- `server.oidc_authentication.client_secret`
- `server.oidc_authentication.enabled`
- `server.oidc_authentication.principal_regex`
- `server.oidc_authentication.provider_url`
- `server.oidc_authentication.redirect_url`
- `server.oidc_authentication.scopes`
- `server.redact_sensitive_settings.enabled`
- `server.shutdown.connections.timeout (alias: server.shutdown.connection_wait)`
- `server.shutdown.initial_wait (alias: server.shutdown.drain_wait)`
- `server.shutdown.transactions.timeout (alias: server.shutdown.query_wait)`
- `server.sql_tcp_keep_alive.count`
- `server.sql_tcp_keep_alive.interval`
- `server.time_until_store_dead`
- `server.user_login.cert_password_method.auto_scram_promotion.enabled`
- `server.user_login.downgrade_scram_stored_passwords_to_bcrypt.enabled`
- `server.user_login.min_password_length`
- `server.user_login.password_encryption`
- `server.user_login.password_hashes.default_cost.crdb_bcrypt`
- `server.user_login.password_hashes.default_cost.scram_sha_256`
- `server.user_login.rehash_scram_stored_passwords_on_cost_change.enabled`
- `server.user_login.timeout`
- `server.user_login.upgrade_bcrypt_stored_passwords_to_scram.enabled`
- `server.web_session.purge.ttl`
- `server.web_session.timeout (alias: server.web_session_timeout)`
- `sql.auth.change_own_password.enabled`
- `sql.auth.grant_option_for_owner.enabled`
- `sql.auth.grant_option_inheritance.enabled`
- `sql.auth.public_schema_create_privilege.enabled`
- `sql.auth.resolve_membership_single_scan.enabled`
- `sql.closed_session_cache.capacity`
- `sql.closed_session_cache.time_to_live`
- `sql.contention.event_store.capacity`
- `sql.contention.event_store.duration_threshold`
- `sql.contention.record_serialization_conflicts.enabled`
- `sql.contention.txn_id_cache.max_size`
- `sql.cross_db_fks.enabled`
- `sql.cross_db_sequence_owners.enabled`
- `sql.cross_db_sequence_references.enabled`
- `sql.cross_db_views.enabled`
- `sql.defaults.cost_scans_with_default_col_size.enabled`
- `sql.defaults.datestyle`
- `sql.defaults.default_hash_sharded_index_bucket_count`
- `sql.defaults.default_int_size`
- `sql.defaults.disallow_full_table_scans.enabled`
- `sql.defaults.distsql`
- `sql.defaults.experimental_alter_column_type.enabled`
- `sql.defaults.experimental_distsql_planning`
- `sql.defaults.experimental_enable_unique_without_index_constraints.enabled`
- `sql.defaults.experimental_implicit_column_partitioning.enabled`
- `sql.defaults.experimental_temporary_tables.enabled`
- `sql.defaults.foreign_key_cascades_limit`
- `sql.defaults.idle_in_session_timeout`
- `sql.defaults.idle_in_transaction_session_timeout`
- `sql.defaults.implicit_select_for_update.enabled`
- `sql.defaults.insert_fast_path.enabled`
- `sql.defaults.intervalstyle`
- `sql.defaults.large_full_scan_rows`
- `sql.defaults.locality_optimized_partitioned_index_scan.enabled`
- `sql.defaults.lock_timeout`
- `sql.defaults.on_update_rehome_row.enabled`
- `sql.defaults.optimizer_use_histograms.enabled`
- `sql.defaults.optimizer_use_multicol_stats.enabled`
- `sql.defaults.override_alter_primary_region_in_super_region.enabled`
- `sql.defaults.override_multi_region_zone_config.enabled`
- `sql.defaults.prefer_lookup_joins_for_fks.enabled`
- `sql.defaults.primary_region`
- `sql.defaults.reorder_joins_limit`
- `sql.defaults.require_explicit_primary_keys.enabled`
- `sql.defaults.results_buffer.size`
- `sql.defaults.serial_normalization`
- `sql.defaults.statement_timeout`
- `sql.defaults.stub_catalog_tables.enabled`
- `sql.defaults.super_regions.enabled`
- `sql.defaults.transaction_rows_read_err`
- `sql.defaults.transaction_rows_read_log`
- `sql.defaults.transaction_rows_written_err`
- `sql.defaults.transaction_rows_written_log`
- `sql.defaults.use_declarative_schema_changer`
- `sql.defaults.vectorize`
- `sql.defaults.zigzag_join.enabled`
- `sql.distsql.temp_storage.workmem`
- `sql.guardrails.max_row_size_err`
- `sql.guardrails.max_row_size_log`
- `sql.hash_sharded_range_pre_split.max`
- `sql.index_recommendation.drop_unused_duration`
- `sql.insights.anomaly_detection.enabled`
- `sql.insights.anomaly_detection.latency_threshold`
- `sql.insights.anomaly_detection.memory_limit`
- `sql.insights.execution_insights_capacity`
- `sql.insights.high_retry_count.threshold`
- `sql.insights.latency_threshold`
- `sql.log.slow_query.experimental_full_table_scans.enabled`
- `sql.log.slow_query.internal_queries.enabled`
- `sql.log.slow_query.latency_threshold`
- `sql.log.user_audit`
- `sql.log.user_audit.reduced_config.enabled`
- `sql.metrics.index_usage_stats.enabled`
- `sql.metrics.max_mem_reported_stmt_fingerprints`
- `sql.metrics.max_mem_reported_txn_fingerprints`
- `sql.metrics.max_mem_stmt_fingerprints`
- `sql.metrics.max_mem_txn_fingerprints`
- `sql.metrics.statement_details.dump_to_logs.enabled (alias: sql.metrics.statement_details.dump_to_logs)`
- `sql.metrics.statement_details.enabled`
- `sql.metrics.statement_details.gateway_node.enabled`
- `sql.metrics.statement_details.index_recommendation_collection.enabled`
- `sql.metrics.statement_details.max_mem_reported_idx_recommendations`
- `sql.metrics.statement_details.plan_collection.enabled`
- `sql.metrics.statement_details.plan_collection.period`
- `sql.metrics.statement_details.threshold`
- `sql.metrics.transaction_details.enabled`
- `sql.multiple_modifications_of_table.enabled`
- `sql.multiregion.drop_primary_region.enabled`
- `sql.notices.enabled`
- `sql.optimizer.uniqueness_checks_for_gen_random_uuid.enabled`
- `sql.spatial.experimental_box2d_comparison_operators.enabled`
- `sql.stats.activity.persisted_rows.max`
- `sql.stats.automatic_collection.enabled`
- `sql.stats.automatic_collection.fraction_stale_rows`
- `sql.stats.automatic_collection.min_stale_rows`
- `sql.stats.automatic_partial_collection.enabled`
- `sql.stats.automatic_partial_collection.fraction_stale_rows`
- `sql.stats.automatic_partial_collection.min_stale_rows`
- `sql.stats.cleanup.recurrence`
- `sql.stats.flush.enabled`
- `sql.stats.flush.interval`
- `sql.stats.forecasts.enabled`
- `sql.stats.forecasts.max_decrease`
- `sql.stats.forecasts.min_goodness_of_fit`
- `sql.stats.forecasts.min_observations`
- `sql.stats.histogram_buckets.count`
- `sql.stats.histogram_buckets.include_most_common_values.enabled`
- `sql.stats.histogram_buckets.max_fraction_most_common_values`
- `sql.stats.histogram_collection.enabled`
- `sql.stats.histogram_samples.count`
- `sql.stats.multi_column_collection.enabled`
- `sql.stats.non_default_columns.min_retention_period`
- `sql.stats.persisted_rows.max`
- `sql.stats.post_events.enabled`
- `sql.stats.response.max`
- `sql.stats.response.show_internal.enabled`
- `sql.stats.system_tables.enabled`
- `sql.stats.system_tables_autostats.enabled`
- `sql.stats.virtual_computed_columns.enabled`
- `sql.telemetry.query_sampling.enabled`
- `sql.telemetry.query_sampling.internal.enabled`
- `sql.telemetry.query_sampling.max_event_frequency`
- `sql.telemetry.query_sampling.mode`
- `sql.telemetry.transaction_sampling.max_event_frequency`
- `sql.telemetry.transaction_sampling.statement_events_per_transaction.max`
- `sql.temp_object_cleaner.cleanup_interval`
- `sql.temp_object_cleaner.wait_interval`
- `sql.log.all_statements.enabled (alias: sql.trace.log_statement_execute)`
- `sql.trace.stmt.enable_threshold`
- `sql.trace.txn.enable_threshold`
- `sql.ttl.changefeed_replication.disabled`
- `sql.ttl.default_delete_batch_size`
- `sql.ttl.default_delete_rate_limit`
- `sql.ttl.default_select_batch_size`
- `sql.ttl.default_select_rate_limit`
- `sql.ttl.job.enabled`
- `sql.txn.read_committed_isolation.enabled`
- `sql.txn.repeatable_read_isolation.enabled (alias: sql.txn.snapshot_isolation.enabled)`
- `sql.txn_fingerprint_id_cache.capacity`
- `storage.ingestion.value_blocks.enabled`
- `storage.max_sync_duration.fatal.enabled`
- `trace.debug_http_endpoint.enabled (alias: trace.debug.enable)`
- `trace.opentelemetry.collector`
- `trace.snapshot.rate`
- `trace.span_registry.enabled`
- `trace.zipkin.collector`
- `ui.display_timezone`
- `version`

## Cluster settings scoped to the system virtual cluster

{% comment %}Class=system-only{% endcomment %}

- `admission.disk_bandwidth_tokens.elastic.enabled`
- `admission.kv.enabled`
- `bulkio.stream_ingestion.minimum_flush_interval`
- `physical_replication.consumer.minimum_flush_interval`
- `kv.allocator.lease_rebalance_threshold`
- `kv.allocator.load_based_lease_rebalancing.enabled`
- `kv.allocator.load_based_rebalancing`
- `kv.allocator.load_based_rebalancing.objective`
- `kv.allocator.load_based_rebalancing_interval`
- `kv.allocator.qps_rebalance_threshold`
- `kv.allocator.range_rebalance_threshold`
- `kv.allocator.store_cpu_rebalance_threshold`
- `kv.bulk_io_write.max_rate`
- `kv.bulk_sst.max_allowed_overage`
- `kv.lease_transfer_read_summary.global_budget`
- `kv.lease_transfer_read_summary.local_budget`
- `kv.log_range_and_node_events.enabled`
- `kv.raft.leader_fortification.fraction_enabled`
- `kv.range.range_size_hard_cap`
- `kv.range_split.by_load.enabled (alias: kv.range_split.by_load_enabled)`
- `kv.range_split.load_cpu_threshold`
- `kv.range_split.load_qps_threshold`
- `kv.replica_circuit_breaker.slow_replication_threshold`
- `kv.replica_stats.addsst_request_size_factor`
- `kv.replication_reports.interval`
- `kv.snapshot_rebalance.max_rate`
- `kv.snapshot_receiver.excise.enabled`
- `kvadmission.store.provisioned_bandwidth`
- `kvadmission.store.snapshot_ingest_bandwidth_control.enabled`
- `server.consistency_check.max_rate`
- `server.rangelog.ttl`
- `server.shutdown.lease_transfer_iteration.timeout (alias: server.shutdown.lease_transfer_wait)`
- `spanconfig.bounds.enabled`
- `spanconfig.range_coalescing.system.enabled`
- `spanconfig.range_coalescing.application.enabled`
- `spanconfig.storage_coalesce_adjacent.enabled`
- `spanconfig.tenant_coalesce_adjacent.enabled`
- `storage.experimental.eventually_file_only_snapshots.enabled`
- `storage.ingest_split.enabled`
- `storage.wal_failover.unhealthy_op_threshold`
- `timeseries.storage.enabled`

## System-visible cluster settings

{% comment %}Class=system-visible{% endcomment %}

- `cluster.organization`
- `diagnostics.active_query_dumps.enabled`
- `diagnostics.memory_monitoring_dumps.enabled`
- `enterprise.license`
- `kv.bulk_sst.target_size`
- `kv.closed_timestamp.follower_reads.enabled (alias: kv.closed_timestamp.follower_reads_enabled)`
- `kv.closed_timestamp.lead_for_global_reads_override`
- `kv.closed_timestamp.side_transport_interval`
- `kv.closed_timestamp.target_duration`
- `kv.protectedts.reconciliation.interval`
- `kv.rangefeed.closed_timestamp_refresh_interval`
- `kv.rangefeed.enabled`
- `security.client_cert.subject_required.enabled`
- `sql.schema.telemetry.recurrence`
- `storage.columnar_blocks.enabled`
- `storage.delete_compaction_excise.enabled`
- `storage.max_sync_duration`
- `storage.sstable.compression_algorithm`
- `storage.sstable.compression_algorithm_backup_storage`
- `storage.sstable.compression_algorithm_backup_transport`
- `timeseries.storage.resolution_10s.ttl`
- `timeseries.storage.resolution_30m.ttl`

## See also

- [Cluster Virtualization Overview]({% link {{ page.version.version }}/cluster-virtualization-overview.md %})
- [Cluster Metric Scopes with Cluster Virtualization Enabled]({% link {{ page.version.version }}/cluster-virtualization-setting-scopes.md %})
- [Physical Cluster Replication]({% link {{ page.version.version }}/physical-cluster-replication-overview.md %})
