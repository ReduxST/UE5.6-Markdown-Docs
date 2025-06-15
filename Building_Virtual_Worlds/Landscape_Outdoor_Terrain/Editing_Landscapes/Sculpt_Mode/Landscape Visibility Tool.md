# Landscape Visibility Tool

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/landscape-visibility-tool-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/landscape-visibility-tool-in-unreal-engine)  
**Processed:** 2025-06-14 16:32:41

---

The **Visibility** tool enables you to mask out (create holes) in parts of your Landscape, for areas such as caves.

## Using the Visibility Tool

In this example, the Visibility tool is used with a Landscape Material that has been setup to use a Landscape Visibility Mask. This enables parts of the Landscape to be painted invisible or visible so that you can create caves and other underground areas using additional Static Mesh Actors. This demonstration shows painting the invisibility and then repainting the visibility.

Use the following controls to paint masked or to unmask areas of visibility for your Landscape:

| **Controls** | **Operation** |
| --- | --- |
| **Left-Click** | Adds the visibility mask, making the Landscape invisible. |
| **Shift + Left-click** | Removes the visibility mask, making the Landscape components visible again. |

![Before](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2c8e2686-28b9-422e-b5a4-4cf54d8d4374/01-before-using-the-visibility-tool.png "Before")

![After](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/03f8a97f-ad87-4f53-96a2-1ecf242a5147/02-after-using-the-visibility-tool.png "After")

In this example, the Landscape Hole Material has been used to paint invisible (or masked out) areas for the Landscape. When painting masked out areas, you only get an on or off state, so there is no way to have a transitional gradient from fully masked to unmasked.

### Using Opacity Mask to Create a Hole

Although you can use the sculpting tools to create a vertical holes in your Landscape, you may find that you also want to create horizontal ones, such as ones for caves. You can do so by using opacity masking to "paint" away the visibility of a section of your Landscape with the Visibility tool.

In order to paint away the visibility of a section of your Landscape, you must set up the Landscape Material correctly using a Landscape Hole Material. For information about setting this up properly, you can read about [Landscape Hole Materials](/documentation/en-us/unreal-engine/landscape-materials-in-unreal-engine#creatinglandscapeholematerials) here.

If you use the Visibility tool without having a Landscape Hole Material assigned, the Visibility tool will remove the Material layers applied to the selected sections, but will not create a hole in the Landscape itself.

After you have set up your Landscape Hole Material, you can use the painting tools to create a hole in your Landscape.

**To create a Landscape hole:**

1.  Make sure you have a **Landscape Hole Material** assigned to your Landscape.
    
    Click image for full size.
    
2.  In the Landscape toolbar, in **Sculpt** mode, select the **Visibility** tool.
    
    Click image for full size.
    
3.  Find the location on your Landscape where you want to create a hole.
    
    ![Landscape Mountain No Cave](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/43abc7f3-1e6d-444d-b806-de43b5f08acb/05-landscape-mountain-no-cave.png "Landscape Mountain No Cave")
4.  Adjust the brush size to the size you want to use.
    
    ![Landscape Mountain Cave Mask](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ff683b18-8627-4581-962f-f07e9c01c1e6/06-landscape-mountain-cave-mask.png "Landscape Mountain Cave Mask")
5.  **Left-click** to create the hole and **Shift + Left-click** to erase a hole that was created.
    
    ![Landscape Mountain Hole](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8f31180f-34aa-43b0-a8aa-8d3c646d6db3/07-landscape-mountain-hole.png "Landscape Mountain Hole")
    
    You can now fit Static Mesh Actors in the hole in the Landscape to create a cave.
    
    To test out the collision of the new hole using Play In Editor (PIE), you may have to change from **Landscape** mode to **Place** mode.
    

## Tool Settings

![Visibility Tool](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4c5f756e-dcc1-4e54-b9b2-54c491e891c5/08-visibility-tool.png "Visibility Tool")

There are no tool settings specific to Visibility that can be adjusted in this section. Follow the steps to setup a proper Landscape Hole Material (detailed above) and use the paint to controls to draw in your masked areas.

If you do not have a **Landscape Hole Material** assigned to your Landscape, you will see the following warning in Visibility tool panel under **Target Layers**:

![Visibility Tool Warning](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a9b43957-ec99-4e69-b48f-85b55212a961/09-visibility-tool-warning.png "Visibility Tool Warning")