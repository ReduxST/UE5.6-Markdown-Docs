# Modular Control Rigs

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/modular-control-rigs-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/modular-control-rigs-in-unreal-engine)  
**Processed:** 2025-06-14 16:36:44

---

A **Modular Control Rig** is a digital animation rig in Unreal Engine that has been created by combining a series of pre-built [Control Rig](/documentation/en-us/unreal-engine/control-rig-in-unreal-engine) assets called **Modules**. A **Module** is a Control Rig component that represents a part of the character’s body, such as an Arm, Leg, or Spine, that can be used to automatically create a set of controls and rig the part of the body, enabling it to receive animation data. Modules can be **connected** together to form a complete animation rig for articulation to drive a skeleton.

This document will provide an overview of how to rig characters using the Modular Control Rig framework.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e78da347-c1d5-4b01-80a4-7d8eddbb9555/image_0.gif)

Creating a Modular Control Rig, by combining a series of Models is called **Visual Rigging.** Visual Rigging allows you to build and connect Modules together entirely in the viewport utilizing the **Schematic Overlay**.

## Getting Started

Here you can read about how to get started rigging characters using the Modular Rigging framework.

#### Prerequisites

-   You have a Skeletal Mesh character in your project. For the example workflow included in this document, the Mannequin character is used.
    
-   Enable the **Control Rig Modules** [Plugin](/documentation/en-us/unreal-engine/working-with-plugins-in-unreal-engine). Navigate in the **Menu Bar** to **Edit > Plugins** and locate the **Control Rig Modules** plugin in the **Animation** section, or use the **Search Bar**. Enable the Plugin and restart the editor.
    

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0bc6e1df-0e34-44e2-8639-6d23b4e92bf2/image_1.png)

This plugin is not required to use Modular Control Rigs in Unreal Engine, however it contains the pre configured [Modules](/documentation/en-us/unreal-engine/modular-control-rigs-in-unreal-engine#module) that the included workflow example uses, and is recommended to get started using Modular Control Rigs. This plugin is designed to be optional and can be loaded and unloaded depending on your project’s needs.

### Preview Scene Settings

Before beginning to rig the mesh, you can adjust a few settings in the **Preview Scene Settings** panel in order to make the **Viewport** easier to navigate. It is recommended to set the following settings:

| Property | Recommended Setting |
| --- | --- |
| **Show Environment** | **Off** |
| **Show Floor** | **Off** |
| **Post Processing** > **Lens** > **Exposure** > **Metering Mode** | **Manual** |
| **Post Processing** > **Lens** > **Exposure** > **Exposure Compensation** | `11.0` |

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b1da83bd-d9dc-434f-847a-98fc44bdf8b1/image_2.gif)

### UI Overview

Here you can reference an overview of the Modular Control Rig Editor.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fdaedb5c-38ac-437b-a2b7-4c410d0a4a88/image_3.png)

1.  **Module Assets**: Here you will find the available Module assets that you can add to your Control Rig.
    
2.  **Viewport**: Here you can view your Mesh and Rig, along with the **Schematic Overlay Sockets**. These sockets indicate a point on the Mesh where a Module can be placed.
    
3.  **Details**: Here you can adjust settings for your rig.
    
4.  **Rig Hierarchy**: Here you can reference and edit the hierarchy of you
    
5.  **Module Hierarchy**: Here you can reference and edit the hierarchy of your Control Rig controls.
    

## Terminology

Here you can read about the different terminology used when rigging a Modular Control Rig.

### Module

A **Module** is a component of a Control Rig created by a Module Author that can be used within the Modular Control Rig framework.

Generally, Modules represent common parts of a character, such as an Arm, Leg, or Spine, although they are not limited to these concepts.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a5ba168a-4178-4c65-bbb8-15d8d44e28be/image_4.png)

### Connector

