# Customizable Sequencer Track

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/customizable-sequencer-track-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/customizable-sequencer-track-in-unreal-engine)  
**Processed:** 2025-06-14 16:18:13

---

Using Blueprints and child classes, you can create your own customizable Sequencer tracks. This feature can be used to extend Sequencer track functionality without using C++. It can be useful for prototyping or implementing new tracks you may need on your project.

This document provides an overview of the Custom Sequencer Track feature, how to create new track types, and the various functions used to communicate with common Sequencer objects.

#### Prerequisites

-   The Customizable Sequencer Track feature is a [Plugin](/documentation/en-us/unreal-engine/working-with-plugins-in-unreal-engine) that must be enabled prior to use. From Unreal Engine's main menu, go to **Edit > Plugins**, locate **Customizable Sequencer Tracks** in the **Runtime** section, and click the checkbox to enable it. Then, restart Unreal Engine.
    
    ![customizable sequencer tracks plugin](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9bb0e03b-da3c-4118-a0a6-7941a04b4211/plugin.png)
    
-   You should be familiar with creating and using [Blueprints](/documentation/en-us/unreal-engine/blueprints-visual-scripting-in-unreal-engine).

## Create New Track

New custom Sequencer tracks require creating three different Blueprint classes that are inherited from:

-   `SequencerSectionBP`
-   `SequencerTrackBP`
-   `SequencerTrackInstanceBP`

To do this, in the **Content Browser**, click **Add (+) > Blueprint Class**, then navigate in the **All Classes** section to these three classes. Create a new child Blueprint class for each one.

![create track classes](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ed3d6383-a18e-403b-80f9-2b96ad83cde5/create1.png)

Next, you must associate the different classes so they communicate. To do this, open the new Blueprint that inherits from `SequencerTrackBP` and set the following properties in the **Class Defaults** section of the **Details** panel:

-   Set **Default Section Type** to the new Blueprint that inherits from `SequencerSectionBP`.
-   Set **Track Instance Type** to the new Blueprint that inherits from `SequencerTrackInstanceBP`.

![set track properties](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5bc80941-770e-4a9b-9cff-fe14c659a3d5/create2.png)

After you compile and save the Blueprint, you can now add the track as a master track from Sequencer's main **Add Track (+)** menu.

![add custom track to sequencer](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/032e31fe-9610-4fe8-8ec7-87401ccd1d4d/create3.png)

## Creating Track Logic

Although you can now create your new track in Sequencer, its sections have no logic, so nothing will happen when you create the track. To start making logic for your track, open the new Blueprint that inherits from `SequencerTrackInstanceBP`. In the Functions section, you can override Events to add them to the Event Graph, where you can create Blueprint logic.

![override functions](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/841f5d36-d866-41a2-909b-18d0c70b760c/logic1.png)

### Section Events

The following section events can be overridden in the `SequencerTrackInstanceBP` Event Graph.

| Name | Image | Description |
| --- | --- | --- |
| **OnBeginUpdateInputs** | ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/11592ef6-0f0d-4f84-94f6-369cc126a72e/event1.png) | This event executes when a section is about to begin or end. It executes first, but after **OnInitialize**. |
| **OnEndUpdateInputs** | ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/82141365-8686-4b77-95af-c639799bb6d0/event2.png) | This event executes when a section has finished beginning or ending. It executes after **OnBeginUpdateInputs** and **OnInputAdded/Removed**. |
| **OnDestroyed** | ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/29f87bc3-0cb3-428a-84da-07ef227af487/event3.png) | This event executes when a section is ending and there are no other sections playing. It executes last. |
| **OnInitialize** | ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/212af769-7097-47ed-92e4-a4b42a349da3/event4.png) | This event executes when a section is starting and there are no other sections playing. It executes first. |
| **OnInputAdded** | ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/35d18414-2272-496e-b242-0ca28decdac9/event5.png) | This event executes when a section is starting. It executes after **OnBeginUpdateInputs**. |
| **OnInputRemoved** | ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9d409ad4-54d8-4901-80eb-c91616d0f2d5/event6.png) | This event executes when a section is ending. It executes after **OnBeginUpdateInputs**. |
| **OnUpdate** | ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/28aa9088-a55e-4b30-9d66-bb058d28d814/event7.png) | This event executes continuously every frame as long as any section is active. When first initializing a section, it starts executing after **OnEndUpdateInputs**. |

As an example, this image shows the total execution order of all singular events in a multi-section scenario:

![execution order](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/81d9ec60-c38d-4ecc-9801-05ac7b091c95/event8.png)

Custom Sequencer Tracks only use [sections](/documentation/en-us/unreal-engine/creating-animation-keyframes-in-unreal-engine#sections), and not keyframes.

### Section Functions

When building logic in the `SequencerTrackInstanceBP` child Blueprint, you can use the following functions to get section or owning object information:

| Name | Image | Description |
| --- | --- | --- |
| Get Animated Object | ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c66a1745-a85a-483f-959f-e1b249829b04/function1.png) | 
Gets the object or Actor that this track is a child of, if [Track Type](/documentation/en-us/unreal-engine/customizable-sequencer-track-in-unreal-engine#sequencertrackbp) is set to **Object Track**. This function should be paired with a **Cast** function to get a usable Blueprint reference of the returned object.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/76ce47e5-46f9-4574-9558-825c3c78768f/function5.png)

 |
| Get Input | ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f8a2a03e-b5fd-4e57-9f2e-967053f26a2b/function2.png) | 

