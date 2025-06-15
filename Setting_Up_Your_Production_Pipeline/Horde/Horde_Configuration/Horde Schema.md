# Horde Schema

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/horde-schema-for-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/horde-schema-for-unreal-engine)  
**Processed:** 2025-06-14 16:28:10

---

## ACL Actions

### Accounts

| Name | Description |
| --- | --- |
| `CreateAccount` | Ability to create new accounts |
| `UpdateAccount` | Update an account settings |
| `DeleteAccount` | Delete an account from the server |
| `ViewAccount` | Ability to view account information |

### Notices

| Name | Description |
| --- | --- |
| `CreateNotice` | Ability to create new notices |
| `UpdateNotice` | Ability to modify notices on the server |
| `DeleteNotice` | Ability to delete notices |

### ServiceAccounts

| Name | Description |
| --- | --- |
| `CreateAccount` | Ability to create new accounts |
| `UpdateAccount` | Update an account settings |
| `DeleteAccount` | Delete an account from the server |
| `ViewAccount` | Ability to view account information |

### Agents

| Name | Description |
| --- | --- |
| `CreateAgent` | Ability to create an agent. This may be done explicitly, or granted to agents to allow them to self-register. |
| `UpdateAgent` | Update an agent's name, pools, etc... |
| `DeleteAgent` | Soft-delete an agent |
| `ViewAgent` | View an agent |
| `ListAgents` | List the available agents |

### Compute

| Name | Description |
| --- | --- |
| `AddComputeTasks` | User can add tasks to the compute cluster |
| `GetComputeTasks` | User can get and list tasks from the compute cluster |

### Leases

| Name | Description |
| --- | --- |
| `ViewLeases` | View all the leases that an agent has worked on |
| `ViewLeaseTasks` | View the task data for a lease |

### Logs

| Name | Description |
| --- | --- |
| `CreateLog` | Ability to create a log. Implicitly granted to agents. |
| `UpdateLog` | Ability to update log metadata |
| `ViewLog` | Ability to view a log contents |
| `WriteLogData` | Ability to write log data |
| `CreateEvent` | Ability to create events |
| `ViewEvent` | Ability to view events |

### Pools

| Name | Description |
| --- | --- |
| `CreatePool` | Create a global pool of agents |
| `UpdatePool` | Modify an agent pool |
| `DeletePool` | Delete an agent pool |
| `ViewPool` | Ability to view a pool |
| `ListPools` | View all the available agent pools |

### Sessions

| Name | Description |
| --- | --- |
| `CreateSession` | Granted to agents to call CreateSession, which returns a bearer token identifying themselves valid to call UpdateSesssion via gRPC. |
| `ViewSession` | Allows viewing information about an agent session |

### Software

| Name | Description |
| --- | --- |
| `UploadSoftware` | Ability to upload new versions of the agent software |
| `DownloadSoftware` | Ability to download the agent software |
| `DeleteSoftware` | Ability to delete agent software |

### Secrets

| Name | Description |
| --- | --- |
| `ViewSecret` | View a credential |

### Artifacts

| Name | Description |
| --- | --- |
| `ReadArtifact` | Permission to read from an artifact |
| `WriteArtifact` | Permission to write to an artifact |
| `DeleteArtifact` | Permission to delete to an artifact |
| `UploadArtifact` | Ability to create an artifact. Typically just for debugging; agents have this access for a particular session. |
| `DownloadArtifact` | Ability to download an artifact |

### Bisect

| Name | Description |
| --- | --- |
| `CreateBisectTask` | Ability to start new bisect tasks |
| `UpdateBisectTask` | Ability to update a bisect task |
| `ViewBisectTask` | Ability to view a bisect task |

### Devices

| Name | Description |
| --- | --- |
| `DeviceRead` | Ability to read devices |
| `DeviceWrite` | Ability to write devices |

### Jobs

| Name | Description |
| --- | --- |
| `CreateJob` | Ability to start new jobs |
| `UpdateJob` | Rename a job, modify its priority, etc... |
| `DeleteJob` | Delete a job properties |
| `ExecuteJob` | Allows updating a job metadata (name, changelist number, step properties, new groups, job states, etc...). Typically granted to agents. Not user facing. |
| `RetryJobStep` | Ability to retry a failed job step |
| `ViewJob` | Ability to view a job |

### Notifications

| Name | Description |
| --- | --- |
| `CreateSubscription` | Ability to subscribe to notifications |

### Projects

| Name | Description |
| --- | --- |
| `CreateProject` | Allows the creation of new projects |
| `DeleteProject` | Allows deletion of projects. |
| `UpdateProject` | Modify attributes of a project (name, categories, etc...) |
| `ViewProject` | View information about a project |

### Replicators

| Name | Description |
| --- | --- |
| `UpdateReplicator` | Allows deletion of projects. |
| `ViewReplicator` | Allows the creation of new projects |

### Streams

| Name | Description |
| --- | --- |
| `CreateStream` | Allows the creation of new streams within a project |
| `UpdateStream` | Allows updating a stream (agent types, templates, schedules) |
| `DeleteStream` | Allows deleting a stream |
| `ViewStream` | Ability to view a stream |
| `ViewChanges` | View changes submitted to a stream. NOTE: this returns responses from the server's Perforce account, which may be a priviledged user. |
| `ViewTemplate` | View template associated with a stream |

### Storage

| Name | Description |
| --- | --- |
| `ReadBlobs` | Ability to read blobs from the storage service |
| `WriteBlobs` | Ability to write blobs to the storage service |
| `ReadRefs` | Ability to read refs from the storage service |
| `WriteRefs` | Ability to write refs to the storage service |
| `DeleteRefs` | Ability to delete refs |

### Symbols

| Name | Description |
| --- | --- |
| `ReadSymbols` | Ability to download symbols |

### Tools

| Name | Description |
| --- | --- |
| `DownloadTool` | Ability to download a tool |
| `UploadTool` | Ability to upload new tool versions |

### Ddc

| Name | Description |
| --- | --- |
| `DdcReadObject` | General read access to refs / blobs and so on |
| `DdcWriteObject` | General write access to upload refs / blobs etc |
| `DdcDeleteObject` | Access to delete blobs / refs etc |
| `DdcDeleteBucket` | Access to delete a particular bucket |
| `DdcDeleteNamespace` | Access to delete a whole namespace |
| `DdcReadTransactionLog` | Access to read the transaction log |
| `DdcWriteTransactionLog` | Access to write the transaction log |
| `DdcAdminAction` | Access to perform administrative task |

## Dashboard

Configuration for dashboard features.

