# World Composition

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/world-composition-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/world-composition-in-unreal-engine)  
**Processed:** 2025-06-14 17:04:59

---

**World Composition** has been designed to simplify managing large worlds. One of the goals is to avoid using a persistent level to store streaming information as it becomes a bottleneck when a team of level designers want to work on levels simultaneously. The persistent level does not store any streaming information and instead scans a folder and treats all found levels as streaming levels. Each streaming level has information stored in the package header, which World Composition can read without loading the level into memory. Initially, all levels except the persistent level are unloaded in World Composition. You can load or unload any part of the world manually at any time.

World Composition relies on a world origin shifting feature which, when used with distance based level streaming, allows you to create worlds which are not limited to the `WORLD_MAX` constant value hard-coded into the engine.

World Composition is a legacy system used for level streaming. It is recommended to use [World Partition](/documentation/en-us/unreal-engine/world-partition-in-unreal-engine) for level streaming in projects using Unreal Engine 5.0 or later.

## Activating World Composition

World Composition managed worlds can be activated by switching on **Enable World Composition** flag in **World Settings**.

You can also disable world origin shifting by switching off Enable World Origin Rebasing flag in World Settings.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/40ef3916-5401-4929-95a4-3bf9cd6b6fd1/worldbrowsersettings.png)

## Levels Hierarchy

After you have activated World Composition, all the levels in your project will be visible in the **Levels** window. To open this window, click on the **Windows** menu, and then select Levels.

The entries in the Levels window represent your world hierarchy.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6149ecd0-25a1-414d-9d48-71dd54b59dc8/levelswindow.png)

The level with its name in blue text is the current level. Currently loaded levels will have their names in white text, while levels that are unloaded have grayed-out names.

To load a level in the world composition, just **double-click** its name. Using drag-and-drop, you can establish relationships between individual levels. Child levels store position relative to the parent level, so when you change the parent level's position all child levels will recalculate their position accordingly.

In the Levels window, you can lock and save levels, as well as open the **Level Blueprint** for each level, with buttons to the right of the level name.

## Levels Composition

When Enable World Composition is on, there is a button to open World Composition at the top of the Levels window.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ff2a80af-6cca-4624-a544-825be0d5c91f/worldcomposition.png)

Here, you can see the layout of your world.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f169deae-5cbb-4936-b85e-4247e78fd2c9/world_layout.png)

### Layers

By default, all levels are assigned to an **Uncategorized** layer. Layers hold information about streaming distances, so levels assigned to a particular layer will inherit that streaming distance. Levels assigned to a layer with streaming distance disabled will be excluded from distance streaming, and can instead be controlled using Blueprints.

You can create new layers by clicking the **Add (+)** button to the right of the existing layer names. Each level can only be assigned to one layer at a time.

Layers cannot be deleted or edited, so if you would like to change streaming distance settings, create a new layer with your desired settings and assign levels to it. Layers which have no assigned levels will be deleted automatically the next time you open a level.

You can filter your levels by layer by clicking on the layer name above the minimap. You can toggle multiple layers by using **Control+Mouse Click**. When there are no layers toggled on, no filtering is performed.

### Minimap

Each level except the persistent level has an image and position in the world, which are displayed in the minimap. The image of the level is updated every time content in the level is changed. This map allows you to preview your world from the top and arrange the position of levels by dragging them. When dragging levels, they will snap to the edges of other levels. Holding the **Control** key will cause the level movement to use the Level Editor's snapping settings. Note that level position is stored as integer coordinates, so for exact matching of adjacent level tiles, your levels must have integer bounds sizes.

Levels based on Landscape Actors have snapping based on the base landscape component size. This is done to enable seamless editing between Landscape Actors in different levels.

All Landscape Actors will have transformations disabled in the Editor Viewport to ensure that the landscape cannot be moved by an arbitrary amount and lose its ability to be aligned with other landscape levels.

The first time a level is loaded in World Composition, a new Level Bounds Actor is automatically created in the level. The Level Bounds Actor is used to calculate the size of the level.

By default, the Level Bounds Actor automatically resizes to include all Actors found in the level. However, some Actors, like skyboxes, can have very large bounding boxes, which will result in overly large level tiles in the world minimap. If you have Actors like this that you do not want to include in the level bounds calculations, you can disable automatic level bounds calculations and set a fixed size for the Level Bounds Actor.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5a6ea535-7208-4b31-9741-5889184a5f36/transform.png)

Currently, Realtime must be enabled in the viewports for the Level Bounds Actor to function.

The minimap has a yellow square indicating the safe edit area. The safe edit area's size is equal to the `WORLD_MAX` constant in the engine. Levels outside of this area will be hidden automatically, and their level images will reflect this. World Composition tries to keep levels you are working on close to the Editor world origin. This feature is called "focusing" and may shift the current world origin to a new position if you begin editing a level outside of the safe edit area. Shifted levels still preserve their Actors' original transformations when they are saved, so saving a level that is currently shifted will not change the Actors' absolute positions.

### UI Key

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d5623ee5-1155-4b11-b288-f44920130f8a/world_layout_ui.jpg)