Gets the currently playing section according to the index (if more than one section is playing). The default return pin is a struct that must be broken to access the actual section object. You can break it either with **Break SequencerTrackInstanceInput**, or by right-clicking the pin and selecting **Split Struct Pin**.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0e9ccc1a-7553-4650-b002-b8999ad826fb/function6.png)

 |
| Get Inputs | ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/66bbc7cb-81a3-4ecd-bb9a-bc87a9b9a632/function3.png) | Returns an array of currently playing sections. |
| Get Num Inputs | ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/02b35a39-eec5-475b-8bf1-3cf798ef4c61/function4.png) | Gets the number of currently playing sections. |

## Overview of Classes

This section contains information about the three main Blueprint classes that make up the custom track as well as their properties.

### SequencerSectionBP

SequencerSectionBP is a transient class that is constructed at runtime. You can also use it to set default section properties, which can be overwritten on the section properties in Sequencer. To access and change these properties, navigate to the **Class Defaults** section in the **Details** panel.

![sequencer section class properties](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/64bd6a89-4bb9-4d8c-bb15-1ae038fad39e/classes1.png)

| Name | Description |
| --- | --- |
| **Timecode Source** | The default timecode information for the section, if timecode is being used. You can also specify delta frames here to control offset information. |
| **Is Active** | Sets whether or not the section is [active](/documentation/en-us/unreal-engine/sequencer-track-list-in-unreal-engine#mute) by default |
| **Is Locked** | Sets whether or not the section is [locked](/documentation/en-us/unreal-engine/sequencer-track-list-in-unreal-engine#lock) by default. |
| **Pre / Post Roll Frames** | Specifies extra padding to apply to the start and end regions of the section by default, which causes the first and last frame of the section to be held for the specified duration |

### SequencerTrackBP

This class is used to set general properties and rules for the track, such as name, type, and supported sections. To access and change these properties, navigate to the **Class Defaults** section of the **Details** panel.

![sequencer track properties](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/587b37a4-4fc3-4aca-9d12-3fa931b55458/classes2.png)

| Name | Description |
| --- | --- |
| **Supports Multiple Rows** | 
If enabled, this allows for the track to encompass multiple sub-tracks (rows). This can be useful if you intend to layer data using this track.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/754254c6-234f-4c1f-aa00-aa3bfef3a99e/classes3.png)

 |
| **Supports Blending** | Enabling this will allow the sections to blend between each other. |
| **Track Type** | 

Sets in what context this track can be added and exist in Sequencer. You can select either:

-   **Master Track**, which adds the track to the main Add Track (+) menu in Sequencer. This makes the track a top-level Sequencer track.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3fef4108-6f22-4328-a038-6e98c9cff009/classes4.png)
    
-   **Object Track**, which adds the track to another track's Add (+) menu. The parent track is dependent on the object class defined in **Supported Object Type**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/48e826e5-6ebd-4afa-aa35-3d2a42093975/classes5.png)
    



 |
| **Supported Object Type** | If **Track Type** is set to **Object Track**, this property is used to specify which object type this track can be added under. |
| **Default Section Type** | Specifies the inherited base `SequencerSectionBP` class created as part of the required track setup. |
| **Supported Sections** | 

An array where you can add additional `SequencerSectionBP` classes to add from the track's **Add Section (+)** menu. You can use the various **Get Input** functions when creating your logic to differentiate these sections.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e64c9329-5e92-4563-aecc-8819d82dca71/classes6.png)

 |
| **Track Instance Type** | Specifies the inherited `SequencerTrackInstanceBP` class created as part of the required track setup. |
| **Icon** | 

Displays a preview of the track's icon. Expanding this property reveals the following icon properties:

-   **Image**: The texture or material to use as the icon image.
-   **Image Size**: The size and X/Y dimensions of the image.
-   **Tint**: The color of the image. Enabling **Inherit** will disable any color tinting and instead use the parent widget color.
-   **Draw As**: You can select different methods to draw the icon: **Box**, **Border**, **Image**, or **Rounded Box**.
-   **Tiling**: Enables tiling the image in **horizontal**, **vertical**, or **both** directions.
-   **Preview**: An area to preview the final look and size of your icon.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/463b27d4-3433-40f9-a8e1-b7d1bf3c64f7/classes7.png)

 |
| **Display Name** | 

The default name for the track. This can be overwritten in Sequencer through normal track renaming operations.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/af32797d-0197-4f64-98f6-9e95f1abbc5d/classes8.png)

 |
| **Track Row Display Names** | 

An array where you can specify row names if **Supports Multiple Rows** is enabled. If more than one array element is added, then adding section rows will add all named rows at once.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e62298b6-8dbe-46bb-931e-aec2458c8dbf/classes9.png)

 |
| **Color** | 

Sets the default color for the track and its sections. You must ensure that the color's alpha value is not 0, otherwise the transparency will fall through to the default gray color.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9325806f-8ac4-4aeb-a5e3-a7c4b5d16286/classes10.png)

 |
| **Show Vertical Frames** | 

If enabled, this will cause section start and end bounds to display vertical lines in the timeline.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9a7c85d6-de12-46d9-86ab-13926991b8b1/classes11.png)

 |

### SequencerTrackInstanceBP

This class is used to create the primary logic and behavior of the track within the **Event Graph** by [overriding events](/documentation/en-us/unreal-engine/customizable-sequencer-track-in-unreal-engine#sectionevents) and [creating functions](/documentation/en-us/unreal-engine/customizable-sequencer-track-in-unreal-engine#sectionfunctions).

![track instance class](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/dcfd5f53-8844-4899-bada-0416594795d9/classes12.png)