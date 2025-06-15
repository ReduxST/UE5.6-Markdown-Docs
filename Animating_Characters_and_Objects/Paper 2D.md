# Paper 2D

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/paper-2d-overview-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/paper-2d-overview-in-unreal-engine)  
**Processed:** 2025-06-14 16:41:49

---

**Paper 2D** is **Unreal Engine**'s gameplay and animation system that you can use to create 2D and 2D/3D hybrid projects. In this document you can read about the components of the Paper 2D system that you can use to create 2D and 2D/3D hybrid games in Unreal Engine.

#### Prerequisites

-   Enable the Paper 2D [Plugin](/documentation/en-us/unreal-engine/working-with-plugins-in-unreal-engine). Navigate in the **Menu Bar** to **Edit > Plugins** and locate the **Paper 2D** plugin in the **2D** section, or by using the **Search Bar**. **Enable** the plugin and restart the editor.

![paper 2d plugin](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/098d0c9f-d8bf-4620-919c-963fe3b13198/image79.png)

## Sprites

Paper 2D's primary asset type is called a **Sprite**. Sprites are static 2-dimensional textures that you can use to represent characters or objects, when developing projects in Unreal Engine.

![single manny sprite example](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/371ea5d1-4a29-4272-b405-02c917642542/sprite.png)

Sprites often come in the form of a **Sprite Sheet**, or a single image file that contains many variations of the sprite, that you can use to animate characters and objects.

![manny running sprite sheet example with every frame of animation](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/24026930-810a-4eb6-a07b-3fefddf4102c/spritesheet.png)

By playing the static sprites from a sprite sheet sequentially, using a [Flipbook](/documentation/en-us/unreal-engine/paper-2d-overview-in-unreal-engine#flipbook), you can animate Sprite based characters and objects.

For more information about importing and editing sprites with the Sprite Editor, please see the Paper 2D Sprites documentation.

### Tiles

**Tiles** are 2D-textures that you can use to create the background and environment of a level.

![example of tile map being used as a level](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2e72894e-1693-42fa-9811-d1a7de1c2d1f/tilemap.png)

Many tiles can be imported as a single image file, and divided into individual tiles using a **TileSet** asset.

![example of tile sheet](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b84e2d49-55c1-499a-8abf-3c489eafe3ed/tilesheet.png)

You can then use TileSets to build a **TileMap** asset, to create a 2D level or environment.

![tile map being built](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/47a62f5c-7fb0-42a2-934c-0fa97d775626/tilemap-1.png)

For more information about importing Tiles and creating TileSets see the [Tiles](/documentation/en-us/unreal-engine/paper-2d-tile-sets-and-tile-maps-in-unreal-engine) documentation.

## Flipbooks

You can use **Flipbooks** in Unreal Engine, to play a sequence of sprites to animate characters and objects in your project.

![flipbook example manny running](run.gif)(convert:false)

After importing a sprite sheet, you can combine the extracted sprites to create a Flipbook to animate a character or object. You can then add FlipBooks directly to your character's or object's Blueprint to dynamically play animations during run time.

For more information about editing and using FlipBooks see the Flipbook documentation.

## Workflow Guides

Here you can find workflow guides that you can reference when creating Paper2D projects in Unreal Engine.