# MetaSound Builder API

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/metasound-builder-api-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/metasound-builder-api-in-unreal-engine)  
**Processed:** 2025-06-14 16:35:57

---

The **MetaSound Builder API** refers to the public Blueprint and C++ API that enables gameplay developers and designers to author MetaSounds procedurally from gameplay code with variations you can use to support different hardware performance levels. With the Builder API, you can create MetaSounds in memory without using the MetaSound Editor.

Additionally, builder-managed MetaSound Sources provide the following benefits:

-   You can serialize them at edit time.
-   You can play them at edit or runtime.
-   You can audition changes live with the Blueprint API. With this, you can produce audible feedback for multiple MetaSound graphs in real time with buffer crossfade support without pops or clicks due to graph changes.

The Builder API does not currently support variables. Paged inputs and graphs also have limited support and are not authorable by Blueprint nor outside of edit time from the frontend Builder API.

## Builder API Overview

The Builder API refers to a loosely related collection of classes or structs in the MetaSound plugin that enable the authoring and execution of MetaSounds.

The MetaSound Editor, Engine, Frontend, and GraphCore modules each have their a builder in charge of:

-   Managing MetaSound visualization,
-   UObject manipulation and reflection,
-   serialization,
-   execution.

This document covers how to author MetaSounds more broadly, the `BuilderSubsystem` class (in the MetaSound Engine module), and the `FrontendDocumentBuilder` struct (in the Frontend module).

![slide_3](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/260ad6ba-5ae3-416e-b0c0-0d3bfe168fc0/slide_3.png)

MetaSound `UObject` asset classes (`UMetaSoundSource` and `UMetaSoundPatch` types) contain a struct called the `MetaSoundFrontendDocument`.

The `MetaSoundFrontendDocument` contains:

-   All graph information necessary to build a `MetaSoundGenerator` instance for playback.
-   Style and display metadata utilized by the graph (including node placement coordinates, graph object display names, and widget display information).

The `MetaSoundFrontendDocumentBuilder` struct manipulates the `MetaSoundFrontendDocument` struct. The Blueprint-friendly classes discussed below wrap the `MetaSoundFrontendDocumentBuilder` struct.

## Introduction to Builder Blueprint UClasses

The following table provides an introduction to the primary Blueprint UClasses used when building MetaSounds.

| **Class Name** | **Context** | **Description** |
| --- | --- | --- |
| **MetaSound Builder Subsystem** | Editor / Runtime | Entry point to create and access MetaSound Builders. |
| **MetaSound Editor Subsystem** | Editor Only | Entry point for manipulating editor-only MetaSound data and exporting or serializing MetaSound assets. |
| **MetaSound Asset Subsystem** | Editor / Runtime | MetaSound-specific asset-loading/unloading related functionality. |
| **MetaSound Patch** | Editor / Runtime | Encapsulates shareable utility MetaSound graph behavior. |
| **MetaSound Source** | Editor / Runtime | Encapsulates a graph that outputs audio as a single sound source. |
| **MetaSound Document Interface** | Editor / Runtime | Base Interface implemented by all MetaSound UObjects as entry point to MetaSound Frontend Document struct. |
| **MetaSound Patch Builder** | Editor / Runtime | UObject used to mutate or query MetaSound Patch UObjects. |
| **MetaSound Source Builder** | Editor / Runtime | UObject used to mutate or query MetaSound Source UObjects. |

## Builder Graph Handles

The following UStructs are handles to various types of graph data found in a MetaSound Document.

Underlying handle IDs may be changed when versioning content or rebuilding a transient asset. You should never serialize these.

| **Handle Name** | **Description** |
| --- | --- |
| **MetaSound Node Handle** | Handle to a node in a MetaSound graph. |
| **MetaSound Node Output Handle** | Handle to a node output in a MetaSound graph. |
| **MetaSound Node Input Handle** | Handle to a node input in a MetaSound graph. |

## Builder Blueprint Functions And Editor Actions

Virtually all functionality in the Blueprint Builder API can be related to executable actions that can be performed in the MetaSound Editor.

The most common actions (paired with their MetaSound Editor equivalents) are listed in the sections below.

### MetaSound Construction

Utilizing the MetaSound Builder Subsystem, the following example shows the construction of a builder that creates a new analogous, internally managed MetaSound as it relates to creating a MetaSound from the Content Browser.

