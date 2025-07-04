# Paper 2D Tile Sets / Tile Maps

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/paper-2d-tile-sets-and-tile-maps-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/paper-2d-tile-sets-and-tile-maps-in-unreal-engine)  
**Processed:** 2025-06-14 16:42:01

---

**Tile Sets** and **Tile Maps** within **Paper 2D**, provide a quick and easy way to layout the framework or "general layout" of your 2D levels. By creating and using a Tile Set (a collection of tiles pulled from a texture) with a Tile map (a 2D grid with a defined width and height in tiles), you can select various tiles to "paint" onto the Tile Map which can be used for your level layout. You can also paint tiles on multiple layers, each of which can specify which tile should appear in each cell of the map for that particular layer.

## Creating Tile Sets

You can create Tile Sets inside the **Content Browser**, similar to other assets. They can be created from scratch as blank assets or generated from other existing assets.

### Blank Tile Set

**To create a new blank Tile Set asset:**

1.  Click the ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/93f9847d-37b3-44d8-b188-754fe1b3999f/addnewbutton.png) button in the **Content Browser**, then under *Miscellaneous*, select **Tile Set**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e04e49ea-a927-474c-b63e-37550442c922/tilesetbutton.png)
2.  Enter in a name for the new Tile Set asset.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a15b4394-d746-41a0-80d3-8078b154956f/papertitleset.png)
3.  **Double-click** on the asset to open it up in the **Tile Set Editor** window.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0cb66b22-51fc-4112-8754-4913320bb4c6/papertitleseteditor.png)
4.  Specify a **Tile Sheet** texture asset to use inside the **Details** panel.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5d5d09c9-5a29-4ee7-86b0-0e1db053d32a/tilesetdata.png)

### Tile Set from Texture

**To create a Tile Set from an existing Texture:**

1.  In the **Content Browser**, **Right-click** on a Texture asset, then under *Sprite Actions* choose **Create Tile Set**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e8cfc227-2a65-4cc7-8ad5-afd9d21aeeba/rightclickmethod.png)
2.  The Tile Set will automatically be created/named based on the Texture you supplied.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4e75f21d-13cd-4aa8-9b27-e5e931ce6fb1/autocreate.png)
    
    You can rename the asset by selecting it and pressing **F2** or **Right-clicking** on it and choosing **Rename**.
    
3.  **Double-click** on the asset to open it up in the **Tile Set Editor** window.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fddef5f1-732c-486f-8dab-380833be6d24/createdtitleset.png)

## Tile Set Editor

Once you have created a new Tile Set asset, **Double-clicking** on the asset will open it in the **Tile Set Editor**.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3ce90cf2-fc14-4fa0-ac97-266983b780d3/tileseteditorwindow.png)

Above in the **Viewport** window (1), you will see the Tile Sheet you've specified to use with your Tile Set. In the **Tile Editor** window (2), the currently selected tile will be displayed. In the **Details** panel (3), you can set various settings that will affect the Tile Set or the individual Sprites that make up the set (see *Configuring Your Tile Set* below).

### Configuring Your Tile Set

You will more than likely need to configure your Tile Set to ensure that you are accurately selecting each tile within your sheet.

Inside the **Viewport**, **Left-clicking** on your Tile Sheet will display a white tile selection box indicating the currently selected tile.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7a12b3ec-11b6-4b4a-9cfa-0a777fb842cc/defaultsettings.png)

**Right Mouse Button** drag inside the Viewport to pan and use the **Mouse Wheel** to zoom in/out on your Tile Sheet.

Above, the default **Tile Width** and **Tile Height** (in pixels) of 32 is being used represented by the white selection box. Unfortunately our tiles are larger than the default values and we want our Tile Width and Height to encompass our entire tile (represented by the yellow box outline).

Inside the **Tile Editor** preview window the currently selected Tile and its associated Tile Number (see below) are displayed. Just below it, inside the **Details** panel, you can adjust the *Tile Width* and *Tile Height* so that it properly encompasses your entire tile.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/50518b29-5e64-4051-9221-5a2b8d1381d5/currentlyselectedtile.png)

