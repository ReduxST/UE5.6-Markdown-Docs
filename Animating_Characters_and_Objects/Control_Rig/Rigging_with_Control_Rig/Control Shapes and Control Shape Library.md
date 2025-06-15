# Control Shapes and Control Shape Library

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/control-shapes-and-control-shape-library-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/control-shapes-and-control-shape-library-in-unreal-engine)  
**Processed:** 2025-06-14 16:15:51

---

When creating controls for your Control Rigs, you may need to differentiate them visually from each other, or use a better-suited shape for a control. Using the **Control Shape** properties, you can affect a control's transform, color, and shape. You can also create and edit **Control Shape Libraries** to add or change the control shapes available to you.

This document provides an overview of these tools and features.

#### Prerequisites

-   You have an understanding of the **[Control Rig Editor](/documentation/en-us/unreal-engine/rigging-with-control-rig-in-unreal-engine)**.
    
-   **[Controls](/documentation/en-us/unreal-engine/controls-bones-and-nulls-in-control-rig-in-unreal-engine)** are added to your Control Rig.
    

## Control Shapes

To view a control's properties, select it in the **Control Rig Editor** and locate the **Control Shape** properties in the **Details** panel.

![control shape property](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/dda31d20-67bc-4a8a-9b81-89e5af5a44b0/properties.png)

### Change Shape

To change your control's shape, select one of the options from the **Shape** drop-down menu.

![control shape circle](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bd31ab92-d476-482e-9fad-9f8b6111e292/shape.png)

You can also change the color of a shape by clicking the **Color** property, which opens the **Color Picker**. Select a color and click **OK** to change the color of the control shape.

![control shape color](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/67285e65-a2d2-474f-83c7-24367869a564/color.png)

## Control Shape Library

If you want to add to or change the list of shapes available, you can do so using the **Control Shape Library**. Each Control Rig asset contains a reference to the library, and you can view it by clicking **Class Settings** in the Control Rig Editor, then locating the **Gizmo Library** property in the **Details** tab.

![class settings library](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/25e51eec-4eea-49b8-80ba-2fa80792750f/library1.png)

You can choose to use the existing library, or assign a different **ControlRigGizmoLibrary** to the control rig class.

You can open the library by either double-clicking the asset from the **Details** tab, or by navigating manually to it in the **Content Browser**. It is located in the **Engine > Plugins > Control Rig Content > Controls** folder. Because it is located within the **Engine > Plugins** folder, you must enable **Show Engine Content** and **Show Plugin Content** from the Content Browser **Settings**.

![control library content browser location](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c93415a6-030f-409d-a357-5d2e68e1c106/library2.png)

### Library Properties

Once opened, the library is populated with the following properties:

![control library properties](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fe5303f6-0722-4b48-abd9-9622b6a5e106/library3.png)

| Name | Description |
| --- | --- |
| **Gizmo Name** | The name of the initial Control Shape when adding a new control. |
| **Static Mesh** | The mesh to use for the initial Control Shape when adding a new control. |
| **Transform** | The location, rotation, and scale to use for the initial Control Shape when adding a new control. |
| **Default Material** | The **[Material](/documentation/en-us/unreal-engine/unreal-engine-materials)** to use for all controls. |
| **Material Color Parameter** | The Vector 3 **[Material Parameter](/documentation/en-us/unreal-engine/instanced-materials-in-unreal-engine#materialparameterization)** from the **Default Material** to affect when you change the **Color** property on the Control Shape. |
| **Gizmos** | The array that populates the **Shape** drop-down menu of the control. Here you can specify each shape's **Name**, **Static Mesh**, and **Transform**. New shapes can be added using the **Add Element** button. Shapes can be removed by clicking the drop-down button and selecting **Delete**. |

### Adding New Shapes

Control Shapes are represented using **[Static Meshes](/documentation/en-us/unreal-engine/static-meshes)**, which you can view in the same folder as the Control Rig Library asset.

![control shape static mesh](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/17437ff2-b933-4b72-8f17-b440f24a85a6/meshes.png)

You can import your own `.fbx` static meshes to expand your library with custom shapes. To do this, assuming you have a `.fbx` model file already exported, import it into Unreal Engine by clicking **Import** in the Content Browser, selecting your `.fbx` file, and clicking **Import**.

![import new control shape](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/eff9d188-5fc1-4511-9dd8-4365ab3bc534/import1.png)

When importing new meshes for use as a control shape, it is not necessary to import any textures or create materials for them. Therefore, ensure that **Import Textures** is **Disabled** and **Material Import Method** is set to **Do Not Create Material** in the **FBX Import Options** menu.

![control shape import settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/48fcf8e3-3992-4467-b276-cb3bad684de3/import2.png)

After your static mesh is imported, add a new shape entry into the array by clicking the **Add Element** button on the **Gizmos** property. Expand the array list and navigate to the newly created entry at the bottom, where you can fill in the **Gizmo Name**, **Static Mesh**, and **Transform** properties.

![add new control shape](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e21baea4-0244-4eda-9f00-db5fd7a641f9/addshape.png)

Now when you return to the Control Rig, your new control should be selectable from the **Shape** property.

![new control shape](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/62375d2c-23b4-457c-a74b-ae1272be16d5/myshape.png)