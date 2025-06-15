# Control Rig Function Libraries

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/control-rig-function-libraries-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/control-rig-function-libraries-in-unreal-engine)  
**Processed:** 2025-06-14 16:15:39

---

Similar to [Blueprints](/documentation/en-us/unreal-engine/blueprints-visual-scripting-in-unreal-engine), you can share user-created functions between asset graphs by making the function "public". Unlike Blueprints, which only share functions to child classes, Control Rig functions can be shared project-wide. You can create custom function libraries, and share them with all Control Rig graphs in your project.

This document provides a guide for the best practices for creating function libraries in Control Rig, and shows how you can access the default engine-provided function library.

## New Function Library

The following steps will show you how to create and use a new Control Rig function library.

### Create Control Rig Container

As custom functions can only exist inside Control Rig Assets, the first step will be to create a Control Rig Asset. This Control Rig should not be linked to any particular Skeletal Mesh, as it will be used primarily to contain your functions.

In the [Content Browser](/documentation/en-us/unreal-engine/content-browser-in-unreal-engine), click **Add (+)**, then select **Animation > Control Rig**. In the **Create Control Rig Blueprint** dialog window, select **ControlRig** and click **Create**. Open the Control Rig after it is created.

![create control rig](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4ec9afad-26bc-4206-819a-a76d0842a919/createrig1.png)

For the purposes of this asset, your function libraries *are* Control Rig Assets, and do not include dependencies on any particular skeleton. As a container of functions, this allows for the asset to be as lightweight as possible.

### Create Public Function

In the [Control Rig Editor](/documentation/en-us/unreal-engine/control-rig-editor-in-unreal-engine), create a new function by clicking **Add (+)** on the **Functions** section of **My Blueprint**.

![create control rig function](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a72d9e45-b4b4-4135-a079-da0c7c72ea5b/createfunction1.png)

Next, select the function, and in the **Details** panel set **Access Specifier** to **Public**. This makes the function publicly accessible in all Control Rigs.

![public function](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/206a721e-e7f9-4470-89ff-c5cdd8ae874c/createfunction2.png)

### Setup Data in Function

From within your function, you can create any arbitrary contained logic you want, including metadata on the function such as tooltip descriptions and context menu categories.

In this example, **For Each** and **Set Control Visibility** nodes were created and connected to the function's **Entry** and **Return** nodes.

![function example](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2c988d2d-5ef3-461c-82a6-a4832f61eb44/functionsetup1.png)

To create variable inputs on the Entry node, select **Entry** and click **Add (+)** on the **Inputs** category in the **Details** panel. In this example, the following variables were created:

-   **Rig Element Key**, as an **Array** type.
-   **Boolean**, as a **Single** type.

![variable setup](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f9ee76da-b076-48bd-ac6e-32421aee4064/functionsetup2.png)

Next, connect the variable inputs to their corresponding nodes.

![variable connection](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/83f768e6-bb87-4a02-af21-3035bfd5105c/functionsetup3.png)

Optionally, you can also edit the **Node Settings** properties in the **Details** panel to add categorization, tooltip, or other helpful properties to the function.

![function settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0079e5a2-ff39-4e9b-9133-d81697e24dbd/functionsetup4.png)

| Name | Description |
| --- | --- |
| **Category** | 
Filling this property puts the node within the named context menu category. This category is visible when adding the node in the Control Rig graph.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ae1a0539-4b3f-4e07-a069-b9a836f00a23/functionsetup5.png)

 |
| **Keywords** | 

Adds search terms you can use to find this function when searching for it using the context menu.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/597607a2-7a69-4126-bf1c-627a3da037e9/functionsetup6.png)

 |
| **Description** | 

Adds a tooltip description for this function. You can view the tooltip when hovering your cursor either on the context menu item, or on the node after it is added to the graph.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3247ccd7-8be5-41df-bf3a-12fa1c42c487/functionsetup7.png)

 |
| **Color** | 

Sets the color of the function node header. You can preview the look of your node by expanding the **Node Defaults** category.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ad9fcd9b-c0f1-4e49-8a44-edf55e7b3829/functionsetup8.png)

 |

### Referencing the Function

To add your shared function in another Control Rig, right-click in the **Rig Graph** and add your function from the context menu. Shared functions also display their folder path in the node header for reference.

![add function](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e26e4ae6-a66f-451b-8872-532abe43fe35/functionref1.png)

Double-clicking on a shared function node opens the Control Rig Asset containing the function, and the function logic.

### Localizing Functions

In cases where you want to diverge the logic of the function from the shared version, you can localize the function, which creates a local copy of the function logic within your current Rig Graph.

To do this, right-click on the function node and select **Localize Function**. In the dialog window, ensure the function is enabled and click **OK**.

![localize function](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f0e1e525-d497-4e1e-9a7a-9dc7e7457eb4/localize1.png)

The function now converts to a local function, where you can diverge the logic locally.

![localized to new function](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0d9c1c27-b97b-4f91-bd12-3dc9b50ddc2d/localize2.png)

## Standard Function Library

By default, Unreal Engine contains a Control Rig **Standard Function Library**, which can be referenced to understand how to construct your own function libraries. Additionally, it contains a variety of functions that can be used to assist your own rigging workflows.

The Standard Function Library is located within the **Control Rig Plugin** folder. To access it, open the **Content Browser** and ensure the plugin folder is enabled by clicking **Settings** and enabling **Show Engine Content** and **Show Plugin Content**.

![show engine and plugin content](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9ffdf863-fda2-437e-9b4a-f2af1c663dd0/standardlibrary1.png)

Next, navigate to and open **StandardFunctionLibrary** located in **Engine > Plugins > Control Rig Content > StandardFunctionLibrary**.

![standard function library](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f492bf59-be74-4982-8ef5-31b760cbb367/standardlibrary2.png)

Once open, you can view the various functions in the **My Blueprint** panel.

![standard functions](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/73c49b60-99c8-4804-9bfb-753679485fb1/standardlibrary3.png)

Because the Standard Function Library is provided by **Engine Content**, any changes that you make in this asset will be overridden if you reinstall or update Unreal Engine. We reccomend instead to create your own Function Library and not modify the Engine Content one.