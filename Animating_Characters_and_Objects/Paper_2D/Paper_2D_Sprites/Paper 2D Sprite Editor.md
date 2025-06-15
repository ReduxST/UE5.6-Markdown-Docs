# Paper 2D Sprite Editor

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/paper-2d-sprite-editor-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/paper-2d-sprite-editor-in-unreal-engine)  
**Processed:** 2025-06-14 16:41:57

---

After adding **Sprites** to your project, you may have adjustments or modifications to the Sprite's size, [collision](/documentation/en-us/unreal-engine/paper-2d-sprite-collision-in-unreal-engine) or rendering behaviors. Using **Unreal Engine**'s **Sprite Editor** you can make adjustments to your character, object and [Tile](/documentation/en-us/unreal-engine/paper-2d-tile-sets-and-tile-maps-in-unreal-engine) Sprites.

To open the Sprite Editor, **double-click** the a sprite in the **Content Browser**, or open multiple by selecting many sprites, **right-clicking**, and selecting **Edit** from the **Context Menu**.

Here you can reference an overview image of the Sprite Editor, with highlighted tools and panels.

![sprite editor overview](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/907948ba-d162-4912-b3a0-4fc7ddface1c/spriteeditor.png)

1: [Toolbar](/documentation/en-us/unreal-engine/paper-2d-sprite-editor-in-unreal-engine#toolbar)

2: [Editor Modes](/documentation/en-us/unreal-engine/paper-2d-sprite-editor-in-unreal-engine#spriteeditormodes)

3: [Sprite List](/documentation/en-us/unreal-engine/paper-2d-sprite-editor-in-unreal-engine#spritelist)

## Toolbar

Here you can reference the unique **Toolbar** tools that you can use when working with Sprites in the Sprite Editor.

| Tool | Icon | Description |
| --- | --- | --- |
| **Scr Tex** | ![scr tex toggle button](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9b8e4b7c-b36f-431f-a1db-15b9dec35bd7/srctexicon.png) | Here you can toggle the sprite viewport to show the current sprite in the context of the sprite sheet it was extracted from while working within the **View** Sprite Editor mode. The current sprite will be highlighted while the remaining sprites in the sprite sheet will appear darker. |
| **Other Sprites** | ![other sprites button](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e072a2c7-667f-4ffe-8f86-7e3de1aa2abf/otherspritesicon.png) | Here you can toggle the bounding boxes that contain the other sprites within the sprite sheet while working within the **Edit Source Region** Sprite Editor mode. |
| **Sprite Names** | ![sprite names button toggle](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b152c2ef-99f0-4da1-929c-f71cdd76f858/spritenamesicon.png) | Here you can toggle the sprite names to be overlaid over the sprites in the viewport while working within the **Edit Source Region** Sprite Editor mode. |
| **Extract Sprites** | ![extract sprites button](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ceccb083-a4da-4fa7-b334-d3e462284d60/extractspritesicon.png) | Here you can open the Extract Sprites window to re extract sprite from the sprite sheet the current sprite is from while working within the **Edit Source Region** Sprite Editor mode. |
| **Add Box** | ![add box collision button](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/53fa22d2-8802-40af-96b1-1580f293ec45/addboxicon.png) | Here you can add a **box** collision or render boundary shape while working within the **Edit Collision** or **Edit RenderGeom** Sprite Editor modes. |
| **Add Polygon** | ![add polygon collision button](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/94012188-294d-44ca-b37c-f9f5d2566b97/addtriicon.png) | Here you can add a **custom polygon** collision or render boundary shape while working within the **Edit Collision** or **Edit RenderGeom** Sprite Editor modes. After selecting the **Add Polygon** tool you can click within the viewport to create a new vertex for the custom shape. The Sprite Editor will automatically connect new vertices with existing ones. |
| **Add Circle** | ![add circle collision button](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/85211d44-d684-471b-b6cc-69c5fa43e47a/addcircleicon.png) | Here you can add a **circle** collision shape while working within the **Edit Collision** Sprite Editor mode. |
| **Snap to pixel grid** | ![snap to pixel grid button](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/74ed1f98-d21c-413d-ad26-ad464541656e/snapicon.png) | Here you can snap all collisions or render boundary shape vertices to the sprites pixel grid. This is helpful to actually align sprites and the collusion and render boundary shapes. |

## Sprite Editor Modes

The Sprite Editor features Four Modes you can use to modify and edit sprites in Unreal Engine.

### View Mode

Using the **View** Sprite Editor mode you can modify the sprite's properties such as its **Materials** and **Pivot Mode**.

![sprite view mode button](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/da6c66dd-1cd9-4034-848c-4b13362fcf89/viewmode.png)

#### Sprite Editor Property Reference

Here you can reference the Sprite Editor properties and a description of their functionality:

Some properties are only accessible within specific Editor modes. These mode restrictions are noted in the editor and within the property descriptions. For mode specific property descriptions, see the associated Sprite Editor Mode section.

![view sprite editor details](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0b5d9066-a89a-44fb-b35c-dfefc16f537b/details.png)

| Property | Description |
| --- | --- |
| **Source UV** | Position within the source texture, or sprite sheet, in pixels. |
| **Source Dimension** | Dimensions within the source texture, or sprite sheet, in pixels. |
| **Source Texture** | Reference the source texture or sprite sheet asset. |
| **Additional Textures** | Set additional source textures that occupy numerical slots. These textures can be referenced and applied during gameplay using [Blueprints](/documentation/en-us/unreal-engine/blueprints-visual-scripting-in-unreal-engine). |
| **Default Material** | 
Assign a **Default Material** to use when rendering the Sprite. This material is the default material used when no other material is assigned.

For more information about Sprite Materials, see the [Sprite Materials](/documentation/en-us/unreal-engine/paper-2d-sprite-material-in-unreal-engine) documentation.



 |
| **Pixels per unit** | Set the scaling of the Sprite in the level. By default, this property is set to 1, which sizes the sprite so that one pixel of the sprite is **1** **Unreal Unit** (**cm**) by **1** **Unreal Unit**. |
| **Pivot Mode** | 

Set the point at which the sprite can pivot. You can set the pivot point in the View Sprite Editor mode's viewport using the widget. You can also set the pivot point by selecting a preset location using the drop down menu.

Selecting the **Custom** option, will allow you to manually set a **Custom Pivot Point** using **X** and **Y** values.



 |
| **Origin in Source Image Before Trimming** | Reference the Sprite's origin within the Source image prior to atlasing. |
| **Source Image Dimension Before Trimming** | Reference the Source Image's Dimensions, **Height** (**X**) and **Width** (**Y**) before any trimming. |
| **Trimmed in Source Image** | When enabled, the source file will use the **Origin in Source Image Before Trimming** and **Source Image Dimension Before Trimming** properties to atlas the sprite. |
| **Rotated in Source Image** | When enabled, the source file swaps the **X** and **Y** dimensions, effectively rotating the Sprite Sheet and all extracted Sprites **90** degrees **counter-clockwise**. |
| **Source Texture Dimension** | Reference the Source Image's Dimensions, **Height** (**X**) and **Width** (**Y**) after any trimming. |
| **Snap Pivot to Pixel Grid** | When enabled, the Sprite's **Pivot Point** will snap to be aligned with the sprites pixel grid. You can set a more precise pivot point by disabling this property. |
| **Sockets** | Here you can **Add** (**+**) **Sprite Sockets** to the sprite. Sprite sockets are used to attach other objects to the sprite at specific locations. After creating a Sprite Socket, you can define its **local transform**, and **name**. Sprite Sockets can then be referenced and used in [Blueprints](/documentation/en-us/unreal-engine/blueprints-visual-scripting-in-unreal-engine). |

### Edit Source Region Mode

Using the **Source Region** Sprite Editor mode, you can edit the extracted sprite from the sprite sheet or source file.

![edit source region button sprite editor](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/156f1e37-cfb3-4c25-9c8f-1a25967f7168/soureregionmode.png)

By **clicking** and **dragging** the edges of the source region of the sprite, represented as a **white box**, you can modify the boundaries of the sprite that have been extracted from the Sprite Sheet.

### Edit Collision Mode

With the **Edit Collision** Sprite Editor mode, you can edit the collision boundary of the sprite.

![edit collision button sprite editor](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a636bff5-1f21-4bcf-8854-15e43b57f265/collisionmode.png)

Here you can reference the specific **Edit Collision** Sprite Editor mode properties and a description of their functionality:

| Property | Description |
| --- | --- |
| **Sprite Collision Domain** | 
Set the type of collision the sprite should use. By selecting **None** the sprite will not collide with physics objects or influence other physics objects. By selecting the **Use 3D Physics** option, the sprite will collide with objects and other objects can collide with the sprite.

The **Use 3D Physics** setting will populate the Sprite Editor's collisions settings with many properties you can use to fine tune the collision properties to fit the needs of your project.



 |
| **Collision Geometry Type** | 

Here you can set the type of Collision Geometry that will surround the Sprite. You can select from the following options:

-   **Source Bounding Box**: Uses a simple bounding box of the sprite, set to the dimensions of the extraction grid.
-   **Tight Bounding Box**: Uses a collision box that is tight to the Sprite's dimensions, excluding any transparent layer or background.
-   **Shrink Wrapped**: Uses a collision box that will conform to the edges of the sprite, creating a cut out of the sprite.



 |
| **Collision Thickness** | When the **Sprite Collision Domain** is set to **Use 3D Physics**, this property sets the extrusion thickness of the sprite's collision geometry. A value of `10` is used as the default. Increasing this value will increase the thickness of the extrusion, decreasing the value will decrease the thickness. |
| **Collision Presets** | 

Here you can select from a list of collision setting presets, or access a range of properties by selecting the **Custom** option. You can select the following collision setting presets: The sprite will act as a

-   **No Collision**: Disables collision interactions with the sprite.
-   **Block All**: The Sprite will act as a **WorldStatic** object that blocks all actors by default. All new custom channels will use its own default response.
-   **OverlapAll**: The Sprite will act as a **WorldStatic** object that overlaps all actors by default. All new custom channels will use its own default response.
-   **BlockAllDynamic**: The Sprite will act as a **WorldDynamic** object that blocks all actors by default. All new custom channels will use its own default response.
-   **OverlapAllDynamic**: The Sprite will act as a **WorldDynamic** object that overlaps all actors by default. All new custom channels will use its own default response.
-   **IgnoreOnlyPawn**: The Sprite will act as a **WorldDynamic** object that ignores **Pawn** and **Vehicle** objects. All other channels will be set to default.
-   **Pawn**: The Sprite will act as a **Pawn object**. Can be used for capsule of any playable character or AI.
-   **Spectator**: The Sprite will act as a **Pawn object** that ignores all other actors except **WorldStatic** objects.
-   **Character Mesh**: The Sprite will act as the same **Pawn** object that is used for **Character Mesh** objects. All other channels will be set to default.
-   **PhysicsActor**: The Sprite will act as a **Simulating** actor.
-   **Destructible**: The Sprite will act as a **Destructible** actor.
-   **InvisibleWall**: The Sprite will act as a **WorldStatic** object that is invisible.
-   **InvisableWallDynamic**: The Sprite will act as a **WorldDynamic** object that is invisible.
-   **Trigger**: The Sprite will act as a **WorldDynamic** object that is used for triggers. All other channels will be set to default.
-   **Ragdoll**: The Sprite will act as a **Simulating Skeletal Mesh Component**. All other channels will be set to default.
-   **Vehicle**: The Sprite will act as a **Vehicle** object that blocks Vehicle, WorldStatic and WorldDynamic objects. All other channels will be set to default.
-   **UI**: The sprite will act as a **WorldStatic** object that overlaps all actors by default. All new custom channels will use its own default response.

If **Custom** is selected, the additional options are available to fine tune the sprites collision properties. [See below for more information](/documentation/en-us/unreal-engine/paper-2d-sprite-editor-in-unreal-engine#collisionpresetscustomoptions).



 |
| **Render Shapes** | 

Here you can add collision shapes to the sprite for dynamic collision boundaries. You can **Add (+)** as many collision shapes as you desire and each collision shape can be modified using its properties. The following properties are adjustable per collision box.

-   **Shape Type**:



 |
| **Collision Shapes** | 

Here you can add collision shapes to the sprite for dynamic collision boundaries. You can Add additional Collision Shapes using the toolbar buttons (**Add Box**, **Add Polygon**, and **Add Circle**). Each collision shape will appear as an array and can be modified using its properties.

The following properties are adjustable per collision shape.

-   **Shape Type**: Reference the shape type of the collision shape.
-   **Vertices**: Set the **X** and **Y** location of the Collision Shape's vertices.
-   **Box Size**: Set the scale of the **X** and **Y** dimensions of the shape. This is option is only editable when working with a **Box** or **Circle** Collision Shape.
-   **Rotation**: Set the rotation of the Collision Shape, in degrees.
-   **Negative Winding**: When enabled, the Collision Shape's winding, or the order the Vertice locations are applied, will be reversed, regardless of the order of the Vertices. This option is only editable when working with a **Polygon** Collision Shape.



 |

#### Collision Presets Custom Options

| Property | Description |
| --- | --- |
| **Collision Enabled** | 
Select the method of collision used when enabled. You can select from the following options:

-   **No Collision**: Will not create any representation in the physics engine. Cannot be used for spatial queries (raycasts, sweets, overlaps) or simulation (rigid body, constraints). Best performance possible (especially for moving objects).
-   **Query Only (No Physics Collision)**: Only used for spatial queries (raycasts, sweeps, and overlaps). Cannot be used for simulation (rigid body, constraints). Useful for character movement and things that don't need physical simulation. Performance gains by keeping data out of the simulation tree.
-   **Physics Only (No Query Collision)**: Only used only for physics simulation (rigidbody and constraints). Cannot be used for spatial queries (raycasts, sweeps, overlaps). Used for jiggly bits on characters that do not need per bone detection. Performance gains by keeping data out of the query tree.
-   **Collision Enabled (Query and Physics)**: Can be used for both spatial queries (raycats, sweeps, overlaps) and simulation (rigid body, constraints).



 |
| **Object Type** | 

Set what layer the Sprite will occupy. You can choose from the following options:

-   **WorldStatic**
-   **WorldDynamic**
-   **Pawn**
-   **PhysicsBody**
-   **Vehicle**
-   **Destructible**



 |
| **Collision Responses** | 

Toggle how the Sprite will behave for specific facets of its collision properties and representation properties, and how it will appear during playback. You can toggle each property to be **Ignored** which will ignore the property, **Overlap** will allow the property to overlap the sprites and **Block** which will block the property from engaging with the sprite. You can toggle one of these behaviors with the following properties:

-   **Visibility**: Toggle if the Sprite will be visible during run time.
-   **Camera**: Toggle if the Sprite can collide with **Camera** actors.
-   **WorldStatic**: Toggle if the Sprite can collide with **WorldStatic** objects in the level.
-   **WorldDynamic**: Toggle if the Sprite can collide with **WordDynamic** objects in the level.
-   **Pawn**: Toggle if the Sprite can collide with **Pawn** objects in the level.
-   **WorldDynamic**: Toggle if the Sprite can collide with **WordDynamic** objects in the level.
-   **PhysicsBody**: Toggle if the Sprite can collide with **PhysicsBody** objects in the level.
-   **Vehicle**: Toggle if the Sprite can collide with **Vehicle** objects in the level.
-   **Descructible**: Toggle if the Sprite can collide with **Destructible** objects in the level.



 |

### Edit RenderGeom Mode

Using the **Edit RenderGeom** Sprite Editor Mode you can edit the sprites render boundary to correct for overdraw.

![edit render geometry geom button sprite editor](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c7229596-8e26-4e21-91a8-2d30f0c1a156/rendermode.png)

Here you can reference the specific **Edit RenderGeom** Sprite Editor mode properties and a description of their functionality:

| Property | Description |
| --- | --- |
| **Render Geometry Type** | 
Select the type of Render Geometry you wish to use to render the sprite in your project. You can choose from the following options:

-   **Source Bounding Box**: This option uses a box of the same dimensions as the source image. If the spite was extracted from a sprite sheet, this render geometry will use a box of the same dimensions as the sprite extraction method.
-   **Tight Bounding Box**: Uses a tightened bounding box gourd the sprite, excluding transparent areas.
-   **Shrink Wrapped**: creates a custom render geometry that molds to the shape of the sprite using the **Avoid Vertex Merging**, **Alpha Threshold**, **Detail Amount**, and **Simplify Epsilon** property values.
-   **Fully Custom**: Set custom **X** and **Y** geometry dimensions to render the Sprite.
-   **Diced**: Spits a single large square render geometry into smaller squares, to include the sprite while including less of the transparent background, using less vertices than the **Shrink Wrapped** method.



 |
| **Pixels Per Subdivision X** | Here you can set the size of a single subdivision (in pixels) on the **X-axis** (when using Diced mode). |
| **Pixel per Subdivision Y** | Here you can set the size of a single subdivision (in pixels) in **Y-axis** (when using Diced mode). |
| **Avoid Vertex Merging** | 

When enabled, you can avoid vertex merging so extra vertices are preserved.

This is an experimental property, and therefore projects should not rely on its functionality.



 |
| **Alpha Threshold** | Set a value to act as the **threshold to ignore** alpha (or transparent) color values. By default this is set to **0.0**, meaning only 100% transparent values will be ignored, you can increase this property to ignore less transparent alpha values with a value of **1.0** ignoring all color values. |
| **Detail Amount** | Amount of detail to consider when shrink-wrapping. 0 = low detail, 1 = high detail. |

## Sprite List

Using the **Sprite List** panel you can access other sprites from the same **Source File**, or **Sprite Sheet**.

By **double-clicking** a sprite in the Sprite List panel, you can open another Sprite in the Sprite Editor.