# Environment Light Mixer

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/environment-light-mixer-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/environment-light-mixer-in-unreal-engine)  
**Processed:** 2025-06-14 16:22:11

---

The **Environment Light Mixer** is an editor window where you can create and edit a Level's environment lighting components for sky, clouds, atmosphere lights, and sky lighting. For designers and artists, it's a single window that enables you to edit these components quickly and choose the amount of properties detail you want access to.

Click image for full size.

## Opening the Environment Light Mixer

Open the Environment Light Mixer from the **Main Menu** by selecting **Window > Env. Light Mixer**.

![From the Main Menu, select Window, then select Env. Light Mixer](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0ed64465-7304-4295-93b8-a34ad0592f1d/02-open-env-light-mixer.png)

## Environment Light Mixer Interface

The Environment Light Mixer's interface is comprised of two primary elements:

Click image for full size.

1.  [Toolbar](/documentation/en-us/unreal-engine/environment-light-mixer-in-unreal-engine#toolbar)
2.  [Components Panels](/documentation/en-us/unreal-engine/environment-light-mixer-in-unreal-engine#componentspanels)

### Toolbar

The **Toolbar** is where you'll add and configure the level of properties detail that is visible in the Components Panels.

Click image for full size.

#### Adding Scene Components

When you open the Environment Light Mixer window, if you are starting from an empty Level, you will find the following components listed:

Click image for full size.

1.  [Sky Light](/documentation/en-us/unreal-engine/sky-lights-in-unreal-engine)
2.  [Atmosphere Lights (2x Directional Lights for sun and moon, or two suns representation)](/documentation/en-us/unreal-engine/directional-lights-in-unreal-engine)
3.  [Sky Atmosphere](/documentation/en-us/unreal-engine/sky-atmosphere-component-in-unreal-engine)
4.  [Volumetric Cloud](/documentation/en-us/unreal-engine/volumetric-cloud-component-in-unreal-engine)

If any of these components is added from the Place Actors panel or already exists in the scene, the list will automatically reflect what is not currently added. Likewise, when you remove a component from the scene, the create button becomes available again in the toolbar.

### Controlling the Amount of Properties Detail

When one of the available components is referenced in your Level – whether you added it through the Environment Light Mixer, or it already exists – the component's properties are added to the Components Panel where you can adjust and edit various properties for each of them.

For those that want maximum control over editing of their components, you can change the amount of properties shown using the **Property Details** dropdown:

![Using the Property Details Dropdown](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5ae31959-7a2e-43b8-a870-4755c4d88e1c/06-elm-toolbar-properties-detail.png)

1.  **Minimal** provides the bare essentials for components.
2.  **Normal** provides the common properties for components.
3.  **Normal+Advanced** provides common and advanced properties for components.

Below are examples of the amount of properties shown for the Directional Light using each detail amount:

|   |   |   |
| --- | --- | --- |
| 
 | 

 | 

 |
| Minimal | Normal | Normal+Advanced |

Click images for full size

### Components Panels

The **Components Panels** lists any of the components available in the Toolbar to add to your scene. It includes components for Sky Atmosphere, Volumetric Clouds, up to two Directional Lights, and a Sky Light.

By Default, the properties displayed for each component is limited to its **Minimal** set but can be extended to show more using the [Property Details](/documentation/en-us/unreal-engine/environment-light-mixer-in-unreal-engine#controllingtheamountofpropertiesdetail) dropdown in the toolbar.

![The Components Panels](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/614a547f-6c5f-43c7-ac97-89dd2165451c/10-elm-components-panel.png)