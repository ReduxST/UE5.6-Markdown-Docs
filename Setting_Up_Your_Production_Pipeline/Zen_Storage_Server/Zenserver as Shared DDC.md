# Zenserver as Shared DDC

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/set-up-zen-storage-server-as-shared-ddc-for-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/set-up-zen-storage-server-as-shared-ddc-for-unreal-engine)  
**Processed:** 2025-06-14 16:48:56

---

Before taking steps to use Zenserver as a shared DDC, it is important to be clear on the appropriate environment for it. Zenserver is an **unauthenticated** storage server.

While authentication might be added in the future, it is currently targeted for use in a trusted environment like an office LAN or VPN, where every user who is able to reach Zenserver is permitted full read/write/delete access to its contents.

Use of Zenserver in public (for example, the Internet) or on untrusted network environments is not advised, and could lead to data leaks, data corruption or poisoning, or data loss for DDC or other data stored within Zenserver.

If you are seeking a storage server for use in public internet or untrusted network environments, see the [Unreal Cloud DDC](/documentation/en-us/unreal-engine/how-to-set-up-a-cloud-type-derived-data-cache-for-unreal-engine) technology, which is appropriate for that use case, and can be combined in a DDC graph along with Zenserver-shared DDC instance(s).

Historically, shared DDCs have been implemented in offices, studios, or VPNs using a network fileshare hosted within the LAN, or on a nearby cloud host that is only accessible from the LAN. Commonly, this would be a CIFS/SMB fileshare hosted either natively on a Windows server, or via a Samba or equivalent technology on a Linux server. This type of DDC storage is appropriate to replace Zenserver as a shared DDC.

## How Zenserver-shared DDC Fits a DDC Graph and Network

The [Derived Data Cache (DDC)](/documentation/en-us/unreal-engine/using-derived-data-cache-in-unreal-engine) document provides an overview of the DDC technology and introduces required prerequisite knowledge. In thinking about how Zenserver-shared DDC fits into the DDC graph for your organization or project, consider three main layers in the DDC graph:

1.  Cloud
    
2.  Shared
    
3.  Local
    

There are good reasons to potentially have other layers in the graph, such as a Pak layer, and there are other implied layers like a memory layer, but for the sake of planning use of Zen Shared DDC, it is sufficient to just consider these three in isolation.

Not every use case will need all three of these layers, but the expectation if they are present is that they are structured as:

1.  Cloud - UE cloud DDC, 20 ms to 100 ms latency, authenticated, available on public internet anywhere, with data replication between regional instances.
    
2.  Shared - Fileshare DDC or Zenserver-shared DDC, 1 ms to 60 ms latency, unauthenticated, available only on LAN or VPN, with one instance per office or region where users/staff are clustered.
    
3.  Local - Zenserver local DDC (default in UE5.4 and later), 0.1 ms to 10 ms latency, unauthenticated and limited to loopback/localhost service, available only on each workstation.
    

If you are a single user, you might only have the local layer.

If you are a medium-sized team in one region, you might have local and shared within your office or in a cloud host for your region available via VPN.

If you are a large organization with teams at multiple regions, you should have local, shared, and cloud DDC layers, with a Zenserver-shared DDC instance in each regional office and the cloud layer permitting sharing of cache data globally and providing replication across regions.

**Example**: You are an organization with staff in three office locations: Montreal, Seattle, and Denver, and a cloud-hosted buildfarm in US-East that produces cooked data builds. Each location has 50+ staff. An optimal setup would be:

1.  **Cloud** - UE cloud DDC setup on a cloud hosting provider available on public internet with instances in US-East and US-West and bidirectional replication between the two.
    
2.  **Shared** - A single host (physical machine or virtual machine) in each of the three regional offices (Montreal, Seattle, and Denver) for Zenserver-shared DDC, without any replication happening between them, and one Zenserver-shared DDC instance hosted privately in the same cloud host and region as your cloud-hosted buildfarm
    
3.  **Local** - Zen Local DDC being used by default on each user's workstation.
    

Example Cloud DDC servers (with bi-directional replication):

-   US-East cloud DDC instance
    
-   US-West cloud DDC instance
    

Example Zenserver-shared DDC servers:

-   Montreal onsite machine
    
-   Seattle onsite machine
    
-   Denver onsite machine
    
