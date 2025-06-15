# Horde Automation Hub

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/horde-automation-hub-for-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/horde-automation-hub-for-unreal-engine)  
**Processed:** 2025-06-14 16:27:42

---

The Horde Automation Hub surfaces individual and suite [Gauntlet](/documentation/en-us/unreal-engine/gauntlet-automation-framework-in-unreal-engine) test results. Horde efficiently generates searchable metadata for streams, platforms, configurations, rendering apis, etc. The automation hub is used at Epic by QA, release managers, and code owners to quickly view and investigate the latest test results across platforms and streams. It provides historical data and views which drill into specific test events which can include screenshots, logging, and callstacks.

In addition to enabling Horde [build automation](/documentation/en-us/unreal-engine/horde-build-automation-for-unreal-engine), the configuration required to surface test results is simply adding the `-WriteTestResultsForHorde` Gauntlet test command line argument. Please see the BuildGraph [example](/documentation/en-us/unreal-engine/horde-automation-hub-for-unreal-engine#buildgraph-example) below for details.

## Automation Filters

The automation UI is data driven and automatically populated from test metadata. Test results can be filtered by project, tests, streams, platforms, configurations, targets, rendering hardware interface, and variations. Detailed selections may also be linked for sharing or to be bookmarked.

![Automation Selection](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1eeecbb2-494c-47f9-b5be-67f8f3960e1e/automationhub-leftpanel.png)

## Test Tiles

Test results are presented as tiles which surface relative test health based on the platforms and streams selected.

![Test Results](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/653e90fb-b2ad-41d1-945c-2934cf242b09/automationhub-testresults.png)

Test tiles can be expanded to view further details such as platforms and changelists, which are linked to individual [Horde CI](/documentation/en-us/unreal-engine/horde-build-automation-for-unreal-engine) job steps to assist in issue investigation.

![Test Card](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/75187f40-c6eb-4f23-9350-0f011bf44701/automationhub-testpanel.png)

Test history graphs and detailed failure reports are also available which include logging and callstacks.

![Test History](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/40096cbb-1d53-4515-a9fb-8163195e7cb0/automationhub-testhistory.png)

## Test Suites

Gauntlet suite tests may contains thousands of individual unit tests. The automation hub can drill into historical data for each unit test with cross stream comparison.

![Suite Results](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0fa2b90f-d86e-44d0-b328-ce832fc96321/automationhub-suiteresults.png)

Suite tests generate test events which can be viewed to help diagnose issues. Test events can include additional data such as logging and screenshots to catch regressions. Alternate platforms of the unit test may also be selected for comparison purposes.

![Screenshot Comparison](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3a14a9c9-9d75-4f26-a7bb-57433f0fc614/automationhub-screenshotcompare.png)

## BuildGraph Example

The following [**BuildGraph**](/documentation/en-us/unreal-engine/buildgraph-for-unreal-engine) fragment declares:

-   `HordeDeviceService` and `HordeDevicePool` properties that specify your Horde server and which device pool to use.
-   Adds a `BootTest Android` node which specifies `-WriteTestResultsForHorde` andh will automatically generate test data to be ingested by Horde, parsed to efficient meta data, and surfaces by the automation hub
    
    ```
          `<Property Name="HordeDeviceService" Value="http://localhost:13440" />       <Property Name="HordeDevicePool" Value="UE5" /> 			       <Node Name="BootTest Android">           <Command Name="RunUnreal" Arguments="-test=UE.BootTest -platform=Android " -deviceurl="$(HordeDeviceService)" -devicepool="$(HordeDevicePool)" -WriteTestResultsForHorde/>       </Node>`
    Copy full snippet
    ```
    <Property Name="HordeDeviceService" Value="http://localhost:13440" /> <Property Name="HordeDevicePool" Value="UE5" /> <Node Name="BootTest Android"> <Command Name="RunUnreal" Arguments="-test=UE.BootTest -platform=Android " -deviceurl="$(HordeDeviceService)" -devicepool="$(HordeDevicePool)" -WriteTestResultsForHorde/> </Node>