| Name | Description |
| --- | --- |
| `showLandingPage` | `boolean` Navigate to the landing page by default |
| `landingPageRoute` | `string` Custom landing page route to direct users to |
| `showCI` | `boolean` Enable CI functionality |
| `showAgents` | `boolean` Whether to show functionality related to agents, pools, and utilization on the dashboard. |
| `showAgentRegistration` | `boolean` Whether to show the agent registration page. When using registration tokens from elsewhere this is not needed. |
| `showPerforceServers` | `boolean` Show the Perforce server option on the server menu |
| `showDeviceManager` | `boolean` Show the device manager on the server menu |
| `showTests` | `boolean` Show automated tests on the server menu |
| `agentCategories` | [DashboardAgentCategoryConfig](/documentation/en-us/unreal-engine/horde-schema-for-unreal-engine#dashboardagentcategoryconfig)`[]` Configuration for different agent pages |
| `poolCategories` | [DashboardPoolCategoryConfig](/documentation/en-us/unreal-engine/horde-schema-for-unreal-engine#dashboardpoolcategoryconfig)`[]` Configuration for different pool pages |
| `include` | [ConfigInclude](/documentation/en-us/unreal-engine/horde-schema-for-unreal-engine#configinclude)`[]` Includes for other configuration files |
| `macros` | [ConfigMacro](/documentation/en-us/unreal-engine/horde-schema-for-unreal-engine#configmacro)`[]` Macros within this configuration |

### DashboardAgentCategoryConfig

Configuration for a category of agents.

| Name | Description |
| --- | --- |
| `name` | `string` Name of the category |
| `condition` | `string` Condition string to be evaluated for this page |

### DashboardPoolCategoryConfig

Configuration for a category of pools.

| Name | Description |
| --- | --- |
| `name` | `string` Name of the category |
| `condition` | `string` Condition string to be evaluated for this page |

### ConfigInclude

Directive to merge config data from another source.

| Name | Description |
| --- | --- |
| `path` | `string` Path to the config data to be included. May be relative to the including file's location. |

### ConfigMacro

Declares a config macro.

| Name | Description |
| --- | --- |
| `name` | `string` Name of the macro property |
| `value` | `string` Value for the macro property |

## Globals

Global configuration. (Globals.json)

| Name | Description |
| --- | --- |
| `version` | `integer` Version number for the server. Values are indicated by the . |
| `include` | [ConfigInclude](/documentation/en-us/unreal-engine/horde-schema-for-unreal-engine#configinclude)`[]` Other paths to include |
| `macros` | [ConfigMacro](/documentation/en-us/unreal-engine/horde-schema-for-unreal-engine#configmacro)`[]` Macros within the global scope |
| `dashboard` | DashboardConfig Settings for the dashboard |
| `downtime` | [ScheduledDowntime](/documentation/en-us/unreal-engine/horde-schema-for-unreal-engine#scheduleddowntime)`[]` List of scheduled downtime |
| `plugins` | [GlobalPluginsConfig](/documentation/en-us/unreal-engine/horde-schema-for-unreal-engine#globalpluginsconfig) Plugin config objects |
| `parameters` | `object` General parameters for other tools. Can be queried through the api/v1/parameters endpoint. |
| `acl` | [AclConfig](/documentation/en-us/unreal-engine/horde-schema-for-unreal-engine#aclconfig) Access control list |

### ConfigInclude

Directive to merge config data from another source.

| Name | Description |
| --- | --- |
| `path` | `string` Path to the config data to be included. May be relative to the including file's location. |

### ConfigMacro

Declares a config macro

| Name | Description |
| --- | --- |
| `name` | `string` Name of the macro property |
| `value` | `string` Value for the macro property |

### ScheduledDowntime

Settings for the maintenance window

| Name | Description |
| --- | --- |
| `startTime` | `string` Start time |
| `finishTime` | `string` Finish time |
| `frequency` | [ScheduledDowntimeFrequency](/documentation/en-us/unreal-engine/horde-schema-for-unreal-engine#scheduleddowntimefrequency-enum) Frequency that the window repeats |

### ScheduledDowntimeFrequency (Enum)

How frequently the maintence window repeats

| Name | Description |
| --- | --- |
| `Once` | Once |
| `Daily` | Every day |
| `Weekly` | Every week |

### GlobalPluginsConfig

| Name | Description |
| --- | --- |
| `compute` | [ComputeConfig](/documentation/en-us/unreal-engine/horde-schema-for-unreal-engine#computeconfig) Configuration for the compute plugin |
| `secrets` | [SecretsConfig](/documentation/en-us/unreal-engine/horde-schema-for-unreal-engine#secretsconfig) Configuration for the secrets plugin |
| `analytics` | [AnalyticsConfig](/documentation/en-us/unreal-engine/horde-schema-for-unreal-engine#analyticsconfig) Configuration for the analytics plugin |
| `build` | [BuildConfig](/documentation/en-us/unreal-engine/horde-schema-for-unreal-engine#buildconfig) Configuration for the build plugin |
| `storage` | [StorageConfig](/documentation/en-us/unreal-engine/horde-schema-for-unreal-engine#storageconfig) Configuration for the storage plugin |
| `symbols` | [SymbolsConfig](/documentation/en-us/unreal-engine/horde-schema-for-unreal-engine#symbolsconfig) Configuration for the symbols plugin |
| `tools` | [ToolsConfig](/documentation/en-us/unreal-engine/horde-schema-for-unreal-engine#toolsconfig) Configuration for the tools plugin |
| `ddc` | [EmptyPluginConfig](/documentation/en-us/unreal-engine/horde-schema-for-unreal-engine#emptypluginconfig) Configuration for the ddc plugin |

### ComputeConfig

Configuration for the compute system

| Name | Description |
| --- | --- |
| `acl` | [AclConfig](/documentation/en-us/unreal-engine/horde-schema-for-unreal-engine#aclconfig) Inherited root acl |
| `versionEnum` | [ConfigVersion](/documentation/en-us/unreal-engine/horde-schema-for-unreal-engine#configversion-enum) Config version number |
| `rates` | [AgentRateConfig](/documentation/en-us/unreal-engine/horde-schema-for-unreal-engine#agentrateconfig)`[]` List of costs of a particular agent type |
| `clusters` | [ComputeClusterConfig](/documentation/en-us/unreal-engine/horde-schema-for-unreal-engine#computeclusterconfig)`[]` List of compute profiles |
| `pools` | [PoolConfig](/documentation/en-us/unreal-engine/horde-schema-for-unreal-engine#poolconfig)`[]` List of pools |
| `software` | [AgentSoftwareConfig](/documentation/en-us/unreal-engine/horde-schema-for-unreal-engine#agentsoftwareconfig)`[]` List of costs of a particular agent type |
| `networks` | [NetworkConfig](/documentation/en-us/unreal-engine/horde-schema-for-unreal-engine#networkconfig)`[]` List of networks |

### AclConfig

Parameters to update an ACL

| Name | Description |
| --- | --- |
| `entries` | [AclEntryConfig](/documentation/en-us/unreal-engine/horde-schema-for-unreal-engine#aclentryconfig)`[]` Entries to replace the existing ACL |
| `profiles` | [AclProfileConfig](/documentation/en-us/unreal-engine/horde-schema-for-unreal-engine#aclprofileconfig)`[]` Defines profiles which allow grouping sets of actions into named collections |
| `inherit` | `boolean` Whether to inherit permissions from the parent ACL |
| `exceptions` | `string[]` List of exceptions to the inherited setting |

### AclEntryConfig

Individual entry in an ACL

| Name | Description |
| --- | --- |
| `claim` | [AclClaimConfig](/documentation/en-us/unreal-engine/horde-schema-for-unreal-engine#aclclaimconfig) Name of the user or group |
| `actions` | `string[]` Array of actions to allow |
| `profiles` | `string[]` List of profiles to grant |

### AclClaimConfig

New claim to create

| Name | Description |
| --- | --- |
| `type` | `string` The claim type |
| `value` | `string` The claim value |

### AclProfileConfig

Configuration for an ACL profile. This defines a preset group of actions which can be given to a user via an ACL entry.

| Name | Description |
| --- | --- |
| `id` | `string` Identifier for this profile |
| `actions` | `string[]` Actions to include |
| `excludeActions` | `string[]` Actions to exclude from the inherited actions |
| `extends` | `string[]` Other profiles to extend from |

### ConfigVersion (Enum)

Global version number for running the server. As new features are introduced that require data migrations, this version number indicates the backwards compatibility functionality that must be enabled. When adding a new version here, also add a message to ConfigService.CreateSnapshotAsync describing the steps that need to be taken to upgrade the deployment.

| Name | Description |
| --- | --- |
| `None` | Not specified |
| `Initial` | Initial version number |
| `PoolsInConfigFiles` | Ability to add/remove pools via the REST API is removed. Pools should be configured through globals.json instead. |
| `Latest` | Latest version number |
| `LatestPlusOne` | One after the l\`ast defined version number |

### AgentRateConfig

Describes the monetary cost of agents matching a particular criteria

| Name | Description |
| --- | --- |
| `condition` | `string` Condition string |
| `rate` | `number` Rate for this agent |

### ComputeClusterConfig

Profile for executing compute requests

| Name | Description |
| --- | --- |
| `id` | `string` Name of the partition |
| `namespaceId` | `string` Name of the namespace to use |
| `requestBucketId` | `string` Name of the input bucket |
| `responseBucketId` | `string` Name of the output bucket |
| `condition` | `string` Filter for agents to include |
| `acl` | [AclConfig](/documentation/en-us/unreal-engine/horde-schema-for-unreal-engine#aclconfig) Access control list |

### PoolConfig

Mutable configuration for a pool

| Name | Description |
| --- | --- |
| `id` | `string` Unique id for this pool |
| `base` | `string` Base pool config to copy settings from |
| `name` | `string` Name of the pool |
| `condition` | `string` Condition for agents to automatically be included in this pool |
| `properties` | `string` `->` `string` Arbitrary properties related to this pool |
| `color` | [PoolColor](/documentation/en-us/unreal-engine/horde-schema-for-unreal-engine#poolcolor-enum) Color to use for this pool on the dashboard |
| `enableAutoscaling` | `boolean` Whether to enable autoscaling for this pool |
| `minAgents` | `integer` The minimum number of agents to keep in the pool |
| `numReserveAgents` | `integer` The minimum number of idle agents to hold in reserve |
| `conformInterval` | `string` Interval between conforms. If zero, the pool will not conform on a schedule. |
| `scaleOutCooldown` | `string` Cooldown time between scale-out events |
| `scaleInCooldown` | `string` Cooldown time between scale-in events |
| `shutdownIfDisabledGracePeriod` | `string` Time to wait before shutting down an agent that has been disabled |
| `sizeStrategy` | [PoolSizeStrategy](/documentation/en-us/unreal-engine/horde-schema-for-unreal-engine#poolsizestrategy-enum) |
| `sizeStrategies` | [PoolSizeStrategyInfo](/documentation/en-us/unreal-engine/horde-schema-for-unreal-engine#poolsizestrategyinfo)`[]` List of pool sizing strategies for this pool. The first strategy with a matching condition will be picked. |
| `fleetManagers` | [FleetManagerInfo](/documentation/en-us/unreal-engine/horde-schema-for-unreal-engine#fleetmanagerinfo)`[]` List of fleet managers for this pool. The first strategy with a matching condition will be picked. If empty or no conditions match, a default fleet manager will be used. |
| `leaseUtilizationSettings` | [LeaseUtilizationSettings](/documentation/en-us/unreal-engine/horde-schema-for-unreal-engine#leaseutilizationsettings) Settings for lease utilization pool sizing strategy (if used) |
| `jobQueueSettings` | [JobQueueSettings](/documentation/en-us/unreal-engine/horde-schema-for-unreal-engine#jobqueuesettings) Settings for job queue pool sizing strategy (if used) |
| `computeQueueAwsMetricSettings` | [ComputeQueueAwsMetricSettings](/documentation/en-us/unreal-engine/horde-schema-for-unreal-engine#computequeueawsmetricsettings) Settings for job queue pool sizing strategy (if used) |

### PoolColor (Enum)

Color to use for labels of this pool

| Name | Description |
| --- | --- |
| `Default` | Default |
| `Blue` | Blue |
| `Orange` | Orange |
| `Green` | Green |
| `Gray` | Gray |

### PoolSizeStrategy (Enum)

Available pool sizing strategies

| Name | Description |
| --- | --- |
| `LeaseUtilization` | Strategy based on lease utilization |
| `JobQueue` | Strategy based on size of job build queue |
| `NoOp` | No-op strategy used as fallback/default behavior |
| `ComputeQueueAwsMetric` | A no-op strategy that reports metrics to let an external AWS auto-scaling policy scale the fleet |
| `LeaseUtilizationAwsMetric` | A no-op strategy that reports metrics to let an external AWS auto-scaling policy scale the fleet |

### PoolSizeStrategyInfo

Metadata for configuring and picking a pool sizing strategy

| Name | Description |
| --- | --- |
| `type` | [PoolSizeStrategy](/documentation/en-us/unreal-engine/horde-schema-for-unreal-engine#poolsizestrategy-enum) Strategy implementation to use |
| `condition` | `string` Condition if this strategy should be enabled (right now, using date/time as a distinguishing factor) |
| `config` | `object` Configuration for the strategy, serialized as JSON |
| `extraAgentCount` | `integer` Integer to add after pool size has been calculated. Can also be negative. |

### FleetManagerInfo

Metadata for configuring and picking a fleet manager

| Name | Description |
| --- | --- |
| `type` | [FleetManagerType](/documentation/en-us/unreal-engine/horde-schema-for-unreal-engine#fleetmanagertype-enum) Fleet manager type implementation to use |
| `condition` | `string` Condition if this strategy should be enabled (right now, using date/time as a distinguishing factor) |
| `config` | `object` Configuration for the strategy, serialized as JSON |

### FleetManagerType (Enum)

Available fleet managers

| Name | Description |
| --- | --- |
| `Default` | Default fleet manager |
| `NoOp` | No-op fleet manager. |
| `Aws` | Fleet manager for handling AWS EC2 instances. Will create and/or terminate instances from scratch. |
| `AwsReuse` | Fleet manager for handling AWS EC2 instances. Will start already existing but stopped instances to reuse existing EBS disks. |
| `AwsRecycle` | Fleet manager for handling AWS EC2 instances. Will start already existing but stopped instances to reuse existing EBS disks. |
| `AwsAsg` | Fleet manager for handling AWS EC2 instances. Uses an EC2 auto-scaling group for controlling the number of running instances. |

### LeaseUtilizationSettings

Lease utilization sizing settings for a pool

| Name | Description |
| --- | --- |
| `sampleTimeSec` | `integer` Time period for each sample |
| `numSamples` | `integer` Number of samples to collect for calculating lease utilization |
| `numSamplesForResult` | `integer` Min number of samples for a valid result |
| `minAgents` | `integer` The minimum number of agents to keep in the pool |
| `numReserveAgents` | `integer` The minimum number of idle agents to hold in reserve |

### JobQueueSettings

Job queue sizing settings for a pool

| Name | Description |
| --- | --- |
| `scaleOutFactor` | `number` Factor translating queue size to additional agents to grow the pool with The result is always rounded up to nearest integer. Example: if there are 20 jobs in queue, a factor 0.25 will result in 5 new agents being added (20 \* 0.25) |
| `scaleInFactor` | `number` Factor by which to shrink the pool size with when queue is empty The result is always rounded up to nearest integer. Example: when the queue size is zero, a default value of 0.9 will shrink the pool by 10% (current agent count \* 0.9) |
| `samplePeriodMin` | `integer` How far back in time to look for job batches (that potentially are in the queue) |
| `readyTimeThresholdSec` | `integer` Time spent in ready state before considered truly waiting for an agent A job batch can be in ready state before getting picked up and executed. This threshold will help ensure only batches that have been waiting longer than this value will be considered. |

### ComputeQueueAwsMetricSettings

| Name | Description |
| --- | --- |
| `computeClusterId` | `string` Compute cluster ID to observe |
| `namespace` | `string` AWS CloudWatch namespace to write metrics in |

### AgentSoftwareConfig

Selects different agent software versions by evaluating a condition

| Name | Description |
| --- | --- |
| `toolId` | `string` Tool identifier |
| `condition` | `string` Condition for using this channel |

### NetworkConfig

Describes a network The ID describes any logical grouping, such as region, availability zone, rack or office location.

| Name | Description |
| --- | --- |
| `id` | `string` ID for this network |
| `cidrBlock` | `string` CIDR block |
| `description` | `string` Human-readable description |
| `computeId` | `string` Compute ID for this network (used when allocating compute resources) |

### SecretsConfig

Configuration for the secrets system

| Name | Description |
| --- | --- |
| `secrets` | [SecretConfig](/documentation/en-us/unreal-engine/horde-schema-for-unreal-engine#secretconfig)`[]` List of secrets |

### SecretConfig

Configuration for a secret value

| Name | Description |
| --- | --- |
| `id` | `string` Identifier for this secret |
| `data` | `string` `->` `string` Key/value pairs associated with this secret |
| `sources` | [ExternalSecretConfig](/documentation/en-us/unreal-engine/horde-schema-for-unreal-engine#externalsecretconfig)`[]` Providers to source key/value pairs from |
| `acl` | [AclConfig](/documentation/en-us/unreal-engine/horde-schema-for-unreal-engine#aclconfig) Defines access to this particular secret |

### ExternalSecretConfig

Configuration for an external secret provider

| Name | Description |
| --- | --- |
| `provider` | `string` Name of the provider to use |
| `format` | [ExternalSecretFormat](/documentation/en-us/unreal-engine/horde-schema-for-unreal-engine#externalsecretformat-enum) Format of the secret |
| `key` | `string` Optional key indicating the parameter to set in the resulting data array. Required if if is . |
| `path` | `string` Optional value indicating what to fetch from the provider |

### ExternalSecretFormat (Enum)

Format describing how to parse external secret values

| Name | Description |
| --- | --- |
| `Text` | Secret is a plain text value which will be stored using the external secret key |
| `Json` | Secret is a JSON formatted string containing key/value pairs |

### AnalyticsConfig

Config settings for analytics

| Name | Description |
| --- | --- |
| `stores` | TelemetryStoreConfig`[]` Metrics to aggregate on the Horde server |

### BuildConfig

Configuration for the build plugin

| Name | Description |
| --- | --- |
| `perforceClusters` | [PerforceCluster](/documentation/en-us/unreal-engine/horde-schema-for-unreal-engine#perforcecluster)`[]` List of Perforce clusters |
| `devices` | [DeviceConfig](/documentation/en-us/unreal-engine/horde-schema-for-unreal-engine#deviceconfig) Device configuration |
| `maxConformCount` | `integer` Maximum number of conforms to run at once |
| `agentShutdownIfDisabledGracePeriod` | `string` Time to wait before shutting down an agent that has been disabled Used if no value is set on the actual pool. |
| `artifactTypes` | [ArtifactTypeConfig](/documentation/en-us/unreal-engine/horde-schema-for-unreal-engine#artifacttypeconfig)`[]` Configuration for different artifact types |
| `projects` | ProjectConfig`[]` List of projects |
| `enableConformTasks` | `boolean` Whether to allow conform tasks to run |
| `issueFixedTag` | `string` Commit tag to use for marking issues as fixed |

### PerforceCluster

Information about a cluster of Perforce servers.

| Name | Description |
| --- | --- |
| `name` | `string` Name of the cluster |
| `serviceAccount` | `string` Username for Horde to log in to this server. Will use the first account specified below if not overridden. |
| `canImpersonate` | `boolean` Whether the service account can impersonate other users |
| `supportsPartitionedWorkspaces` | `boolean` Whether to use partitioned workspaces on this server |
| `servers` | [PerforceServer](/documentation/en-us/unreal-engine/horde-schema-for-unreal-engine#perforceserver)`[]` List of servers |
| `credentials` | [PerforceCredentials](/documentation/en-us/unreal-engine/horde-schema-for-unreal-engine#perforcecredentials)`[]` List of server credentials |
| `autoSdk` | [AutoSdkWorkspace](/documentation/en-us/unreal-engine/horde-schema-for-unreal-engine#autosdkworkspace)`[]` List of autosdk streams |

### PerforceServer

Information about an individual Perforce server

| Name | Description |
| --- | --- |
| `serverAndPort` | `string` The server and port. The server may be a DNS entry with multiple records, in which case it will be actively load balanced. If "ssl:" prefix is used, ensure P4 server's fingerprint/certificate is trusted. See Horde's documentation on connecting to SSL-enabled Perforce servers. |
| `healthCheck` | `boolean` Whether to query the healthcheck address under each server |
| `resolveDns` | `boolean` Whether to resolve the DNS entries and load balance between different hosts |
| `maxConformCount` | `integer` Maximum number of simultaneous conforms on this server |
| `condition` | `string` Optional condition for a machine to be eligible to use this server |
| `properties` | `string[]` List of properties for an agent to be eligible to use this server |

### PerforceCredentials

Credentials for a Perforce user

| Name | Description |
| --- | --- |
| `userName` | `string` The username |
| `password` | `string` Password for the user |
| `ticket` | `string` Login ticket for the user (will be used instead of password if set) |

### AutoSdkWorkspace

Path to a platform and stream to use for syncing AutoSDK

| Name | Description |
| --- | --- |
| `name` | `string` Name of this workspace |
| `properties` | `string[]` The agent properties to check (eg. "OSFamily=Windows") |
| `userName` | `string` Username for logging in to the server |
| `stream` | `string` Stream to use |

### DeviceConfig

Configuration for devices

| Name | Description |
| --- | --- |
| `platforms` | [DevicePlatformConfig](/documentation/en-us/unreal-engine/horde-schema-for-unreal-engine#deviceplatformconfig)`[]` List of device platforms |
| `pools` | [DevicePoolConfig](/documentation/en-us/unreal-engine/horde-schema-for-unreal-engine#devicepoolconfig)`[]` List of device pools |

### DevicePlatformConfig

Configuration for a device platform

| Name | Description |
| --- | --- |
| `id` | `string` The id for this platform |
| `name` | `string` Name of the platform |
| `models` | `string[]` A list of platform models |
| `legacyNames` | `string[]` Legacy names which older versions of Gauntlet may be using |
| `legacyPerfSpecHighModel` | `string` Model name for the high perf spec, which may be requested by Gauntlet |

### DevicePoolConfig

Configuration for a device pool

| Name | Description |
| --- | --- |
| `id` | `string` The id for this platform |
| `name` | `string` The name of the pool |
| `poolType` | [DevicePoolType](/documentation/en-us/unreal-engine/horde-schema-for-unreal-engine#devicepooltype-enum) The type of the pool |
| `projectIds` | `string[]` List of project ids associated with pool |

### DevicePoolType (Enum)

The type of device pool

| Name | Description |
| --- | --- |
| `Automation` | Available to CIS jobs |
| `Shared` | Shared by users with remote checking and checkouts |

### ArtifactTypeConfig

Configuration for an artifact

| Name | Description |
| --- | --- |
| `name` | `string` Legacy 'Name' property |
| `type` | `string` Name of the artifact type |
| `acl` | [AclConfig](/documentation/en-us/unreal-engine/horde-schema-for-unreal-engine#aclconfig) Acl for the artifact type |
| `keepCount` | `integer` Number of artifacts to retain |
| `keepDays` | `integer` Number of days to retain artifacts of this type |
| `namespaceId` | `string` Storage namespace to use for this artifact types |

### StorageConfig

Configuration for storage

| Name | Description |
| --- | --- |
| `enableGc` | `boolean` Whether to enable garbage collection |
| `enableGcVerification` | `boolean` Whether to enable garbage collection in verification mode (nothing deleted, just logging on access to deleted blobs) |
| `backends` | [BackendConfig](/documentation/en-us/unreal-engine/horde-schema-for-unreal-engine#backendconfig)`[]` List of storage backends |
| `namespaces` | [NamespaceConfig](/documentation/en-us/unreal-engine/horde-schema-for-unreal-engine#namespaceconfig)`[]` List of namespaces for storage |

### BackendConfig

Common settings object for different providers

| Name | Description |
| --- | --- |
| `id` | `string` The storage backend ID |
| `base` | `string` Base backend to copy default settings from |
| `secondary` | `string` Specifies another backend to read from if an object is not found in this one. Can be used when migrating data from one backend to another. |
| `type` | [StorageBackendType](/documentation/en-us/unreal-engine/horde-schema-for-unreal-engine#storagebackendtype-enum) |
| `baseDir` | `string` |
| `awsBucketName` | `string` Name of the bucket to use |
| `awsBucketPath` | `string` Base path within the bucket |
| `awsCredentials` | [AwsCredentialsType](/documentation/en-us/unreal-engine/horde-schema-for-unreal-engine#awscredentialstype-enum) Type of credentials to use |
| `awsRole` | `string` ARN of a role to assume |
| `awsProfile` | `string` The AWS profile to read credentials form |
| `awsRegion` | `string` Region to connect to |
| `azureConnectionString` | `string` Connection string for Azure |
| `azureContainerName` | `string` Name of the container |
| `relayServer` | `string` |
| `relayToken` | `string` |
| `gcsBucketName` | `string` Name of the GCS bucket to use |
| `gcsBucketPath` | `string` Base path within the bucket |

### StorageBackendType (Enum)

Types of storage backend to use

| Name | Description |
| --- | --- |
| `FileSystem` | Local filesystem |
| `Aws` | AWS S3 |
| `Azure` | Azure blob store |
| `Gcs` | Google Cloud Storage |
| `Memory` | In-memory only (for testing) |

### AwsCredentialsType (Enum)

Credentials to use for AWS

| Name | Description |
| --- | --- |
| `Default` | Use default credentials from the AWS SDK |
| `Profile` | Read credentials from the profile in the AWS config file |
| `AssumeRole` | Assume a particular role. Should specify ARN in |
| `AssumeRoleWebIdentity` | Assume a particular role using the current environment variables. |

### NamespaceConfig

Configuration of a particular namespace

| Name | Description |
| --- | --- |
| `id` | `string` Identifier for this namespace |
| `backend` | `string` Backend to use for this namespace |
| `prefix` | `string` Prefix for items within this namespace |
| `gcFrequencyHrs` | `number` How frequently to run garbage collection, in hours. |
| `gcDelayHrs` | `number` How long to keep newly uploaded orphanned objects before allowing them to be deleted, in hours. |
| `enableAliases` | `boolean` Support querying exports by their aliases |
| `acl` | [AclConfig](/documentation/en-us/unreal-engine/horde-schema-for-unreal-engine#aclconfig) Access list for this namespace |

### SymbolsConfig

Configuration for the tools system

| Name | Description |
| --- | --- |
| `stores` | [SymbolStoreConfig](/documentation/en-us/unreal-engine/horde-schema-for-unreal-engine#symbolstoreconfig)`[]` List of symbol stores |

### SymbolStoreConfig

Configuration for a symbol store

| Name | Description |
| --- | --- |
| `id` | `string` Identifier for this store |
| `namespaceId` | `string` Configuration for the symbol store backend |
| `public` | `boolean` Whether to make this store available without auth |
| `acl` | [AclConfig](/documentation/en-us/unreal-engine/horde-schema-for-unreal-engine#aclconfig) Access to the symbol store |

### ToolsConfig

Configuration for the tools system

| Name | Description |
| --- | --- |
| `tools` | [ToolConfig](/documentation/en-us/unreal-engine/horde-schema-for-unreal-engine#toolconfig)`[]` Tool configurations |

### ToolConfig

Options for configuring a tool

| Name | Description |
| --- | --- |
| `id` | `string` Unique identifier for the tool |
| `name` | `string` Name of the tool |
| `description` | `string` Description for the tool |
| `category` | `string` Category for the tool. Will cause the tool to be shown in a different tab in the dashboard. |
| `group` | `string` Grouping key for different variations of the same tool. The dashboard will show these together. |
| `platforms` | `string[]` Platforms for this tool. Takes the form of a NET RID (https://learn.microsoft.com/en-us/dotnet/core/rid-catalog). |
| `public` | `boolean` Whether this tool should be exposed for download on a public endpoint without authentication |
| `showInUgs` | `boolean` Whether to show this tool for download in the UGS tools menu |
| `showInDashboard` | `boolean` Whether to show this tool for download in the dashboard |
| `showInToolbox` | `boolean` Whether to show this tool for download in Unreal Toolbox |
| `metadata` | `string` `->` `string` Metadata for this tool |
| `namespaceId` | `string` Default namespace for new deployments of this tool |
| `acl` | [AclConfig](/documentation/en-us/unreal-engine/horde-schema-for-unreal-engine#aclconfig) Permissions for the tool |

## Project

Stores configuration for a project. (\*.project.json)

| Name | Description |
| --- | --- |
| `id` | `string` The project id |
| `name` | `string` Name for the new project |
| `path` | `string` Direct include path for the project config. For backwards compatibility with old config files when including from a GlobalConfig object. |
| `include` | [ConfigInclude](/documentation/en-us/unreal-engine/horde-schema-for-unreal-engine#configinclude)`[]` Includes for other configuration files |
| `macros` | [ConfigMacro](/documentation/en-us/unreal-engine/horde-schema-for-unreal-engine#configmacro)`[]` Macros within the global scope |
| `order` | `integer` Order of this project on the dashboard |
| `logo` | `string` Path to the project logo |
| `logoDarkTheme` | `string` Optional path to the project logo for the dark theme |
| `pools` | [PoolConfig](/documentation/en-us/unreal-engine/horde-schema-for-unreal-engine#poolconfig)`[]` List of pools for this project |
| `categories` | [ProjectCategoryConfig](/documentation/en-us/unreal-engine/horde-schema-for-unreal-engine#projectcategoryconfig)`[]` Categories to include in this project |
| `jobOptions` | [JobOptions](/documentation/en-us/unreal-engine/horde-schema-for-unreal-engine#joboptions) Default settings for executing jobs |
| `workspaceTypes` | `string` `->` [WorkspaceConfig](/documentation/en-us/unreal-engine/horde-schema-for-unreal-engine#workspaceconfig) Default workspace types for streams These are added to the list of each stream's workspace types. |
| `telemetryStoreId` | `string` Telemetry store for Horde data for this project |
| `streams` | StreamConfig`[]` List of streams |
| `artifactTypes` | [ArtifactTypeConfig](/documentation/en-us/unreal-engine/horde-schema-for-unreal-engine#artifacttypeconfig)`[]` Permissions for artifact types |
| `acl` | [AclConfig](/documentation/en-us/unreal-engine/horde-schema-for-unreal-engine#aclconfig) Acl entries |

### ConfigInclude

Directive to merge config data from another source

| Name | Description |
| --- | --- |
| `path` | `string` Path to the config data to be included. May be relative to the including file's location. |

### ConfigMacro

Declares a config macro

| Name | Description |
| --- | --- |
| `name` | `string` Name of the macro property |
| `value` | `string` Value for the macro property |

### PoolConfig

Mutable configuration for a pool

| Name | Description |
| --- | --- |
| `id` | `string` Unique id for this pool |
| `base` | `string` Base pool config to copy settings from |
| `name` | `string` Name of the pool |
| `condition` | `string` Condition for agents to automatically be included in this pool |
| `properties` | `string` `->` `string` Arbitrary properties related to this pool |
| `color` | [PoolColor](/documentation/en-us/unreal-engine/horde-schema-for-unreal-engine#poolcolor-enum) Color to use for this pool on the dashboard |
| `enableAutoscaling` | `boolean` Whether to enable autoscaling for this pool |
| `minAgents` | `integer` The minimum number of agents to keep in the pool |
| `numReserveAgents` | `integer` The minimum number of idle agents to hold in reserve |
| `conformInterval` | `string` Interval between conforms. If zero, the pool will not conform on a schedule. |
| `scaleOutCooldown` | `string` Cooldown time between scale-out events |
| `scaleInCooldown` | `string` Cooldown time between scale-in events |
| `shutdownIfDisabledGracePeriod` | `string` Time to wait before shutting down an agent that has been disabled |
| `sizeStrategy` | [PoolSizeStrategy](/documentation/en-us/unreal-engine/horde-schema-for-unreal-engine#poolsizestrategy-enum) |
| `sizeStrategies` | [PoolSizeStrategyInfo](/documentation/en-us/unreal-engine/horde-schema-for-unreal-engine#poolsizestrategyinfo)`[]` List of pool sizing strategies for this pool. The first strategy with a matching condition will be picked. |
| `fleetManagers` | [FleetManagerInfo](/documentation/en-us/unreal-engine/horde-schema-for-unreal-engine#fleetmanagerinfo)`[]` List of fleet managers for this pool. The first strategy with a matching condition will be picked. If empty or no conditions match, a default fleet manager will be used. |
| `leaseUtilizationSettings` | [LeaseUtilizationSettings](/documentation/en-us/unreal-engine/horde-schema-for-unreal-engine#leaseutilizationsettings) Settings for lease utilization pool sizing strategy (if used) |
| `jobQueueSettings` | [JobQueueSettings](/documentation/en-us/unreal-engine/horde-schema-for-unreal-engine#jobqueuesettings) Settings for job queue pool sizing strategy (if used) |
| `computeQueueAwsMetricSettings` | [ComputeQueueAwsMetricSettings](/documentation/en-us/unreal-engine/horde-schema-for-unreal-engine#computequeueawsmetricsettings) Settings for job queue pool sizing strategy (if used) |

### PoolColor (Enum)

Color to use for labels of this pool

| Name | Description |
| --- | --- |
| `Default` | Default |
| `Blue` | Blue |
| `Orange` | Orange |
| `Green` | Green |
| `Gray` | Gray |

### PoolSizeStrategy (Enum)

Available pool sizing strategies

| Name | Description |
| --- | --- |
| `LeaseUtilization` | Strategy based on lease utilization |
| `JobQueue` | Strategy based on size of job build queue |
| `NoOp` | No-op strategy used as fallback/default behavior |
| `ComputeQueueAwsMetric` | A no-op strategy that reports metrics to let an external AWS auto-scaling policy scale the fleet |
| `LeaseUtilizationAwsMetric` | A no-op strategy that reports metrics to let an external AWS auto-scaling policy scale the fleet |

### PoolSizeStrategyInfo

Metadata for configuring and picking a pool sizing strategy

| Name | Description |
| --- | --- |
| `type` | [PoolSizeStrategy](/documentation/en-us/unreal-engine/horde-schema-for-unreal-engine#poolsizestrategy-enum) Strategy implementation to use |
| `condition` | `string` Condition if this strategy should be enabled (right now, using date/time as a distinguishing factor) |
| `config` | `object` Configuration for the strategy, serialized as JSON |
| `extraAgentCount` | `integer` Integer to add after pool size has been calculated. Can also be negative. |

### FleetManagerInfo

Metadata for configuring and picking a fleet manager

| Name | Description |
| --- | --- |
| `type` | [FleetManagerType](/documentation/en-us/unreal-engine/horde-schema-for-unreal-engine#fleetmanagertype-enum) Fleet manager type implementation to use |
| `condition` | `string` Condition if this strategy should be enabled (right now, using date/time as a distinguishing factor) |
| `config` | `object` Configuration for the strategy, serialized as JSON |

### FleetManagerType (Enum)

Available fleet managers

| Name | Description |
| --- | --- |
| `Default` | Default fleet manager |
| `NoOp` | No-op fleet manager. |
| `Aws` | Fleet manager for handling AWS EC2 instances. Will create and/or terminate instances from scratch. |
| `AwsReuse` | Fleet manager for handling AWS EC2 instances. Will start already existing but stopped instances to reuse existing EBS disks. |
| `AwsRecycle` | Fleet manager for handling AWS EC2 instances. Will start already existing but stopped instances to reuse existing EBS disks. |
| `AwsAsg` | Fleet manager for handling AWS EC2 instances. Uses an EC2 auto-scaling group for controlling the number of running instances. |

### LeaseUtilizationSettings

Lease utilization sizing settings for a pool

| Name | Description |
| --- | --- |
| `sampleTimeSec` | `integer` Time period for each sample |
| `numSamples` | `integer` Number of samples to collect for calculating lease utilization |
| `numSamplesForResult` | `integer` Min number of samples for a valid result |
| `minAgents` | `integer` The minimum number of agents to keep in the pool |
| `numReserveAgents` | `integer` The minimum number of idle agents to hold in reserve |

### JobQueueSettings

Job queue sizing settings for a pool

| Name | Description |
| --- | --- |
| `scaleOutFactor` | `number` Factor translating queue size to additional agents to grow the pool with The result is always rounded up to nearest integer. Example: if there are 20 jobs in queue, a factor 0.25 will result in 5 new agents being added (20 \* 0.25) |
| `scaleInFactor` | `number` Factor by which to shrink the pool size with when queue is empty The result is always rounded up to nearest integer. Example: when the queue size is zero, a default value of 0.9 will shrink the pool by 10% (current agent count \* 0.9) |
| `samplePeriodMin` | `integer` How far back in time to look for job batches (that potentially are in the queue) |
| `readyTimeThresholdSec` | `integer` Time spent in ready state before considered truly waiting for an agent A job batch can be in ready state before getting picked up and executed. This threshold will help ensure only batches that have been waiting longer than this value will be considered. |

### ComputeQueueAwsMetricSettings

Settings for

| Name | Description |
| --- | --- |
| `computeClusterId` | `string` Compute cluster ID to observe |
| `namespace` | `string` AWS CloudWatch namespace to write metrics in |

### ProjectCategoryConfig

Information about a category to display for a stream

| Name | Description |
| --- | --- |
| `name` | `string` Name of this category |
| `row` | `integer` Index of the row to display this category on |
| `showOnNavMenu` | `boolean` Whether to show this category on the nav menu |
| `includePatterns` | `string[]` Patterns for stream names to include |
| `excludePatterns` | `string[]` Patterns for stream names to exclude |

### JobOptions

Options for executing a job

| Name | Description |
| --- | --- |
| `executor` | `string` Name of the executor to use |
| `useWine` | `boolean` Whether to execute using Wine emulation on Linux |
| `runInSeparateProcess` | `boolean` Executes the job lease in a separate process |
| `workspaceMaterializer` | `string` What workspace materializer to use in WorkspaceExecutor. Will override any value from workspace config. |
| `container` | [JobContainerOptions](/documentation/en-us/unreal-engine/horde-schema-for-unreal-engine#jobcontaineroptions) Options for executing a job inside a container |
| `expireAfterDays` | `integer` Number of days after which to expire jobs |
| `driver` | `string` Name of the driver to use |

### JobContainerOptions

Options for executing a job inside a container

| Name | Description |
| --- | --- |
| `enabled` | `boolean` Whether to execute job inside a container |
| `imageUrl` | `string` Image URL to container, such as "quay.io/podman/hello" |
| `containerEngineExecutable` | `string` Container engine executable (docker or with full path like /usr/bin/podman) |
| `extraArguments` | `string` Additional arguments to pass to container engine |

### WorkspaceConfig

Information about a workspace type

| Name | Description |
| --- | --- |
| `base` | `string` Base workspace to derive from |
| `cluster` | `string` Name of the Perforce server cluster to use |
| `serverAndPort` | `string` The Perforce server and port (eg. perforce:1666) |
| `userName` | `string` User to log into Perforce with (defaults to buildmachine) |
| `password` | `string` Password to use to log into the workspace |
| `identifier` | `string` Identifier to distinguish this workspace from other workspaces. Defaults to the workspace type name. |
| `stream` | `string` Override for the stream to sync |
| `view` | `string[]` Custom view for the workspace |
| `incremental` | `boolean` Whether to use an incrementally synced workspace |
| `useAutoSdk` | `boolean` Whether to use the AutoSDK |
| `autoSdkView` | `string[]` View for the AutoSDK paths to sync. If null, the whole thing will be synced. |
| `method` | `string` Method to use when syncing/materializing data from Perforce |
| `minScratchSpace` | `integer` Minimum disk space that must be available *after* syncing this workspace (in megabytes) If not available, the job will be aborted. |
| `conformDiskFreeSpace` | `integer` Threshold for when to trigger an automatic conform of agent. Measured in megabytes free on disk. Set to null or 0 to disable. |

### ArtifactTypeConfig

Configuration for an artifact

| Name | Description |
| --- | --- |
| `name` | `string` Legacy 'Name' property |
| `type` | `string` Name of the artifact type |
| `acl` | [AclConfig](/documentation/en-us/unreal-engine/horde-schema-for-unreal-engine#aclconfig) Acl for the artifact type |
| `keepCount` | `integer` Number of artifacts to retain |
| `keepDays` | `integer` Number of days to retain artifacts of this type |
| `namespaceId` | `string` Storage namespace to use for this artifact types |

### AclConfig

Parameters to update an ACL

| Name | Description |
| --- | --- |
| `entries` | [AclEntryConfig](/documentation/en-us/unreal-engine/horde-schema-for-unreal-engine#aclentryconfig)`[]` Entries to replace the existing ACL |
| `profiles` | [AclProfileConfig](/documentation/en-us/unreal-engine/horde-schema-for-unreal-engine#aclprofileconfig)`[]` Defines profiles which allow grouping sets of actions into named collections |
| `inherit` | `boolean` Whether to inherit permissions from the parent ACL |
| `exceptions` | `string[]` List of exceptions to the inherited setting |

### AclEntryConfig

Individual entry in an ACL

| Name | Description |
| --- | --- |
| `claim` | [AclClaimConfig](/documentation/en-us/unreal-engine/horde-schema-for-unreal-engine#aclclaimconfig) Name of the user or group |
| `actions` | `string[]` Array of actions to allow |
| `profiles` | `string[]` List of profiles to grant |

### AclClaimConfig

New claim to create

| Name | Description |
| --- | --- |
| `type` | `string` The claim type |
| `value` | `string` The claim value |

### AclProfileConfig

Configuration for an ACL profile. This defines a preset group of actions which can be given to a user via an ACL entry.

| Name | Description |
| --- | --- |
| `id` | `string` Identifier for this profile |
| `actions` | `string[]` Actions to include |
| `excludeActions` | `string[]` Actions to exclude from the inherited actions |
| `extends` | `string[]` Other profiles to extend from |

## Stream

Config for a stream. (\*.stream.json)

| Name | Description |
| --- | --- |
| `id` | `string` Identifier for the stream |
| `path` | `string` Direct include path for the stream config. For backwards compatibility with old config files when including from a ProjectConfig object. |
| `include` | [ConfigInclude](/documentation/en-us/unreal-engine/horde-schema-for-unreal-engine#configinclude)`[]` Includes for other configuration files |
| `macros` | [ConfigMacro](/documentation/en-us/unreal-engine/horde-schema-for-unreal-engine#configmacro)`[]` Macros within this stream |
| `name` | `string` Name of the stream |
| `enginePath` | `string` Path to the engine directory within the workspace. Used for launching UAT. |
| `clusterName` | `string` The perforce cluster containing the stream |
| `order` | `integer` Order for this stream |
| `initialAgentType` | `string` Default initial agent type for templates |
| `notificationChannel` | `string` Notification channel for all jobs in this stream |
| `notificationChannelFilter` | `string` Notification channel filter for this template. Can be Success, Failure, or Warnings. |
| `triageChannel` | `string` Channel to post issue triage notifications |
| `jobOptions` | [JobOptions](/documentation/en-us/unreal-engine/horde-schema-for-unreal-engine#joboptions) Default settings for executing jobs |
| `telemetryStoreId` | `string` Telemetry store for Horde data for this stream |
| `autoSdkView` | `string[]` View for the AutoSDK paths to sync. If null, the whole thing will be synced. |
| `defaultPreflightTemplate` | `string` Legacy name for the default preflight template |
| `defaultPreflight` | [DefaultPreflightConfig](/documentation/en-us/unreal-engine/horde-schema-for-unreal-engine#defaultpreflightconfig) Default template for running preflights |
| `commitTags` | [CommitTagConfig](/documentation/en-us/unreal-engine/horde-schema-for-unreal-engine#committagconfig)`[]` List of tags to apply to commits. Allows fast searching and classification of different commit types (eg. code vs content). |
| `tabs` | [TabConfig](/documentation/en-us/unreal-engine/horde-schema-for-unreal-engine#tabconfig)`[]` List of tabs to show for the new stream |
| `environment` | `string` `->` `string` Global environment variables for all agents in this stream |
| `agentTypes` | `string` `->` [AgentConfig](/documentation/en-us/unreal-engine/horde-schema-for-unreal-engine#agentconfig) Map of agent name to type |
| `workspaceTypes` | `string` `->` [WorkspaceConfig](/documentation/en-us/unreal-engine/horde-schema-for-unreal-engine#workspaceconfig) Map of workspace name to type |
| `templates` | [TemplateRefConfig](/documentation/en-us/unreal-engine/horde-schema-for-unreal-engine#templaterefconfig)`[]` List of templates to create |
| `acl` | [AclConfig](/documentation/en-us/unreal-engine/horde-schema-for-unreal-engine#aclconfig) Custom permissions for this object |
| `pausedUntil` | `string` Pause stream builds until specified date |
| `pauseComment` | `string` Reason for pausing builds of the stream |
| `replicators` | [ReplicatorConfig](/documentation/en-us/unreal-engine/horde-schema-for-unreal-engine#replicatorconfig)`[]` Configuration for workers to replicate commit data into Horde Storage. |
| `workflows` | [WorkflowConfig](/documentation/en-us/unreal-engine/horde-schema-for-unreal-engine#workflowconfig)`[]` Workflows for dealing with new issues |
| `tokens` | [TokenConfig](/documentation/en-us/unreal-engine/horde-schema-for-unreal-engine#tokenconfig)`[]` Tokens to create for each job step |
| `artifactTypes` | [ArtifactTypeConfig](/documentation/en-us/unreal-engine/horde-schema-for-unreal-engine#artifacttypeconfig)`[]` Permissions for artifact types |

### ConfigInclude

Directive to merge config data from another source

| Name | Description |
| --- | --- |
| `path` | `string` Path to the config data to be included. May be relative to the including file's location. |

### ConfigMacro

Declares a config macro

| Name | Description |
| --- | --- |
| `name` | `string` Name of the macro property |
| `value` | `string` Value for the macro property |

### JobOptions

Options for executing a job

| Name | Description |
| --- | --- |
| `executor` | `string` Name of the executor to use |
| `useWine` | `boolean` Whether to execute using Wine emulation on Linux |
| `runInSeparateProcess` | `boolean` Executes the job lease in a separate process |
| `workspaceMaterializer` | `string` What workspace materializer to use in WorkspaceExecutor. Will override any value from workspace config. |
| `container` | [JobContainerOptions](/documentation/en-us/unreal-engine/horde-schema-for-unreal-engine#jobcontaineroptions) Options for executing a job inside a container |
| `expireAfterDays` | `integer` Number of days after which to expire jobs |
| `driver` | `string` Name of the driver to use |

### JobContainerOptions

Options for executing a job inside a container

| Name | Description |
| --- | --- |
| `enabled` | `boolean` Whether to execute job inside a container |
| `imageUrl` | `string` Image URL to container, such as "quay.io/podman/hello" |
| `containerEngineExecutable` | `string` Container engine executable (docker or with full path like /usr/bin/podman) |
| `extraArguments` | `string` Additional arguments to pass to container engine |

### DefaultPreflightConfig

Specifies defaults for running a preflight

| Name | Description |
| --- | --- |
| `templateId` | `string` The template id to query |
| `change` | [ChangeQueryConfig](/documentation/en-us/unreal-engine/horde-schema-for-unreal-engine#changequeryconfig) Query for the change to use |

### ChangeQueryConfig

Query selecting the base changelist to use

| Name | Description |
| --- | --- |
| `name` | `string` Name of this query, for display on the dashboard. |
| `condition` | `string` Condition to evaluate before deciding to use this query. May query tags in a preflight. |
| `templateId` | `string` The template id to query |
| `target` | `string` The target to query |
| `outcomes` | [JobStepOutcome](/documentation/en-us/unreal-engine/horde-schema-for-unreal-engine#jobstepoutcome-enum)`[]` Whether to match a job that produced warnings |
| `commitTag` | `string` Finds the last commit with this tag |

### JobStepOutcome (Enum)

Outcome for a jobstep

| Name | Description |
| --- | --- |
| `Unspecified` | Outcome is not known |
| `Failure` | Step failed |
| `Warnings` | Step completed with warnings |
| `Success` | Step succeeded |

### CommitTagConfig

Configuration for custom commit filters

| Name | Description |
| --- | --- |
| `name` | `string` Name of the tag |
| `base` | `string` Base tag to copy settings from |
| `filter` | `string[]` List of files to be included in this filter |

### TabConfig

Information about a page to display in the dashboard for a stream

| Name | Description |
| --- | --- |
| `title` | `string` Title of this page |
| `type` | `string` Type of this tab |
| `style` | [TabStyle](/documentation/en-us/unreal-engine/horde-schema-for-unreal-engine#tabstyle-enum) Presentation style for this page |
| `showNames` | `boolean` Whether to show job names on this page |
| `showPreflights` | `boolean` Whether to show all user preflights |
| `jobNames` | `string[]` Names of jobs to include on this page. If there is only one name specified, the name column does not need to be displayed. |
| `templates` | `string[]` List of job template names to show on this page. |
| `columns` | [TabColumnConfig](/documentation/en-us/unreal-engine/horde-schema-for-unreal-engine#tabcolumnconfig)`[]` Columns to display for different types of aggregates |

### TabStyle (Enum)

Style for rendering a tab

| Name | Description |
| --- | --- |
| `Normal` | Regular job list |
| `Compact` | Omit job names, show condensed view |

### TabColumnConfig

Describes a column to display on the jobs page

| Name | Description |
| --- | --- |
| `type` | [TabColumnType](/documentation/en-us/unreal-engine/horde-schema-for-unreal-engine#tabcolumntype-enum) The type of column |
| `heading` | `string` Heading for this column |
| `category` | `string` Category of aggregates to display in this column. If null, includes any aggregate not matched by another column. |
| `parameter` | `string` Parameter to show in this column |
| `relativeWidth` | `integer` Relative width of this column. |

### TabColumnType (Enum)

Type of a column in a jobs tab

| Name | Description |
| --- | --- |
| `Labels` | Contains labels |
| `Parameter` | Contains parameters |

### AgentConfig

Mapping from a BuildGraph agent type to a set of machines on the farm

| Name | Description |
| --- | --- |
| `base` | `string` Base agent config to inherit settings from |
| `pool` | `string` Pool of agents to use for this agent type |
| `workspace` | `string` Name of the workspace to sync |
| `tempStorageDir` | `string` Path to the temporary storage dir |
| `environment` | `string` `->` `string` Environment variables to be set when executing the job |
| `tokens` | [TokenConfig](/documentation/en-us/unreal-engine/horde-schema-for-unreal-engine#tokenconfig)`[]` Tokens to allocate for this agent type |

### TokenConfig

Configuration for allocating access tokens for each job

| Name | Description |
| --- | --- |
| `url` | `string` URL to request tokens from |
| `clientId` | `string` Client id to use to request a new token |
| `clientSecret` | `string` Client secret to request a new access token |
| `envVar` | `string` Environment variable to set with the access token |

### WorkspaceConfig

Information about a workspace type

| Name | Description |
| --- | --- |
| `base` | `string` Base workspace to derive from |
| `cluster` | `string` Name of the Perforce server cluster to use |
| `serverAndPort` | `string` The Perforce server and port (eg. perforce:1666) |
| `userName` | `string` User to log into Perforce with (defaults to buildmachine) |
| `password` | `string` Password to use to log into the workspace |
| `identifier` | `string` Identifier to distinguish this workspace from other workspaces. Defaults to the workspace type name. |
| `stream` | `string` Override for the stream to sync |
| `view` | `string[]` Custom view for the workspace |
| `incremental` | `boolean` Whether to use an incrementally synced workspace |
| `useAutoSdk` | `boolean` Whether to use the AutoSDK |
| `autoSdkView` | `string[]` View for the AutoSDK paths to sync. If null, the whole thing will be synced. |
| `method` | `string` Method to use when syncing/materializing data from Perforce |
| `minScratchSpace` | `integer` Minimum disk space that must be available *after* syncing this workspace (in megabytes) If not available, the job will be aborted. |
| `conformDiskFreeSpace` | `integer` Threshold for when to trigger an automatic conform of agent. Measured in megabytes free on disk. Set to null or 0 to disable. |

### TemplateRefConfig

Parameters to create a template within a stream

| Name | Description |
| --- | --- |
| `id` | `string` Optional identifier for this ref. If not specified, an id will be generated from the name. |
| `base` | `string` Base template id to copy from |
| `showUgsBadges` | `boolean` Whether to show badges in UGS for these jobs |
| `showUgsAlerts` | `boolean` Whether to show alerts in UGS for these jobs |
| `notificationChannel` | `string` Notification channel for this template. Overrides the stream channel if set. |
| `notificationChannelFilter` | `string` Notification channel filter for this template. Can be a combination of "Success", "Failure" and "Warnings" separated by pipe characters. |
| `triageChannel` | `string` Triage channel for this template. Overrides the stream channel if set. |
| `workflowId` | `string` Workflow to user for this stream |
| `annotations` | `string` `->` `string` Default annotations to apply to nodes in this template |
| `schedule` | [ScheduleConfig](/documentation/en-us/unreal-engine/horde-schema-for-unreal-engine#scheduleconfig) Schedule to execute this template |
| `chainedJobs` | [ChainedJobTemplateConfig](/documentation/en-us/unreal-engine/horde-schema-for-unreal-engine#chainedjobtemplateconfig)`[]` List of chained job triggers |
| `acl` | [AclConfig](/documentation/en-us/unreal-engine/horde-schema-for-unreal-engine#aclconfig) The ACL for this template |
| `name` | `string` Name for the new template |
| `description` | `string` Description for the template |
| `priority` | [Priority](/documentation/en-us/unreal-engine/horde-schema-for-unreal-engine#priority-enum) Default priority for this job |
| `allowPreflights` | `boolean` Whether to allow preflights of this template |
| `updateIssues` | `boolean` Whether issues should be updated for all jobs using this template |
| `promoteIssuesByDefault` | `boolean` Whether issues should be promoted by default for this template, promoted issues will generate user notifications |
| `initialAgentType` | `string` Initial agent type to parse the buildgraph script on |
| `submitNewChange` | `string` Path to a file within the stream to submit to generate a new changelist for jobs |
| `submitDescription` | `string` Description for new changelists |
| `defaultChange` | [ChangeQueryConfig](/documentation/en-us/unreal-engine/horde-schema-for-unreal-engine#changequeryconfig)`[]` Default change to build at. Each object has a condition parameter which can evaluated by the server to determine which change to use. |
| `arguments` | `string[]` Fixed arguments for the new job |
| `parameters` | [TextParameterData](/documentation/en-us/unreal-engine/horde-schema-for-unreal-engine#textparameterdata)/[ListParameterData](/documentation/en-us/unreal-engine/horde-schema-for-unreal-engine#listparameterdata)/[BoolParameterData](/documentation/en-us/unreal-engine/horde-schema-for-unreal-engine#boolparameterdata)`[]` Parameters for this template |
| `jobOptions` | [JobOptions](/documentation/en-us/unreal-engine/horde-schema-for-unreal-engine#joboptions) Default settings for jobs |

### ScheduleConfig

Parameters to create a new schedule

| Name | Description |
| --- | --- |
| `claims` | [AclClaimConfig](/documentation/en-us/unreal-engine/horde-schema-for-unreal-engine#aclclaimconfig)`[]` Roles to impersonate for this schedule |
| `enabled` | `boolean` Whether the schedule should be enabled |
| `maxActive` | `integer` Maximum number of builds that can be active at once |
| `maxChanges` | `integer` Maximum number of changes the schedule can fall behind head revision. If greater than zero, builds will be triggered for every submitted changelist until the backlog is this size. |
| `requireSubmittedChange` | `boolean` Whether the build requires a change to be submitted |
| `gate` | [ScheduleGateConfig](/documentation/en-us/unreal-engine/horde-schema-for-unreal-engine#schedulegateconfig) Gate allowing the schedule to trigger |
| `commits` | `string[]` Commit tags for this schedule |
| `filter` | [ChangeContentFlags](/documentation/en-us/unreal-engine/horde-schema-for-unreal-engine#changecontentflags-enum)`[]` The types of changes to run for |
| `files` | `string[]` Files that should cause the job to trigger |
| `templateParameters` | `string` `->` `string` Parameters for the template |
| `patterns` | [SchedulePatternConfig](/documentation/en-us/unreal-engine/horde-schema-for-unreal-engine#schedulepatternconfig)`[]` New patterns for the schedule |

### AclClaimConfig

New claim to create

| Name | Description |
| --- | --- |
| `type` | `string` The claim type |
| `value` | `string` The claim value |

### ScheduleGateConfig

Gate allowing a schedule to trigger.

| Name | Description |
| --- | --- |
| `templateId` | `string` The template containing the dependency |
| `target` | `string` Target to wait for |

### ChangeContentFlags (Enum)

Flags identifying content of a changelist

| Name | Description |
| --- | --- |
| `ContainsCode` | The change contains code |
| `ContainsContent` | The change contains content |

### SchedulePatternConfig

Parameters to create a new schedule

| Name | Description |
| --- | --- |
| `daysOfWeek` | [DayOfWeek](/documentation/en-us/unreal-engine/horde-schema-for-unreal-engine#dayofweek-enum)`[]` Days of the week to run this schedule on. If null, the schedule will run every day. |
| `minTime` | `string` Time during the day for the first schedule to trigger. Measured in minutes from midnight. |
| `maxTime` | `string` Time during the day for the last schedule to trigger. Measured in minutes from midnight. |
| `interval` | `string` Interval between each schedule triggering |

### DayOfWeek (Enum)

| Name | Description |
| --- | --- |
| `Sunday` | Sunday |
| `Monday` | Monday |
| `Tuesday` | Tuesday |
| `Wednesday` | Wednesday |
| `Thursday` | Thursday |
| `Friday` | Friday |
| `Saturday` | Saturday |

### ChainedJobTemplateConfig

Trigger for another template

| Name | Description |
| --- | --- |
| `trigger` | `string` Name of the target that needs to complete before starting the other template |
| `templateId` | `string` Id of the template to trigger |
| `useDefaultChangeForTemplate` | `boolean` Whether to use the default change for the template rather than the change for the parent job. |

### AclConfig

Parameters to update an ACL

| Name | Description |
| --- | --- |
| `entries` | [AclEntryConfig](/documentation/en-us/unreal-engine/horde-schema-for-unreal-engine#aclentryconfig)`[]` Entries to replace the existing ACL |
| `profiles` | [AclProfileConfig](/documentation/en-us/unreal-engine/horde-schema-for-unreal-engine#aclprofileconfig)`[]` Defines profiles which allow grouping sets of actions into named collections |
| `inherit` | `boolean` Whether to inherit permissions from the parent ACL |
| `exceptions` | `string[]` List of exceptions to the inherited setting |

### AclEntryConfig

Individual entry in an ACL

| Name | Description |
| --- | --- |
| `claim` | [AclClaimConfig](/documentation/en-us/unreal-engine/horde-schema-for-unreal-engine#aclclaimconfig) Name of the user or group |
| `actions` | `string[]` Array of actions to allow |
| `profiles` | `string[]` List of profiles to grant |

### AclProfileConfig

Configuration for an ACL profile. This defines a preset group of actions which can be given to a user via an ACL entry.

| Name | Description |
| --- | --- |
| `id` | `string` Identifier for this profile |
| `actions` | `string[]` Actions to include |
| `excludeActions` | `string[]` Actions to exclude from the inherited actions |
| `extends` | `string[]` Other profiles to extend from |

### Priority (Enum)

Priority of a job or step

| Name | Description |
| --- | --- |
| `Unspecified` | Not specified |
| `Lowest` | Lowest priority |
| `BelowNormal` | Below normal priority |
| `Normal` | Normal priority |
| `AboveNormal` | Above normal priority |
| `High` | High priority |
| `Highest` | Highest priority |

### TextParameterData

Free-form text entry parameter

| Name | Description |
| --- | --- |
| `type` | Text Type discriminator |
| `id` | `string` Identifier for this parameter |
| `label` | `string` Name of the parameter associated with this parameter. |
| `argument` | `string` Argument to pass to the executor |
| `default` | `string` Default value for this argument |
| `scheduleOverride` | `string` Override for the default value for this parameter when running a scheduled build |
| `hint` | `string` Hint text for this parameter |
| `validation` | `string` Regex used to validate this parameter |
| `validationError` | `string` Message displayed if validation fails, informing user of valid values. |
| `toolTip` | `string` Tool-tip text to display |

### ListParameterData

Allows the user to select a value from a constrained list of choices

| Name | Description |
| --- | --- |
| `type` | List Type discriminator |
| `label` | `string` Label to display next to this parameter. Defaults to the parameter name. |
| `style` | [ListParameterStyle](/documentation/en-us/unreal-engine/horde-schema-for-unreal-engine#listparameterstyle-enum) The type of list parameter |
| `items` | [ListParameterItemData](/documentation/en-us/unreal-engine/horde-schema-for-unreal-engine#listparameteritemdata)`[]` List of values to display in the list |
| `toolTip` | `string` Tool tip text to display |

### ListParameterStyle (Enum)

Style of list parameter

| Name | Description |
| --- | --- |
| `List` | Regular drop-down list. One item is always selected. |
| `MultiList` | Drop-down list with checkboxes |
| `TagPicker` | Tag picker from list of options |

### ListParameterItemData

Possible option for a list parameter

| Name | Description |
| --- | --- |
| `id` | `string` Identifier for this parameter |
| `group` | `string` Optional group heading to display this entry under, if the picker style supports it. |
| `text` | `string` Name of the parameter associated with this list. |
| `argumentIfEnabled` | `string` Argument to pass with this parameter. |
| `argumentsIfEnabled` | `string[]` Arguments to pass with this parameter. |
| `argumentIfDisabled` | `string` Argument to pass with this parameter. |
| `argumentsIfDisabled` | `string[]` Arguments to pass if this parameter is disabled. |
| `default` | `boolean` Whether this item is selected by default |
| `scheduleOverride` | `boolean` Overridden value for this property in schedule builds |

### BoolParameterData

Allows the user to toggle an option on or off

| Name | Description |
| --- | --- |
| `type` | Bool Type discriminator |
| `id` | `string` Identifier for this parameter |
| `label` | `string` Name of the parameter associated with this parameter. |
| `argumentIfEnabled` | `string` Argument to add if this parameter is enabled |
| `argumentsIfEnabled` | `string[]` Argument to add if this parameter is enabled |
| `argumentIfDisabled` | `string` Argument to add if this parameter is enabled |
| `argumentsIfDisabled` | `string[]` Arguments to add if this parameter is disabled |
| `default` | `boolean` Whether this argument is enabled by default |
| `scheduleOverride` | `boolean` Override for this parameter in scheduled builds |
| `toolTip` | `string` Tool tip text to display |

### ReplicatorConfig

Configuration for a stream replicator

| Name | Description |
| --- | --- |
| `id` | `string` Identifier for the replicator within the current stream |
| `enabled` | `boolean` Whether the replicator is enabled |
| `minChange` | `integer` Minimum change number to replicate |
| `maxChange` | `integer` Maximum change number to replicate |
| `includeContent` | `boolean` Whether to include content in the replication, or just metadata |
| `namespaceId` | `string` Namespace to replicate data to |

### WorkflowConfig

Configuration for an issue workflow

| Name | Description |
| --- | --- |
| `id` | `string` Identifier for this workflow |
| `reportTimes` | `string[]` Times of day at which to send a report |
| `summaryTab` | `string` Name of the tab to post summary data to |
| `reportChannel` | `string` Channel to post summary information for these templates. |
| `reportWarnings` | `boolean` Whether to include issues with a warning status in the summary |
| `groupIssuesByTemplate` | `boolean` Whether to group issues by template in the report |
| `triageChannel` | `string` Channel to post threads for triaging new issues |
| `triagePrefix` | `string` Prefix for all triage messages |
| `triageSuffix` | `string` Suffix for all triage messages |
| `triageInstructions` | `string` Instructions posted to triage threads |
| `triageAlias` | `string` User id of a Slack user/alias to ping if there is nobody assigned to an issue by default. |
| `triageTypeAliases` | `string` `->` `string` Slack user/alias to ping for specific issue types (such as Systemic), if there is nobody assigned to an issue by default. |
| `escalateAlias` | `string` Alias to ping if an issue has not been resolved for a certain amount of time |
| `escalateTimes` | `integer[]` Times after an issue has been opened to escalate to the alias above, in minutes. Continues to notify on the last interval once reaching the end of the list. |
| `maxMentions` | `integer` Maximum number of people to mention on a triage thread |
| `allowMentions` | `boolean` Whether to mention people on this thread. Useful to disable for testing. |
| `inviteRestrictedUsers` | `boolean` Uses the admin.conversations.invite API to invite users to the channel |
| `skipWhenEmpty` | `boolean` Skips sending reports when there are no active issues. |
| `showMergeWarnings` | `boolean` Whether to show warnings about merging changes into the origin stream. |
| `annotations` | `string` `->` `string` Additional node annotations implicit in this workflow |
| `externalIssues` | [ExternalIssueConfig](/documentation/en-us/unreal-engine/horde-schema-for-unreal-engine#externalissueconfig) External issue tracking configuration for this workflow |
| `issueHandlers` | `string[]` Additional issue handlers enabled for this workflow |

### ExternalIssueConfig

External issue tracking configuration for a workflow

| Name | Description |
| --- | --- |
| `projectKey` | `string` Project key in external issue tracker |
| `defaultComponentId` | `string` Default component id for issues using workflow |
| `defaultIssueTypeId` | `string` Default issue type id for issues using workflow |

### ArtifactTypeConfig

Configuration for an artifact

| Name | Description |
| --- | --- |
| `name` | `string` Legacy 'Name' property |
| `type` | `string` Name of the artifact type |
| `acl` | [AclConfig](/documentation/en-us/unreal-engine/horde-schema-for-unreal-engine#aclconfig) Acl for the artifact type |
| `keepCount` | `integer` Number of artifacts to retain |
| `keepDays` | `integer` Number of days to retain artifacts of this type |
| `namespaceId` | `string` Storage namespace to use for this artifact types |

## Telemetry

Config for metrics. (\*.telemetry.json)

| Name | Description |
| --- | --- |
| `id` | `string` Identifier for this store |
| `acl` | [AclConfig](/documentation/en-us/unreal-engine/horde-schema-for-unreal-engine#aclconfig) Permissions for this store |
| `metrics` | [MetricConfig](/documentation/en-us/unreal-engine/horde-schema-for-unreal-engine#metricconfig)`[]` Metrics to aggregate on the Horde server |
| `views` | [TelemetryViewConfig](/documentation/en-us/unreal-engine/horde-schema-for-unreal-engine#telemetryviewconfig)`[]` Configuration for telemetry views |
| `include` | [ConfigInclude](/documentation/en-us/unreal-engine/horde-schema-for-unreal-engine#configinclude)`[]` Includes for other configuration files |
| `macros` | [ConfigMacro](/documentation/en-us/unreal-engine/horde-schema-for-unreal-engine#configmacro)`[]` Macros within this configuration |

### AclConfig

Parameters to update an ACL

| Name | Description |
| --- | --- |
| `entries` | [AclEntryConfig](/documentation/en-us/unreal-engine/horde-schema-for-unreal-engine#aclentryconfig)`[]` Entries to replace the existing ACL |
| `profiles` | [AclProfileConfig](/documentation/en-us/unreal-engine/horde-schema-for-unreal-engine#aclprofileconfig)`[]` Defines profiles which allow grouping sets of actions into named collections |
| `inherit` | `boolean` Whether to inherit permissions from the parent ACL |
| `exceptions` | `string[]` List of exceptions to the inherited setting |

### AclEntryConfig

Individual entry in an ACL

| Name | Description |
| --- | --- |
| `claim` | [AclClaimConfig](/documentation/en-us/unreal-engine/horde-schema-for-unreal-engine#aclclaimconfig) Name of the user or group |
| `actions` | `string[]` Array of actions to allow |
| `profiles` | `string[]` List of profiles to grant |

### AclClaimConfig

New claim to create

| Name | Description |
| --- | --- |
| `type` | `string` The claim type |
| `value` | `string` The claim value |

### AclProfileConfig

Configuration for an ACL profile. This defines a preset group of actions which can be given to a user via an ACL entry.

| Name | Description |
| --- | --- |
| `id` | `string` Identifier for this profile |
| `actions` | `string[]` Actions to include |
| `excludeActions` | `string[]` Actions to exclude from the inherited actions |
| `extends` | `string[]` Other profiles to extend from |

### MetricConfig

Configures a metric to aggregate on the server

| Name | Description |
| --- | --- |
| `id` | `string` Identifier for this metric |
| `filter` | `string` Filter expression to evaluate to determine which events to include. This query is evaluated against an array. |
| `property` | `string` Property to aggregate |
| `groupBy` | `string` Property to group by. Specified as a comma-separated list of JSON path expressions. |
| `function` | [AggregationFunction](/documentation/en-us/unreal-engine/horde-schema-for-unreal-engine#aggregationfunction-enum) How to aggregate samples for this metric |
| `percentile` | `integer` For the percentile function, specifies the percentile to measure |
| `interval` | `string` Interval for each metric. Supports times such as "2d", "1h", "1h30m", "20s". |

### AggregationFunction (Enum)

Method for aggregating samples into a metric

| Name | Description |
| --- | --- |
| `Count` | Count the number of matching elements |
| `Min` | Take the minimum value of all samples |
| `Max` | Take the maximum value of all samples |
| `Sum` | Sum all the reported values |
| `Average` | Average all the samples |
| `Percentile` | Estimates the value at a certain percentile |

### TelemetryViewConfig

A telemetry view of related metrics, divided into categofies

| Name | Description |
| --- | --- |
| `id` | `string` Identifier for the view |
| `name` | `string` The name of the view |
| `telemetryStoreId` | `string` The telemetry store this view uses |
| `variables` | [TelemetryVariableConfig](/documentation/en-us/unreal-engine/horde-schema-for-unreal-engine#telemetryvariableconfig)`[]` The variables used to filter the view data |
| `categories` | [TelemetryCategoryConfig](/documentation/en-us/unreal-engine/horde-schema-for-unreal-engine#telemetrycategoryconfig)`[]` The categories contained within the view |

### TelemetryVariableConfig

A telemetry view variable used for filtering the charting data

| Name | Description |
| --- | --- |
| `name` | `string` The name of the variable for display purposes |
| `group` | `string` The associated data group attached to the variable |
| `defaults` | `string[]` The default values to select |

### TelemetryCategoryConfig

A chart categody, will be displayed on the dashbord under an associated pivot

| Name | Description |
| --- | --- |
| `name` | `string` The name of the category |
| `charts` | [TelemetryChartConfig](/documentation/en-us/unreal-engine/horde-schema-for-unreal-engine#telemetrychartconfig)`[]` The charts contained within the category |

### TelemetryChartConfig

Telemetry chart configuraton

| Name | Description |
| --- | --- |
| `name` | `string` The name of the chart, will be displayed on the dashboard |
| `display` | [TelemetryMetricUnitType](/documentation/en-us/unreal-engine/horde-schema-for-unreal-engine#telemetrymetricunittype-enum) The unit to display |
| `graph` | [TelemetryMetricGraphType](/documentation/en-us/unreal-engine/horde-schema-for-unreal-engine#telemetrymetricgraphtype-enum) The graph type |
| `metrics` | [TelemetryChartMetricConfig](/documentation/en-us/unreal-engine/horde-schema-for-unreal-engine#telemetrychartmetricconfig)`[]` List of configured metrics |
| `min` | `integer` The min unit value for clamping chart |
| `max` | `integer` The max unit value for clamping chart |

### TelemetryMetricUnitType (Enum)

The units used to present the telemetry

| Name | Description |
| --- | --- |
| `Time` | Time duration |
| `Ratio` | Ratio 0-100% |
| `Value` | Artbitrary numeric value |

### TelemetryMetricGraphType (Enum)

The type of

| Name | Description |
| --- | --- |
| `Line` | A line graph |
| `Indicator` | Key performance indicator (KPI) chart with thrasholds |

### TelemetryChartMetricConfig

Metric attached to a telemetry chart

| Name | Description |
| --- | --- |
| `id` | `string` Associated metric id |
| `threshold` | `integer` The threshold for KPI values |
| `alias` | `string` The metric alias for display purposes |

### ConfigInclude

Directive to merge config data from another source

| Name | Description |
| --- | --- |
| `path` | `string` Path to the config data to be included. May be relative to the including file's location. |

### ConfigMacro

Declares a config macro

| Name | Description |
| --- | --- |
| `name` | `string` Name of the macro property |
| `value` | `string` Value for the macro property |