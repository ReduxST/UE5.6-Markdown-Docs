# Material Instance Editor UI

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/unreal-engine-material-instance-editor-ui](https://dev.epicgames.com/documentation/en-us/unreal-engine/unreal-engine-material-instance-editor-ui)  
**Processed:** 2025-06-14 16:56:56

---

The Material Instance Editor is used for modifying parameters in Material Instances. If you are unfamiliar with Material parameterization and instancing, read the following pages:

1.  [Material Instances Overview](/documentation/en-us/unreal-engine/instanced-materials-in-unreal-engine)
2.  [Creating and Using Material Instances](/documentation/en-us/unreal-engine/creating-and-using-material-instances-in-unreal-engine)

## Opening the Material Instance Editor

Double-click a **Material Instance** asset in the Content Browser to open the Material Instance Editor.

![Double-click instance](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cf1bef8c-b3a2-4e69-93c3-75a76642a2d3/click-asset.png)

You can also **Right-click** the Material Instance thumbnail in the Content Browser and choose **Edit** from the context menu.

## Material Instance Editor Interface

The Material Instance Editor is comprised of these regions:

1.  [Toolbar](/documentation/en-us/unreal-engine/unreal-engine-material-instance-editor-ui#toolbar) - Save your asset, locate it in the Content Browser, show hidden parameters, display inheritance hierarchy and platform stats.
2.  [Viewport](/documentation/en-us/unreal-engine/unreal-engine-material-instance-editor-ui#viewport) - A realtime viewport showing a preview of the Material instance.
3.  [Viewport display options](/documentation/en-us/unreal-engine/unreal-engine-material-instance-editor-ui#viewportdisplayoptions) - Allows you to edit the camera and display settings in the viewport, and change the mesh used for the Material preview.
4.  [Details Panel](/documentation/en-us/unreal-engine/unreal-engine-material-instance-editor-ui#detailspanel) - All exposed Material parameters and properties are found here.

### Toolbar

| **Icon** | **Description** |
| --- | --- |
| ![Save icon](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/33212d92-fc7f-423b-8b5f-d185145e0b77/save.png) | Saves the current asset. |
| ![Content Browser](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c2f2b4fe-4f10-4c89-915a-ee5ee09d63ea/browse.png) | Finds and selects the Material instance in the **Content Browser**. |
| ![Show hidden](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/15e39722-2fd9-4a84-b6e8-e48929ea0aa4/show-inactive.png) | Displays inactive parameters that are hidden behind static swtiches. |
| ![Hierarchy](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/29d10648-9a10-4a4b-ad96-b8ccac2fb091/hierarchy-sm.png) | Shows the inheritance hierarchy of the Material instance. [See below](/documentation/en-us/unreal-engine/unreal-engine-material-instance-editor-ui#hierarchymenu). |
| ![Platform Stats](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6a394e8b-4283-4669-99cb-9200e09554cf/platform-sm.png) | Opens a window displaying render statistcs for different target platforms. |

#### Hierarchy Menu

The **Hierarchy menu** displays the inheritance chain for the current Material instance. Since Material instances can be used as the parent for other Material instances, both parents and children are listed in the Hierarchy menu.

![Hierarchy](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3dc0163e-8427-4bcf-be51-89dc2ac26d4c/hierarchy.png)

-   **Parents** of the current Material Instance are listed under Parent Chain. If there are multiple parents, the first one listed is at the top of the inheritance hierarchy.
-   **Children** of the current Material Instances are listed under Material Instances.

Selecting a parent Material or Material instance from the Hierarchy menu opens that asset in a **new tab** of the Material Instance Editor window.

![Material parent tab](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a1792f4d-1607-469b-a10e-2a7459995bb3/parent-tab.png)

### Viewport

![Preview Viewport](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bb85ec1c-2236-4c4b-81f7-32fb8977c7ac/viewport-window.png)

The viewport shows a preview of your Material instance applied to a Static Mesh. The Material preview updates in real time as you make changes to the parameters in your Material Instance.

You can interact with the viewport using these controls:

-   Click and drag the **left mouse button** to rotate the preview mesh.
-   Click and drag the **middle mouse button** to pan the camera.
-   Click and drag the **right mouse button** to zoom in an out, or use your scroll wheel.
-   Rotate the light direction by holding down the **L** key and dragging with the **left mouse button**.

### Viewport Display Options

| **Icon** | **Description** |
| --- | --- |
| ![Viewport options](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/40ed0d22-63cf-421e-bdfe-97985b75faaf/viewport-options.png) | Contains toggle to enable real time preview, display FPS, and change FOV of the preview window. |
| ![Camera options](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0fce603b-733d-4c59-bf67-32d6d4af3c10/camera-options.png) | Switch between Perspective and Orthographic viewport cameras. |
| ![View mode options](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/141a74cc-f100-4e35-bde7-9c159bae9bff/lighting-options.png) | lContains standard view modes like Lit, Unlit, Wireframe and others. Also contains an exposure override. |
| ![Show options](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a424a2d2-f064-4343-a033-e2b096c25407/show-options.png) | Enable or disable rendering stats, the grid and the background. |
| ![Cylinder preview](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/334ca621-5e19-4078-a7f6-17190de078c2/cylinder.png) | Preview the Material instance on a cylinder. |
| ![Sphere preview](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9dae7689-9758-4c0d-8887-b8e684c68c43/sphere.png) | Preview the Material instance on a sphere. |
| ![Plane preview](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ce1df979-e64d-4f77-809b-ca6f61f1322c/plane.png) | Preview the Material instance on a plane. |
| ![Cube preview](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/45c36efb-2793-4808-ad2c-0920bb154832/cube.png) | Preview the Material instance on a cube. |
| ![Custom static mesh](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/34b9a82d-fea8-464a-beaa-249129f87632/custom-mesh.png) | Preview the Material instance on a custom Static Mesh. |

You can change the Material preview mesh by clicking one of the shape icons at the bottom of the Viewport.

![Preview Mesh options](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/46ce7f71-f7c6-4a2c-b826-917db8145160/preview-mesh-options.png)

To preview your Material instance on a custom mesh, select a **Static Mesh** asset in the Content Browser, and then click the **brick icon**. The preview mesh is saved with the Material instance so that the next time it is opened it will appear on the same preview mesh.

![Custom mesh preview](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ae993b0d-05e3-4990-87d7-fe21ee943b49/custom-mesh-example.png)

The Viewport also displays statistics about the Material, such as instruction counts for the various shader types as well as the number of Texture samples used by the Material.

![Viewport statistics](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/577f4512-a0a8-48b4-8475-5e066157b678/viewport-stats.png)

To preview any sort of movement or animation in your Material Instance, you must enable the **Realtime** Viewport option. Click the hambuerger menu to open Viewport options and make sure Realtime is checked. This option is enabled by default.

![Toggle Realtime](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/19a57647-c481-4078-9c3b-b1f72c004e56/toggle-realtime.png)

You can also press **Ctrl+R** to toggle real-time rendering.

### Details Panel

The Details panel is where you can override the parameters and settings in your Material Instance. All of the changes you make to your Material instance will occur in this interface.

![Details Panel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/990457fc-5f41-4d37-87b4-ce7abf387b7c/details-panel.png)

There are three main subsections in the Details Panel:

#### Parameter Groups

Material attributes that you have exposed through parameters in your parent Material are listed here. To override the value in a parameter, check the box to the left of the parameter name and modify the value in the field. [See here](/documentation/en-us/unreal-engine/unreal-engine-material-instance-editor-ui#overridingmaterialinstanceparameters) for more information about overriding parameters.

#### General

The General section allows you to select a different Parent Material, or Physical Material. You can also adjust how this Material Instance will influence the Lightmass build and override some of the properties inherited from the parent Material. Read more about [these settings here](/documentation/en-us/unreal-engine/unreal-engine-material-instance-editor-ui#overridingmaterialinstancelightmasssettings).

#### Previewing

This section provides another input to change the static mesh used for the Material Instance preview.

## Overriding Material Instance Parameters

Parameters are listed under the **Parameter Groups** section in the Details panel. To override a Material parameter:

1.  Place a check in the box to the left of the parameter name.
2.  Type a new value into the field or use the color picker to set a new value.

![Override parameters](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/219987ae-1099-4783-b0fa-749cda6c7281/override-params.png)

Any parameter that is checked is currently overridden in the Material Instance. Unchecked parameters use the value from the parent Material, even if there is a different value in the field:

![Unchecked parameter](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4584b195-55ce-46c7-b876-27a90af2d192/not-overridden.png)

Remember to **Save** your Material instance when you are finished editing parameters so that your work is not lost. For memory conservation, values in unchecked fields will be lost when the Material Instance Editor window is closed.

To reset a parameter to its default value, click the **Reset** button to the right of the parameter.

![Reset parameter](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3812a799-b130-4229-b664-05a1d1e0bc68/reset-parameter.png)

### Overriding Material Instance Lightmass Settings

You can override the way your Material interacts with Lightmass under the **General > Lightmass Settings** section.

For example, if you increase the Emissive Boost attribute of an emissive Material, the Material will contribute more emissive light to the static lighting solution produced by Lightmass. This makes the result brighter.

![Override Emissive Boost](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/93f002ff-3341-4058-a432-8cfdd2eeb43a/emissive-boost.png)

### Overriding Parent Material Properties

The Material Property Overrides section allows you to override some of the Material Properties in the parent Material of your instance.

For example, if you need an instance of your Material to render on both the front and back side of a surface, you can enable the Two Sided option.

![Override Two Sided](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6830edbe-3495-4f72-bc0d-d4b529d35c6a/two-sided.png)

The advantage of overriding these properties in the Material Instance Editor instead of editing the parent is that it only affects a single instance of the Material. Every other instance will inherit settings from the parent.