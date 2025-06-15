# Creating a New Physics Body in the Physics Asset Editor

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/creating-a-new-physics-body-in-unreal-engine-by-using-the-physics-asset-editor](https://dev.epicgames.com/documentation/en-us/unreal-engine/creating-a-new-physics-body-in-unreal-engine-by-using-the-physics-asset-editor)  
**Processed:** 2025-06-14 16:16:55

---

The Physics Asset Tool enables you to add or replace the **Physics Bodies** and their associated **Shapes** (**Boxes**, **Spheres**, **Capsules**, **Tapered Capsules**, and so on) attached to the **Bones** make up your Physics Asset.

By default, the **Physics Editor Skeleton Tree** panel only shows the Physics Bodies. Adding and replacing Physics Bodies is easier if you use the **Options** dropdown menu in the Skeleton Tree panel to show the **Bones** and **Primitives** as well.

## Adding Physics Bodies to Bones

![The right-click context menu for a bone](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e98cc6dc-6b50-4127-ac31-55fcb27ff21d/add-body.png)

1.  Right-click on a **Bone** in the **Skeleton Tree** panel, then click on **Add/Replace Body** in the **Context Menu**.
    
    -   You can also right-click on a **Bone** in the **VIewport** to open the Context Menu.
2.  A new Physics Body will be added to the Bone, with the default Capsule Shape attached.
    
    -   If there was already a Physics Body attached to the Bone, the new Physics Body and Capsule Shape will replace it.
3.  Alternatively, when starting with a Bone with no attached Physics Body, you can directly select one of the shapes under **Add Shape** in the **Context Menu**. This will create a new Physics Body with the selected Shape attached.
    
4.  If you right-click on a **Physics Body** and select **Regenerate Bodies**, a new Physics Body with a default Capsule Shape attached will be created to replace every currently-selected Physics Body.
    

## Adding Shapes to Physics Bodies

![The right-click context menu for a physics body](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2be66b1b-7ec6-4760-ae41-ab060b0ae674/add-shape.png)

To add a Shape to an existing Physics Body, right-click the Physics Body, then under **Add Shape** in the **Context Menu**, select the Shape you wish to add.

-   A Physics Body can have more than one attached Shape, so delete the default Capsule if you do not want it to remain attached to the Physics Body.

## Result

You should see that a corresponding body and shape have been added (and parented) to the selected bone.