# Horde Analytics Tutorial

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/horde-analytics-tutorial-for-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/horde-analytics-tutorial-for-unreal-engine)  
**Processed:** 2025-06-14 16:27:37

---

## Introduction

**Horde** implements a telemetry collector which can receive and process events sent by the Unreal Editor.

Horde aggregates telemetry events into **metrics** for discrete time intervals, which can then be charted by the Horde dashboard to give valuable insights into the bottlenecks experienced by your team.

![Analytics](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b3f576fd-ab23-4400-b312-07ed449281c4/analytics-main.png)

## Prerequisites

-   Horde Server installation (see [Getting Started: Install Horde](/documentation/en-us/unreal-engine/horde-installation-tutorial-for-unreal-engine)).
-   An Unreal Engine project targetting Unreal Engine 5.5 or later.

## Steps

1.  Open your project in the Unreal Editor and go to the `Edit > Plugins` menu. Search for the `Studio Telemetry` plugin and make sure it is enabled. It should be enabled by default.
2.  Open your project's `DefaultEngine.ini` file (in the `Config` folder next to your `.uproject` file) and add the following lines:
    
    ```
         `[StudioTelemetry.Provider.HordeAnalytics]      Name=HordeAnalytics      ProviderModule=AnalyticsET      UsageType=EditorAndClient      APIKeyET=HordeAnalytics.Dev      APIServerET="http://localhost:13340/"      APIEndpointET="api/v1/telemetry/engine"`
    Copy full snippet
    ```
    \[StudioTelemetry.Provider.HordeAnalytics\] Name=HordeAnalytics ProviderModule=AnalyticsET UsageType=EditorAndClient APIKeyET=HordeAnalytics.Dev APIServerET="http://localhost:13340/" APIEndpointET="api/v1/telemetry/engine"
    
    Make sure to replace the value for `APIServerET` with the address of your Horde Server.
    
3.  Configure a telemetry store to aggregate metrics from your telemetry events. There are some default metrics and charts included with the Horde installation, which can be added by adding the following snippet to your [globals.json](/documentation/en-us/unreal-engine/horde-orientation-for-unreal-engine) file:
    
    ```
             `// Define the 'Engine' telemetry store and create some standard metrics within it.          "telemetryStores": [              {                  "id": "engine",                  "include": [                      {                          "path": "$(HordeDir)/Defaults/default-metrics.telemetry.json"                      }                  ]              }          ], 		          // Configure a default dashboard to render them          "dashboard": {              "include": [                  {                      "path": "$(HordeDir)/Defaults/default-analytics.dashboard.json"                  }              ]          },`
    Copy full snippet
    ```
    // Define the 'Engine' telemetry store and create some standard metrics within it. "telemetryStores": \[ { "id": "engine", "include": \[ { "path": "$(HordeDir)/Defaults/default-metrics.telemetry.json" } \] } \], // Configure a default dashboard to render them "dashboard": { "include": \[ { "path": "$(HordeDir)/Defaults/default-analytics.dashboard.json" } \] },

## See Also

-   [Configuration > Analytics](/documentation/en-us/unreal-engine/horde-analytics-for-unreal-engine)