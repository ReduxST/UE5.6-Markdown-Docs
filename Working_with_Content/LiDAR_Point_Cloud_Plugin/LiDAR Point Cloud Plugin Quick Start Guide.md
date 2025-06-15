# LiDAR Point Cloud Plugin Quick Start Guide

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/lidar-point-cloud-plugin-quick-start-guide-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/lidar-point-cloud-plugin-quick-start-guide-in-unreal-engine)  
**Processed:** 2025-06-14 16:33:27

---

This Quick Start guide covers the following steps:

1.  Enabling the LiDAR Point Cloud plugin.
    
2.  Importing a point cloud and placing it into a scene.
    
3.  Building collision for the point cloud so you can explore it in real time.
    
4.  Editing the point cloud.
    

## 1\. Enabling the Plugin

The LiDAR Point Cloud plugin is included with the Unreal Engine, but you must enable it for your Project before you can use it.

1.  Open the **Plugins** window (main menu: **Edit > Plugins**).
    
2.  In the **Plugins** window, search for the **LiDAR Point Cloud Support** plugin, then click the **Enabled** option.
    
    ![LiDAR Point Cloud Support plugin](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7e9a2798-294a-4404-a6d2-f2ccb227600c/ue5-1_01-lidar-point-cloud-support-plugin.png "LiDAR Point Cloud Support plugin")
3.  Save your project and restart Unreal Engine.
    

## 2\. Importing the Point Cloud

1.  Create a new project. Use a template that includes a character controller, such as [Third Person Template](/documentation/en-us/unreal-engine/third-person-template-in-unreal-engine).
    
2.  Choose the point cloud file you want to import and drag it into the **Content Browser**.
    
3.  Drag the point cloud from the **Content Browser** into the **Viewport**. This will automatically create an instance of a **LidarPointCloudActor** and assign your specified cloud to it.
    

## 3\. Building and Testing Collision

Before you can move around the imported point cloud scan like any other Level, you need to build and enable collision for it.

1.  In the **Main Toolbar**, click the **Modes** button, select **Lidar Mode**.
    
    Click image for full size.
    
2.  Select **Add Collision**.
    
    Click image for full size.
    
3.  Click **Save** to save your changes.
    
4.  Back in the main editor window, from the **Place Actors** panel, search for a **Player Start** component and drag it into your level. Place it above the ground.
    
5.  Click **Play** to start **Play in Editor** mode and move around the imported scan.
    
    Click image for full size.
    

## 4\. Editing the Point Cloud

Next, you'll be making some simple edits to the point cloud. You can select and edit individual points and point groups using a range of tools.

1.  To edit points, you must select them first. Choose one of the available selection methods:
    
    -   Box Selection
    -   Polygonal Selection
    -   Lasso Selection
    -   Paint Selection
        
        Click image for full size.
        
    
    Selected points will be highlighted. Press the **Esc** key on your keyboard to clear your selection.
    
    Click image for full size.
    
2.  You can **Hide**, **Delete**, or **Crop** the selected points.
    

After you edit the point cloud, you must rebuild its collision.

## On Your Own!

Explore some of the other functionality the LiDAR Point Cloud plugin offers:

-   Enable [Eye-Dome Lighting](/documentation/en-us/unreal-engine/eye-dome-lighting-mode-for-point-clouds-in-unreal-engine) to enhance depth perception.
    
-   See the [LiDAR Point Cloud Reference](/documentation/en-us/unreal-engine/lidar-point-cloud-plugin-reference) for the full range of available options.