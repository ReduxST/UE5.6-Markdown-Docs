# In-Camera VFX Template

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/in-camera-vfx-template-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/in-camera-vfx-template-in-unreal-engine)  
**Processed:** 2025-06-14 16:30:50

---

The **In-Camera VFX Template** is the starting point for creating the complex configuration that goes into a live-action LED stage. It provides a basic map and a variety of features to help you get started with your in-camera VFX project.

## Creating a Project from the Template

1.  Launch **Unreal Engine**.
    
2.  Select the **Film, Television, and Live Events** template category.
    
    Click image for full size.
    
3.  Click **InCamera VFX**.
    
    Click image for full size.
    
4.  Choose whether to include starter content and whether to enable retracing, and select the path and name for your project.
    
5.  Click **Create**.
    

## Template Features

-   An nDisplay configuration and Blueprint set up for In-Camera VFX
-   Configurable inner frustum and outer frustum
-   Live Link
-   A chroma key and tracking markers
-   Color Correction Regions
-   Web remote control
-   OSC

Refer to the [In-Camera VFX Overview](/documentation/en-us/unreal-engine/in-camera-vfx-overview-in-unreal-engine) and [In-Camera VFX Quick Start](/documentation/en-us/unreal-engine/in-camera-vfx-quick-start-for-unreal-engine) for information on how to use these features.

In order to access the **Blueprints** and other assets described in the template, make sure to enable **Show Engine Content** and **Show Plugin Content** in the **View Options** menu in the **Content Browser**.

![View engine content and plugin content options](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6507451f-f012-4133-b511-d4e930b10f00/ue5_03-enable-engin-plugin-content.png "View engine content and plugin content options")

## Maps

Click image for full size.

**LED\_CurvedStage** is the main map. It is provided for typical in-camera VFX set-ups and configurations.

### LED Curved Stage

![LED Curved Stage](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/630a5611-93b8-450b-989f-4389cc032a9f/ue5_05-curved-stage-example.png "LED Curved Stage")

This map provides an alternative set up with a curved mesh used for the LED wall. The LED wall is composed of four sub-sections, two on the left and two on the right, hence why there are four screens within **nDisplay\_InCamVFX\_Config** under the root component. You can customize these sub-sections to use this as a starting point to describe any type of curved LED displays, so that it matches your hardware configuration.

![Curved screen section in the hierarchy](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3191f6ea-e58c-4bb0-a940-9e8d6e37a4f0/ue5_06-screen-components.png "Curved screen section in the hierarchy")

#### Chroma Key

In the Details for **nDisplay\_InCamVFX\_Config** in the Curved Stage map, there is a control setting to enable the chroma key, allowing control over the visibility of that layer.

Click image for full size.