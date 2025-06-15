# Horde Settings

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/horde-settings-for-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/horde-settings-for-unreal-engine)  
**Processed:** 2025-06-14 16:28:16

---

## Server Settings

### Server.json

All Horde-specific settings are stored in a root object called `Horde`. Other .NET functionality may be configured using properties in the root of this file.

| Name | Description |
| --- | --- |
| `runModes` | [RunMode](/documentation/en-us/unreal-engine/horde-settings-for-unreal-engine#runmode-enum)`[]` Modes that the server should run in. Runmodes can be used in a multi-server deployment to limit the operations that a particular instance will try to perform. |
| `dataDir` | `string` Override the data directory used by Horde. Defaults to C:\\ProgramData\\HordeServer on Windows, {AppDir}/Data on other platforms. |
| `installed` | `boolean` Whether the server is running in 'installed' mode. In this mode, on Windows, the default data directory will use the common application data folder (C:\\ProgramData\\Epic\\Horde), and configuration data will be read from here and the registry. This setting is overridden to false for local builds from appsettings.Local.json. |
| `httpPort` | `integer` Main port for serving HTTP. |
| `httpsPort` | `integer` Port for serving HTTP with TLS enabled. Disabled by default. |
| `http2Port` | `integer` Dedicated port for serving only HTTP/2. |
| `mongoConnectionString` | `string` Connection string for the Mongo database |
| `databaseConnectionString` | `string` MongoDB connection string |
| `mongoDatabaseName` | `string` MongoDB database name |
| `databaseName` | `string` |
| `mongoPublicCertificate` | `string` Optional certificate to trust in order to access the database (eg. AWS public cert for TLS) |
| `databasePublicCert` | `string` |
| `mongoReadOnlyMode` | `boolean` Access the database in read-only mode (avoids creating indices or updating content) Useful for debugging a local instance of HordeServer against a production database. |
| `databaseReadOnlyMode` | `boolean` |
| `shutdownMemoryThreshold` | `integer` Shutdown the current server process if memory usage reaches this threshold (specified in MB) Usually set to 80-90% of available memory to avoid CLR heap using all of it. If a memory leak was to occur, it's usually better to restart the process rather than to let the GC work harder and harder trying to recoup memory. Should only be used when multiple server processes are running behind a load balancer and one can be safely restarted automatically by the underlying process handler (Docker, Kubernetes, AWS ECS, Supervisor etc). The shutdown behaves similar to receiving a SIGTERM and will wait for outstanding requests to finish. |
| `serverPrivateCert` | `string` Optional PFX certificate to use for encrypting agent SSL traffic. This can be a self-signed certificate, as long as it's trusted by agents. |
| `authMethod` | [AuthMethod](/documentation/en-us/unreal-engine/horde-settings-for-unreal-engine#authmethod-enum) Type of authentication (e.g anonymous, OIDC, built-in Horde accounts) If "Horde" auth mode is used, be sure to configure "ServerUrl" as well. |
| `oidcProfileName` | `string` Optional profile name to report through the /api/v1/server/auth endpoint. Allows sharing auth tokens between providers configured through the same profile name in OidcToken.exe config files. |
| `oidcAuthority` | `string` OpenID Connect (OIDC) authority URL (required when OIDC is enabled) |
| `oidcAudience` | `string` Audience for validating externally issued tokens (required when OIDC is enabled) |
| `oidcClientId` | `string` Client ID for the OIDC authority (required when OIDC is enabled) |
| `oidcClientSecret` | `string` Client secret for the OIDC authority |
| `oidcSigninRedirect` | `string` Optional redirect url provided to OIDC login |
| `oidcLocalRedirectUrls` | `string[]` Optional redirect url provided to OIDC login for external tools (typically to a local server) Default value is the local web server started during signin by EpicGames.OIDC library |
| `oidcDebugMode` | `boolean` Debug mode for OIDC which logs reasons for why JWT tokens fail to authenticate Also turns off HTTPS requirement for OIDC metadata fetching. NOT FOR PRODUCTION USE! |
| `oidcRequestedScopes` | `string[]` OpenID Connect scopes to request when signing in |
| `oidcClaimNameMapping` | `string[]` List of fields in /userinfo endpoint to try map to the standard name claim (see System.Security.Claims.ClaimTypes.Name) |
| `oidcClaimEmailMapping` | `string[]` List of fields in /userinfo endpoint to try map to the standard email claim (see System.Security.Claims.ClaimTypes.Email) |
| `oidcClaimHordeUserMapping` | `string[]` List of fields in /userinfo endpoint to try map to the Horde user claim (see HordeClaimTypes.User) |
| `oidcClaimHordePerforceUserMapping` | `string[]` List of fields in /userinfo endpoint to try map to the Horde Perforce user claim (see HordeClaimTypes.PerforceUser) |
| `serverUrl` | `string` Base URL this Horde server is accessible from For example https://horde.mystudio.com If not set, a default is used based on current hostname. In more advanced setups where a reverse proxy is present in front of Horde, this must manually be set. |
| `jwtIssuer` | `string` Name of the issuer in bearer tokens from the server |
| `jwtExpiryTimeHours` | `integer` Length of time before JWT tokens expire, in hours |
| `adminClaimType` | `string` The claim type for administrators |
| `adminClaimValue` | `string` Value of the claim type for administrators |
| `corsEnabled` | `boolean` Whether to enable Cors, generally for development purposes |
| `corsOrigin` | `string` Allowed Cors origin |
| `enableDebugEndpoints` | `boolean` Whether to enable debug/administrative REST API endpoints |
| `enableNewAgentsByDefault` | `boolean` Whether to automatically enable new agents by default. If false, new agents must manually be enabled before they can take on work. |
| `schedulePollingInterval` | `string` Interval between rebuilding the schedule queue with a DB query. |
| `noResourceBackOffTime` | `string` Interval between polling for new jobs |
| `initiateJobBackOffTime` | `string` Interval between attempting to assign agents to take on jobs |
| `unknownErrorBackOffTime` | `string` Interval between scheduling jobs when an unknown error occurs |
| `redisConnectionString` | `string` Config for connecting to Redis server(s). Setting it to null will disable Redis use and connection See format at https://stackexchange.github.io/StackExchange.Redis/Configuration.html |
| `redisConnectionConfig` | `string` |
| `redisReadOnlyMode` | `boolean` Whether to disable writes to Redis. |
| `logServiceWriteCacheType` | `string` Overridden settings for storage backends. Useful for running against a production server with custom backends. |
| `logJsonToStdOut` | `boolean` Whether to log json to stdout |
| `logSessionRequests` | `boolean` Whether to log requests to the UpdateSession and QueryServerState RPC endpoints |
| `scheduleTimeZone` | `string` Timezone for evaluating schedules |
| `dashboardUrl` | `string` The URl to use for generating links back to the dashboard. |
| `helpEmailAddress` | `string` Help email address that users can contact with issues |
| `helpSlackChannel` | `string` Help slack channel that users can use for issues |
| `globalThreadPoolMinSize` | `integer` Set the minimum size of the global thread pool This value has been found in need of tweaking to avoid timeouts with the Redis client during bursts of traffic. Default is 16 for .NET Core CLR. The correct value is dependent on the traffic the Horde Server is receiving. For Epic's internal deployment, this is set to 40. |
| `withDatadog` | `boolean` Whether to enable Datadog integration for tracing |
| `configPath` | `string` Path to the root config file. Relative to the server.json file by default. |
| `forceConfigUpdateOnStartup` | `boolean` Forces configuration data to be read and updated as part of appplication startup, rather than on a schedule. Useful when running locally. |
| `openBrowser` | `boolean` Whether to open a browser on startup |
| `featureFlags` | [FeatureFlagSettings](/documentation/en-us/unreal-engine/horde-settings-for-unreal-engine#featureflagsettings) Experimental features to enable on the server. |
| `openTelemetry` | [OpenTelemetrySettings](/documentation/en-us/unreal-engine/horde-settings-for-unreal-engine#opentelemetrysettings) Options for OpenTelemetry |
| `plugins` | [ServerPluginsConfig](/documentation/en-us/unreal-engine/horde-settings-for-unreal-engine#serverpluginsconfig) Configuration for plugins |

#### RunMode (Enum)

Type of run mode this process should use. Each carry different types of workloads. More than one mode can be active. But not all modes are not guaranteed to be compatible with each other and will raise an error if combined in such a way.

| Name | Description |
| --- | --- |
| `None` | Default no-op value (ASP.NET config will default to this for enums that cannot be parsed) |
| `Server` | Handle and respond to incoming external requests, such as HTTP REST and gRPC calls. These requests are time-sensitive and short-lived, typically less than 5 secs. If processes handling requests are unavailable, it will be very visible for users. |
| `Worker` | Run non-request facing workloads. Such as background services, processing queues, running work based on timers etc. Short periods of downtime or high CPU usage due to bursts are fine for this mode. No user requests will be impacted directly. If auto-scaling is used, a much more aggressive policy can be applied (tighter process packing, higher avg CPU usage). |

#### AuthMethod (Enum)

Authentication method used for logging users in

| Name | Description |
| --- | --- |
| `Anonymous` | No authentication enabled. *Only* for demo and testing purposes. |
| `Okta` | OpenID Connect authentication, tailored for Okta |
| `OpenIdConnect` | Generic OpenID Connect authentication, recommended for most |
| `Horde` | Authenticate using username and password credentials stored in Horde OpenID Connect (OIDC) is first and foremost recommended. But if you have a small installation (less than ~10 users) or lacking an OIDC provider, this is an option. |

#### FeatureFlagSettings

Feature flags to aid rollout of new features. Once a feature is running in its intended state and is stable, the flag should be removed. A name and date of when the flag was created is noted next to it to help encourage this behavior. Try having them be just a flag, a boolean.

#### OpenTelemetrySettings

OpenTelemetry configuration for collection and sending of traces and metrics.

| Name | Description |
| --- | --- |
| `enabled` | `boolean` Whether OpenTelemetry exporting is enabled |
| `serviceName` | `string` Service name |
| `serviceNamespace` | `string` Service namespace |
| `serviceVersion` | `string` Service version |
| `enableDatadogCompatibility` | `boolean` Whether to enrich and format telemetry to fit presentation in Datadog |
| `attributes` | `string` `->` `string` Extra attributes to set |
| `enableConsoleExporter` | `boolean` Whether to enable the console exporter (for debugging purposes) |
| `protocolExporters` | `string` `->` [OpenTelemetryProtocolExporterSettings](/documentation/en-us/unreal-engine/horde-settings-for-unreal-engine#opentelemetryprotocolexportersettings) Protocol exporters (key is a unique and arbitrary name) |

#### OpenTelemetryProtocolExporterSettings

Configuration for an OpenTelemetry exporter

| Name | Description |
| --- | --- |
| `endpoint` | `string` Endpoint URL. Usually differs depending on protocol used. |
| `protocol` | `string` Protocol for the exporter ('grpc' or 'httpprotobuf') |

#### ServerPluginsConfig

| Name | Description |
| --- | --- |
| `compute` | [ComputeServerConfig](/documentation/en-us/unreal-engine/horde-settings-for-unreal-engine#computeserverconfig) Configuration for the compute plugin |
| `secrets` | [PluginServerConfig](/documentation/en-us/unreal-engine/horde-settings-for-unreal-engine#pluginserverconfig) Configuration for the secrets plugin |
| `analytics` | [AnalyticsServerConfig](/documentation/en-us/unreal-engine/horde-settings-for-unreal-engine#analyticsserverconfig) Configuration for the analytics plugin |
| `build` | [BuildServerConfig](/documentation/en-us/unreal-engine/horde-settings-for-unreal-engine#buildserverconfig) Configuration for the build plugin |
| `storage` | [StorageServerConfig](/documentation/en-us/unreal-engine/horde-settings-for-unreal-engine#storageserverconfig) Configuration for the storage plugin |
| `symbols` | [PluginServerConfig](/documentation/en-us/unreal-engine/horde-settings-for-unreal-engine#pluginserverconfig) Configuration for the symbols plugin |
| `tools` | [ToolsServerConfig](/documentation/en-us/unreal-engine/horde-settings-for-unreal-engine#toolsserverconfig) Configuration for the tools plugin |
| `ddc` | [PluginServerConfig](/documentation/en-us/unreal-engine/horde-settings-for-unreal-engine#pluginserverconfig) Configuration for the ddc plugin |

#### ComputeServerConfig

Static configuration for the compute plugin

| Name | Description |
| --- | --- |
| `enableUpgradeTasks` | `boolean` Whether to enable the upgrade task source. |
| `withAws` | `boolean` Whether to enable Amazon Web Services (AWS) specific features |
| `awsRegions` | `string[]` List of AWS regions for Horde to be aware of (e.g. us-east-1 or eu-central-1) Right now, this is only used for replicating CloudWatch metrics to multiple regions |
| `awsAutoScalingQueueUrls` | `string[]` AWS SQS queue URLs where lifecycle events from EC2 auto-scaling are received |
| `fleetManagerV2` | [FleetManagerType](/documentation/en-us/unreal-engine/horde-settings-for-unreal-engine#fleetmanagertype-enum) Default fleet manager to use (when not specified by pool) |
| `fleetManagerV2Config` | `object` Config for the fleet manager (serialized JSON) |
| `autoEnrollAgents` | `boolean` Whether to automatically enroll agents in the farm |
| `defaultAgentPoolSizeStrategy` | [PoolSizeStrategy](/documentation/en-us/unreal-engine/horde-settings-for-unreal-engine#poolsizestrategy-enum) Default agent pool sizing strategy for pools that doesn't have one explicitly configured |
| `agentPoolScaleOutCooldownSeconds` | `integer` Scale-out cooldown for auto-scaling agent pools (in seconds). Can be overridden by per-pool settings. |
| `agentPoolScaleInCooldownSeconds` | `integer` Scale-in cooldown for auto-scaling agent pools (in seconds). Can be overridden by per-pool settings. |
| `computeTunnelPort` | `integer` Port to listen on for tunneling compute sockets to agents |
| `computeTunnelAddress` | `string` What address (host:port) clients should connect to for compute socket tunneling Port may differ from if Horde server is behind a reverse proxy/firewall |
| `enabled` | `boolean` Whether the plugin should be enabled or not |

#### FleetManagerType (Enum)

Available fleet managers

| Name | Description |
| --- | --- |
| `Default` | Default fleet manager |
| `NoOp` | No-op fleet manager. |
| `Aws` | Fleet manager for handling AWS EC2 instances. Will create and/or terminate instances from scratch. |
| `AwsReuse` | Fleet manager for handling AWS EC2 instances. Will start already existing but stopped instances to reuse existing EBS disks. |
| `AwsRecycle` | Fleet manager for handling AWS EC2 instances. Will start already existing but stopped instances to reuse existing EBS disks. |
| `AwsAsg` | Fleet manager for handling AWS EC2 instances. Uses an EC2 auto-scaling group for controlling the number of running instances. |

#### PoolSizeStrategy (Enum)

Available pool sizing strategies

| Name | Description |
| --- | --- |
| `LeaseUtilization` | Strategy based on lease utilization |
| `JobQueue` | Strategy based on size of job build queue |
| `NoOp` | No-op strategy used as fallback/default behavior |
| `ComputeQueueAwsMetric` | A no-op strategy that reports metrics to let an external AWS auto-scaling policy scale the fleet |
| `LeaseUtilizationAwsMetric` | A no-op strategy that reports metrics to let an external AWS auto-scaling policy scale the fleet |

#### PluginServerConfig

Base class for plugin server config objects |

| Name | Description |
| --- | --- |
| `enabled` | `boolean` Whether the plugin should be enabled or not |

#### AnalyticsServerConfig

Server configuration for the analytics system

| Name | Description |
| --- | --- |
| `sinks` | [TelemetrySinkConfig](/documentation/en-us/unreal-engine/horde-settings-for-unreal-engine#telemetrysinkconfig) Settings for the various telemetry sinks |
| `enabled` | `boolean` Whether the plugin should be enabled or not |

#### TelemetrySinkConfig

Telemetry sinks

| Name | Description |
| --- | --- |
| `epic` | [EpicTelemetryConfig](/documentation/en-us/unreal-engine/horde-settings-for-unreal-engine#epictelemetryconfig) Settings for the Epic telemetry sink |
| `mongo` | [MongoTelemetryConfig](/documentation/en-us/unreal-engine/horde-settings-for-unreal-engine#mongotelemetryconfig) Settings for the MongoDB telemetry sink |

#### EpicTelemetryConfig

Configuration for the telemetry sink

| Name | Description |
| --- | --- |
| `url` | `string` Base URL for the telemetry server |
| `appId` | `string` Application name to send in the event messages |
| `enabled` | `boolean` Whether to enable this sink |

#### MongoTelemetryConfig

Configuration for the telemetry sink

| Name | Description |
| --- | --- |
| `retainDays` | `number` Number of days worth of telmetry events to keep |
| `enabled` | `boolean` Whether to enable this sink |

#### BuildServerConfig

Static configuration for the build plugin

| Name | Description |
| --- | --- |
| `perforce` | [PerforceConnectionSettings](/documentation/en-us/unreal-engine/horde-settings-for-unreal-engine#perforceconnectionsettings)`[]` Perforce connections for use by the Horde server (not agents) |
| `useLocalPerforceEnv` | `boolean` Whether to use the local Perforce environment |
| `perforceConnectionPoolSize` | `integer` Number of pooled perforce connections to keep |
| `enableConformTasks` | `boolean` Whether to enable the conform task source. |
| `p4SwarmUrl` | `string` Url of P4 Swarm installation |
| `jiraUsername` | `string` The Jira service account user name |
| `jiraApiToken` | `string` The Jira service account API token |
| `jiraUrl` | `string` The Uri for the Jira installation |
| `sharedDeviceCheckoutDays` | `integer` The number of days shared device checkouts are held |
| `deviceProblemCooldownMinutes` | `integer` The number of cooldown minutes for device problems |
| `deviceReportChannel` | `string` Channel to send device reports to |
| `disableSchedules` | `boolean` Whether to run scheduled jobs. |
| `slackToken` | `string` Bot token for interacting with Slack (xoxb-\*) |
| `slackSocketToken` | `string` Token for opening a socket to slack (xapp-\*) |
| `slackAdminToken` | `string` Admin user token for Slack (xoxp-\*). This is only required when using the admin endpoints to invite users. |
| `slackUsers` | `string` Filtered list of slack users to send notifications to. Should be Slack user ids, separated by commas. |
| `slackErrorPrefix` | `string` Prefix to use when reporting errors |
| `slackWarningPrefix` | `string` Prefix to use when reporting warnings |
| `configNotificationChannel` | `string` Channel for sending messages related to config update failures |
| `updateStreamsNotificationChannel` | `string` Channel to send stream notification update failures to |
| `jobNotificationChannel` | `string` Slack channel to send job related notifications to. Multiple channels can be specified, separated by ; |
| `agentNotificationChannel` | `string` Slack channel to send agent related notifications to. |
| `testDataRetainMonths` | `integer` The number of months to retain test data |
| `blockCacheDir` | `string` Directory to store the fine-grained block cache. This caches individual exports embedded in bundles. |
| `blockCacheSize` | `string` Maximum size of the block cache. Accepts standard binary suffixes. Currently only allocates in multiples of 1024mb. |
| `blockCacheSizeBytes` | `integer` Accessor for the block cache size in bytes |
| `commits` | [CommitSettings](/documentation/en-us/unreal-engine/horde-settings-for-unreal-engine#commitsettings) Options for the commit service |
| `enabled` | `boolean` Whether the plugin should be enabled or not |

#### PerforceConnectionSettings

Perforce connection information for use by the Horde server (for reading config files, etc...)

| Name | Description |
| --- | --- |
| `id` | `string` Identifier for this server |
| `serverAndPort` | `string` Server and port |
| `credentials` | [PerforceCredentials](/documentation/en-us/unreal-engine/horde-settings-for-unreal-engine#perforcecredentials) Credentials for the server |

#### PerforceCredentials

Credentials for a Perforce user

| Name | Description |
| --- | --- |
| `userName` | `string` The username |
| `password` | `string` Password for the user |
| `ticket` | `string` Login ticket for the user (will be used instead of password if set) |

#### CommitSettings

Options for the commit service

| Name | Description |
| --- | --- |
| `replicateMetadata` | `boolean` Whether to mirror commit metadata to the database |
| `replicateContent` | `boolean` Whether to mirror commit data to storage |
| `bundle` | [BundleOptions](/documentation/en-us/unreal-engine/horde-settings-for-unreal-engine#bundleoptions) Options for how objects are packed together |
| `chunking` | [ChunkingOptions](/documentation/en-us/unreal-engine/horde-settings-for-unreal-engine#chunkingoptions) Options for how objects are sliced |

#### BundleOptions

Options for configuring a bundle serializer

| Name | Description |
| --- | --- |
| `maxVersion` | [BundleVersion](/documentation/en-us/unreal-engine/horde-settings-for-unreal-engine#bundleversion-enum) Maximum version number of bundles to write |
| `maxBlobSize` | `integer` Maximum payload size fo a blob |
| `compressionFormat` | [BundleCompressionFormat](/documentation/en-us/unreal-engine/horde-settings-for-unreal-engine#bundlecompressionformat-enum) Compression format to use |
| `minCompressionPacketSize` | `integer` Minimum size of a block to be compressed |
| `maxWriteQueueLength` | `integer` Maximum amount of data to store in memory. This includes any background writes as well as bundles being built. |

#### BundleVersion (Enum)

Bundle version number

| Name | Description |
| --- | --- |
| `Initial` | Initial version number |
| `ExportAliases` | Added the BundleExport.Alias property |
| `RemoveAliases` | Back out change to include aliases. Will likely do this through an API rather than baked into the data. |
| `InPlace` | Use data structures which support in-place reading and writing. |
| `ImportHashes` | Add import hashes to imported nodes |
| `LatestV1` | Last version using the V1 pipeline |
| `PacketSequence` | Structure bundles as a sequence of self-contained packets (uses V2 code) |
| `Latest` | The current version number |
| `LatestV2` | Last version using the V2 pipeline |
| `LatestPlusOne` | Last item in the enum. Used for |

#### BundleCompressionFormat (Enum)

Indicates the compression format in the bundle

| Name | Description |
| --- | --- |
| `None` | Packets are uncompressed |
| `LZ4` | LZ4 compression |
| `Gzip` | Gzip compression |
| `Oodle` | Oodle compression (Selkie) |
| `Brotli` | Brotli compression |
| `Zstd` | ZStandard compression |

#### ChunkingOptions

Options for creating file nodes

| Name | Description |
| --- | --- |
| `leafOptions` | [LeafChunkedDataNodeOptions](/documentation/en-us/unreal-engine/horde-settings-for-unreal-engine#leafchunkeddatanodeoptions) Options for creating leaf nodes |
| `interiorOptions` | [InteriorChunkedDataNodeOptions](/documentation/en-us/unreal-engine/horde-settings-for-unreal-engine#interiorchunkeddatanodeoptions) Options for creating interior nodes |

#### LeafChunkedDataNodeOptions

Options for creating a specific type of file nodes

| Name | Description |
| --- | --- |
| `minSize` | `integer` Minimum chunk size |
| `maxSize` | `integer` Maximum chunk size. Chunks will be split on this boundary if another match is not found. |
| `targetSize` | `integer` Target chunk size for content-slicing |

#### InteriorChunkedDataNodeOptions

Options for creating interior nodes

| Name | Description |
| --- | --- |
| `minChildCount` | `integer` Minimum number of children in each node |
| `targetChildCount` | `integer` Target number of children in each node |
| `maxChildCount` | `integer` Maximum number of children in each node |
| `sliceThreshold` | `integer` Threshold hash value for splitting interior nodes |

#### StorageServerConfig

Static settings for the storage system

| Name | Description |
| --- | --- |
| `bundleCacheDir` | `string` Directory to use for the coarse-grained backend cache. This caches full bundles downloaded from the upstream object store. |
| `bundleCacheSize` | `string` Maximum size of the storage cache on disk. Accepts standard binary suffixes (kb, mb, gb, tb, etc...) |
| `bundleCacheSizeBytes` | `integer` Accessor for the bundle cache size in bytes |
| `backends` | [BackendConfig](/documentation/en-us/unreal-engine/horde-settings-for-unreal-engine#backendconfig)`[]` Overridden settings for storage backends. Useful for running against a production server with custom backends. |
| `enabled` | `boolean` Whether the plugin should be enabled or not |

#### BackendConfig

Common settings object for different providers

| Name | Description |
| --- | --- |
| `id` | `string` The storage backend ID |
| `base` | `string` Base backend to copy default settings from |
| `secondary` | `string` Specifies another backend to read from if an object is not found in this one. Can be used when migrating data from one backend to another. |
| `type` | [StorageBackendType](/documentation/en-us/unreal-engine/horde-settings-for-unreal-engine#storagebackendtype-enum) |
| `baseDir` | `string` |
| `awsBucketName` | `string` Name of the bucket to use |
| `awsBucketPath` | `string` Base path within the bucket |
| `awsCredentials` | [AwsCredentialsType](/documentation/en-us/unreal-engine/horde-settings-for-unreal-engine#awscredentialstype-enum) Type of credentials to use |
| `awsRole` | `string` ARN of a role to assume |
| `awsProfile` | `string` The AWS profile to read credentials form |
| `awsRegion` | `string` Region to connect to |
| `azureConnectionString` | `string` Connection string for Azure |
| `azureContainerName` | `string` Name of the container |
| `relayServer` | `string` |
| `relayToken` | `string` |
| `gcsBucketName` | `string` Name of the GCS bucket to use |
| `gcsBucketPath` | `string` Base path within the bucket |

#### StorageBackendType (Enum)

Types of storage backend to use

| Name | Description |
| --- | --- |
| `FileSystem` | Local filesystem |
| `Aws` | AWS S3 |
| `Azure` | Azure blob store |
| `Gcs` | Google Cloud Storage |
| `Memory` | In-memory only (for testing) |

#### AwsCredentialsType (Enum)

Credentials to use for AWS

| Name | Description |
| --- | --- |
| `Default` | Use default credentials from the AWS SDK |
| `Profile` | Read credentials from the profile in the AWS config file |
| `AssumeRole` | Assume a particular role. Should specify ARN in |
| `AssumeRoleWebIdentity` | Assume a particular role using the current environment variables. |

#### ToolsServerConfig

Server configuration for bundled tools

| Name | Description |
| --- | --- |
| `bundledTools` | [BundledToolConfig](/documentation/en-us/unreal-engine/horde-settings-for-unreal-engine#bundledtoolconfig)`[]` Tools bundled along with the server. Data for each tool can be produced using the 'bundle create' command, and should be stored in the Tools directory. |
| `enabled` | `boolean` Whether the plugin should be enabled or not |

#### BundledToolConfig

Configuration for a tool bundled alongsize the server

| Name | Description |
| --- | --- |
| `version` | `string` Version string for the current tool data |
| `refName` | `string` Ref name in the tools directory |
| `dataDir` | `string` Directory containing blob data for this tool. If empty, the tools/{id} folder next to the server will be used. |
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
| `acl` | [AclConfig](/documentation/en-us/unreal-engine/horde-settings-for-unreal-engine#aclconfig) Permissions for the tool |

#### AclConfig

Parameters to update an ACL

| Name | Description |
| --- | --- |
| `entries` | [AclEntryConfig](/documentation/en-us/unreal-engine/horde-settings-for-unreal-engine#aclentryconfig)`[]` Entries to replace the existing ACL |
| `profiles` | [AclProfileConfig](/documentation/en-us/unreal-engine/horde-settings-for-unreal-engine#aclprofileconfig)`[]` Defines profiles which allow grouping sets of actions into named collections |
| `inherit` | `boolean` Whether to inherit permissions from the parent ACL |
| `exceptions` | `string[]` List of exceptions to the inherited setting |

#### AclEntryConfig

Individual entry in an ACL

| Name | Description |
| --- | --- |
| `claim` | [AclClaimConfig](/documentation/en-us/unreal-engine/horde-settings-for-unreal-engine#aclclaimconfig) Name of the user or group |
| `actions` | `string[]` Array of actions to allow |
| `profiles` | `string[]` List of profiles to grant |

#### AclClaimConfig

New claim to create

| Name | Description |
| --- | --- |
| `type` | `string` The claim type |
| `value` | `string` The claim value |

#### AclProfileConfig

Configuration for an ACL profile. This defines a preset group of actions which can be given to a user via an ACL entry.

| Name | Description |
| --- | --- |
| `id` | `string` Identifier for this profile |
| `actions` | `string[]` Actions to include |
| `excludeActions` | `string[]` Actions to exclude from the inherited actions |
| `extends` | `string[]` Other profiles to extend from |

## Agent Settings

### Agent.json (Agent)

All Horde-specific settings are stored in a root object called `Horde`. Other .NET functionality may be configured using properties in the root of this file.

| Name | Description |
| --- | --- |
| `serverProfiles` | `string` `->` [ServerProfile](/documentation/en-us/unreal-engine/horde-settings-for-unreal-engine#serverprofile) Known servers to connect to |
| `server` | `string` The default server, unless overridden from the command line |
| `name` | `string` Name of agent to report as when connecting to server. By default, the computer's hostname will be used. |
| `installed` | `boolean` Whether the server is running in 'installed' mode. In this mode, on Windows, the default data directory will use the common application data folder (C:\\ProgramData\\Epic\\Horde), and configuration data will be read from here and the registry. This setting is overridden to false for local builds from appsettings.Local.json. |
| `ephemeral` | `boolean` Whether agent should register as being ephemeral. Doing so will not persist any long-lived data on the server and once disconnected it's assumed to have been deleted permanently. Ideal for short-lived agents, such as spot instances on AWS EC2. |
| `workingDir` | [DirectoryReference](/documentation/en-us/unreal-engine/horde-settings-for-unreal-engine#directoryreference) Working directory for leases and jobs (i.e where files from Perforce will be checked out) |
| `logsDir` | [DirectoryReference](/documentation/en-us/unreal-engine/horde-settings-for-unreal-engine#directoryreference) Directory where agent and lease logs are written |
| `shareMountingEnabled` | `boolean` Whether to mount the specified list of network shares |
| `shares` | [MountNetworkShare](/documentation/en-us/unreal-engine/horde-settings-for-unreal-engine#mountnetworkshare)`[]` List of network shares to mount |
| `wineExecutablePath` | `string` Path to Wine executable. If null, execution under Wine is disabled |
| `containerEngineExecutablePath` | `string` Path to container engine executable, such as /usr/bin/podman. If null, execution of compute workloads inside a container is disabled |
| `writeStepOutputToLogger` | `boolean` Whether to write step output to the logging device |
| `enableAwsEc2Support` | `boolean` Queries information about the current agent through the AWS EC2 interface |
| `useLocalStorageClient` | `boolean` Option to use a local storage client rather than connecting through the server. Primarily for convenience when debugging / iterating locally. |
| `computeIp` | `string` Incoming IP for listening for compute work. If not set, it will be automatically resolved. |
| `computePort` | `integer` Incoming port for listening for compute work. Needs to be tied with a lease. Set port to 0 to disable incoming compute requests. |
| `openTelemetry` | [OpenTelemetrySettings](/documentation/en-us/unreal-engine/horde-settings-for-unreal-engine#opentelemetrysettings) Options for OpenTelemetry |
| `enableTelemetry` | `boolean` Whether to send telemetry back to Horde server |
| `telemetryReportInterval` | `integer` How often to report telemetry events to server in milliseconds |
| `bundleCacheSize` | `integer` Maximum size of the bundle cache, in megabytes. |
| `cpuCount` | `integer` Maximum number of logical CPU cores workloads should use Currently this is only provided as a hint and requires leases to respect this value as it's set via an env variable (UE\_HORDE\_CPU\_COUNT). |
| `cpuMultiplier` | `number` CPU core multiplier applied to CPU core count setting For example, 32 CPU cores and a multiplier of 0.5 results in max 16 CPU usage. |
| `properties` | `string` `->` `string` Key/value properties in addition to those set internally by the agent |

#### ServerProfile

Information about a server to use

| Name | Description |
| --- | --- |
| `name` | `string` Name of this server profile |
| `environment` | `string` Name of the environment (currently just used for tracing) |
| `url` | `string` Url of the server |
| `token` | `string` Bearer token to use to initiate the connection |
| `thumbprint` | `string` Thumbprint of a certificate to trust. Allows using self-signed certs for the server. |
| `thumbprints` | `string[]` Thumbprints of certificates to trust. Allows using self-signed certs for the server. |

#### DirectoryReference

Representation of an absolute directory path. Allows fast hashing and comparisons.

| Name | Description |
| --- | --- |
| `parentDirectory` | [DirectoryReference](/documentation/en-us/unreal-engine/horde-settings-for-unreal-engine#directoryreference) Gets the directory containing this object |
| `fullName` | `string` The path to this object. Stored as an absolute path, with O/S preferred separator characters, and no trailing slash for directories. |

#### MountNetworkShare

Describes a network share to mount

| Name | Description |
| --- | --- |
| `mountPoint` | `string` Where the share should be mounted on the local machine. Must be a drive letter for Windows. |
| `remotePath` | `string` Path to the remote resource |

#### OpenTelemetrySettings

OpenTelemetry configuration for collection and sending of traces and metrics.

| Name | Description |
| --- | --- |
| `enabled` | `boolean` Whether OpenTelemetry exporting is enabled |
| `serviceName` | `string` Service name |
| `serviceNamespace` | `string` Service namespace |
| `serviceVersion` | `string` Service version |
| `enableDatadogCompatibility` | `boolean` Whether to enrich and format telemetry to fit presentation in Datadog |
| `attributes` | `string` `->` `string` Extra attributes to set |
| `enableConsoleExporter` | `boolean` Whether to enable the console exporter (for debugging purposes) |
| `protocolExporters` | `string` `->` [OpenTelemetryProtocolExporterSettings](/documentation/en-us/unreal-engine/horde-settings-for-unreal-engine#opentelemetryprotocolexportersettings) Protocol exporters (key is a unique and arbitrary name) |

#### OpenTelemetryProtocolExporterSettings

Configuration for an OpenTelemetry exporter

| Name | Description |
| --- | --- |
| `endpoint` | `string` Endpoint URL. Usually differs depending on protocol used. |
| `protocol` | `string` Protocol for the exporter ('grpc' or 'httpprotobuf') |