In our example, we've increased the *Tile Width* and *Tile Height* to 64 to match our tile size.

*Click for full view.*

In the Viewport, the white tile selection box now fully highlights an individual tile on the Tile Sheet (you may need to experiment with different values depending on how your Tile Sheet is set up). The Tile Editor window also updates to show a single tile from our Tile Sheet that is selected.

In addition to setting *Tile Width* and *Tile Height*, you can use the following settings to further adjust your Tile Set from the **Details** panel.

| Setting | Description |
| --- | --- |
| **Tile Width** | The width of a single tile (in pixels). |
| **Tile Height** | The height of a single tile (in pixels). |
| **Margin** | The amount of padding around the perimeter of the tile sheet (in pixels). |
| **Spacing** | The amount of padding between tiles in the tile sheet (in pixels). |
| **Drawing Offset** | The drawing offset for tiles from this set (in pixels). |
| **Background Color** | The background color displayed in the tile set viewer. |

### Per Tile Settings / Applying Tile Collision

Also inside the **Details** panel, you can specify per tile settings (such as applying collision to a particular tile).

**To apply collision to a tile**:

1.  Select the tile in the viewport (1) then click the type of shape you want to use for collision (2).
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/63ac4079-a7df-46bc-a0e4-b6d47bd7b499/collision_1.png)
2.  The shape will be applied and can be further edited inside the **Tile Editor** window.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/197b6032-16dc-43e8-a933-0b3954696738/collision_2.png)
    
    Note the tile number you are editing (green box above), you will need this to apply settings to this particular tile.
    
3.  In the **Details** panel under the **Sprite** section, find the selected tile and change to the desired **Geometry Type**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/76fe6478-c778-46c9-8a08-d5e5cb22bdd1/collision_3.png)
    
    For information on sprite collision types, see the [**Sprite Collision**](/documentation/en-us/unreal-engine/paper-2d-sprite-collision-in-unreal-engine) documentation.
    

This will set this tile up for collision based on the specified geometry type and shape used. For the collision to actually take effect in-game, when creating your **Tile Map** you will need to set the **Sprite Collision Domain** (see below for information on creating/using Tile Maps).

## Creating Tile Maps

Tile Maps are created inside the **Content Browser** and edited inside the **Tile Map Editor**.

### New Tile Map

**To create a new Tile Map asset:**

1.  Click the ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f137fc62-ce9d-4ba5-a792-89d057914d53/addnewbutton.png) button in the **Content Browser**, then under *Miscellaneous*, select **Tile Map**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4789a52f-f5c8-4321-b8ab-643843731096/newtilemap.png)
2.  Enter in a name for the new Tile Map asset.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0fefbbf5-5b14-4f11-9a0a-c8aee40aee2d/newpapertilemap.png)
3.  **Double-click** on the asset to open it up in the **Tile Map Editor** window.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/eef54f3d-cc67-40f0-80ba-e70b2e753ad8/tilemapeditorwindow.png)

## Tile Map Editor

After opening a new Tile Map asset, before you can work within the Tile Map editor you will need to assign an **Active Tile Set** to work with.

1.  You can specify the **Active Tile Set** to use inside the **Toolbox** window by clicking the **Selection** box.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e608d75a-336e-4cc1-9f02-5c49307a988d/selecttilesetwindow.png)
    
    Then selecting the Tile Set you wish to currently work with.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d22efcc7-f08d-40d8-87f2-de3a89299045/selecttileset.png)
    
    Any Tile Sets that you have created will be displayed in the window above, allowing you to switch between the "Active Tile Set".
    
2.  Once you have selected a Tile Set, the viewer will become updated with your selection.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3ca6e2b7-75de-496e-a8f2-7fcabce9f585/tilemapreadytoedit.png)

The three windows that comprise the Tile Map Editor are outlined below.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/836432f6-9cb8-4ef0-86be-7f4070792d4e/tilemapeditoroverview.png)

