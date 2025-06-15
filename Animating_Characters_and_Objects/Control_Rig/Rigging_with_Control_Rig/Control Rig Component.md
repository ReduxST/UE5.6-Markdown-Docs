# Control Rig Component

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/control-rig-in-blueprints-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/control-rig-in-blueprints-in-unreal-engine)  
**Processed:** 2025-06-14 16:15:42

---

**Control Rig** can be called in Blueprints using the **Control Rig Component**. Using this component, you can drive Control Rigs with gameplay logic in Blueprints, reinitialize Control Rigs to fit differently proportioned characters, and attach non-skeletal mesh objects to the Control Rig hierarchy.

This document provides an overview of the Control Rig Component, how to add it to your Blueprint, and the features it enables.

#### Prerequisites

-   You have created a Control Rig asset for a character and know how to create controls. See the **[Control Rig Quick Start](/documentation/en-us/unreal-engine/how-to-create-control-rigs-in-unreal-engine)** page for information on how to do this.
-   You have created an **Actor Blueprint** that contains a skeletal mesh component, and have an understanding of **[Blueprints Visual Scripting](/documentation/en-us/unreal-engine/blueprints-visual-scripting-in-unreal-engine)**.

## Component Setup

The **Control Rig Component** is created by clicking the **Add (+)** button in the Blueprint Components panel and selecting **Control Rig** in the **Animation** category.

![create control rig component](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/204272d7-8a19-4d5c-b0fe-f907c6b32d1b/addcomponent.png)

Next, select the **Control Rig Component** and assign your default **Control Rig Class** in the **Details** panel. Click the dropdown menu next to Control Rig Class and assign your class.

![control rig class](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bce65278-78ea-48cf-9d7e-df841ef00e8c/class.png)

After assigning the Control Rig Class, bones from the Control Rig will be visible in the viewport. You can hide these by disabling **Draw Bones** in the Control Rig Component Details panel.

![draw bones](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/542cac33-3c9b-46f4-a9cf-b6c0506c24c1/drawbones2.gif)

### Mapping Setup

Lastly, you will need to **map** the Control Rig to the Skeletal Mesh, which must be done on the **Pre Initialize Event** from the Control Rig Component. This is done to form the connection between the **Skeletal Mesh Component** and the **Control Rig Component**.

With the Control Rig Component selected, click the **Add (+)** button next to **On Pre Initialize** in the Details panel. This will create the corresponding event in the Event Graph.

![on pre initialize event](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2dd9a962-94d5-4cac-b3ff-fdf0919ca69a/preinitial.png)

Next, drag from the **Component** pin and select **Add Mapped Skeletal Mesh** from the context menu. Add a reference to your Skeletal Mesh Component, and connect it to the **Skeletal Mesh Component** pin.

![add mapped skeletal mesh](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/451c5e8d-53aa-4717-bc31-fb3b5d7ddb3e/mapping.png)

## Overview