In order to build a full character rig, Modules need to be connected together using **Connectors.** A **Connector** is a relationship between two modules. Modules can have multiple connector points. These connector points are created by the **Module Authors** to direct how modules should connect to each other inside the Modular Control Rig.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c12fbb93-c676-423b-85bc-aa5b29dd9d84/image_5.gif)

Connectors need to be **resolved** to a rig element for the module to operate correctly**.** Connectors are usually automatically resolved when adding Modules to your Modular Control Rig, however, you can manually assign these resolves in the Module Hierarchy panel, using the drop down associated with each Module and Module Component.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/46bf510f-f8b9-482d-95c9-c10246fd53f5/image_6.png)

### Sockets

**Sockets** are nodes that can be used to connect rig Modules together at specific locations with Connectors. For example connecting the shoulder of an arm to the chest location of the spine. A Connector will automatically **resolve** to a socket**.** A socket can resolve to the following types of hierarchy elements:

-   **Bones**
-   **Controls**
-   **Nulls**

You will visually see if a Connector is resolved to a socket in the Editor’s Viewport. A Circle with a large gray circle within it will indicate a resolved Connector. A circle with a small gray dot within it will indicate an unresolved socket. If there are multiple Connectors resolved to the same socket, a number will be present indicating the number of Connectors resolved to the same socket.

| Socket | Description |
| --- | --- |
| ![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f445072b-544d-4fcb-99e4-3b0e5cdf2272/image_7.png) | Socket is **unresolved** to a connector. |
| ![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/aff27dd0-a672-40bf-be29-2feb5eae75d7/image_8.png) | Socket is **resolved** to a connector. |
| ![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ac7a1f50-83bd-43e9-ab02-deead9e7cf01/image_9.png) | Multiple connectors are **resolved** to this socket. |

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/77a89765-0d7b-4900-8c53-b6c87367b111/image_10.png)

Connectors can have **rules,** meaning that they can only resolve to a specific type of socket. For example, some Connectors can only resolve to Bones or Sockets.

## Create your first Modular Rig

Here you can follow an example walk through about getting started with your

### Create a Modular Rig Asset

You can create a Modular Rig, using (**+**) **Add** in the **Content Browser** and selecting **Animation** > **Control Rig** \> **Control Rig**.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/08825070-98f1-419d-bda5-0237c0f6e148/image_11.gif)

When prompted, select the **ModularRig** option in the **Create Control Rig Blueprint** window and then select the **Create** button.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2c23213e-f19d-48c9-bc5b-db218eebebcd/image_12.png)

You can now open the Control Rig Asset, by **double-clicking** it in the **Content Browser**. After opening the asset, select the Skeletal Mesh Character you want to rig using the **Preview Mesh** property’s drop down menu in the **Details** panel, or using the prompt in the bottom right corner of the Viewport.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f7d92cb8-842f-48fd-a202-28d811ab86d5/image_13.png)

After defining your Character Mesh, you can **drag and drop** the **Spine** Module from the Module Assets panel onto the unresolved Socket in the Viewport.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/908b0e39-396a-4855-8111-3915178bcdf4/image_14.gif)

After adding the Spine Module, more Connectors will appear that you can add additional Modules to. Next, **drag and drop** the **Neck** Module onto the unresolved Neck socket.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a4d7bad3-af91-48c6-b3f7-eb1b5057c8c9/image_15.gif)

Then, **drag and drop** the a **Leg** Modules onto each of the available Leg sockets.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0f9bb120-1ec2-4d6b-a523-a3f6cde96273/image_16.gif)

Then, **drag and drop** the Foot Modules onto each of the available Foot sockets.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/198448c3-6eb5-4957-9e7b-74c404a2ddfb/image_17.gif)

Similar to the process of adding the Leg and Foot modules, **drag and drop** a **Shoulder** Module onto each of the Shoulder sockets, and then drag and drop an **Arm** Module onto each of the Arm sockets.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ba35668f-736f-4c7a-9ce7-2878472a12a8/image_18.gif)