Above in the **Toolbox** window (1), you can switch between different Tile Sets to use for the creation of your Tile Map. The Tools used to **Paint**, **Erase** or **Fill** tiles on the map are also presented (in addition to options for flipping or rotating the currently selected tile). The bottom section of this window contains the Viewer, which uses the same controls for navigation as the Tile Set viewer (**Right Mouse Button** drag to pan and **Mouse Wheel** to zoom in/out).

The center window, the **Viewport** (2), is used for filling out the Tile Map layout. Using the tools from the Toolbox, you can fill in tiles on the map to create the desired effect by painting, erasing or filling the tiles that comprise your Tile Map. This is where you can "paint" how you want your map to appear in-game.

In the **Details** panel (3), you can configure how many layers your Tile Map consists of as well as adjust various settings such as the width/height of the Tile Map itself, the width/height of the Tiles that comprise the map, the scaling factor between pixels and Unreal Units, the type of collision to use, etc.

### Enabling Collision for your Tile Map

As noted in the Tile Set section, once you've specified which tiles use collision and which do not, you will also need to set your Tile Map to use a collision type. You can do so from the **Details** panel under the **Collision** section.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/af37336c-37d5-4414-8858-c4303f1b1085/collision_4.png)

You can set the collision thickness (which is the extrusion thickness of collision geometry when using a 3D collision domain) as well as the Collision Domain itself (which determines if the Tile Map should have collision geometry and participate in the physical world).

The **Use 2D Physics** option is currently experimental and may not work properly, it is suggested that the **Use 3D Physics** option be used instead.

When you play in your level, you can check which tiles have collision and which do not with the **Show Collision** console command.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/833a775a-e9aa-41c3-a9a9-bab41f7e103e/showcollision.png)

Above, the upper most ground tiles that the player walks on have collision applied to them while the lower ground and water tiles do not.

## Example Tile Map Workflow

Below is an example of a typical workflow for creating a Tile Map.

1.  Open your Tile Map asset.
    
2.  In the **Details** panel, set the **Map Width** and **Map Height** for your Tile Map.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3076e3e1-904c-4f2c-8500-3017abe010d1/setmapsize.png)
    
    This is essentially the size you want your map or level to be.
    
3.  Also set the **Tile Width** and **Tile Height** of the individual tiles in your map.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c4528263-9e86-4bb7-9389-d9d03ddd8656/tilesizesinmap.png)
    
    These are usually going to be the same size you defined in your Tile Set.
    
4.  Assign an **Active Tile Set** to work with for the construction of your Tile Map.
    
5.  Also add some additional layers to work with (one for background, one for foreground and one for the playable level geometry).
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5603f631-8099-494e-8cc8-c5a0878e197a/readytopaint.png)
    
    This is optional, but usually good to have a layer that has your background elements and another for any foreground elements and having your level geometry (the ground, boxes, platforms, etc.) that the player will walk around on placed on a separate layer.
    
6.  Select a tile in the viewer, then in the map **Left-click** to paint it onto the map.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ecd8b7bc-4dcd-43f1-a50c-d24021161cb5/beginpainting.png)
    
    You can also select multiple tiles at once and paint multiple tiles in the map by **Left-click** and dragging over tiles in the viewer.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/eda97890-f087-450f-8c00-85ad0f038f8b/multipletiles.png)
    
    In the map, you can then paint with the selected tiles.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0053afa7-4c19-4ce5-bb96-ff168cabb544/inmapmultipletiles.png)
7.  Continue Painting, Filling or Erasing Tiles on our map to reach your desired layout.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/993326ee-e6e9-48f7-bf49-ad866cc7e919/examplemap.png)
8.  Be sure to enable collision from the **Collision** section of the **Details** panel.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5c3289d1-00cf-4aa3-b83b-a0fb20cfd75b/collision_4.png)
    
    You must have specified in your Tile Set which tiles have collision and which do not for collision to take effect.
    
9.  Drag the Tile Map asset into your level and scale or move based on your needs.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/caadea1a-2ceb-451a-9d11-5bbf7cfc68ff/examplegameimage.png)