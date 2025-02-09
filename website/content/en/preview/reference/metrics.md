---
title: "Metrics"
linkTitle: "Metrics"
weight: 7

description: >
  Inspect Karpenter Metrics
---
<!-- this document is generated from hack/docs/metrics_gen_docs.go -->
Karpenter makes several metrics available in Prometheus format to allow monitoring cluster provisioning status. These metrics are available by default at `karpenter.karpenter.svc.cluster.local:8000/metrics` configurable via the `METRICS_PORT` environment variable documented [here](../settings)
### `karpenter_build_info`
A metric with a constant '1' value labeled by version from which karpenter was built.

## Nodepool Metrics

### `karpenter_nodepool_usage`
The nodepool usage is the amount of resources that have been provisioned by a particular nodepool. Labeled by nodepool name and resource type.

### `karpenter_nodepool_limit`
The nodepool limits are the limits specified on the nodepool that restrict the quantity of resources provisioned. Labeled by nodepool name and resource type.

## Nodeclaims Metrics

### `karpenter_nodeclaims_termination_duration_seconds`
Duration of NodeClaim termination in seconds.

### `karpenter_nodeclaims_terminated_total`
Number of nodeclaims terminated in total by Karpenter. Labeled by reason the nodeclaim was terminated and the owning nodepool.

### `karpenter_nodeclaims_registered_total`
Number of nodeclaims registered in total by Karpenter. Labeled by the owning nodepool.

### `karpenter_nodeclaims_launched_total`
Number of nodeclaims launched in total by Karpenter. Labeled by the owning nodepool.

### `karpenter_nodeclaims_instance_termination_duration_seconds`
Duration of CloudProvider Instance termination in seconds.

### `karpenter_nodeclaims_initialized_total`
Number of nodeclaims initialized in total by Karpenter. Labeled by the owning nodepool.

### `karpenter_nodeclaims_drifted_total`
Number of nodeclaims drifted reasons in total by Karpenter. Labeled by drift type of the nodeclaim and the owning nodepool.

### `karpenter_nodeclaims_disrupted_total`
Number of nodeclaims disrupted in total by Karpenter. Labeled by disruption type of the nodeclaim and the owning nodepool.

### `karpenter_nodeclaims_created_total`
Number of nodeclaims created in total by Karpenter. Labeled by reason the nodeclaim was created and the owning nodepool.

## Nodes Metrics

### `karpenter_nodes_total_pod_requests`
Node total pod requests are the resources requested by non-DaemonSet pods bound to nodes.

### `karpenter_nodes_total_pod_limits`
Node total pod limits are the resources specified by non-DaemonSet pod limits.

### `karpenter_nodes_total_daemon_requests`
Node total daemon requests are the resource requested by DaemonSet pods bound to nodes.

### `karpenter_nodes_total_daemon_limits`
Node total daemon limits are the resources specified by DaemonSet pod limits.

### `karpenter_nodes_termination_time_seconds`
The time taken between a node's deletion request and the removal of its finalizer

### `karpenter_nodes_terminated_total`
Number of nodes terminated in total by Karpenter. Labeled by owning nodepool.

### `karpenter_nodes_system_overhead`
Node system daemon overhead are the resources reserved for system overhead, the difference between the node's capacity and allocatable values are reported by the status.

### `karpenter_nodes_leases_deleted_total`
Number of deleted leaked leases.

### `karpenter_nodes_eviction_queue_depth`
The number of pods currently waiting for a successful eviction in the eviction queue.

### `karpenter_nodes_created_total`
Number of nodes created in total by Karpenter. Labeled by owning nodepool.

### `karpenter_nodes_allocatable`
Node allocatable are the resources allocatable by nodes.

## Pods Metrics

### `karpenter_pods_state`
Pod state is the current state of pods. This metric can be used several ways as it is labeled by the pod name, namespace, owner, node, nodepool name, zone, architecture, capacity type, instance type and pod phase.

### `karpenter_pods_startup_time_seconds`
The time from pod creation until the pod is running.

## Provisioner Metrics

### `karpenter_provisioner_scheduling_simulation_duration_seconds`
Duration of scheduling simulations used for deprovisioning and provisioning in seconds.

### `karpenter_provisioner_scheduling_queue_depth`
The number of pods currently waiting to be scheduled.

### `karpenter_provisioner_scheduling_duration_seconds`
Duration of scheduling process in seconds.

## Interruption Metrics

### `karpenter_interruption_received_messages_total`
Count of messages received from the SQS queue. Broken down by message type and whether the message was actionable.

### `karpenter_interruption_message_queue_duration_seconds`
Length of time between message creation in queue and an action taken on the message by the controller.

### `karpenter_interruption_deleted_messages_total`
Count of messages deleted from the SQS queue.

## Disruption Metrics

### `karpenter_disruption_replacement_nodeclaim_initialized_seconds`
Amount of time required for a replacement nodeclaim to become initialized.

### `karpenter_disruption_queue_failures_total`
The number of times that Karpenter failed to launch a replacement node for disruption. Labeled by disruption method.

### `karpenter_disruption_queue_depth`
The number of commands currently being waited on in the disruption orchestration queue.