Finally, select each finger socket, and then drag and drop a Finger module onto one of the selected sockets to create multiple Modules at the same time.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3b80f40b-0643-44df-b0b5-7cf30d173d0f/image_19.gif)

### Mirroring

You can also mirror modules to make the process of creating a Modular Control Rig more efficient. To mirror a module, first select the Module or Modules you would like to mirror in the Module Hierarchy panel. Then right click the selection and use the **Mirror** property in the Context Menu. You can then define the property with which to mirror the selected modules, such as the **Mirror Axis**, the **Axis to Flip**, and a **search** and **replace** function for renaming the new Modules. The mirroring operation will attempt to rename Modules contextually based on the original Module’s name and location in the rig.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/139c1a0a-f665-43ce-8b19-603c9db1891c/image_20.gif)

Sockets need to exist for the mirrored module connectors’ to resolve properly.

### Resolving Connectors

There will be times when a Module cannot automatically resolve the Connector and it needs to be resolved manually. A module that is not resolved will appear as an Unresolved Connector in the Viewport and have a red `none` definition in the Module Hierarchy panel. Connectors can be manually resolved using the following methods:

-   Selecting an unresolved element in the Viewport and using the **Use Selected Arrow** button adjacent to the element in the Module Hierarchy panel will input that element to the Connector and may resolve the issue. ![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/aa5c993c-c002-47fd-9ae1-f8e793c476e1/image_21.gif)
    
-   In the Module Hierarchy panel, you can use the hierarchy drop down menu on the unresolved Connector in order to manually assign the bone or socket to be used as the resolve. This will respect the Connector rules and only show the type filtered by the rules. ![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/78600786-11c0-4bf0-81fc-2c67f406f7d2/image_22.gif)
    
-   When a Module is added to the rig, the **Connector Event** included with the Module will execute automatically, thus trying to resolve all the connectors with the logic provided.
    

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b6a2c69b-68b5-417b-943a-3a570f68d337/image_23.png)

You can also manually execute this function by **right clicking** on the unresolved Connector or Connectors in the **Module Hierarchy** panel and selecting the **Auto Resolve** option in the Context Menu**.** ![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4cc043e6-bebf-4cc1-8947-eeaf8ed35efb/image_24.gif)

## Animate a Modular Control Rig

Modular Control Rigs work exactly the same as a regular Control Rig inside of Sequencer and the viewport. For more information about animation Control Rigs in Unreal Engine, see the following documentation:

You can drag and drop a Modular Control Rig asset directly into the level to start animating the character.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d4562c68-12c1-49e0-9d22-216ff97ddea2/image_25.gif)

## Module Authoring

A **Module Author** creates the Modules that will be utilized by a Modular Control Rig. Unreal Engine’s Control Rig is the underlying framework for authoring modules so an understanding how to create Control Rig graphs is a prerequisite. For more information about Control Rigs in Unreal Engine, see the following documentation:

%animating-characters-and-objects/ControlRig:topic%

### Control Rig Modules Plugin

The Modular Control Rig system does not require the installation of the Control Rig Modules plugin, and is not required to start building and using Modular Control Rigs in Unreal Engine. However, in order to use the pre-configured Modules, you can optionally install the Control Rig Modules plugin to use, edit, or learn from. The plugin contains example custom Modules that you can use to build a Modular Control Rigs or to create your own custom Modules. This plugin is designed to be optional and can be loaded and unloaded depending on your project’s needs.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b3018756-cf16-4ba5-aa2c-282312aae652/image_26.png)

#### Root Module

If you are creating and using custom Control Rig modules, you can set which Root Modules should be used when creating new Modular Control Rigs. The initial Root module can be changed inside the **Project Settings** using the **Default Root Module** setting in the **Control Rig** section**.** The default Root module asset is located in the Control Rig Plugin folder and should be **edited with caution**.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/abf06488-e1c1-4c1f-85af-6242c2d6acc3/image_27.png)

