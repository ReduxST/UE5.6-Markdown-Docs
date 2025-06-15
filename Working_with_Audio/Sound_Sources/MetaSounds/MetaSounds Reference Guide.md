# MetaSounds Reference Guide

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/metasounds-reference-guide-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/metasounds-reference-guide-in-unreal-engine)  
**Processed:** 2025-06-14 16:36:05

---

The **MetaSound Editor** is where MetaSounds are created, modified, and previewed. The **MetaSound Graph**, contained within the MetaSound Editor, is composed of a variety of pins and nodes which make up the design of every MetaSound.

The **MetaSound Graph** functions a bit differently than the graph found in Blueprints. In Blueprints, the graph functions as an execution graph, while in MetaSounds, the graph functions as a flow graph.

The pin and node types listed in this document are built-in types, but you can add your own types by using the C++ API.

## Asset Types

MetaSounds have two main asset types: **MetaSound Source** and **MetaSound Patch**. These two types are identical in terms of graph manipulation; however, only MetaSound Sources can generate audio on their own. MetaSound Patches are intended to be referenced by other MetaSounds to encapsulate and reuse functionality.

You can create a MetaSound asset by clicking the **Add** button in the **Content Browser** and selecting **Audio > MetaSound Source** or **Audio > MetaSounds > MetaSound Patch**. You can edit a MetaSound asset in the MetaSound Editor by double-clicking it in the **Content Browser** or by right-clicking it and selecting **Edit…** from the context menu.

## Presets

**MetaSound Presets** are a special type of asset that inherits a read-only graph from a parent MetaSound and provides the ability to override default Input values. This allows you to create multiple versions of the same MetaSound with different sets of Inputs, which can be helpful to decrease graph duplication.

Any changes to the parent MetaSound asset will be reflected in the child Presets. This ensures consistency among the affected assets and reduces the workload associated with applying changes in multiple MetaSounds.

You can create a MetaSound Preset in the **Content Browser** by right-clicking on the MetaSound Source or Patch you wish to be the parent, and then selecting **Create MetaSound Preset** from the context menu. In the MetaSound Editor, you can modify a Preset's Input values by selecting an Input in the **Members** panel, enabling **Default Value > Override Inherited Default** in the **Details** panel, and then changing the **Default Value > Default**.

If you want to convert a MetaSound Preset into a standard MetaSound asset, you can click the **Convert From Preset** button on the toolbar at the top of the MetaSound Editor.

## Adding Nodes

![Node Search](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f6ca4dd4-a4ef-4317-9560-3f215dcf91f9/node_search.png)

You can add nodes to your graph by right-clicking empty space in the graph and selecting the desired node type from the context menu. You can also drag a pin connection into empty space to create a connected node.

The context menu is equipped with a search box you can use to find node types by name and tag. For example, searching for "synth" will find nodes with names containing "synth" but also nodes relevant to synthesis.

## Pin Types

MetaSound nodes interact with a variety of data types through pin connections, both individual (circle connector) and array (block connector).

| Pin Type | Description |
| --- | --- |
| ![Trigger Pin](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cc15e7c2-f02a-4873-8025-9b76a69a248f/pin_trigger.png) Trigger | Comparable to modular synthesis triggers and are used to execute other nodes, similar to execution pins in Blueprints. They can be connected to multiple (or even zero) other nodes at once. |
| ![Audio Pin](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b2357698-fc93-4eba-b1cc-bd7ac3e5942d/pin_audio.png) Audio | Represent an actual audio buffer that can be manipulated by MetaSound nodes. In some instances, these pins may be parameters intended to be consumed at audio-rate, such as for frequency modulation synthesis. |
| ![Time Pin](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7ed52ee2-6942-44e0-8264-8d3ab3a72b52/pin_time.png) ![Time Array Pin](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8cb50cd2-7959-4e4b-9a66-59e87f744c69/pin_time_array.png) Time | Represent a time value (in seconds). |
| ![String Pin](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/78fc32d3-593c-48fb-9101-b1cc71ef3883/pin_string.png) ![String Array Pin](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/563deef4-ce05-44be-8e6d-9ed8e3aeb9d2/pin_string_array.png) String | Provide labeling and debugging functionality. These pins are not directly used during playback, but are useful for relaying information to the audio designer, such as outputting node information to the console log. |
| ![UObject Pin](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/62f6caf5-1ce6-4732-8c13-f7c3887ac2c8/pin_uobject.png) ![UObject Array Pin](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5664324b-cc78-4407-bdf5-9f4f31cae091/pin_uobject_array.png) UObject | Represent a supported UObject type, such as USoundWave which is commonly used to provide the **Wave Player** node with a reference to the asset to be played. |
| ![Bool Pin](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7e6f9ec3-b5fa-4470-8cf6-8470edf148dc/pin_bool.png) ![Boo Arrayl Pin](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/354a627e-ff74-4b63-bf22-e1d4793dceb3/pin_bool_array.png) Bool | Represent a boolean variable. |
| ![Float Pin](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/05f6d1b1-1789-4635-9d7b-f290471dbb3b/pin_float.png) ![Float Array Pin](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/067fbc20-ed2a-4af3-8925-2e3e89525575/pin_float_array.png) Float | Represent a floating-point number variable. |
| ![Int32 Pin](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/75bbc42d-48a1-4eb1-8f17-a2b97a9613e0/pin_int32.png) ![Int32 Array Pin](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/730994d3-d90f-401b-93d8-709f8b42d92b/pin_int32_array.png) Int32 | Represent an integer (4 bytes) variable. |
| ![Int32 Pin](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2c6706b3-2aed-4515-b40e-260a404c989b/pin_int32.png) ![Int32 Array Pin](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2c7812c1-97ba-4b2a-b3f6-d2996b73edaa/pin_int32_array.png) Enum | Represent an enumerated variable. |

