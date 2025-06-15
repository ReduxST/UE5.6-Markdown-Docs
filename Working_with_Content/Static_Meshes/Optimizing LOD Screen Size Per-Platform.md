# Optimizing LOD Screen Size Per-Platform

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/optimizing-lod-screen-size-per-platform-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/optimizing-lod-screen-size-per-platform-in-unreal-engine)  
**Processed:** 2025-06-14 16:40:32

---

To control when one Level Of Detail (LOD) Static Mesh transitions into another one, Unreal Engine 5 (UE5) uses the current size of the Static Meshes size in Screen Space. While this method of controlling LOD transitions works quite well the numbers used for one platform might not work for another one. In the following How - To we will take a look at customizing the LOD Screen Size for each platform your UE5 project can be used on.

## Steps

In the following section we will take a look at how to specify the Screen Size at which LOD transactions should take place on a per platform basis.

1.  First, inside the **Content Browser**, locate a **Static Mesh** that has a few LODs to work with and open it up inside the **Static Mesh Editor**. For this example the Static Mesh that was selected has four LODs however you can pick one that has more or less depending on the needs of your project.
    
    Click image for full size.
    
2.  Once the Static Mesh is open in the Static Mesh Editor, go to the **Details Panel** and expand the **LOD Settings** category.
    
    Click image for full size.
    
3.  Disable the checkmark box next to **Auto Compute LOD Distances** so that we can manually set the distance at which LOD transition should take place.
    
    Click image for full size.
    
4.  Next, go to the **LOD Picker** section and enable the **Custom** option by clicking on the checkmark box next to it. This will allow you to see all LODs at the same time in the Static Mesh editor.
    
    Click image for full size.
    
5.  Expand the **LOD1** section and next to the **Screen Size** option,click on the **small white triangle** to expose the option to add per-platform LOD overrides.
    
    Click image for full size.
    
6.  From the displayed per-platform override list, select the **Add Override for Mobile** option.
    
    Click image for full size.
    
7.  Repeat the above step for **LOD 2** and **LOD 3** and when completed your Details panel should look like the following image.
    
    Click image for full size.
    
8.  You can now adjust the Mobile Screen size by inputting a new number in the box under the **Mobile** option. To figure out which screen size you should use for which LOD, the **Viewport** inside the Static Mesh Editor displays the **Current Screen Size**. 
    
    Click image for full size.
    

## End Result

With the ability to override the distance at which LODs will transition on Mobile devices set, you can now go back and setup the transition distance for Console and PC using the exact same steps if that is required for your project. If you decide to do this then your LOD sections will look like the following image.

Click image for full size.