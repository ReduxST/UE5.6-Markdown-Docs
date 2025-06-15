# Using the Stage Tab with the Unreal Stage App

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/using-the-stage-tab-with-the-unreal-stage-app-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/using-the-stage-tab-with-the-unreal-stage-app-in-unreal-engine)  
**Processed:** 2025-06-14 17:01:56

---

## Editor Preview

The Stage tab shows a live preview of nDisplay's output on the LED wall with touch-capable, interactive ICVFX content. This is the same preview shown in Unreal Engine's nDisplay Editor Preview and ICVFX Editor on the desktop.

### View Options

You can toggle the view of the nDisplay Editor Preview via the dropdown menu. There are four different view options:

-   **Dome**
    -   The most commonly-used view option for hemispheric LED volumes with ceilings
-   **Orthographic**
    -   Another popular projection option for hemispheric stages
-   **Perspective**
    -   Typically most useful for configurations with flat LED walls
-   **UV**
    -   A flattened representation of the LED volume that can more easily show both the walls and ceiling simultaneously and requires secondary UVs to be set up for the nDisplay configuration meshes

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ee72e954-5576-4247-9907-ea724e07699a/stagetab-1.gif)

### Navigation

The preview can be navigated to view exactly what you want. Interact with the preview as follows:

-   **Pinch Zoom**
    -   Zoom in and out of the preview
-   **One Finger**
    -   Tumble the preview
-   **Two Fingers**
    -   Pan across the preview

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2126c8b7-4048-48e6-a8ea-20cd83efe5f3/stagetab-2.gif)

## Content Controls

The same ICVFX content that can be placed in Unreal Engine's ICVFX Editor can also be placed via Unreal Stage:

-   Light Cards
-   Flags
-   Color Correction Windows
-   Chromakey Cards
-   Templates

### Place Actors

Use the Add button in the top-right to add new content at the default location, which may be off-screen. You can also press and hold at a specific location in the Stage tab to add content at that exact spot.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/15aa653c-351a-4251-a34d-c831da3cd82d/stagetab-3.gif)

### Position and Reposition Content

You can reposition any ICVFX content placed within the scene by using a single finger to press and hold the object until it is selected. You can then drag it freely via touch and position it wherever you want.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/17a9ca52-151e-4e1b-af82-4ef8ff30b998/stagetab-4.gif)

### Object Mode

Object Mode allows you to further modify content beyond placement. Using the same press-and-hold action as before, select the content and toggle to Object Mode. Controls will only focus on the selected content while in Object Mode, so you can quickly and easily make changes without accidentally modifying anything else in the scene. Pinch zoom will scale the size of the selected object. You can also quickly reposition the selected content while in Object Mode by tapping anywhere on the screen to grab it before dragging it to your desired location.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bee80ae6-9888-4006-8814-ca690345e2d8/stagetab-5.gif)