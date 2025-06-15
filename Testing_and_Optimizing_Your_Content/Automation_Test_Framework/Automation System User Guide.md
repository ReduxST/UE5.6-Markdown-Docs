# Automation System User Guide

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/automation-system-user-guide-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/automation-system-user-guide-in-unreal-engine)  
**Processed:** 2025-06-14 16:09:27

---

![Banner Image](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ff3be0a1-6659-4861-bb6b-486574e1bdf6/automation-banner.png "Banner Image")

Session Frontend with the Automation tab in focus.

The **Automation** tab is part of the **Unreal (Session) Frontend** of **Unreal Engine**. It is located here because it enables you to run automation tests on any other devices that are connected to your machine or are on your local network.

There are two ways you can access the frontend suite:

-   **Session Frontend** - Opens the local Editor as an automation worker to run automation on external devices.
    
    -   Navigate to **Tools > Session Frontend**
-   **Unreal Frontend** - Opens a standalone version of the Frontend that includes the **Session Frontend**, **Device Manager**, and **Project Launcher**.
    
    -   Navigate to your **\[Unreal Engine Root Directory\]** > **Engine** > **Binaries** > **Win64** > **UnrealFrontend.exe**

## Enabling Plugins

In the latest versions of Unreal Engine, all the **Automation Tests** have been moved from the **Engine Content** folder to their plugins that must be enabled before they will be visible in the **Automation** tab.

|   |   |
| --- | --- |
| ![Open Plugins](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3978f501-5cec-4c74-9ab6-2879d4954b17/ue5_1-01-open-plugins.png "Open Plugins") | 
 |
| To enable the plugins, select **Edit > Plugins > Testing**. | Plugins Browser with Automation Tests |

If you are using the standalone **Unreal Frontend**, all the automation tests will be available without any additional steps to enable it.

## User Interface

When you open the **Session Frontend**, you will have access to a few tabs, such as the **Console**, **Automation**, **Screenshot Comparison**, and **Profiler**. For all your automation testing needs, the **Automation** tab will house all of the functionality you need with some additional functionality falling under the [Screenshot Comparison](/documentation/en-us/unreal-engine/screenshot-comparison-tool-in-unreal-engine) tab for rendering functionality comparison.

Click image for full view.

If you do not see anything listed in the **Automation** tab window, select an active session from the **Session Browse** on the left. For example, under **This Application** the machine named **PC-xxx** is selected.

### Session Browser

The **Sessions Browser** enables you to connect to specific instances of the Editor. You will only see the Automation window populate with the available automation tests once a session has been selected.

![Sessions Browser](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6f6bbbfd-a512-4831-88a4-19c67390cd58/ue5_1-04-session-browser.png "Sessions Browser")

### Toolbar

The **toolbar** in the **Automation** tab enables you to control how you start, refresh, and filter errors and warnings for your automation tests.

Click image for full view.

| Icon | Title | Description |
| --- | --- | --- |
| ![Start Test button](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/59264fd3-241a-4a88-8dfa-b20e01badfcb/ue5_1-06-start-test-button.png "Start Test button") | **Start Tests** | Starts and stops the currently selected automation test(s) that are enabled. The number of tests that will be run is also listed under the button for reference. |
| ![Run Level Test button](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9e8647b2-2777-4d1b-b597-571f8d3ebe2d/ue5_1-07-run-level-test-button.png "Run Level Test button") | **Run Level Test** | If the currently loaded level is a test map, you can click this button to select the tests and run it immediately. |
| ![Refresh Test button](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/dbe0e0d9-4554-4655-ae3d-c6cf146fb0c7/ue5_1-08-refresh-tests-button.png "Refresh Test button") | **Refresh Tests** | This will refresh the Test Name list for any test that is added to the project. |
| ![Find Workers button](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d230ab0f-4261-4e72-898d-395dc7e595df/ue5_1-09-find-workers-button.png "Find Workers button") | **Find Workers** | This will find local workers that can be used to perform the tests. |
| ![Errors button](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e22ff385-4bf5-473d-b72c-3e4d08810eb5/ue5_1-10-errors-button.png "Errors button") | **Errors** | Toggles a filter for the Test window that displays any tests that ran into an error while attempting to complete. |
| ![Warnings button](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e1451191-e8d5-40da-81be-b96130a859b6/ue5_1-11-warnings-button.png "Warnings button") | **Warnings** | Toggles a filter for the Test window that displays any tests that ran into a warning while attempting to complete. |
| ![Dev Content button](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/439fb35d-c221-4f73-ae2c-29759e686fce/ue5_1-12-dev-content-button.png "Dev Content button") | **Dev Content** | When enabled, developer directories will be included for automation tests. |
| ![Device Group button](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6195a2b8-1d49-4cb5-9546-85a8257aecfa/ue5_1-14-device-grups-button.png "Device Group button") | **Device Groups** | Enables you to group the tests based on a series of options, such as the machine name, platform, operating system version, and much more. |
| ![Excluded Tests button](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0e942181-f1d1-4104-8fdf-6518714e7899/ue5_1-13-excluded-tests-button.png "Excluded Tests button") | **Excluded Tests** | Toggle Excluded Tests only. |
| ![Presets panel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7644b518-a06b-4184-a8b6-f6ab71886251/ue5_1-15-presets-panel.png "Presets panel") | **Preset** | Enables you to add your own presets for automation tests with the selected tests and settings so that you can use them again at a later date. |

### Tests Window and Results

In the **Automation Tests Window** and the **Automation Test Results** panel, you'll find information relevant to the tests that have been run, such as the Machine that it was completed, number of tests that were run, the number of fails, and much more.

Click image for full view.

You can use the **Device Groups** button to determine how information should be grouped in the results panel when starting a new run of automation tests.

Click image for full view.

When looking at the results, use the **Display** selection to show the **Name** of the test or the **Time** the test took to complete.

Click image for full view.

### Export

Once the tests have been completed, it is possible to export the results to a **CSV** file via the **Export** drop-down.

Click image for full view.

Choose from the available filters that you'd like to export and then select the **Export Data** button.

![Export Data button](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/63052160-9651-4eec-a3fa-ab52a2137116/ue5_1-20-export-data.png "Export Data button")

When your data is exported, a pop-up will indicate if it was successful and the save location of the **CSV** file.

![Export Data success message](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b510d91a-2b58-46d1-847f-e77a7fa4f67c/ue5_1-21-export-data-success-message.png "Export Data success message")

The **Export** drop-down will only be active once reports have been generated, and the **Export Data** button will only become active if there are reports that meet the filter criteria.

### Copy

Once the tests have been completed, you can select any lines that appear in the **Automation Test Results** panel and click the **Copy** button to copy them to your clipboard and paste elsewhere.

Click image for full view.