# Rigging with Control Rig

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/rigging-with-control-rig-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/rigging-with-control-rig-in-unreal-engine)  
**Processed:** 2025-06-14 16:47:26

---

In order to animate characters in Unreal Engine, you must first create controls for it. Control Rig contains various features and tools to create unique rigs for characters of all shapes and sizes.

This page provides an overview of creating Control Rigs, and the primary features of rigging.

## Create Control Rig Asset

You can view the **Control Rig Editor** when you open a **Control Rig Asset** from the [Content Browser](/documentation/en-us/unreal-engine/content-browser-in-unreal-engine). This Asset can be created in the following ways.

In the first method you can right-click on your Skeletal Mesh Asset and select **Create > Control Rig**. This creates a Control Rig Asset in the same directory with the postfix `_CtrlRig`. Double click the Asset to open it.

![create control rig](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/66a9442a-82dd-453a-ad1c-464da660eb58/createcontrolrig.png)

The second method is to create a Control Rig manually. You can do this by clicking in the Content Browser and selecting **Animation > Control Rig**. Next, in the pop-up window, select **ControlRig** and click **Create**. Double click the Asset to open it.

![create control rig](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/37731880-a60d-4254-a356-dcbca0474aae/createcontrolrig2.png)

If you create a Control Rig this way, you will need to manually assign the Skeletal Mesh to your Control Rig Asset after opening. This is done by clicking **Import Hierarchy** in the **Rig Hierarchy** tab, then specifying your Skeletal Mesh.

![import hierarchy](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/008421d2-8bb7-49ce-8df7-687dc9a694c2/importhierarchy.png)

Refer to the [Control Rig Editor](/documentation/en-us/unreal-engine/control-rig-editor-in-unreal-engine) page to learn more about the Control Rig Editor's interface and features.

## Rigging Features

The following features are available to help you rig your Control Rig in Unreal Engine.