# City Sample Quick Start - Generating a City and Freeway in Unreal Engine 5

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/city-sample-quick-start-for-generating-a-city-and-freeway-in-unreal-engine-5](https://dev.epicgames.com/documentation/en-us/unreal-engine/city-sample-quick-start-for-generating-a-city-and-freeway-in-unreal-engine-5)  
**Processed:** 2025-06-14 16:13:32

---

The **City Sample** project is a technical demonstration of how you can use procedurally generated data from SideFX's Houdini Engine in Unreal Engine 5 to create a working simulated world. The City Sample uses the data generated from Houdini to populate assets, drive artificial intelligence simulations, audio simulations, and much more.

This guide is part two of a two-part series that walks you through importing data which you generated in Houdini Engine into Unreal Engine 5.

To complete this part of the guide, you must have first followed [City Sample - Generating a City and Freeway using Houdini](/documentation/en-us/unreal-engine/city-sample-quick-start-for-generating-a-city-and-freeway-using-houdini).

In this guide, you will learn how to:

-   Import data you generated from Houdini Engine into Unreal Engine 5.
-   Prepare an open world environment to support your city.
-   Use the Rule Processor to import Houdini procedural data to generate your city.
-   Use the point cloud data with Zone Graph for Traffic simulation.
-   Generate Hierarchical Level of Detail meshes for World Partition.

## Prerequisites for this Guide

-   Completion of [City Sample - Generating a City and Freeway using Houdini](/documentation/en-us/unreal-engine/city-sample-quick-start-for-generating-a-city-and-freeway-using-houdini)
-   [SideFX Houdini](https://www.sidefx.com/products/houdini-engine/)
    -   We recommend using version 18.5.532 since it's the version that was used to develop the City Sample project.
-   At least 2 gigabytes (GB) of free hard disk space to extract the data and generate small-sized cities. For bigger cities, you can expect to use from 5 to 10 GB of space.
-   Refer to the [City Sample Recommended System Specifications](/documentation/en-us/unreal-engine/city-sample-project-unreal-engine-demonstration#recommendedsystemspecifications).
-   Download the [City Sample](https://www.fab.com/listings/4898e707-7855-404b-af0e-a505ee690e68) Unreal Engine 5 project through the Epic Games Launcher.

### Additional Notes about this guide

-   The workflow and files used in this guide work with the Windows 10 operating system. While Unreal Engine and Houdini support Mac and Linux, the workflows and source files have not been tested with those systems and we cannot guarantee they will work as intended.
-   This guide also assumes you have knowledge of Windows operating systems when using something like Command Prompt.

## Step 1 - Project Setup and Configuration

Before you can use your own city's data you generated while following the City Sample: Generating a City and Freeway using Houdini guide, you'll first need to open and set up a few things in Unreal Engine 5.

1.  Open the **City Sample** project with Unreal Engine 5.
    
    ![Opening City Sample the first time](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4da2d413-c99e-428c-bf3e-34d71b5663bb/1-open-city-sample.png)
2.  In the **Content Browser** under the **Content > City**, create a folder with the exact same name as the city you created in Houdini. For example, the sample Houdini city file you created in Part 1 was named "MyCity". Therefore, name the folder you create in the Content Browser **MyCity**.
    
    ![Creating a folder named after your city](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c39dcbf5-5884-4fc4-a7fe-c02543653894/1-create-city-folder.png)
3.  Open your named city folder and create two new folders named **Geometry** and **PBC**.
    
    ![Create two folder named PBC and Geometry](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/db8d9720-2d79-4f84-ac61-12fd5d12b5be/1-create-city-geometry-pbc-folders.png)
4.  The City Sample project includes the **Houdini Engine Plugin**, which is already enabled. From the main menu, open the **Houdini Engine** dropdown menu and select **Create Session**.
    
    ![Create a Houdini Session in Unreal Engine](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4ab80292-02d8-447b-a8b0-5e3550a29b01/1-create-houdini-session.png)
    
    If a session cannot be created, check the **Output Log** for additional context as to why it failed to do so.
    

At this point, you have opened the City Sample project and created folder locations to import the data you generated in Houdini for your own city. You have a new folder named for your city, and two folders within it named **Geometry** and **PBC**.

## Step 2 - Importing the City Data into Unreal Engine 5

With your own city's folders created and a Houdini Engine session started in the previous step, you can now import your data into Unreal Engine 5.

1.  In Windows, open the file location where you saved your Houdini city data. In the first part of the Quick Start Guide for [Generating a City and Freeway using Houdini](/documentation/en-us/unreal-engine/city-sample-quick-start-for-generating-a-city-and-freeway-using-houdini), you set the folder path as `D:/CitySampleSource/MyCity`.
    
    ![Windows Folder import city date to Unreal Engine](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/09bd6401-8183-4893-b0a0-0765cb4cef7c/2-windows-folder-houdini-generated-city-data.png)
2.  Inside the Windows **MyCity** folder, open the **PBC** folder. In Unreal Engine, use the **Content Browser** to open the **City > MyCity > PBC** folder. Select all the files in the PBC folder in Windows and drag them to the PBC folder in Unreal Engine.
    
    Once the import process completes, your **PBC** folder should look like the one below with the imported point cloud data generated by Houdini.
    
    ![Imported point cloud data in Unreal Engine Content Browser](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/76049ec1-15c6-48d9-8654-d493092ec8ab/2-imported-pbc-files.png)
3.  Inside the Windows **MyCity** folder, open the **EXPORT** folder. In Unreal Engine, use the **Content Browser** to open the **City > MyCity > Geometry** folder. Select all the files in the EXPORT folder in Windows and drag them to the Geometry folder in Unreal Engine.
    
    This video has been sped up to show the full import process of a smaller city created in Houdini being imported. The import process can take some time depending on the size of your city. For example, the cities included with the City Sample project can take less than 10 minutes for the Small\_City to import and upwards of 40 minutes for the Big\_City to import.
    
4.  Use the **File** menu to **Save All**.
    

At this point, you should see all your geometry and point cloud data files have been imported and saved as assets in the folders you created in Step 1 of this guide. These assets are used in the steps that follow to start generating your city.

## Step 3 - Preparing an Open World Level

In this step, you will create a new level from a templated City Open World level. This template level provides a starting point for creating your own city like the one from City Sample, with its own lighting and skybox set up and Blueprint spawners used to populate data.

1.  Using the **File** menu, select **New Level** (1). Choose **City Open World Empty** (2) from the available templates and click **Create** (3).
    
    ![Create a new City Open World Empty Template level](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/99fe041b-a7ca-44f6-b110-014728178736/3-create-new-city-tempate-level.png)
2.  Once the new level has been created, use the **File** menu to **Save Current Level As** (1). Save the map in the **Content > Maps** (2) folder and enter the **Name** (3) of your city into the text field. For example, this guide uses **MyCity** as the level name.
    
    ![Save the level and name it after your city](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/23b1ae6a-637d-473c-a86f-84b27439ec15/3-file-save-level-as.png)
3.  Click **Save** in the **Save Level As** window.
    
    ![Save the Level](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cf096c1d-dbd1-4906-bfc6-5043f19f6429/3-save-level-as-window.png)

You now have a level that you can use to generate and build your city.

![Empty City Level](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a588e2e1-cad1-46c3-8751-9351c199a6b1/3-end-result-empty-city-level.png)

## Step 4 - Running the Rule Processor Generation

All the data needed to start generating your city has been imported into the engine and you have a map with which to load and save it. In this step, you'll use the Rules Processor for the City and Freeway point cloud data you imported into the engine. The Rules Processor maps the generated point cloud data from Houdini Engine to rules that tell Unreal Engine how to use that data to populate the world.

1.  From the main menu, use **Window > Rule Processor** to open **RuleProcessor\_City**. This opens the window where the files you generated in Houdini will be used to generate the city in Unreal Engine.
    
    Click image for full size.
    
2.  In the **RuleProcessor\_City** window, replace the **Point Cloud** column's assigned assets with ones of the same name from the **City > \[YourCityName\] > PBC** folder. For example, this guide uses the files imported in Step 2 located in the **City > MyCity > PBC** folder.
    
3.  In the **RuleProcessor\_City** window, click **Run Rules** to process your imported city files.
    
    ![Run the Rules Processor for the City PBC Files](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e206abec-c2d4-4831-a0c5-e2444d8077fd/4-rules-processor-freeway-click-run-rules.png)
4.  A pop-up window asks you to confirm the processing. When ready, click **OK**.
    
    ![Confirm running rules processor](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5471ade0-5e21-4934-9bdc-a2806b69730e/4-run-rules-processor-city-popup.png)
    
    The time it takes to generate your city can vary based on the size of your city. It can take 15 minutes to an hour to finish processing.
    
5.  Repeat the process for the **Freeway** PBC files located in the **PBC** folder. From the main menu, use **Window > Rule Processor** to open **Rule Processor\_Freeway**. Replace the **Point Cloud** column's assets with ones of the same name from the **City > \[YourCityName\] > PBC**. For example, this guide uses the files imported in Step 2 located in the **City > MyCity > PBC** folder.
    
6.  In the **RuleProcessor\_Freeway** window, click **Run Rules** to process your imported freeway files.
    
    ![Run freeway Rules Processor](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/50b67ae4-411d-4c58-8b0b-88ea64ad9eb3/4-rules-processor-freeway-click-run-rules.png)
7.  A pop-up window asks you to confirm the processing. When ready, click **OK**.
    
    ![Confirm running rules processor](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9be8bad7-bf6e-4e5e-a710-f10d276f256f/4-run-rules-processor-city-popup.png)
    
    The time it takes to generate your city can vary based on the size of your city. It can take 15 minutes to an hour to finish processing.
    
8.  In the **World Partition** panel, **left-click and drag** to select all the cells in the world partition map. **Right-click** and select **Load Selected Cells**.
    

Using the Rule Processor for the City and Freeway point cloud data provides Unreal Engine with information to generate your city based on sets of rules. This lets the engine place assets to build out the city.

Once the Rules Processor has completed processing the data, the city can be loaded into the Level Viewport using the World Partition Editor. Once loaded, you can fly out and inspect your city.

![Your city loaded in Unreal Editor](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/65086325-7be5-45be-8bcd-390d9f31dbe6/4-mycity-loaded.png)

## Step 5 - Setting up Point Cloud Data for the Zone Graph for Traffic

Now that you have a city you can work with, there are two Blueprint Spawners included with the level that configure and set up the city. This means you need to duplicate some Data Assets used with the Small City for your own city. These data assets rely on point cloud data you imported.

1.  In the Level Viewport, use the **Show** dropdown menu to ensure that **Navigation** is enabled.
    
    ![Level Viewport Show menu enable Navigation](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d5c8676b-c55a-419b-9566-c95e84ae67d6/5-show-navigation.png)
2.  In the **Content Browser**, navigate to the **Content > AI > Traffic** folder.
    
    ![Open the AI > Traffic Folder in the Content Browser](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/dd2b8f68-1146-4327-9dbb-549194079182/5-content-browser-ai-traffic-folder.png)
3.  In the **ParkingSpaces** folder, make a copy of the **CitySampleSmallCityParkingSpaces** Data Asset. Rename it, replacing "SmallCity" with the name of your city. For example, this guide uses **CitySampleMyCityParkingSpaces**.
    
    ![Open the Parking Spaces Folder and make a copy of the asset](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c9781a26-dc8f-4b3b-afe4-669984bbf71b/5-content-browser-ai-traffic-parkingspaces-folder.png)
4.  Open the **CitySampleMyCityParkingSpace** Data Asset. In the **Parking Spaces Point Cloud** assignment slot, replace **City\_cars\_parked** with the one of the same name found in your city's **Content > City > \[YourCityName\] > PBC** folder. This guide uses `Content/City/MyCity/PBC`.
    
    ![Assign the data asset to the PBC slot](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6c03abba-98ae-449f-beec-b554ad114f74/5-data-asset-parkingspaces-pointclouddata.png)
5.  Return to the folder **Content > AI > Traffic**.
    
6.  In the **TrafficLights** folder, make a copy of the **CitySampleSmallCityTrafficLights** Data Asset. Rename it, replacing "SmallCity" with the name of your city. For example, this guide uses **CitySampleMyCityTrafficLights**.
    
    ![Open the TrafficLights Folder and make a copy of the asset](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ac15e50c-9935-410b-b50a-db7db3be6902/5-content-browser-ai-traffic-trafficlights-folder.png)
7.  Open the **CitySampleMyCityTrafficLights** Data Asset. In the **Traffic Lights Point Cloud** assignment slot, replace **City\_traffic** with the one of the same name found in your city's **Content > City > \[YourCityName\] > PBC** folder.
    
    ![Assign the data asset to the PBC slot](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/65700626-b274-4384-acba-3ae37475980e/5-data-asset-trafficlights-pointclouddata.png)
8.  In the **World Outliner**, enter "Builder" into the **Search** text field (1). This returns both the **CityTrafficBuilder\_BP** and **FreewayTrafficBuilder\_BP** Blueprints. Next to each of these line items, hover over each of them and click the **Pin** (2) icon next to their names to force them to load in the Level for purposes of editing it.
    
    ![Search for the builder blueprints in the world outliner](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/76913678-b920-4a22-a386-a32ee6f921e4/5-search-builder-blueprints-and-load.png)
9.  With the **CityTrafficBuilder\_BP loaded, select it in the** World Outliner **(1). Use the** Details **panel to replace the existing point cloud data with the one you imported for your city. Under the section named** Mantle**, assign your** City\_traffic **point cloud data to the** Epic Intersections Mantle Point Cloud\*\* assignment slot (2).
    
    Click image for full size.
    
10.  With the **FreewayTrafficBuilder\_BP** loaded, select it in the **World Outliner** (1). Use the **Details** panel to replace the existing point cloud data with the one you imported for your city. Under the section named **Mantle**, assign your **Freeway\_traffic\_data** point cloud data to the **Epic Freeway Mantle Point Cloud** assignment slot (2).
    
    Click image for full size.
    
11.  In the **World Outliner, search for and select** BP\_MassTrafficIntersectionSpawner **(1). Use the** Details **panel and locate the** Traffic Light Instance Data **(2) assignment slot found under** Mass > Spawn Data Generators > Index \[0\] > Generator Instance > Traffic Lights**. Replace the Data Asset with the one you created earlier in this part of the guide named** CitySampleMyCityTrafficLights\*\*.
    
    Click image for full size.
    
12.  In the **World Outliner**, search for and select **BP\_MassTrafficParkedVehicleSpawner** (1). Use the **Details** panel and locate the Parking Spaces **(2) assignment slot found under** Mass > Spawn Data Generators > Index \[0\] > Generator Instance > Entity Type to Parking Space Type**. Replace the Data Asset with the one you created earlier in this part of the guide named** CitySampleMyCityParkingSpaces\*\*.
    
    Click image for full size.
    

You should now have two Data Assets that are duplicates of the Parking Spaces and Traffic Lights ones used with the Small City. In these Data Assets, you have assigned your own city's point cloud data for use in the next section for Zone Graph Generation.

## Step 6 - Running the Zone Graph Generation for Traffic

At this point, you have created some Data Assets to use with the various Blueprint Spawners found in your city level. You've assigned some of the generated point cloud data from Houdini Engine to these Spawners through the Data Assets.

In this step, you will use an Editor Utility Widget made specifically for performing tasks of generating a Zone Graph for lanes of traffic using the point cloud data you assigned to Data Assets and Blueprint Spawners in the previous section.

1.  In the **Content Browser**, navigate to **Content > AI > ZoneGraphBuilder**. Right-click on the **Editor Utility Widget** named **WBP\_CitySampleZoneGraphBuilder** and click on **Run Editor Utility Widget**.
    
    Click image for full size.
    
2.  In the **Editor Utility Widget** window, click both buttons for **Build Zone Shapes** next to **City Traffic Builder** (1) and **Freeway Traffic Builder** (2), then click **Do All The Things!** (3).
    
    ![Zone Graph Editor Utility Widget Interface](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7bcd771e-798e-4d6e-8539-efc52a22f897/6-editor-utility-widget-build-zones.png)
3.  In the **Content Browser**, navigate to the **Content > AI > Traffic > ParkingSpaces** folder. Open the **CitySampleMyCityParkingSpaces** Data Asset.
    
    ![Content Browser Traffic / Parking Spaces folder data asset](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2643a691-d5d4-4831-8873-d14c5850783b/6-content-browser-parkingspaces-folder.png)
4.  In the **Parking Spaces Point Cloud** assignment slot, replace the **City\_cars\_parked** (1) with the one from your city's **Content > City > \[YourCityName\] > PBC** folder, then click the **Populate Parking Spaces from Point Cloud** (2) button.
    
    ![Data Asset Parking Spaces Point Cloud data assignment slot](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0c3afd54-3e23-43c1-8aae-80eefc60caa6/6-mycity-parkingspace-data-asset.png)
5.  In the **Content Browser**, navigate to the **Content > AI > Traffic > TrafficLights** folder. Open the **CitySampleMyCityTrafficLights** Data Asset.
    
    ![Content Browser Traffic / TrafficLights folder data asset](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/024a5d30-e035-4df7-9bc0-7f651bf02f10/6-content-browser-trafficlights-folder.png)
6.  In the **Traffic Lights Point Cloud** assignment slot, replace the **City\_traffic** (1) with the one from your city's **Content > City > \[YourCityName\] > PBC** folder, then click the **Populate Traffic Lights from Point Cloud** (2) button.
    
    ![Data Asset Traffic Lights Point Cloud data assignment slot](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/55a5e970-1d3b-4f7b-9b30-841a8284b0af/6-mycity-trafficlights-data-asset.png)

Once you have run the Zone Graph Editor Utility Widget and populated the data from both the Parking Spaces and Traffic Lights Data Assets, you can now visualize the navigation that is generated from that data inside the Level Viewport. If you do not see the navigation data (like below), use the Level Viewport's **Show** menu to ensure that **Navigation** is enabled, or press the hotkey **P** to toggle it on and off.

![Navigation Paths for traffic and pedestrians](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/619c78cf-11c8-4389-93bc-cfcca9740012/6-navigation-paths.png)

## Step 7 - Generate World Partition HLODs for Your City

An important part of building your city — no matter its size — is that it likely has parts that need to be seen from far distances. The [World Partition](/documentation/en-us/unreal-engine/world-partition-in-unreal-engine) system handles far distances through Hierarchical Level of Detail (or HLODs) that can combine many objects into single, large Actors that can be streamed in and out dynamically. See [World Partition - Hierarchical Level of Detail](/documentation/en-us/unreal-engine/world-partition---hierarchical-level-of-detail-in-unreal-engine) to learn more about them.

For your city, the next step is to generate your own HLODs that can be streamed in and out dynamically using World Partition. The size of your city can contribute to how long it takes for HLODs to be generated for your level. You can use the in-editor tools to do this through the Build menu, or by closing the project and using a Windows Command Prompt to do so, with the latter method taking less time.

**Using Windows Command Prompt with Command Line Arguments**

1.  In Windows, open a **Command Prompt** window.
    
2.  Enter the following command into window, accounting for your own project's folder location:
    
    ```
         `"D:\Builds\UE_5.0\Engine\Binaries\Win64\UnrealEditor-Win64-DebugGame-Cmd.exe" D:\UE5 Test Projects\CitySample MyCity.umap -run=WorldPartitionBuilderCommandlet -AllowCommandletRendering -Builder=WorldPartitionHLODsBuilder -D3D11`
    Copy full snippet
    ```
    "D:\\Builds\\UE\_5.0\\Engine\\Binaries\\Win64\\UnrealEditor-Win64-DebugGame-Cmd.exe" D:\\UE5 Test Projects\\CitySample MyCity.umap -run=WorldPartitionBuilderCommandlet -AllowCommandletRendering -Builder=WorldPartitionHLODsBuilder -D3D11
3.  Press **Enter** to start the process.
    
    The command line arguments are set up as follows:
    
    ```
         `"[FilePathOfYourEngineBuild]" [FilePathOfYourCitySampleProject] [YourMapName].umap -run=WorldPartitionBuilderCommandlet -AllowCommandletRendering -Builder=WorldPartitionHLODsBuilder -D3D11`
    Copy full snippet
    ```
    "\[FilePathOfYourEngineBuild\]" \[FilePathOfYourCitySampleProject\] \[YourMapName\].umap -run=WorldPartitionBuilderCommandlet -AllowCommandletRendering -Builder=WorldPartitionHLODsBuilder -D3D11
    -   The engine file path to the UnrealEditor-Win64-DebugGame-Cmd.exe
    -   The file path to the CitySample project. If the project is located in the Engine directory, you can use just the name of the project.
    -   The map file you want to open.
    -   The remaining command arguments to run World Partition and build HLODs.

**Using In-Editor Tools to Build HLODs**

1.  From the main menu, click **Build** and select **Build HLODs** from the menu.
    
    ![Build HLODs from the Editor main menu](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f5bba1d5-9361-4e65-a438-72958e55a4c1/7-build-hlod-ineditor-menu.png)
2.  **Save** your Level.
    

While working in the Level Editor, you may not notice anything has changed. This is because when you work with World Partition to edit the level, you are choosing what cells from the World Partition Editor to load in. However, if you were to **Play-in-Editor (PIE)** or **Simulate** prior to building the HLODs, you'd have seen that only objects within a certain distance are loading in. Anything beyond that distance is empty and not loaded for performance reasons.

Once HLODs are built, they are dynamically loaded and unloaded by World Partition during PIE and Simulate modes. In the examples below, if HLODs are not built, you'll only see parts of the city loaded near the camera within a set range. However, once HLODs are built, World Partition will load the HLODs for anything beyond the set range.

|   |   |
| --- | --- |
| ![before HLODs have been built](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2b2f0730-e6ff-4e5d-a067-265de142f779/7-before-building-hlod.png) | ![After HLODs have been built](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/817d5bb1-c4aa-4c1e-8408-07fb3d7ead58/7-after-building-hlod.png) |
| Before Building HLODs | After Building HLODs |

## Step 8 - End Results

In this final step, you'll place a Player Start in your City level where you want to spawn in when you launch the game.

1.  Find a location in your city you want to designate as a starting location when you use Play-in-Editor (PIE) to launch the project.
    
2.  Right-click in the **Level Viewport** near the ground and use the context menu to select **Place Actor > Player Start**.
    
    ![Place Player Start](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7a6d3076-47c8-49be-a8c7-efe6e44d460f/8-right-click-place-player-start.png)
    
    Depending on where you clicked in the scene, your placed Player Start may be intersecting another object or above the ground. Move the Player Start so that it doesn't display any error messages, such as "Bad Size."
    
    ![Examples of properly and badly placed Player Starts](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d6770631-1a90-44db-89be-9518e7d89e98/8-player-start-placement-good-bad.png)
    
    Left, good Player Start placement; Right, bad Player Start placement.
    
3.  Using the **Level Viewport** controls, press the **Play-in-Editor** button.
    
    ![Use the Level Editor Play Options to Play-in-editor](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b4a3b0a8-1e8f-4f0e-acc3-2a44a0279438/8-press-play-button.png)
    
    The first time you play-in-editor or simulate can take a moment to load. Subsequent times will load more quickly.
    

At this point, you should have a city that you've successfully built using the source files provided for Houdini Engine for you to build a procedural city and be able to import and set it up in Unreal Engine 5. You should also be able to explore and play through your own city, similarly to how Small City and Big City have been set up.