# Motion Controller Component Setup

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/motion-controller-component-setup-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/motion-controller-component-setup-in-unreal-engine)  
**Processed:** 2025-06-14 16:36:53

---

No matter which Virtual Reality platform you are developing for, adding support for Motion Controllers can add a level of immersion and interaction that is just not possible to achieve with a controller or mouse and keyboard. In the following How - To we will take a look at how to add Motion Controller support to the VR Platforms that support it.

## Supported Platforms

The Motion Controller component that is found in the Components tab will work on the following VR platforms.

-   Oculus VR
-   Steam VR
-   Gear VR
-   Playstation VR
-   Google VR

If you do not see the platform you are developing for listed above, make sure to check that platform's documentation for how to go about setting use of Motion Controllers.

## Motion Controller Setup

In the following section we will take a look at how to add and setup the components that are needed for Motion Controllers to work.

This How - To has been written assuming that you have setup your Pawn to work with the VR Head Mounted Display (HMD) that you are developing for. If you are not sure how to do this, check please check out the getting [started guide](/documentation/en-us/unreal-engine/developing-for-xr-experiences-in-unreal-engine) for the VR Head Mounted Display (HMD) you are developing for.

1.  First, inside the **Content Drawer** locate and open up your **Player Pawn** Blueprint.
    
    Click for full image.
    
2.  In the **Components** section click on the **Add Component** button to expose the components that can be added to this Blueprint.
    
    Click for full image.
    
3.  Input **Motion** in the search box and then click on the **Motion Controller** component to add it to the components list, giving it a name of **MC\_Left**..
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3db95fa5-8eb3-475b-b2da-bb4e066c6d27/03-motion-controller_ue5.png)
4.  Select the newly added Motion Controller component and over in the **Details** panel under the **Motion Controller** section make sure the **Motion Source** is set to **Left**.
    
    Click for full image.
    
5.  Next, select the **Motion Controller Component** in the **Components panel** and click the **Add Component** button and then search for and add a **Static Mesh Component**, calling it **SM\_Left**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/126572b1-2b0f-4f78-ba5b-2f2a2b4a3f5d/05-sm-left_ue5.png)
    
    Make sure that the Static Mesh Component is a child of the Motion Controller Component otherwise the Static Mesh will not follow along when the Motion Controller is moved.
    
6.  Now, in the Details panel of the Static Mesh Component under the **Static Mesh** section input a Static Mesh to represent what the Motion Controllers will look like. For this example we are using a simple box, but feel free to use any Static Mesh you have available.
    
    Click for full image.
    
7.  Now, duplicate the entire Left hand Motion Controller setup and re-place the word **Left** with **Right**. Also make sure to change the which hand this Motion Controller is used for by going to the Motion Controller component and then changing **Motion Source** from Left to **Right**.
    
    Click for full image.
    
8.  Compile and save your Pawn Blueprint, make sure it is placed in your test level and then launch your project. When you put on your HMD and pick up your Motion Controlers you should be able to now do what is shown in the following video.
    

## Motion Controller Component Visualization

Motion Controllers have a **Visualization** category that enables you to quickly and more easily add a display model Static Mesh to your Motion Controllers. By default, the system attempts to load a Static Mesh model matching the device driving the Motion Controller.  The visualization fields  offer the following options: 

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/10b5a0f7-7a3b-4602-82d2-387934e590f2/08-visualization-settings_ue5.png "08-visualization-settings_ue5.png")

| Property Name | Description |
| --- | --- |
| **Display Device Model** | Used to automatically render a model associated with the set hand. |
| **Display Model Source** | Determines the source of the desired model. Ny default, the active XR system(s) will be queried and (if available) will provide a model for the associated device. Note: This may fail if there's no default model; use 'Custom' to specify your own mode. |
| **Custom Display Mesh** | A mesh override that'll be displayed attached to this Motion Controller. |
| **Display Mesh Material Overrides** | Material overrides for the specified Display mesh. |

## Training Streams