It is recommended to use this Module as it exists. It is better to create a new Root Module to edit that resides in your project or with your asset.

## Creating your first Module

Here you can reference an example workflow of creating a custom Module for a Modular Control Rig.

### Create a New Module

1.  Create a new **Control Rig** asset in the Content Browser.
    
2.  Open up the Control Rig and convert it to a module by using **Switch to Rig Module**.
    

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6f3d7aca-7422-4ca4-8042-dffea8465a1a/image_28.png) ![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8f108600-ffa7-4db2-907b-c5dc16b87f82/image_29.png)

1.  Import a Skeletal Mesh. This will serve as a **template** for building your Module. There are prebuilt **templates** that can be used in the **ControlRigModules** plugin as shown below, or you can use your own. ![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/aa91a2bd-e992-44b9-8dd9-a3caaaebc7a4/image_30.png)

Since the module will be referencing this asset, it should be as lightweight as possible.

1.  Set the following properties in the **Class Settings:**

| Property | Setting |
| --- | --- |
| **Name** | Set the Module name that will show in the Modular Rig editor. |
| **Type** | Set the kind of Module this is (default to Module). |
| **Icon** | 
Set a visual icon to show in the Modular Rig editor. You can select one of the provided icons using the drop down menu in the property.

Packaged with the Control Rig Modules plugin is a series of prebuilt icons that you can use or modify for your new modules. You can find these assets located in the following file path: `…Engine > Plugins > Control Rig Modules Content > Modules > Icons`

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/660d3779-4819-4b60-ac3f-de2efda50e7d/image_31.png)

 |
| **Category** | Here you can set a categorization value for the module. |
| **Keywords** | Keywords to describe the module. |
| **Description** | Here you can give a description of the Module that will appear in instances such as when you hover over the Module in the Editor. |

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/47df35ab-b93a-45e7-9865-dc9ebb377a2d/image_32.png)

### Creating Connectors

Rig Authors need to tell the Module how to connect to a Skeleton. This is accomplished by using **Connectors.** Connectors are responsible for returning hierarchy information such as bones and Controls. They act as a reference for these hierarchy elements so an Author can create a module that potentially works on many different skeletons that might have a different hierarchy structure or naming scheme.

There are two **types** of Connectors:

| Type | Description |
| --- | --- |
| **Primary** | 
Modules can only contain one Primary Connector. It is recommended that Primary Connector resolves to a socket on the Skeletal Mesh.

When creating a Primary Connector you should consider the following:

-   There can be only one Primary Connector per Module which is created automatically when a Control Rig asset is converted to a Module.
-   The Primary Connector is the first connector to be resolved, and should resolve to a socket on the Skeletal Mesh.
-   It is recommended to give the Primary Connector the Socket Type Rule.



 |
| **Secondary** | 

Modules can contain multiple Secondary Connectors. It is recommended that these Connectors resolve to Bones, Nulls, or Controls.

When creating Secondary Connectors, you can think of them as any additional Connectors that need to be resolved for the Module to function for the purpose you are designing it. There can be multiple Secondary Connectors per module.

It is recommended to give Secondary Connectors the Bones, Controls, or Nulls Type Rules, depending on how it is resolving to your Skeletal Mesh.

If a Secondary Connector is Optional the connector does not have to resolve for the module to work properly.



 |

Connectors can contain **Rules.** These rules dictate what can resolve to that connector. Here you can reference a list of the available rules you can assign to a Connector, and a description of their functionality:

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c75b2059-333d-4db5-b043-24fa86447a3a/image_33.png)

| Rule | Description |
| --- | --- |
| And Rule | Resolved element must meet all rules set. |
| Child of Primary | Element exists under the hierarchy of the Primary Connector. |
| Or Rule | Resolved element must meet either of the rules set. |
| Tag Rule | Resolved element must be tagged with this tag. |
| Type Rule | Resolved element is of specified type. |