-   US-East cloud-hosted buildfarm machine
    

This arrangement gives the organization a global replicated caching layer, a LAN-speed sharing layer that avoids large amounts of network traffic ingress for sharing within a single office, and an efficient local caching layer. When the buildfarm cooks, it will write any new DDC data to its shared layer and also to the cloud layer, which will then replicate it to other region(s) and be available to users in those regions.

## Setting Up a Shared DDC Server with Zenserver

### Hardware

The specifications for your shared DDC server are going to be tailored and tuned to the specifics of your organization and dataset. Within Epic, we have found that it makes sense to bias for more memory and IO capabilities than for CPU core count or single core speed.

For comparison, our hardware specs are:

Large-sized office (a few hundred developers):

-   8 core CPU w/ hyperthreading (16 logical processors) @ 2.40 GHz
    
-   64 GB RAM
    
-   4 TB SSD separate from system drive, biased toward high IOPS and throughput if virtual disk
    
-   10 Gbps LAN link preferred
    

Most of the memory usage will not be consumed by the Zenserver process itself, but its presence will make the OS-level file caching (standby memory) more effective.

For a buildfarm environment, we disable the local DDC entirely and rely more on heavy usage of the shared DDC from every buildfarm machine that does cooking. In this very heavy usage scenario, we rely on higher specs on the cloud-hosted Zenserver-shared DDC server:

-   24 core CPU w/ hyperthreading (48 logical processors) @ 3.80 GHz
    
-   192 GB RAM
    
-   12 TB SSD separate from system drive, biased toward high IOPS and throughput if virtual disk
    
-   100 Gbps LAN link available within the cloud zone
    

The specifications above are not minimum requirements but are recommended configurations based on Epic Games' internal needs. Zenserver will run on much lower hardware specifications that are appropriate for smaller teams.

We recommended keeping the Zenserver data on a separate drive from the operating system to:

-   Allow for easier expansion/replacement of the Zenserver data drive in the future.
    
-   Avoid out-of-disk-space issues leading to the system becoming unusable.
    

If you are replacing an existing fileshare DDC with a Zenserver-shared DDC, best practice is to:

1.  **Match disk size** - Whatever the disk capacity/quota for DDC on the fileshare is the disk capacity/quota to allow for a Zenserver-shared DDC as its disk space needs should be the same.
    
2.  **Match or improve proximity/network latency** - DDC is sensitive to the latency of communications between the server and connecting clients. The change from a fileshare DDC to a Zenserver-shared DDC should keep the host hardware at equal proximity or latency for users to avoid any regression in user experience. If you have fileshare DDCs in multiple regions, plan for a 1-to-1 duplication for a Zenserver-shared DDC host in each of the regions in which you have a fileshare DDC host. Once the Zenserver-shared DDCs are online and in use by all projects, you can consider downsizing or eliminating the fileshare DDCs.
    

### Software

We recommend a Windows Server data center for the operating system (2019 in extended support, or 2022 in mainstream support at the time of writing, with newer versions appropriate for consideration on release), but Zenserver is capable of operating on the same supported Windows versions (Desktop and Server editions) as Unreal Engine.

Zenserver is available for Windows, Linux, and Mac. However, only the Windows version is considered production-ready for shared DDC usage in UE5.5, and has been used extensively in production within Epic.

Linux Zenserver is usable for local DDC, and future UE releases are expected to have Zenserver on Linux to reach production readiness for shared DDC after further tuning, optimization, and testing.

## Version Compatibility and Multiple Project Considerations

Zenserver is designed to be backward compatible. This means that you can take the Zenserver executables included in the Engine\\Binaries\\ directory of the engine release you’re using and use that version of Zenserver for your shared DDC. If you are in an environment where there are multiple projects on different versions of Unreal Engine, you can still share a Zenserver between projects as long as you run the Zenserver version from the newest Unreal Engine release you’re using. The newest version of Zenserver will be compatible with older versions of Unreal Engine.