Once you have completed the [**Component Setup**](/documentation/en-us/unreal-engine/control-rig-in-blueprints-in-unreal-engine#componentsetup), you can start using the Control Rig Component in your blueprints. With it, you can use basic functions, such as getting or setting **[Rig Elements](/documentation/en-us/unreal-engine/controls-bones-and-nulls-in-control-rig-in-unreal-engine)**, editing details, and creating new mapping connections.

![control rig functions](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a4657d7b-1798-45c6-bf20-38515c56864a/overview.png)

### Details

The following is the list of relevant details of the Control Rig Component:

| Name | Description |
| --- | --- |
| **Control Rig Class** | The Control Rig Class to instantiate. A Control Rig asset must be specified here. |
| **Mapped Elements** | This array is used to manually define default mappings for the Control Rig |
| **Reset Transform Before Tick** | Enabling this will cause Control Rig transforms to update before each tick. |
| **Reset Initials Before Setup** | Enabling this will cause the initial transforms on Bones, Nulls, and Controls to reset prior to the **Setup Event**. |
| **Update Rig on Tick** | Enabling this ensures the rig will update when the component ticks. |
| **Update in Editor** | Allows for Control Rig behavior to be visible in the viewport without needing to play or simulate. |
| **Enable Lazy Evaluation** | Enabling this will make the Control Rig only evaluate if any of the mapped inputs have changed. |
| **Position Threshold** | The position or translation threshold to use when **Lazy Evaluation** is enabled. |
| **Rotation Threshold** | The rotation threshold in degrees to use when **Lazy Evaluation** is enabled. |
| **Scale Threshold** | The scale threshold to use when **Lazy Evaluation** is enabled. |
| **Draw Bones** | 
Enables drawing bones imported from the **Control Rig Class**.

![draw bones](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ff75ba3b-fd5d-47d0-b88f-a5b315232f71/drawbones2.gif)

 |

### Events

Control Rig can call the following events from the Control Rig Component. These events can be added to the Event Graph by either selecting the Control Rig Component and navigating to the **Events** category in the Details panel, or by right-clicking in the Event Graph and selecting **Add Event for Control Rig > Control Rig**.

![control rig blueprint events](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/053fed63-5267-40a0-96d9-8aa9799bfad9/events.png)

| Name | Image | Description |
| --- | --- | --- |
| **On Pre Initialize** | ![on pre intiialize](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0571fa02-4c68-4494-bd39-22f1e6569f1d/event_preinitial.png) | This event gets called before the Component's Control Rig is initialized. It can be used for setting transforms or additional variables in Control Rig before the Control Rig Component is initialized. In typical Control Rig setups, this event fires once, similar to Event Begin Play. |
| **On Post Initialize** | ![on post initialize](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/06b60aaf-dab8-4288-9364-e999a1200dee/event_postinitial.png) | This event gets called after the Component's Control Rig is initialized. It can be used to set transforms or additional variables in Control Rig after the Control Rig Component is initialized. In typical Control Rig setups, this event fires once, similar to Event Begin Play. |
| **On Pre Setup** | ![on pre setup](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/696ba314-0754-4c0d-9806-3a27e198d186/event_presetup.png) | This event gets called before the Setup Event of the Component's Control Rig. It can be used for setting transforms or additional variables in Control Rig before Control Rig's Setup Event. In typical Control Rig setups, this event fires once, similar to Event Begin Play. |
| **On Post Setup** | ![on post setup](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/56f7bbc2-4b46-4b9e-a325-c78f19f0b92e/event_postsetup.png) | This event gets called after the Setup Event of the Component's Control Rig. It can be used for setting transforms or additional variables in Control Rig after Control Rig Setup Event. In typical Control Rig setups, this event fires once, similar to Event Begin Play. |
| **On Pre Forwards Solve** | ![on pre forwards solve](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b7e5b0b8-6951-4615-9e8f-fd5e4be87e55/event_preforwards.png) | This event gets called before the Forward Solve of the Component's Control Rig. It can be used for setting transforms or additional variables in Control Rig before its Forwards Solve. In typical Control Rig setups, this event continuously fires, similar to Event Tick. |
| **On Post Forwards Solve** | ![on post forwards solve](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/103bcd8f-c33c-43fd-83ae-07f09d92b00f/event_postforwards.png) | This event gets called after the Forward Solve of the Component's Control Rig. It can be used for setting transforms or additional variables in Control Rig after its Forwards Solve. In typical Control Rig setups, this event continuously fires, similar to Event Tick. |

## Mapping

During the Setup phase, you are required to map the entire Skeletal Mesh Component to the Control Rig Component. However, you can also map specific elements within your Control Rig to other Components. Mapping is bi-directional, meaning that Control Rig elements can either affect Components, or be affected by them. In this way, mapping is somewhat similar to attaching.

By default, mapping is generally achieved by matching the bone names from the **Control Rig Class** to the **Skeletal Mesh Component**. In this way, you can imagine that when both components are in use, that there are two different skeletons operating within your Blueprint. Mapping allows for both of these skeletons — and other components — to affect one another.

Mapping elements can be done in the following ways:

### Manual Details Mapping

In the **Details** panel, under the **Animation** section, the Control Rig Component has a **Mapped Elements** array. By clicking the **Add (+)** button, you can manually add information to map and connect elements to the Control Rig.

![details mapping](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3c3eb1b4-913f-4f66-928c-17b7f51a9532/detailmap.png)

For example, if you want to map a Camera Component in your blueprint so that a Control affects its position, then input the following properties:

-   Set **Component Name** to **Camera**, so it matches the Camera Component.
-   Set **Element Type** to **Control**, as that is the Control Rig element you are mapping to.
-   Set **Element Name** to **Camera\_ctrl**, which is the name of the Control Rig Element you are mapping to.
-   Set **Direction** to **Output**, in order to define the direction of the mapping. In this case, Output is causing the Control element to dictate the transform of the Camera. If **Input** was specified, then the Camera Component would dictate the Control element instead.

![details mapping](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f642b868-0f9d-4dea-b930-55fbbf76a453/detailmap2.png)

The following properties can be used to create your mapping settings.

| Name | Description |
| --- | --- |
| **Component Reference** | The Blueprint Component to define by name. If the Control Rig Component is in an Actor-based Blueprint, it defaults to **Self** as the Referenced Actor if no name is specified. |
| **Transform Index** | An optional index value for Components with multiple transforms. |
| **Transform Name** | An optional name value for Components with multiple individualized transform names, such as sockets in skeletal meshes. |
| **Element Type** | The Rig Element type in Control Rig that the Component is an input or output of. You can choose from Bones, Controls, Nulls, Curves, Rigid Bodies, and References. |
| **Element Name** | The Rig Element name in Control Rig that the Component is an input or output of. |
| **Direction** | 
Determines the direction of control between the mapped Blueprint Component and Control Rig Element.

-   **Output** will cause the Control Rig Element to affect a Blueprint Component.
-   **Input** will cause a Blueprint Component to affect the Control Rig Element.



 |
| **Offset** | A transform offset to apply to the mapping. |
| **Weight** | The factor of the mapping. |
| **Space** | The transform space that the mapping should be defined on. |

### Dynamic Graph Mapping

You can also dynamically add, or change mappings in the Event Graph. This is done using several different Functions and Structs, which achieve different levels of mapping.

#### Add Mapped Skeletal Mesh

This node takes a Skeletal Mesh Component and maps the bones of the Skeletal Mesh to the Preview Mesh in the Control Rig used in the Control Rig Component. This is a Control Rig to Skeletal Mesh mapping link. Typically this node is used when performing initialization of the Control Rig in Blueprints.

![add mapped skeletal mesh](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b53b757d-0d80-4689-8cb4-c2bc7fa04bf9/map_skelmesh.png)

#### Add Mapped Skeletal Mesh Bone Array

This node maps either an array of **Bones** or **Curves** between a Skeletal Mesh Component and Control Rig Component. Additionally, you can specify **Source** and **Target** names if the Control Rig Skeleton and Skeletal Mesh Skeleton contain different bone or curve names from one another. This provides a similar workflow to "Find and Replace" names, however it operates only for individual bones or curves.

![add mapped skeletal mesh bone array](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8248530f-b335-44b5-a2c2-aafe9c2c18ee/map_skelmesharray.png)

Only the bones or curves from either array will be mapped. If you want to map the entire skeleton as well, then you can follow this node with [**Add Mapped Skeletal Mesh**](/documentation/en-us/unreal-engine/control-rig-in-blueprints-in-unreal-engine#addmappedskeletalmesh).

#### Add Mapped Elements

This node maps an array of Blueprint Components to the Control Rig Component. These components are defined by the **Make ComponentReference** and **Make ControlRigComponentMappedElement** structs. The properties and format of these structs are the same as when [**mapping from the Details panel**](/documentation/en-us/unreal-engine/control-rig-in-blueprints-in-unreal-engine#manualdetailsmapping).

![add mapped elements](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1ca719ee-f615-4a7a-85b2-b8d65139e8b4/map_elements.png)

#### Add Mapped Components

This node maps an array of Blueprint Components to the Control Rig Component. These components are defined by directly referencing the component and the **Make ControlRigComponentMappedComponent** struct. The properties of this struct is a streamlined variant of the **Make ControlRigComponentMappedElement**, providing only the most common mapping properties.

![add mapped components](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/30b39670-2491-414c-a00c-e2f44012b382/map_components.png)