When Trigger nodes are triggered through timing nodes or through gameplay events, they are sample-accurate and will execute on a precise sample index in the audio rendering block. However, since other node types do not operate at audio rate, a Trigger input may generate a block rate output if it is connected to another node type.

## Connections

![Connections](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/21425d5c-4bc3-4db6-b8e2-7debb1ae3f4b/connections.gif)

The connections between nodes are visualized on play to make understanding their behavior easier. Trigger connections pulse when they activate, Audio connections change in thickness with signal strength, and Float connections color shift based on value.

![Connection Visualization Customization](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1a614723-07a8-4548-b5a8-e10b19318a71/connection_visualization_customization.png)

Float connection visualization is disabled by default. While the MetaSound is playing, you can enable it by hovering your mouse cursor over the connection until a context menu appears. The context menu provides a toggle to enable or disable visualization, two numeric inputs to define the expected value range, and two color inputs to blend between.

Additional visualization settings are available in **Editor Preferences > MetaSound Editor > Graph Animation**.

![Reroute Node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/54d303f2-6874-470b-9515-d1dc4f57deae/reroute_node.gif)

You can use Reroute nodes to keep your connections organized. MetaSound Reroute nodes function similarly to those found in Blueprints. You can create one by double-clicking a connection. Afterwards, you can move it by dragging the border that appears while it is selected. You can make additional connections from the node by dragging from the node itself.

![Connection Straighten](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1bbc5782-cb19-49b8-bea8-e6dcc2e958e2/connection_straighten.gif)

You can also organize your graph with Alignment and Distribution operations by selecting all relevant nodes, right-clicking a selected node, and then selecting the desired operation from the context menu.

## Input and Output Nodes

![Input Nodes](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b2706161-61c4-43d5-8398-384697426ffa/input_nodes.png) ![Output Nodes](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b9aa4b3f-565a-48e1-b44f-47f38c2db7bf/output_nodes.png)

**Input** and **Output** nodes provide access to pins that typically begin or end a data flow through a MetaSound. For example, every MetaSound Source asset starts with an **On Play** Input node and an **On Finished** Output node. The On Play Input node has a Trigger pin output used to signal other nodes to begin when the MetaSound plays, and the On Finished Output node has a Trigger pin input used to receive a signal when the MetaSound finishes playing.

The On Finished Output node is added to the graph by the `UE.Source.OneShot` Interface, which is enabled on new MetaSound Sources by default. If the On Finished node is not triggered, the MetaSound will play indefinitely. To create a sound with an indefinite duration, such as for music or ambience, remove the `UE.Source.OneShot` Interface in the **Interfaces** panel.

![Channel Configuration](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d418b1fd-e71f-4ebc-88cc-818b3e2c9b9c/channel_configuration.png)

Some of the Output nodes, such as **Out Left**, correspond to an audio channel output. Each MetaSound has an Output Format setting to support different audio channel configurations, including Mono, Stereo, Quad (4.0), 5.1, and 7.1. You can find the setting by clicking the **MetaSound** button located next to the **Play** button, and then checking the **Details** panel.

You can create additional Inputs and Outputs in the **Members** panel of the MetaSound Editor. Afterwards, you can set the desired properties, such as **Display Name** and **Type**, in the **Details** panel. Next, you can create a new node instance by right-clicking an empty space in the graph and selecting the corresponding **Get Input** or **Set Output** node option from the context menu. You can also drag the Input or Output from the **Members** panel into the graph to create the new Input node instance.