Zenserver is developed and released in an isolated environment from Unreal Engine, and is mirrored to the git repo under the Unreal Engine organization [https://github.com/EpicGames/zen/](https://github.com/EpicGames/zen/).

Accessing the Zenserver repository requires access to the Epic repository which can be obtained [here](https://www.unrealengine.com/en-US/ue-on-github). Releases are published to the zen repository. If users want to evaluate a newer revision of Zenserver on their shared DDC, they can obtain newer releases in the GitHub repository, as they will be backward compatible with their current Unreal Engine release.

Running newer releases of Zenserver from the GitHub repository should not be done in production. Always evaluate newer releases on non-production shared DDC instances only.

Zenserver uses its own version numbering scheme that can differ from engine version numbering. When taking releases of Zenserver, always inspect the version number on the executable you have and compare it with the version of the release you’re obtaining. You should always go forward in version numbers, not backward.

## Network Infrastructure

At this time, the guidance for Zen as a shared DDC is that it not be put behind a load balancer. The current design of the server allows a single instance to serve heavy workloads, and it should be able to serve large team workloads for a project within a single studio or buildfarm location.

As noted previously, the expectation is that the Zenserver-shared DDC exists within a hierarchical cache that can also contain cloud and local layers. If you have either cloud or local layers in your cache, downtime of the shared layer is not expected to compromise Unreal Engine’s access to the cache, but just reduces cache latency/performance for the duration of the downtime.

Communication with Zenserver is currently done via unencrypted HTTP1.1 on port 8558 by default. The Unreal Engine DDC client for Zenserver will bypass any client proxy configuration and attempt direct connection to the configured Zenserver host(s). It is advised that you allow direct non-proxied access between the Zenserver and the Unreal Engine client, but if you want to use an HTTP proxy, you can configure the Zenserver-shared DDC graph node in the Unreal Engine INIs to include a **BypassProxy=false** parameter.

Future versions of Unreal Engine and Zenserver may change or add additional communication protocols on other ports. It is essential that firewalls or traffic shaping on your network allow for fast and efficient communication between Zenserver and the Unreal Engine client. Otherwise, the editor, cook, and pak functionality may experience slow performance.

## Server Setup/Update (Windows)

During the setup/update process, two distinct folders are referenced. Their location is chosen by you, but there is guidance on where you put them.

-   **{ZenInstall}** - This is the folder that will contain the executables and configuration. It can be put on the system drive or elsewhere. It expects to be read-only under normal usage, and is only modified when upgrading to newer versions of Zenserver.
    
-   **{ZenData}** - this is the folder that will contain the operating data for Zenserver. It is preferable to put this **off** the system drive. It eExpects to be read-write under normal usage.
    

Aside from folders, you will have to select the user that Zenserver will run as (hereafter referred to as **{ZenUser}** and expect to have a password known as **{ZenPassword}**).

You can choose to run Zenserver as a non-admin user, and there are security advantages to doing so. If running as a non-admin user, it assumed that you have prepared the environment for use by this user by ensuring:

-   {ZenUser} has **"log on as a service"** permission
    
-   {ZenUser} has read access to the {ZenInstall} directory
    
-   {ZenUser} has read+write access to the {ZenData} directory
    
-   {ZenUser} has been granted URL reservation for the entire endpoint space under port 8558 in the http.sys urlacl system. This can be granted by issuing this command once on an elevated command prompt:
    

Command Line

```
	`netsh http add urlacl url=http://*:8558/ user={ZenUser}`
Copy full snippet
```
netsh http add urlacl url=http://\*:8558/ user={ZenUser}

To setup/update a machine as a Zenserver-shared DDC:

1.  Stop the Zen Store (Zenserver) service if it is running by issuing the following command:
    
    Command Line
    
    ```
         `sc stop "Zen Store"`
    Copy full snippet
    ```
    sc stop "Zen Store"
2.  Copy the following files from your depot to the chosen {ZenInstall} folder on the server host machine:
    
    -   `Engine\Binaries\Win64\zenserver.exe`
        
    -   `Engine\Binaries\Win64\zenserver.pdb`
        
    -   `Engine\Binaries\Win64\crashpad_handler.exe`
        
    -   `Engine\Binaries\Win64\zen.exe`
        
    -   `Engine\Binaries\Win64\zen.pdb`
        
    
    The files will be flattened into the {ZenInstall} folder and should not be in any subdirectories of the selected {ZenInstall} folder.
    
3.  Copy the following Zenserverconfig file template to {ZenInstall}\\zen\_config.lua to use as a starting point.
    
    zen\_config.lua
    
    ```
         `-- Zen Store Lua config       server = {           dedicated = true,           datadir = "{ZenData}",           abslog = "{ZenData}\\local.log",           debug = false,           sentry = {               disable = false,               allowpersonalinfo = false,           }       }       network = {           httpserverclass = "httpsys", -- httpsys|asio           port = 8558,       }       gc = {           intervalseconds = 28800, -- every 8 hour           lightweightintervalseconds = 3600, -- every hour           cache = {               maxdurationseconds = 864000, -- 10 days           }       }       cache = {           enable = true,           accesslog = false,           upstream = {               upstreamthreadcount = 4,               policy = "disabled", -- readwrite|readonly|writeonly|disabled           },           memlayer = {               targetfootprint = 1073741824, -- 1 GB               triminterval = 120, -- max every 2 minutes               maxage = 172800, -- 2 days           }       }`
    Copy full snippet
    ```
    \-- Zen Store Lua config server = { dedicated = true, datadir = "{ZenData}", abslog = "{ZenData}\\\\local.log", debug = false, sentry = { disable = false, allowpersonalinfo = false, } } network = { httpserverclass = "httpsys", -- httpsys|asio port = 8558, } gc = { intervalseconds = 28800, -- every 8 hour lightweightintervalseconds = 3600, -- every hour cache = { maxdurationseconds = 864000, -- 10 days } } cache = { enable = true, accesslog = false, upstream = { upstreamthreadcount = 4, policy = "disabled", -- readwrite|readonly|writeonly|disabled }, memlayer = { targetfootprint = 1073741824, -- 1 GB triminterval = 120, -- max every 2 minutes maxage = 172800, -- 2 days } }
4.  Modify your zen\_config.lua to ensure that:
    
    -   `server\data_dir` is set to be equal to your {ZenData} directory with **all backslashes replaced with double backslashes** (for example `C:\myfolder\mysubfolder` becomes `C:\\myfolder\\mysubfolder`).
        
    -   `server\abslog` is set to be the path to a location that can be used to write the log file with **all backslashes replaced with double backslashes** (for example `C:\myfolder\mysubfolder\local.log` becomes `C:\\myfolder\\mysubfolder\\local.log`).
        
    
    Also make an informed choice about whether you want to share crash information for Zenserver with Epic Games using the Sentry service:
    
    -   `server\sentry\disable` is false in the configuration above, meaning that crash information for Zenserver will be shared with Epic Games using the Sentry service. If you want to prevent that, you can set this value to true.
        
    -   `server\sentry\allowpersonalinfo` is false to prevent upload of logs or usernames to the crash recording system in case of crash. If sentry is not disabled, crash records will still be sent to Epic Games when this value is set to false, but they will not include logs, usernames, or other potentially identifiable information.
        
    
    When modifying the `zen_config.lua` file, remember:
    
    -   Escape special characters like backslashes with a preceding backslash.
        
    -   Encompass string values in double quotes.
        
    -   Retain commas following fields or structure endings.
        
    -   Comments are prefixed with double dash "**\--**" and everything on the line after the double dash is ignored.
        
5.  Ensure Zenserver is installed as a service that automatically runs on startup and restarts upon failure. This can be accomplished from an elevated command prompt with the following commands:
    
    Command Line
    
    ```
         `sc create "Zen Store" start=auto binpath="{ZenInstall}\zenserver.exe --config={ZenInstall}\zen_config.lua" obj={ZenUser} password={ZenPassword} 		      sc failure "Zen Store" reset=60 actions=restart/60000`
    Copy full snippet
    ```
    sc create "Zen Store" start=auto binpath="{ZenInstall}\\zenserver.exe --config={ZenInstall}\\zen\_config.lua" obj={ZenUser} password={ZenPassword} sc failure "Zen Store" reset=60 actions=restart/60000
    
    If running as the system user, you can omit the `obj={ZenUser} password={ZenPassword}` portion of the command line.
    
6.  Start Zenserver service using the following command:
    
    Command Line
    
    ```
         `sc start "Zen Store"`
    Copy full snippet
    ```
    sc start "Zen Store"
7.  Confirm that zenserver.exe is running and reachable by:
    
    -   Checking for its presence in the task manager.
        
    -   Opening `http://localhost:8558/dashboard` in your browser on the server host machine and ensuring it is responding.
        
    -   Opening `http://<public_hostname_or_ip>:8558/dashboard` in your browser on another machine in your network and ensuring it is responding.
        
    
    If the process is not running, check the configured log location and see if the log file indicates the issue.
    
    If the process is running and reachable as localhost but not using , then ensure you’ve configured the `http.sys` URL reservation noted earlier in the setup steps.
    
8.  Restart the server host machine and ensure that Zenserver starts up automatically on boot.
    

## Setting Up Unreal Engine Client to Use Your Zenserver-shared DDC Server

### Understanding and Selecting Namespaces

Namespaces are a feature of both Zenserver-shared DDC and UE cloud DDC. They are used to separate DDC data for projects into separate logical spaces that can have [separate access permissions in UE Cloud DDC](/documentation/en-us/unreal-engine/how-to-set-up-a-cloud-type-derived-data-cache-for-unreal-engine#namespaceaccess).

Zenserver does not currently enforce the access controls for namespaces (all users can access all data regardless of what namespace it is in). However, it does keep the data in one namespace semi-distinct from the data in another namespace.

There is a content-addressable storage layer that allows for de-duplication of bytes, but two DDC keys are permitted to store different data blobs in two namespaces, and writing to the key in one namespace doesn’t influence the key in another namespace.

Multiple projects can share one namespace, but the general rule of thumb is that if you want to have some difference in who can access the data for a project, you should give that project a distinct namespace. Zenserver and Unreal Cloud DDC will accept arbitrary namespace names that adhere to these restrictions:

-   64 characters or less
    
-   Does not start or end with a period
    
-   Consists of lowercase latin alphanumeric characters (a through z, 0 through 9) or the dash (-), underscore (\_), or dot (.) characters
    

### Standard Configuration

Once the server has been set up and is confirmed to be reachable in a web browser, you can change the configuration for one or more of your Unreal Engine projects to make use of the server. To accomplish this, you will focus on the `[DerivedDataBackendGraph]` and `[StorageServers]` section of the DefaultEngine.ini for your project(s).

The stock configuration in `BaseEngine.ini` specifies two named shared layers:

-   **Shared** \- Configured as a traditional fileshare DDC (type=FileSystem)
    
-   **ZenShared** - Configured as a Zenserver-shared DDC (type=Zen)
    

It is important to note that ZenShared has a special feature that allows it to redirect its configuration to the `[StorageServers]` section of the config using a `ServerID=<StorageServersKeyName>` parameter. Specifically, it uses `ServerID=Shared` to redirect to the shared key under `[StorageServers]`.

The base/stock configuration of `StorageServers\Shared` looks like this:

BaseEngine.ini

```
	`[StorageServers]  	Shared=(Host=**None**, Namespace="**ue.ddc**", EnvHostOverride=UE-ZenSharedDataCacheHost, CommandLineHostOverride=ZenSharedDataCacheHost, DeactivateAt=60)`
Copy full snippet
```
\[StorageServers\] Shared=(Host=\*\*None\*\*, Namespace="\*\*ue.ddc\*\*", EnvHostOverride=UE-ZenSharedDataCacheHost, CommandLineHostOverride=ZenSharedDataCacheHost, DeactivateAt=60)

There is an extensive comment in `BaseEngine.ini` that explains the parameters available on each entry. However, for the purposes of getting set up, you will focus on two parameters in particular:

-   **Host:** The URL for the server to connect to. Locally autolaunched Zen instances can exclude this. For example: `http://sharedzen.example.com:8558`.
    
-   **Namespace:** The cache namespace to use on the server (required).
    

To get Unreal Engine to use the Zen-shared DDC, you must copy the stock configuration for this line from BaseEngine.ini, paste it into our project’s `DefaultEngine.ini` file, then modify it to specify a Host and Namespace appropriate for our environment. For example:

BaseEngine.ini

```
	`[StorageServers]  	Shared=(Host="**http://public_hostname_or_ip:8558”**, Namespace="**myproject.ddc**", EnvHostOverride=UE-ZenSharedDataCacheHost, CommandLineHostOverride=ZenSharedDataCacheHost, DeactivateAt=60)`
Copy full snippet
```
\[StorageServers\] Shared=(Host="\*\*http://public\_hostname\_or\_ip:8558”\*\*, Namespace="\*\*myproject.ddc\*\*", EnvHostOverride=UE-ZenSharedDataCacheHost, CommandLineHostOverride=ZenSharedDataCacheHost, DeactivateAt=60)

In this example, we are configuring Unreal Engine to connect to a Zenserver-shared DDC at hostname `public_hostname_or_ip` on port 8558, and we’re instructing it to store the DDC data in a namespace with the name `myproject.ddc`.

When you have this configuration in your `DefaultEngine.ini` file, you can launch your game editor and check the log to confirm the presence of the following log line:

Log Output

```
	`LogDerivedDataCache: Display: ZenShared: Using ZenServer HTTP service at http://public_hostname_or_ip:8558/ with namespace myproject.ddc status: OK!.`
Copy full snippet
```
LogDerivedDataCache: Display: ZenShared: Using ZenServer HTTP service at http://public\_hostname\_or\_ip:8558/ with namespace myproject.ddc status: OK!.

With this confirmation, you are now successfully using Zenserver-shared DDC, and if you had a fileshare DDC, it could be in use at the same time.

If you have a fileshare DDC that is populated with past data, we suggest that you run with both the fileshare DDC and Zenserver-shared DDC for a transition period of two weeks. After that time, it is appropriate to consider disabling use of the fileshare DDC by setting it to have a `Path=None` in your project’s `DefaultEngine.ini`, or removing it entirely from your project’s graph by overriding this base set of graph nodes:

DefaultEngine.ini

```
	`Root=(Type=Hierarchical, Inner=Pak, Inner=EnginePak, Inner=ZenLocal, Inner=Local, Inner=ZenShared**, Inner=Shared**, Inner=Cloud)`
Copy full snippet
```
Root=(Type=Hierarchical, Inner=Pak, Inner=EnginePak, Inner=ZenLocal, Inner=Local, Inner=ZenShared\*\*, Inner=Shared\*\*, Inner=Cloud)

So that Shared is no longer in the list, like this:

DefaultEngine.ini

```
	`Root=(Type=Hierarchical, Inner=Pak, Inner=EnginePak, Inner=ZenLocal, Inner=Local, Inner=ZenShared, Inner=Cloud)`
Copy full snippet
```
Root=(Type=Hierarchical, Inner=Pak, Inner=EnginePak, Inner=ZenLocal, Inner=Local, Inner=ZenShared, Inner=Cloud)

If you are setting up a Zenserver-shared DDC and have no historical fileshare DDC, there is no need for the two-week transition period, and you can remove Shared from the list immediately.

### Multi-Region Configuration

If you have users spread out over multiple regions, you may have a fileshare DDC per region/office. Moving over to a Zenserver-shared DDC will mean setting up a Zenserver-shared DDC in each region/office, then choosing a strategy to have each Unreal Engine client choose the regionally appropriate server. This choosing of regionally appropriate servers can be done in different ways.

-   It can be accomplished using an environment variable that is set on the machines per office/region using group policy, or alternative mechanisms, such as:
    
    -   Environment variable in Seattle: `UE-ZenSharedDataCacheHost=seattle-zen.domain.com`
        
    -   Environment variable in Denver: `UE-ZenSharedDataCacheHost=denver-zen.domain.com`
        
    -   Environment variable in Montreal: `E-ZenSharedDataCacheHost=montreal-zen.domain.com`
        
-   It can be accomplished using site-specific DNS that allows the same hostname to direct to different IP addresses at different sites.
    

## Using Redirection from Shared to Zenserver-Shared

A final option to consider is using a redirection mechanism to have Unreal Engine automatically switch from using a fileshare DDC over to using a Zenserver-shared DDC. Redirection can be set up by overriding your fileshare DDC configuration from this:

ddc.ini

```
	`Shared=(Type=FileSystem, UnusedFileAge=10, FoldersToClean=10, ConsiderSlowAt=70, Path=?EpicDDC, EnvPathOverride=UE-SharedDataCachePath, EditorOverrideSetting=SharedDerivedDataCache, CommandLineOverride=SharedDataCachePath)`
Copy full snippet
```
Shared=(Type=FileSystem, UnusedFileAge=10, FoldersToClean=10, ConsiderSlowAt=70, Path=?EpicDDC, EnvPathOverride=UE-SharedDataCachePath, EditorOverrideSetting=SharedDerivedDataCache, CommandLineOverride=SharedDataCachePath)

To this:

ddc.ini

```
	`Shared=(Type=FileSystem, UnusedFileAge=10, FoldersToClean=10, ConsiderSlowAt=70, Path=?EpicDDC, EnvPathOverride=UE-SharedDataCachePath, EditorOverrideSetting=SharedDerivedDataCache, CommandLineOverride=SharedDataCachePath**, RedirectionFileName=ddc.ini**)`
Copy full snippet
```
Shared=(Type=FileSystem, UnusedFileAge=10, FoldersToClean=10, ConsiderSlowAt=70, Path=?EpicDDC, EnvPathOverride=UE-SharedDataCachePath, EditorOverrideSetting=SharedDerivedDataCache, CommandLineOverride=SharedDataCachePath\*\*, RedirectionFileName=ddc.ini\*\*)

Note the addition of **", RedirectionFileName=ddc.ini".** This indicates that the fileshare DDC should look for a file named ddc.ini at the root of the fileshare and, if it is present, attempt to read redirection information from it.

If it is not present, or if it does not contain redirection information, the fileshare DDC will be used as is. In order to redirect Shared to ZenShared, you can then place a `ddc.ini` file at the root of your fileshare DDC that contains the following:

ddc.ini

```
	`[Redirect] 	 	Default=(Target=ZenShared, SetEnvName=UE-ZenSharedDataCacheHost, SetEnvValue=public_hostname_or_ip)`
Copy full snippet
```
\[Redirect\] Default=(Target=ZenShared, SetEnvName=UE-ZenSharedDataCacheHost, SetEnvValue=public\_hostname\_or\_ip)

This redirection instructs Unreal Engine to set the `UE-ZenSharedDataCacheHost` environment variable for its own process alone to public\_hostname\_or\_ip and attempt to use the ZenShared node configuration.

Using redirection can be useful for multi-region DDC configurations if you make use of a distributed file system (DFS) architecture for your fileshares where one hostname maps to different actual hosts, depending on region. Each actual host can then have its own `ddc.ini` file that redirects to the regionally appropriate Zenserverhostname. For example:

Seattle: `\\seattle-fileshare.domain.com\ddc\ddc.ini` contains configuration to redirect to `seattle-zen.domain.com`.

Denver: `\\denver-fileshare.domain.com\ddc\ddc.ini` contains configuration to redirect to `denver-zen.domain.com`.

Montreal: `\\montreal-fileshare.domain.com\ddc\ddc.ini` contains configuration to redirect to `montreal-zen.domain.com`.

## Validating Performance in the Editor

Once you have set up the Zenserver-shared DDC on the server side and configured it for use on the Unreal Engine or client side, you should validate that the latency to the Zenserver-shared DDC is matching expectations. This can be done by clicking the Derived Data widget in the bottom right corner of the main Unreal Editor window and selecting View Cache Statistics.

This will display the Cache Statistics panel. Within this panel, you should be able to observe the active layers of your DDC hierarchy. As discussed before, you should see:

1.  The local DDC - Cache Type = Zen, Location = Local
    
2.  The newly established Zen Shared DDC - Cache Type = Zen, Location = Remote
    
3.  (if setup) The cloud DDC - Cache Type = Unreal Cloud DDC, Location = Remote
    

If you still have the fileshare DDC in your graph, you should see it listed as well. You can use this panel to inspect the latency for the Zenserver-shared DDC and ensure it is matching expectations. Ideally, you should have a latency below 20 ms for the Zenserver-shared DDC, but it can be larger when your client machine is farther away from the Zenserver-shared DDC. As long as the latency is below 60 ms for the Zen Shared DDC, it will be used by the editor and cooker.

## References

-   [Zen Public GitHub Repository](https://github.com/EpicGames/zen)
    
-   [Zen Development Readme](https://github.com/EpicGames/zen/blob/main/README.md)
    
-   [Epic Zen Configuration Template](https://github.com/EpicGames/zen/blob/main/upstream-config-templates/zen_config.lua.j2)
    
-   [DDC User Guide](/documentation/en-us/unreal-engine/using-derived-data-cache-in-unreal-engine)
    
-   [UE Cloud DDC Set Up Guide](/documentation/en-us/unreal-engine/how-to-set-up-a-cloud-type-derived-data-cache-for-unreal-engine)