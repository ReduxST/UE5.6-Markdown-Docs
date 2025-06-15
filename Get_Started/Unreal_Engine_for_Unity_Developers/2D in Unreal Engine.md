# 2D in Unreal Engine

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/2d-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/2d-in-unreal-engine)  
**Processed:** 2025-06-14 16:04:01

---

**Paper 2D** is a plugin for **Unreal Engine (UE)** that you can use to create 2D and 2D/3D hybrid gameplay and animation systems. The Paper 2D plugin contains support for the various 2D asset types, such as Sprites for 2D characters and objects, Flipbooks for animating Sprites, TileSets, and TileMaps, which you can use to create 2D levels and environments, along with all of the associated editors you will need to create and edit your assets.

The Paper 2D system offers many choices when building projects with 2D elements. The plugin is feature-rich with assets and editors that you can use to create high-quality 2D content, from characters to environments. The plugin is also completely compatible with UE’s 3D rendering capabilities, meaning 2D elements can be seamlessly integrated with 3D characters, objects, or environments.

![paper 2d hybrid example](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2c2a5504-b38a-44d2-b48a-4b1cf6354fa1/image-0.png)

#### Prerequisites

To start creating 2D and 2D/3D hybrid projects in UE, ensure the Paper 2D plugin is installed.

-   In the Unreal Editor, navigate to the **Menu Bar** to **Edit** > **Plugins** and locate the **Paper 2D** plugin in the **2D section** or by using the **Search Bar**. If the plugin is not enabled, enable it by checking the box then restart the editor.

![paper 2d plugin](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bf608523-51a7-4f44-ae2a-2d3621f694b0/image-1.png)

## Migrating Projects from Unity

When migrating a 2D project from Unity to UE, use the following steps:

1.  Locate your 2D assets’ associated image files in your Unity Project’s **Assets** folder, which is found in the root directory of your Unity project.
    
    All 2D image files that Unity supports are also supported in UE, such as `.jpg` and `.png`.
    
2.  After locating your image files in your Unity project folder, you can drag and drop them into your UE project’s **Content Browser** or browse to the file's location on your computer using the Content Browser’s **Import** button.
    

Image files imported to UE will be imported as Texture Assets, which can be used to create Paper 2D assets such as Sprites, Flipbooks, and TileMaps.

When importing low-resolution images, such as sprite-based artwork, you can apply sprite-specific settings to the texture to sharpen and enhance the look of pixel art, by right-clicking the asset in the Content Browser and selecting the **Sprite Actions** > **Apply Paper 2D Import Settings** option in the Context Menu.

For more information about importing sprite-based assets into UE, see the [Importing Sprites section](/documentation/en-us/unreal-engine/how-to-import-and-use-paper-2d-sprites-in-unreal-engine#importingsprites) of the Paper 2D Sprites document.

After importing your image assets into UE, you can create Sprite and TileSet assets and use their respective editors to begin building your game objects.

## Assets

The following sections provide a quick overview of the Paper 2D system and contain links to more extensive documentation.

### Sprites

Like Unity, the main asset you can use to create 2D characters and objects is called a **Sprite** asset. Sprites are a planer game object that you can map an image to be used as a character or an object. While any image can be used as a Sprite asset, the Paper 2D plugin comes packaged with specialized settings and materials to help improve the look of low-resolution pixel style graphics typically found in 2D style projects.

![manny sprite](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ccc508ac-d181-4eb8-9131-552815788867/image-2.png)

Sprites can then be added to any UE **Actor** or **Paper 2D Character Actor**, as a **Sprite Component**.

For more information about Sprites in UE, such as settings, and a reference to using the Sprite Editor, see the following documentation:

### Flipbooks

Sprite actors can be animated using **Flipbooks** assets, which store a linear sequential playback of different sprite assets. Unlike Unity, Flipbooks are unique assets that can be used independently of an individual Sprite asset or even Actor object. This means animations are more versatile and reusable and can be played anytime using Blueprints or C++ code.

![manny flipbook](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/60f5fd3b-ba04-4178-9237-d198fc26ad0a/image-3.gif)

For more information about creating, using and editing Flipbooks in UE, see the following documentation:

### TileSets and TileMaps

The Paper 2D plugin also contains the TileSet and TileMap assets, along with their corresponding editors that you can use to create 2D levels and environments. Using TileSet assets, you can import one large asset containing all of your background assets for a level, extract each tile, and define collision settings that will influence how your player can interact with the environment.

You can then assemble the tiles into a TileMap asset to build levels, using tools like layers to build dynamic and interesting environments for your project.

![tilemap in unreal engine](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/816556bb-e331-43f9-a1dc-56300eb9d2bf/image-4.png)

For more information about using TileSets and TileMaps in UE, see the following documentation: