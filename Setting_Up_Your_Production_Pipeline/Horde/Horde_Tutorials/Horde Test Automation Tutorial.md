# Horde Test Automation Tutorial

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/horde-test-automation-tutorial-for-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/horde-test-automation-tutorial-for-unreal-engine)  
**Processed:** 2025-06-14 16:28:22

---

## Introduction

The Horde Automation Hub surfaces individual and suite [Gauntlet](/documentation/en-us/unreal-engine/gauntlet-automation-framework-in-unreal-engine) test results. Horde efficiently generates searchable metadata for streams, platforms, configurations, rendering apis, etc. The automation hub is used at Epic by QA, release managers, and code owners to quickly view and investigate the latest test results across platforms and streams. It provides historical data and views which drill into specific test events which can include screenshots, logging, and callstacks.

## Prerequisites

-   The Horde Server installed (see the [Horde Installation Tutorial](/documentation/en-us/unreal-engine/horde-installation-tutorial-for-unreal-engine)).
-   A Horde Agent with AutoSDK configured (see Engine\\Extras\\AutoSDK\\README.md in the Engine sources)
-   The Horde Build example project configured (see the [Horde Build Automation Tutorial](/documentation/en-us/unreal-engine/horde-build-automation-tutorial-for-unreal-engine)).
-   An Android phone or tablet added to the Device Manager (see the [Horde Device Manager Tutorial](/documentation/en-us/unreal-engine/horde-device-manager-tutorial-for-unreal-engine)).

## Steps

1.  The Horde example UE5 project includes a reference template for building, packaging, and testing the Lyra example game project. The build graph for this example is intended to be general purpose and extensible and is a good source of a real world graph used at Epic for automated testing.
    
    ![New Build](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/73b63c5c-7a35-400c-aa37-0ed2619585e1/tutorial-testautomation-newbuild.png)
    
    From the UE5 project stream view, select the Packaged Build category, and click `New Build`, and then select `Packaged Lyra Build`. Add the Android target platform and click `Start Job`
    
    ![Select Android](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a35a596f-d366-4e56-a743-1e96891c7788/tutorial-testautomation-android.png)
    
    Please note that the Device Manager URL field is for example purposes and you would generally set this in the related Gauntlet build graph configuration.
    
2.  The job will build, cook, and run a Lyra Boot Test on the Android device, reserving it from the device manager during the process.
    
    ![Automation Labels](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/95bde8e5-39a9-4075-b74a-6c21f181a731/tutorial-testautomation-labels.png)
3.  Once completed the test results will be availble in the [Automation Hub](/documentation/en-us/unreal-engine/horde-automation-hub-for-unreal-engine) which features finely grained filters and views that can cross compare platforms and streams.
    
    ![Test Results](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/29214101-f6c7-467e-a07b-547b2a96039b/tutorial-testautomation-testresult.png)