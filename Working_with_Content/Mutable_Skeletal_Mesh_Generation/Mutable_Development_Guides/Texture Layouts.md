# Texture Layouts

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/texture-layouts](https://dev.epicgames.com/documentation/en-us/unreal-engine/texture-layouts)  
**Processed:** 2025-06-14 16:54:07

---

As introduced in the [Overview page](/documentation/en-us/unreal-engine/mutable-overview-in-unreal-engine#texturelayouts), you can use Mutable to manage UV layouts of every mesh to optimize their use. They can be separated and organized into blocks to achieve some rendering, optimization and organization benefits. This page explains three examples of what it can do.

## Texture and Mesh Section Merge

Mutable can merge the textures of different meshes if they share material. This example shows a simple Customizable Object with a Child Object that adds a mesh and its texture to a base one. The example consists of a yellow and black pillar which can be extended with small pink pillars on the side.

### Assets

![Image](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fc9ce4b0-6b9d-4ea3-ad29-088ba8b03538/mutable-texture-layouts-1.png)

The base object has its UVs ready to be organized in two blocks

![Image](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e1fa6c71-421b-41f6-b517-ab291f42b9a4/mutable-texture-layouts-2.png)

This accessory's UVs will form only one block

All these skeletal meshes share the same material with only a texture parameter that is the color texture map (shown in the middle of the previous images).

### Object Structure

The node graph of this example consist of a Base Object with a Child Object. The Child Object uses an Extend Mesh Section modifier to add a mesh fragment with its texture to the base mesh.

![Image](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6db38899-f432-4832-bb24-95ee9630abfc/mutable-texture-layouts-3.png)

### UV Layout Settings

In the properties tab of the the [Skeletal Mesh Node](https://github.com/anticto/Mutable-Documentation/wiki/Node-Skeletal-Mesh), you can set a grid resolution in which to create the blocks. The resolution of the base mesh's Mesh Layout establishes the resolution of all the child meshes of the same Customizable Object hierarchy.

In this example, the base mesh has a resolution of 2x2 and is organized in two blocks. These two blocks were strategically set as the mesh inside one of them will be entirely removed in a future customization.

![Image](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cf18359e-8870-4f2c-aa4f-e978f4b5f20f/mutable-texture-layouts-4.png)

In this case, the original texture set in this mesh is 256x256 and the block resolution is 2x2. This means that any block unit of a child mesh will be 128x128.

The following image shows the resulting UV layout if no Child Object is active.

![Image](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/efc7bc20-ccf2-4aba-bee3-ae97a8250d8c/mutable-texture-layouts-5.png)

Resulting UV layouts of each mesh section can be displayed by clicking on the "UV" button in the Preview Instance Viewport tab in Mutable editor.

### Texture Merge

The Extend Mesh modifier extends the mesh sections it is applied to, based on its tags (see [Tags and Modifiers](https://github.com/anticto/Mutable-Documentation/wiki/Node-Modifier-Properties)). This means that its mesh is added to the modified mesh section and its textures are added to the modified section's textures. The block resolution of this child's Mesh Layout is set to 1x1. This 1x1 block will be added to the base blocks.

![Image](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c9eb3e33-e5e9-4317-8366-1d8b507f5502/mutable-texture-layouts-6.png)

In this case, the original texture of this child mesh is 256x256, but as it is set in a 1x1 block, it will be resized to 128x128 when merged with the modified object texture. If the texture was already 128x128 no resizing would be applied.

Texture size and block resolution must be planned when creating asset's UV layouts in order to have the most optimized and desired quality and appearance.

The following image shows the resulting UV layout with this Child Object active.

![Image](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7c2bf005-b9bf-4039-be81-ea9287962c61/mutable-texture-layouts-7.png)

The 1x1 block has been added to the empty spot.

### Resulting Textures

The following images show the resulting textures.

![Image](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fb3b5492-e6d2-496c-9195-c3f15761ade2/mutable-texture-layouts-8.png)

When there is only the base mesh

![Image](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f261b0df-bdfc-4e4f-b19a-a6b5e9ef2d5f/mutable-texture-layouts-9.png)

When the child mesh is active

## Use Blocks for Mesh Removal

Mutable allows mesh removal by selecting blocks in their UV layout. This can be achieved with the [Remove Mesh Blocks](https://github.com/anticto/Mutable-Documentation/wiki/Node-Remove-Mesh-Blocks) modifier node.

In this extension of the previous example, a bigger and blue base is added to the yellow pillar. A part of the yellow pillar mesh will be overlapped by the new blue base, so this part will be removed.

### Assets

![Image](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c8d74ee4-2163-4a19-adf8-8d7263e1e212/mutable-texture-layouts-10.png)

This other accessory's UVs will consist on only one 2x1 block that will replace a block from its parent.

## Object Structure

A second Child Object has been added to the example. This child has the same structure as the previous one but with an addition.

![Image](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4fc88dc4-1258-49b9-87b4-3516c4a2b79d/mutable-texture-layouts-11.png)

### How It Works

In this case, the child mesh has a UV layout grid with a resolution of 2x2 with only a 1x2 block.

![Image](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/77de8008-5758-43e7-a009-00a57a1e81bc/mutable-texture-layouts-12.png)

One of the two blocks of this child will be placed in the empty space of the base layout and the other will replace the removed mesh of the base mesh.

In addition to the Mesh Layout node, this Child Object has a Remove Mesh Blocks modifier node that affects the Base Object mesh section. By setting the right tags in the Node Properties tab, you can display the UV layout of the modified mesh and add UV layout blocks. The Remove Mesh Blocks node will remove any mesh that is inside any of these blocks.

![Image](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/720737c0-fa2d-4b71-bea5-a513e9c27ad7/mutable-texture-layouts-13.png)

In this case, the top-right 1x1 block is selected. This block contains the black base part of the yellow pillar. This part will be removed.

When the Customizable Object is compiled and the blue base Child Object is active, the black base is removed and the blocks of the new blue base are merged to the resulting UV layout.

![Image](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/80564e61-5609-4d86-89f8-99cdce2f671d/mutable-texture-layouts-14.png)

### Resulting Textures

The following image shows the resulting texture when the second Child Object is applied.

![Image](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/39f6a22c-94ef-49ec-a88a-600cedc8e225/mutable-texture-layouts-15.png)

## Example With A Complex Block Structure

The following images show the block structure of the Customizable Object example character "Bandit\_forRPG".

![Image](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8d285754-7052-42fe-84ca-08d5757f10ae/mutable-texture-layouts-16.png)

Mesh Layout node properties showing the block structure of the character.

![Image](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5e8af7f7-bb62-4071-a522-c616a618644e/mutable-texture-layouts-17.png)

Parameters of the instance set to default.

![Image](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/642eec74-36df-48fa-a655-079744a31928/mutable-texture-layouts-18.png)

Instance example with its resulting color texture.

![Image](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7e9680c1-9964-4ac4-93f2-73aaf93e19f6/mutable-texture-layouts-19.png)

Another instance example with its resulting texture.