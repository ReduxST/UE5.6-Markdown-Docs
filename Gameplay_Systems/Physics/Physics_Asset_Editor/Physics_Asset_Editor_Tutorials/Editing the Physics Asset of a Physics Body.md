# Editing the Physics Asset of a Physics Body

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/editing-the-physics-asset-of-a-physics-body-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/editing-the-physics-asset-of-a-physics-body-in-unreal-engine)  
**Processed:** 2025-06-14 16:21:42

---

Below are several common procedures and steps associated with editing **Physics Bodies** in the **Physics Asset Editor**.

If it is difficult to see the Physics Body you want to edit, in the **Viewport** select **Character > Mesh > Wireframe/None** to adjust the visibility of the **Skeletal Mesh**.

![Character Mesh options in the Viewport](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/87086ba3-707b-40a1-9303-a5aa6df22a5f/mesh-none.png)

## Editing a Physics Body

1.  Double-click your **Physics Asset** to open it in the Physics Asset Editor.
2.  Select a Physics Body in the **Viewport** or in the **Skeleton Tree** panel.
3.  **Select, move, rotate, and scale** the Physics Body using the **Selection**, **Translation**, **Rotation**, and **Scale** tools so it fits the **Skeletal Mesh Bone**.
    
    ![Select, move, Rotate, and Scale tools](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/754a028d-9e09-4f60-93a8-53a503520133/move-rotate-scale.png)
4.  Edit the Physics Body's properties in the **Details** panel.
5.  Use the **Enable Collision** and **Disable Collision** tools in the toolbar to edit Collisions between the current Physics Bodies and others in the Physics Asset. Any Physics Bodies that can collide with the currently selected Physics Body will be blue; if they cannot collide, they will be gray.
    
    ![Enable Collision and Disable Collision tools](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4c673caf-68dc-4d42-a812-d3f99179e2d7/enable-disable-collision.png)
6.  If a series of bodies should act as one, such as with the twist joints that form a wrist, use the [Weld](/documentation/en-us/unreal-engine/welding-physics-bodies-in-unreal-engine-by-using-the-physics-asset-editor) tool to prevent undesired physics simulation behavior. Welded Physics Bodies will be yellow.
7.  **Save** often.

See the [Physics Bodies Reference](/documentation/en-us/unreal-engine/physics-bodies-reference-for-unreal-engine) for more information on the Physics Bodies properties in the Physics Asset Editor.

## Copying Physics Bodies

While in either mode, properties from one Physics Body can be copied to other Physics Bodies:

1.  Select the **Physics Body** you wish to copy data from.
2.  **Press Ctrl + C**.
3.  Select the **Physics Bodies** you wish to apply data to.
4.  **Press Ctrl + V**.

This will not overwrite the shape of a Physics Body.

## Deleting Physics Bodies

1.  Double-click your **Physics Asset** to open it in the Physics Asset Editor.
2.  Select a **Physics Body** you wish to delete in the **Viewport** or in the **Skeleton Tree** panel.
3.  Press the **Delete** key.

## Physical Materials

Each Physics Body in a Physics Asset can have a **Physical Material** assigned to it. To apply a Physical Material to a single Physics Body:

1.  Double-click your **Physics Asset** to open it in the Physics Asset Editor.
2.  Select a **Physics Body** in the **Viewport** or in the **Skeleton Tree** panel.
3.  In the **Details** panel, locate the **Simple Collision Physical Material** property and assign a **Physical Material**.

![Apply a Physical Material to a single Physics Body](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/143f8aa2-494e-40f6-aa6a-1c7ef04e765a/physical-materials-physics-asset-04.png)