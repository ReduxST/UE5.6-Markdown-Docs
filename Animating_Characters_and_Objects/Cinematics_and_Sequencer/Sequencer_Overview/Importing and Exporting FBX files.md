# Importing and Exporting FBX files

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/import-and-export-cinematic-fbx-animations-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/import-and-export-cinematic-fbx-animations-in-unreal-engine)  
**Processed:** 2025-06-14 16:30:01

---

This page describes how you can export a scene from Sequencer as an FBX file and make alterations to that file inside a third-party application like 3ds Max or Maya. Once satisfied with your changes, you can then import the FBX file back into your Sequencer scene in Unreal Engine 4 (UE4) along with your updated changes.

There are some caveats to this process that you should keep in mind:

-   When exporting, you can export all the objects with animations in your scene to your FBX file.
-   Importing FBX files will only import animation. It will not create new objects.
-   Export/Import does not work with **Master Sequences**, **Shots** within a Master, or **Subscenes**.
-   Make sure that the time settings in your third-party application matches the time frame used for your scene in Unreal Engine.

As long as you export from a source Level Sequence and not a shot that sits inside a Master, and are only altering the animation of existing assets, you will be able to import your changes directly back into your scene inside UE4. Also, using the same time frames in both UE4 and your third-party application will ensure that they line up, and that the imported scene is not resampled at a different time rate.

## Example Workflow

Below, we export a scene from the Sequencer Subway Project (pictured below) available for free from the **Learn** tab of the Launcher. We then take it into Maya and alter the camera movement in the scene, then import that FBX along with our changes back into UE4 where our existing scene is automatically updated with our changes.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5336d51d-8107-4ab5-b825-08c11b193cfc/sequencersample4-23.png)

### Exporting from Sequencer

First, determine which Level Sequence to export.

1.  In the clip below, we pick the shot we want to alter and open it up. We then go into the **General Options** and choose **Export**. We have a Master Track that includes **shot0040\_001** so we open that particular Level Sequence to export it.
    
    Upon performing the FBX Export process, you will be shown the **FBX Export Options** window where you can define how to export your content.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/33670749-c2b1-4171-9237-1449b517c0c5/fbxexportoptions4-24.png)
    
    Use these options to choose the **FBX Export Compatibility** version as well as the option to export the Skeletal Mesh's **Vertex Color**, **Level of Detail** or **Collision** settings.
    
    There is also the option to **Map Skeletal Motion to Root** which will (if enabled) map the Skeletal Actor motion to the root bone of the Skeleton. For this example, we use the default settings and choose **Export** to export our content.
    

#### Exporting Shots by Local or Master Time

When exporting an object in a Shot or Subsequence, you can determine if you want to export the Shot by Master Sequence time or Local Sequence time. Master Sequence time is useful when you are looking at the animation holistically and in comparison to other shots. Local Sequence time is useful when you are working shot by shot. Exporting to either time maps to the shot keys in Maya, and in Sequencer you can move from Local to Master time easily.

The default setting is to **Export Local Time** (checked). To export by Master Time, uncheck the box.

![Export Local Time checkbox](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d0b7f837-5412-48ed-ad6c-435fd8bf5255/export_time2.png)

### External Editing

Once we have an exported FBX from Sequencer, we open our third-party application to import it so we can start editing.

1.  Before we import our FBX into Maya, we set our working units for **Time** to match our **Time Rate** used in Unreal Engine.
    
2.  We then import our FBX into Maya and set up our scene so that we can begin making edits. After importing:
    
    1.  Set the Perspective under **Panel** to use the camera **shotCamA** in our scene.
    2.  Hide any elements obstructing the view (such as the god ray mesh) by pressing **Ctrl + H** with it selected.
    3.  Then, under **View** we **Select Camera** to display the properties and keyframes for **shotCamA**, which we can then begin to edit.
    
3.  Next, we make edits to the movement of our camera. Below, we select the **Translation** and **Rotation** properties of our **shotCamA**. Then, right-click and select **Break Connections**. We then pick a new starting point for the camera to be in, to start our scene, pressing the **S** key to keyframe the new position. We scrub ahead slightly and move the camera to the ending position. Press the **S** key again to keyframe the end position so that our camera moves along a new path.
    
4.  With our changes in place, we then export our scene using **Export Selection** from the **File** menu. During the export process from Maya, we first change the export type to **FBX export**. Then, under **Advanced Options** and **Axis Conversion**, we change the **Up Axis** to follow the Z-axis to allow for a compatible import into Unreal Engine. Future versions of the engine may address this so that you do not have to convert the axis, but you will need to do this for now to avoid any importing problems.
    

### Importing to Sequencer

Now that we have an edited version in FBX format we can import it and the changes into Unreal Engine, updating our scene.

1.  Inside our **shot0040\_001** that we wanted to edit, we right-click on our **shotCamA** and select **Import**. This will take the transform data inside the FBX and apply it to the selected object in Unreal Engine. This can be useful if you want to apply the same transform data to multiple objects inside your scene.1.
    
    Upon importing our FBX we are presented with the **Import FBX** window.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/41e63636-a948-49ad-9452-05c2d02b5c3d/importfbx.png)
    
    This (if enabled) allows you to **Force Front XAxis** which will convert the scene from the FBX coordinate system to UE4 coordinate system with front X axis instead of -Y. If cameras do not already exist in the Level, go ahead and enable the **Create Cameras** option.
    
    You can also import the FBX from the **General Options** window instead of using the right-click method.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b8cb8fd6-bd91-434f-889c-36894cfa0095/importoption.png)
    
    When choosing this method, Unreal Engine will try to match the names of your objects. For example, we have **shotCamA** in both our FBX file and our Sequence so it will apply the data from the FBX file to that object inside Unreal Engine.
    

In our example, we only applied Transform changes to our camera. However, we could have keyframed new values for our **Focal Length** to produce a different looking shot as well.

You can experiment with this workflow and use what works best in your given situation. There may be times when you want to export to a 3D package like Maya or 3ds Max to fine-tune aspects of your scene and then import your changes back into your scene in Unreal Engine.