# Working with Multiple UV Channels

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/working-with-multiple-uv-channels-with-mutable-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/working-with-multiple-uv-channels-with-mutable-in-unreal-engine)  
**Processed:** 2025-06-14 17:04:51

---

Mutable supports using multiple UV channels in Mesh Sections, each with its [layout strategy](/documentation/en-us/unreal-engine/texture-layouts). This means texture parameters can have different customization options per UV channel.

## How to use them?

To use multiple UV channels inside Mutable, the material graph and the Customizable Object graph must follow some rules.

Textures must be declared as texture parameters inside the material graph to be accessible. Texture parameters should have a valid UV channel, which can be set in the material graph and the Mesh Section node. Some nodes need to be set up accordingly.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d97d7770-3d0f-422f-845f-e10931db9ae3/mutable-multiple-uvs-1.png) ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/02c679cf-82c8-45d9-9936-11f72dc668ec/mutable-multiple-uvs-2.png)

Below, you will find the list of the nodes that can interact with different or multiple UV channels and an overview of how they do it.

### Mesh Section node

In the Node Properties tab of this node, we can decide which texture parameters are exposed to it and how the layout will affect the texture.

[Mesh Section node reference page](https://github.com/anticto/Mutable-Documentation/wiki/Node-Mesh-Section)

### Skeletal Mesh node

The behavior of each UV channel can be defined per mesh section in the Layout Editor category inside the Node Properties tab.

[Skeletal Mesh node reference page](https://github.com/anticto/Mutable-Documentation/wiki/Node-Skeletal-Mesh)

### Table node

The behavior of each UV channel can be defined per mesh section in the Layout Editor category inside the Node Properties tab.

[Table node reference page](https://github.com/anticto/Mutable-Documentation/wiki/Node-Table)

### Edit Mesh Section Modifier node

It is possible to edit texture parameters from a Mesh Section with an Edit Mesh Section modifier node in any Object. This node lets you select which textures are edited and specify which part of the texture is affected by using UV layout blocks.

Edit Mesh section nodes can only edit textures from a single UV channel. To edit all textures from Mesh Sections with multiple UV channels, an edit node will be required for each of the channels to modify.

[Edit Mesh Section node reference page](https://github.com/anticto/Mutable-Documentation/wiki/Node-Edit-Mesh-Section)

### Remove Mesh Blocks modifier node

The "UV Layout" property in the node properties can be used to select the UV channel to remove blocks from. The mesh fragment within the layout blocks will be removed from all textures and UV channels.

[Remove Mesh Blocks node reference page](https://github.com/anticto/Mutable-Documentation/wiki/Node-Remove-Mesh-Blocks).

### Texture Project node

The UV channel to project to can be specified in the node’s properties tab with the option “Layout”.

[Texture Project node reference page](https://github.com/anticto/Mutable-Documentation/wiki/Node-Texture-Project).

### Group Projector Parameter node

The UV channel to project to can be specified in the node’s properties tab with the option “UVLayout”.

[Group Projector Parameter node reference page](https://github.com/anticto/Mutable-Documentation/wiki/Node-Group-Projector-Parameter).