| Number | Status Bar | Description |
| --- | --- | --- |
| 1 | Layers | Click on a layer name to toggle filtering by that layer, or click on the **+** to create a new layer. |
| 2 | `WORLD_MAX` | Bar indicating the scale of the `WORLD_MAX` constant. |
| 3 | World Origin | Current position of the world origin. |
| 4 | Current Level | Name of the current level. |
| 5 | Mouse Cursor Position | Current world position of the mouse cursor. |
| 6 | Marquee Selection | Size of the marquee selection box in the world units. |
| 7 | World Size | Size of the world, calculated as the sum of all level bounding boxes. |

## Level Details

To see the details for any level in the Level window, select it and then click on the magnifying glass icon in the toolbar. This will summon the **Level Details** window, where you can also swap between available levels' information with a dropdown menu.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ed0f9a10-ac1c-40fc-b3c2-4144ecc13249/level_details.png)

### Tile Settings

| Setting | Description |
| --- | --- |
| Package Name | Package name of the selected level. This information is read-only. |
| Parent Package Name | Package name of the parent level. If the level has specified a parent, its position becomes relative to the parent level. |
| Position | Level offset from the zero world origin, stored as an integer 2D vector. All Actors in the level will be shifted by this value when the level is added to the world (becomes visible), and shifted back when the level is removed from the world (hidden). |
| Absolute Position | Absolute position of the level. This is the same as **Position** when the level has no parent. This information is read-only. |
| Z Order | Defines Z sorting order of the level tile in the minimap. This can be useful when there are several overlapping tiles and you want to sort them in a specific order. |

### LOD Settings

Each level in the world composition can have up to 4 LOD streaming levels. LOD streaming levels are similar to mesh LOD. Depending on streaming distance settings streaming level will be replaced with corresponding LOD level. LOD levels automatically discovered by World Composition using pattern \[Package name\]\_LOD#. Where number should be from 1 to 4. LOD levels can be created manually or with automatic LOD map generator.

| Setting | Description |
| --- | --- |
| Num LOD | Number of LOD levels for selected level. |
| LOD\[1..4\] |   |
| Generate | Generates simplified version of an original level to merge Static Mesh Actors found in the level into one simplified proxy mesh. Landscape Actors will be converted to Static Meshes using highest landscape LOD. In general, a level with landscape, an Actor, and a bunch of Static Mesh Actors will result in LOD level which contain 2 simplified Static Mesh Actors. This operation will overwrite previous LOD level if it exists on the disk. |
| Distance | Distance relative to original level streaming distance. For example, if original level has streaming distance = 1000, and LOD1 level has distance 1500, then LOD1 level will be visible at \[1000..2500\] range and original at \[0..1000\] range. |
| Details percentage | Percent of details to preserve when reducing original meshes. |

## World Origin Shifting

The World Composition editor supports shifting of the world origin by some arbitrary amount. Shifting the world origin results in adding an offset vector to all registered **Actors** in the world. Each Actor has an ApplyWorldOffset function which can be overridden in the child classes to do additional things. In case you have created a new AActor derived class and store absolute position values in it, you have to override ApplyWorldOffset function to make it work correctly with world origin changes and shift your absolute values in it. Rendering and physics primitives will be shifted in parallel to Actors in game thread.

## Big Worlds and Multiplayer

Right now world origin shifting is not supported in the multiplayer games. Here are two solutions that can be implemented for your specific needs:

1.  Implement your own server solution. MMO licensees mostly do this.
2.  Implement some layer between clients and unreal dedicated servers which will transform shifted absolute positions from the clients and route them to the right dedicated server, which only holds part of the world where client is.

However if you disable world origin, shifting you can run a tiled world with a dedicated server. Dedicated servers will load all distance dependent levels, and each connected client will work as usual loading only level that satisfy streaming distance settings. A server holds a list of visible levels for each client and filters Actor replication by this list.

## Creating Landscape Levels

**Right-clicking** on a level tile to summon the context menu which has a Landscape Actor inside will bring an option for adding adjacent levels with landscape proxy Actors in them. This requires the adjacent levels landscapes have size equal to source Landscape size.

### Tiled Landscape Import

In the **Levels** panel toolbar you can find an option for importing tiled landscape. Tiled landscapes are created from a tiled heightmap, where each heightmap tile will represent a level with a landscape Actor in it. Tiled heightmaps/weightmaps can be exported from an application like World Machine. Adjacent heightmaps tiles should share border vertices ("Share edge vertices" in World Machine). And, each tile resolution should follow the recommendations from this page [Creating Landscapes](/documentation/en-us/unreal-engine/creating-landscapes-in-unreal-engine).

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a3310325-db7b-4ff2-a82c-4cf6405ef307/tiled_heightmap_import.png)

| Setting | Description |
| --- | --- |
| Select Heightmap Tiles... | Allows you to select multiple heightmap tiles you want to import. |
| Flip Tile Y Coordinate | Whether tiles should be imported with Y coordinate flipped. This option should be turned on when importing tiles created in World Machine. |
| Tile Coordinates Offset | Offset in tiles from origin. If set to zero, tile with coordinates x0\_y0 will be created at world origin. |
| Import Configuration | Generates all possible landscape configurations depending on resolution of selected tiles. |
| Landscape Scale | How much to scale the tiled landscape by. |
| Material | Material to use. When a material has be chosen, you will be able to assign weightmap tiles for each landscape layer found in the material and how each layer is blended. |

When you have imported a tiled landscape, you can reimport heightmaps and weightmaps for selected levels using the **right-click** context menu on the minimap.