#### Connector Event

The Connector Event provides a way to build graph logic that will try to **Auto-Resolve** the Secondary Connectors in the Module upon creation during the drag and drop phase while rigging a Modular Asset.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c1f2a4a5-989e-42ad-87e6-008329b7a59f/image_34.png)

### Sockets

A **Socket** is defined in the Character’s Skeleton asset and is used to connect the Modules to the Skeletal Mesh. For example, an Arm Module can be set to connect to the Spine Socket, allowing the Spine to drive the Arm. Sockets are displayed visually in the Editor Viewport as a circle.

### Metadata

Modules can contain metadata on the module level that external modules can access. There are two Control Rig Nodes that utilize this metadata:

| Control Rig Node | Description |
| --- | --- |
| Get Module Metadata | Retrieve the specific metadata at the scope provided. |
| Set Module Metadata | Create new metadata at the scope provided. |

Metadata can be accessed at the Root, Parent, or current Module level. For example, metadata for storing the global size of the controls might live at the Root level, whereas the hand control created in the Arm Module might live in the parent metadata scope.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1a75fd96-8aba-444a-899d-6152124d9277/image_35.png)

### Pre and Post Forwards Solve

The **Pre Forwards Solve** allows rig logic to be executed before the Forwards solve is executed. The **Post Forwards Solve** allows rig logic to be executed after the Forwards solve is executed.

This is helpful for having a Module edit the rig logic of another Module that pre-existed, such as a Foot Module editing the Leg Module to create a Foot Roll setup.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7d8a51e9-5c90-4e99-9188-509a1e2a3900/image_36.png)

## Technical Appendix

Here you can reference additional technical information about using Modular Control Rigs in Unreal Engine.

### Execution Order

The Modular Control Rig contains references to its Modules. Each Module runs independently from the other Modules, but there’s a concrete order of execution. Modules are executed in the order in which they appear in the module tree, for example, root to leaf, or *Spine > Leg > Foot*. All modules are executed on the same thread sequentially, so it is not possible to multithread the Modular Control Rig Graph execution.

For example, the Construction event runs for all Modules, the Forwards solve runs for all modules, and so on.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/80533ab0-c073-485a-a449-c2e6b6cc9e1b/image_37.png)

In future releases we may offer more control over how the order of Module execution is determined. Certain scenarios may require skipping a module temporarily, or running a Module twice. We may also offer to change the order of execution completely.

### Execution Stack

Modular Control Rigs do not use a VM (Virtual Machine) for itself, even though each module may use a VM. As a result of the execution stack, the Modular Rig is empty or not visible in the user interface.

In a future release we may add more functionality to allow the Modular Rig to use its own VM for advanced scenarios, at which point the execution stack may become visible again.

### Performance

Modular Control Rigs are currently more performance expensive than a single inlined Control Rig, the performance difference should be marginal though.

We expect the benefits of ease-of-use and speed of building a character rig to outweigh the performance hit. We’ll improve the performance in the future however, in order to close the gap and possibly even succeed to make the Modular Rig faster than a comparable inlined Control Rig. There are many potential performance improvements on the horizon to look forward to.

### API

The Modular Rig *(`UModularRig`)* is managed by its *model (`FModularRigModel`)*, which contains the list of module references, resolved connectors, and variable bindings. Additionally we offer the *controller (`UModularRigController`)*, which can be used to perform changes to the Modular Rig.

The Modular Rig is a special Control Rig, so it shares all of the Control Rig API, and adds its own additional API to it.

#### Python

In Python the model and controller can be accessed using the following scripts:

```

`model = rig_blueprint.modular_rig_model  controller = rig_blueprint.get_modular_rig_controller()`

Copy full snippet
```
model = rig\_blueprint.modular\_rig\_model controller = rig\_blueprint.get\_modular\_rig\_controller()