Constructing a Source builder returns the builder and handles the underlying MetaSound graph's inputs and outputs.

![slide_8](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0c3d5057-914b-4a22-997d-e6d3a7e99eb5/slide_8.png)

Some handles may be invalid or contextual depending on the options set on the Create Source Builder Blueprint node's input. For example, depending on the Is One Shot Blueprint input options, the returned OnFinished node input handle may or may not be valid.

![slide_9](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/351c04b7-430b-454c-a16d-803a070fa283/slide_9.png)

### Adding Or Removing Interfaces

Similar to utilizing the interface MetaSound panel in the MetaSound Editor, the Blueprint API enables adding and removing entire related sets of inputs and outputs using interfaces.

![slide_10](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7eb98081-9256-4126-845d-6e86ebf0864d/slide_10.png)

### Adding Nodes

You can add nodes with two functions. The first requires a class name and is for natively-defined node classes such as Mixer, Math, or Generator. The second function requires a reference to an object reference that implements a MetaSound Document Interface (for example, MetaSound Source or MetaSound Patch).

![slide_11](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d34db649-21e5-4481-88a8-131f83a530bb/slide_11.png)

You can determine the name of a natively-defined node class without access to the code by holding **Shift** while hovering a node's name in the MetaSound Editor. A tooltip will display debug info for that node, including the full class name.

![slide_12](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8495afc1-edc0-439a-bbdf-f21ac5eef3a5/slide_12.png)

The Blueprint Builder API does not support adding template nodes like reroutes. However, the native Frontend Document Builder API does.

### Accessing MetaSound Node Vertices

You can access individual inputs and outputs on a node with the **Find Node Input/Output** functions.

![slide_13](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1bc1c434-d931-4dd3-a584-231c9ed8b3f3/slide_13.png)

Depending on the module / code layer, node connection points may be called pins, vertices, or node inputs and outputs.

### Connecting MetaSound Node Vertices

You can apply connections between nodes by using the **Connect Nodes** function with corresponding input and output handles. This is equivalent to dragging connections between nodes in the MetaSound Editor.

![slide_14](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/01fd0600-a6f9-4652-b9d6-f27cd145fb4e/slide_14.png)

Depending on the module / code layer, the associations between vertices may be called connections or edges.

### Accessing Graph Input/Output Nodes

You can retrieve member node handles with the **Find Graph Input/Output** functions.

![slide_15](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5a0ce21d-1c18-4c19-8887-a40ca47b9f27/slide_15.png)

In the MetaSound Editor, you can hold **Shift** while hovering over a node's pin to display a tooltip with the code name of a given member. Vertices may have display names that differ from the FName.

### Element Removal

You can remove graph elements with the following functions:

-   **Disconnect Node** - Removes the connection between the provided input and output handles.
-   **Remove Node** - Removes the node associated with the given handle and any associated connections.
-   **Remove Graph Input/Output** - Removes the given graph vertex, node, and any associated connections.
-   **Remove Interface** - Removes the given interface and all related inputs, outputs, nodes, and connections.

![slide_16](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/25087b3a-e486-495b-ac0a-ea4ae685f775/slide_16.png)

## Builder Auditioning

One of the MetaSound Source Builder's most powerful features is the ability to audition changes to the underlying MetaSound Source's graph topology in real time.

You can use the **Audition** function on a source builder to play the managed MetaSound Source on the provided AudioComponent. If you set **Live Updated Enabled**, changes to the graph's topology will be instantly reflected.

![slide_17](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0d49db03-1176-41dd-a691-74a8e02ac17b/slide_17.png)

As of 5.5, Live Updates is a beta feature.

## MetaSound Editor Subsystem Builder Functions

You can use the **Find Or Begin Building** function to modify an existing MetaSound.

Due to requiring the **MetaSound Editor Subsystem**, you can only modify serialized MetaSound assets in editor builds.

![slide_18](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/611ad4d4-94c7-4286-97cc-9d127db67256/slide_18.png)

To set a node's graph position, you can use the **Set Node Location** function on the MetaSound Editor Subsystem at edit time.

![slide_19](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/060c437b-d783-4cd4-8411-1220892ed067/slide_19.png)

The **Build To Asset** function exports the Builder's MetaSound to a serialized asset with the provided name and path.

Use the right-click context menu in the **Content Browser** to get path information quickly.

![slide_20](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f87e8d87-d2fb-4f25-9abc-5d543f147cac/slide_20.png)