![Input Widgets](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/912145d1-1b30-46b7-9d97-5f63e7d00e1d/input_widgets.png)

You can use a **Slider** or **Knob** widget on Float and Time Input nodes to easily change values while the MetaSound is playing for a much smoother workflow. This is set in the **Details** panel (with the Input selected), under **Editor Options > Widget**. You can also change the **Range**, **Orientation** (for Sliders), and **Value Type** in the panel.

### Output Watching

You can watch MetaSound Source Outputs with Blueprint or C++ to drive gameplay systems.

When watching an Output, you can do the following:

-   Fire events when the Output value changes.
-   Access the changed Output value.

To watch an Output, use the [Watch Output Blueprint node](/documentation/unreal-engine/BlueprintAPI/MetaSoundOutput/WatchOutput) or the [Watch Output C++ function](/documentation/en-us/unreal-engine/API/Plugins/MetasoundEngine/UMetasoundGeneratorHandle/WatchOutput).

In order for an Output to be watched, the containing MetaSound Source must be playing. Additionally, an Output on a MetaSound Patch cannot be watched.

If a watched Output is updated multiple times in a frame, the `On Output Value Changed` delegate will fire once for every update.

The following Output types are watchable:

-   Float
-   Int32
-   Bool
-   Time
-   FString
-   Trigger

You can also watch an Envelope Follower on an Audio Output by setting the following parameter values on the Watch Output function:

1.  **Output Name**: The exact name of the Audio Output in the MetaSound Source graph, such as `UE.OutputFormat.Mono.Audio:0`. You can find this by selecting the Audio Output node and looking at the **Details** panel under **General > Output**.
2.  **Analyzer Name**: `UE.Audio.EnvelopeFollower`
3.  **Analyzer Output Name**: `EnvelopeValue`

## Constructor Pins

![Constructor Pins](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/19950289-e5c5-475a-bebe-8de2e60cdd42/constructor_pins.png)

**Constructor** pins are indicated by diamond-shaped icons. They have read-only values which can improve the performance of a MetaSound by not dynamically updating at runtime. In this way, they are similar to the `const` declaration in C++.

You can make pins on **Input** and **Output** nodes into constructor pins by checking the **Is Constructor Pin** checkbox in the **Details** panel. All data types (including array types) that support copy assignment and construction can support constructor pins. However, **Trigger** and **Audio** types cannot be constructor pins.

You can only set Constructor pin values before playing the MetaSound. You can do so in the **Details** panel or by using the **SetParameter** node in Blueprint.

Connection constraints apply when working with constructor pins. You can connect an output constructor pin to both constructor and non-constructor input pins, but an input constructor pin can only be connected to constructor output pins.

You cannot override Constructor pin status on MetaSound Presets.

## Variable Nodes

![Variable Nodes](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6cc2c421-d552-497f-8362-4102ff1db09b/variable_nodes.png)

You can use **Variable** nodes to access and manipulate variables that support Function nodes in your MetaSound. Three node types exist for each individual variable in your asset: **Get Variable**, **Get Delayed Variable**, and **Set Variable**. Get Variable and Set Variable provide immediate read or write access to the associated variable, whereas Get Delayed Variable delays the read by a block and can be used to mitigate cycles.

Changes to Variables are not registered while a MetaSound is playing. Use Inputs instead to allow for value changes during playback.

Like Inputs and Outputs, Variables can be created in the **Members** panel of the MetaSound Editor and their properties set in the **Details** panel. You can create Variable node instances using the right-click context menu in the graph, but only the Get Variable node can be created by dragging from the **Members** panel.

MetaSound Variables cannot be accessed by Blueprints.

## Interfaces

**Interfaces** allow MetaSounds to work with other systems within the Unreal Audio Engine by providing access to specialized Inputs and Outputs. You can add or remove an Interface from your MetaSound from the **Interfaces** panel of the MetaSound Editor.

The following Interfaces are available:

-   **UE.Source.OneShot** - Allows you to create one-shot sounds by providing an **On Finished** Output which stops the MetaSound when triggered. This Interface is added by default and should be removed on MetaSounds with indefinite durations.
-   **UE.Attenuation** - Provides a **Distance** Input with a value based on the distance between the MetaSound and the listener.
-   **UE.Spatialization** - Provides **Azimuth** and **Elevation** Inputs with values based on the MetaSound's position in relation to the listener.

