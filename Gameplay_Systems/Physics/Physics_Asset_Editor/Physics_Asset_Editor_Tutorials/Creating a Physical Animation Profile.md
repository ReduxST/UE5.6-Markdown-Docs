# Creating a Physical Animation Profile

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/creating-a-physical-animation-profile-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/creating-a-physical-animation-profile-in-unreal-engine)  
**Processed:** 2025-06-14 16:16:58

---

In this How-To, we will cover the basics of creating a **Physical Animation Profile** and adding **Physics Bodies** to it.

## Steps

1.  Find or [Create](/documentation/en-us/unreal-engine/creating-a-new-physics-asset-in-unreal-engine) a **Physics Asset** for your **Skeletal Mesh** using the **Content Drawer**.
    
    ![Physics Asset in the Content Browser](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f601a80e-3416-4125-aabb-09ff3d3a7dc8/physics-asset.png)
    
    If opting to create a new **Physics Asset**, you will need to set it up before continuing.
    
2.  Double-click the Physics Asset to open the **Physics Asset Editor**.
    
    ![The Physics Asset Editor main user interface](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/176798d2-9ac8-4d82-b526-e809e68b9004/physics-asset-editor.png)
3.  Under the **Windows** menu, select **Profiles**; the **Profiles** window should appear as a docked tab.
    
    ![Windows menu with Profiles highlighted](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c41028b5-1d51-4b2d-b075-ad7ad02b3a3c/profiles-window-menu.png)
4.  Add a **Profile** using the **New** button on the **Physical Animation Profiles** entry, and set its name (in the image below we've named it `DocsProfile`).
    
    ![Adding and naming a new Physical Animation Profile](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1cafc9a3-a50c-4049-9b85-7d5369b22b46/docs-physical-animation-profile.png)
5.  Select the **Physics Body** you want to include in your new **Physical Animation Profile** in the **Skeleton Tree** panel, the **Physics Graph** panel, or the **Viewport**.
    
    To see Constraints in the Skeleton Tree panel, select **Show Constraints** in the **Options** dropdown menu.
    
6.  Press the **Assign** button in the **Profiles** panel.
    
    ![Assigning Constraints to a Profile](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/713414b2-3d5a-4878-a5b6-8fc24e795b55/assign-physics-bodies-to-profile-2.png)
    
    1 - Assign a button 2 - Physics Bodies selected in the Skeleton Tree panel 3 - Physics Bodies selected in the Physics Graph panel 4 - Physics Bodies selected in the Viewport
    
7.  Adjust the properties for the selected **Physics Bodies**.
    
    ![Physical animation properties in the details panel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/83157720-820a-4dc2-a1de-bce79f07e1b7/physical-animation-details.png)
    
    A good set of starting values is 1000, 100, 1000, 100, 0, 0
    
    ![Physical animation recommended default values](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cf659932-defd-4b05-a585-68eba442b473/physical-animation-recommended-defaults.png)
8.  Repeat steps 5-7 for all the **Physics Bodies** you want to add to the **Physics Animation Profile**.
    
    You can select, assign, and edit the Properties of multiple Physics Bodies simultaneously. You only need to edit them individually if you want their properties to be different.
    
9.  Save your **Physics Asset** using the **Save** button in the **Physics Asset Editor**.
    
    ![Save your Physics Asset using the Save button in the Physics Asset Editor](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/44e60a6d-be4b-4044-8e42-b6f65966784d/save-button.png)

You can edit an existing Physics Animation Profile by selecting it in the dropdown menu, then using **Assign** to add new Physics Bodies, or using **Unassign** to remove existing Physics Bodies.

## Result

The **Physics Asset** will have a profile that can be called upon from Blueprint or C++ to change the **Physical Animation** properties of its **Physics Bodies**.

## Additional Resources