### `karpenter_disruption_pods_disrupted_total`
Total number of reschedulable pods disrupted on nodes. Labeled by NodePool, disruption action, method, and consolidation type.

### `karpenter_disruption_evaluation_duration_seconds`
Duration of the disruption evaluation process in seconds. Labeled by method and consolidation type.

### `karpenter_disruption_eligible_nodes`
Number of nodes eligible for disruption by Karpenter. Labeled by disruption method and consolidation type.

### `karpenter_disruption_consolidation_timeouts_total`
Number of times the Consolidation algorithm has reached a timeout. Labeled by consolidation type.

### `karpenter_nodepools_allowed_disruptions`
The number of nodes for a given NodePool that can be disrupted at a point in time. Labeled by NodePool. Note that allowed disruptions can change very rapidly, as new nodes may be created and others may be deleted at any point.

### `karpenter_disruption_decisions_total`
Number of disruption actions performed. Labeled by disruption action, method, and consolidation type.

## Consistency Metrics

### `karpenter_consistency_errors_total`
Number of consistency checks that have failed.

## Cluster State Metrics

### `karpenter_cluster_state_synced`
Returns 1 if cluster state is synced and 0 otherwise. Synced checks that nodeclaims and nodes that are stored in the APIServer have the same representation as Karpenter's cluster state

### `karpenter_cluster_state_node_count`
Current count of nodes in cluster state

## Cloudprovider Metrics

### `karpenter_cloudprovider_instance_type_offering_price_estimate`
Instance type offering estimated hourly price used when making informed decisions on node cost calculation, based on instance type, capacity type, and zone.

### `karpenter_cloudprovider_instance_type_offering_available`
Instance type offering availability, based on instance type, capacity type, and zone

### `karpenter_cloudprovider_instance_type_memory_bytes`
Memory, in bytes, for a given instance type.

### `karpenter_cloudprovider_instance_type_cpu_cores`
VCPUs cores for a given instance type.

### `karpenter_cloudprovider_errors_total`
Total number of errors returned from CloudProvider calls.

### `karpenter_cloudprovider_duration_seconds`
Duration of cloud provider method calls. Labeled by the controller, method name and provider.

## Cloudprovider Batcher Metrics

### `karpenter_cloudprovider_batcher_batch_time_seconds`
Duration of the batching window per batcher

### `karpenter_cloudprovider_batcher_batch_size`
Size of the request batch per batcher

## Controller Runtime Metrics

### `controller_runtime_terminal_reconcile_errors_total`
Total number of terminal reconciliation errors per controller

### `controller_runtime_reconcile_total`
Total number of reconciliations per controller

### `controller_runtime_reconcile_time_seconds`
Length of time per reconciliation per controller

### `controller_runtime_reconcile_errors_total`
Total number of reconciliation errors per controller

### `controller_runtime_max_concurrent_reconciles`
Maximum number of concurrent reconciles per controller

### `controller_runtime_active_workers`
Number of currently used workers per controller

## Workqueue Metrics

### `workqueue_work_duration_seconds`
How long in seconds processing an item from workqueue takes.

### `workqueue_unfinished_work_seconds`
How many seconds of work has been done that is in progress and hasn't been observed by work_duration. Large values indicate stuck threads. One can deduce the number of stuck threads by observing the rate at which this increases.

### `workqueue_retries_total`
Total number of retries handled by workqueue

### `workqueue_queue_duration_seconds`
How long in seconds an item stays in workqueue before being requested

### `workqueue_longest_running_processor_seconds`
How many seconds has the longest running processor for workqueue been running.

### `workqueue_depth`
Current depth of workqueue

### `workqueue_adds_total`
Total number of adds handled by workqueue

## Status Condition Metrics

### `operator_status_condition_transition_seconds`
The amount of time a condition was in a given state before transitioning. e.g. Alarm := P99(Updated=False) > 5 minutes

### `operator_status_condition_count`
The number of an condition for a given object, type and status. e.g. Alarm := Available=False > 0

## Client Go Metrics

### `client_go_request_total`
Number of HTTP requests, partitioned by status code and method.

### `client_go_request_duration_seconds`
Request latency in seconds. Broken down by verb, group, version, kind, and subresource.

## AWS SDK Go Metrics

### `aws_sdk_go_request_total`
The total number of AWS SDK Go requests

### `aws_sdk_go_request_retry_count`
The total number of AWS SDK Go retry attempts per request

### `aws_sdk_go_request_duration_seconds`
Latency of AWS SDK Go requests

### `aws_sdk_go_request_attempt_total`
The total number of AWS SDK Go request attempts

### `aws_sdk_go_request_attempt_duration_seconds`
Latency of AWS SDK Go request attempts

## Leader Election Metrics

### `leader_election_slowpath_total`
Total number of slow path exercised in renewing leader leases. 'name' is the string used to identify the lease. Please make sure to group by name.

### `leader_election_master_status`
Gauge of if the reporting system is master of the relevant lease, 0 indicates backup, 1 indicates master. 'name' is the string used to identify the lease. Please make sure to group by name.