## Graph Nodes

![Graph Node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e3938f38-ae7d-479d-82b9-9b443713ab4f/graph_node.png)

**Graph** nodes allow for composition capability as they provide an access point to the graphs of other MetaSounds in your project. These nodes have connection pins based on the Inputs and Outputs of another MetaSound, so you can use them to influence the design of the MetaSound containing it.

Graph nodes can provide many workflow improvements. You can use them to:

-   Reduce the complexity and size of MetaSounds by separating the functionality into several smaller MetaSounds.
-   Reuse functionality from existing MetaSounds and eliminate the need for duplication.
-   Simultaneously alter MetaSounds containing the same Graph node by changing the referenced graph.

When using Graph nodes representing a MetaSound Patch, you must use a MetaSound Source in the composition to be audible.

## Conversion Nodes

![Conversion Nodes](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/83b54eaa-56d6-483c-aa0b-cb568f631c80/conversion_nodes.png)

**Conversion** nodes change one pin type into another supported pin type, similar to Blueprint conversion nodes.

#### Supported Conversions

| From | To |
| --- | --- |
| Audio | Float |
| Bool | Float or Int32 |
| Float | Audio, Bool, Int32, or Time |
| Frequency Multiplier | Semitone |
| Int32 | Bool, Float, Time, or Enum |
| Semitone | Frequency Multiplier |
| String | Transmission:Address |
| Time | Float or Int32 |
| Enum | Int32 |

## Comments

![Comment Box](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d3477d7d-e646-445b-9954-18d9c24b1294/comment_box.gif)

Putting comments in your graph is a great way to organize and document your design. You can add a comment box to your graph by right-clicking empty space and selecting **Add Comment** from the context menu, or by selecting multiple nodes, right-clicking, and then selecting **Create Comment from Selection** from the context menu. Afterwards, you can change the comment by double-clicking the text to select it and typing your desired comment.

The comment box's size can be adjusted by dragging the handle displayed on the lower-right corner. You can also change the color of a comment box by selecting it and modifying the **Comment Color** property in the **Details** panel.

By default, moving comment boxes in the graph moves all of the contained nodes as well. If desired, you can remove this behavior by changing the comment box's **Move Mode** to **Comment** in the **Details** panel.

![Comment Bubble](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/58f68f76-2381-46c2-b591-e0e9aae9a919/comment_bubble.gif)

You can also put Comment bubbles on individual nodes by hovering your pointer over the node and selecting the comment bubble button that appears at the top-left corner, or by right-clicking the node and inputting the desired comment into the **Node Comment** text box.

## Function Nodes

**Function** nodes come in many types and provide the functionality required to play audio files, mix sounds, apply filters and effects, and more.

For information on MetaSound Function nodes, see [MetaSound Function Nodes Reference Guide](/documentation/en-us/unreal-engine/metasound-function-nodes-reference-guide-in-unreal-engine).

## Builder API

![Builder API](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f583d80b-f972-4486-8a3f-f94cb7d42f12/builder_api.png)

By using the **MetaSound Builder API** with Blueprint or C++, you can dynamically create and modify MetaSound Sources and Patches in the Unreal Editor and at runtime. This speeds up MetaSound production and opens up powerful runtime possibilities.

The MetaSound Builder API has two subsystems that provide its functionality:

-   **MetaSound Builder Subsystem**: Supports dynamic generation of MetaSounds at runtime.
-   **MetaSound Editor Subsystem**: Supports building MetaSound assets using [Editor Utility Blueprints](/documentation/en-us/unreal-engine/scripting-the-unreal-editor-using-blueprints).

Use the MetaSound Builder Subsystem for:

-   Creating and auditioning MetaSounds at runtime
-   Creating inputs and outputs of all supported types.
-   Adding, connecting, and removing interfaces by referencing handles to nodes and inputs / outputs.
-   Setting and changing output formats.
-   Connecting and disconnecting MetaSound nodes.
-   Changing MetaSounds dynamically at runtime (after Audition, if Live Updates is enabled).

Use the MetaSound Editor Subsystem for:

-   Creating new MetaSound Source, Patch, or Preset assets.
-   Using other `USoundWave` assets as templates for Source settings.

For more information on the C++ API, see [MetasoundEngine C++ API Reference](/documentation/en-us/unreal-engine/API/Plugins/MetasoundEngine).

For more information on the Blueprint API, see [MetaSound Builder Blueprint API Reference](/documentation/unreal-engine/BlueprintAPI/Audio/MetaSound/Builder).

The supported Blueprint functions are found under **Audio > MetaSound > Builder**.