# Using Profiles for Bodies and Constraints

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/using-profiles-for-bodies-and-constraints-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/using-profiles-for-bodies-and-constraints-in-unreal-engine)  
**Processed:** 2025-06-14 17:00:40

---

The [Physics Asset Editor](/documentation/en-us/unreal-engine/physics-asset-editor-interface-in-unreal-engine) enables you to create your own [Profiles](/documentation/en-us/unreal-engine/physics-asset-editor-in-unreal-engine---tools-and-profiles) that can be used to assign Physical Animation settings to [Bodies](/documentation/en-us/unreal-engine/physics-bodies-in-unreal-engine) and Constraint settings to [Constraints](/documentation/en-us/unreal-engine/physics-constraint-reference-in-unreal-engine).

![Profiles properties](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ad1cd6b7-76c0-4647-a4a5-c1f2cd9e9654/profiles.png)

Use the sections below to learn how to create and assign, unassign, and delete your profiles:

## Create and Assign a Profile

To create and assign a profile, follow these steps:

1.  Select a **Physics Body** or **Physics Constraint** from the **Skeleton Tree**.
    
    ![Select a Physics Body or Constraint](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/76c7231e-611a-463e-8c26-85757cb5dbbd/create-assign-01.png)
2.  In the **Profiles** tab, click the **New** button next to the type of profile you want to create; **Physical Animation** or **Constraint**. Then under the **Current Profile** in the text box, give your profile a name to reference later.
    
    ![Create new profile](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2ceec65f-aba1-41f5-9ca9-9d599a704c58/create-assign-02.png)
    
    When profiles are created, they are initialized "empty" meaning they use default settings.
    
3.  Use the **Graph** or **Skeleton Tree** to select the bodies or constraints you want to assign to a profile.
    
    ![Bodies selected in the Graph](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d78821f1-1780-4544-a2d0-111520722b30/create-assign-03.png)
    
    The Graph for the selected body.
    
    Then in the **Profiles** tab, set the **Current Profile** to the one you want to use and click **Assign**. The selected nodes will change from shaded to their fill color.
    
    ![Assign button in Profiles panel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9dd95c14-9278-4095-9c7d-26af4ac5a889/create-assign-03a.png)
    
    The color change indicates they are assigned this profile, while the other Body node (shaded) is not.
    
    ![Profile association node color change](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c46a565c-21ba-4da4-9b00-67b7a154d25a/create-assign-03b.png)
4.  In the **Details** panel for the selected body, the assigned profile will be displayed, and you can adjust the properties for the type of profile you're creating.
    
    ![Profile in the Details panel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7df75ff4-ee89-4398-9648-36aaa74b7aad/create-assign-04.png)
    
    A Physical Animation profile is assigned to this selected Body.
    
    For a Physical Animation profile, a solid place to start for these values is 1000, 100, 1000, 100, 0, 0
    
    ![Recommended default Physical Animation values](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/953a2e35-46cf-4137-ab54-96a27e5abba2/physical-animation-start-values.png)

## Unassigning a Profile

To **Unassign** a body or constraint from a profile, follow these steps:

1.  Select a **Physics Body** or **Physics Constraint** from the **Skeleton Tree** that you want to edit.
    
    ![Select a Physics Body or Constraint](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/109f7686-2c6c-431c-ae81-58ae8ecf61ad/create-assign-01.png)
2.  In the **Profiles** tab, set the **Current Profile** to the one you want to edit. Use the **dropdown menu** to select the assigned profile, if needed.
    
    ![Select profile](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7bd1c295-8866-4eef-ad81-087ee999c9f4/unassign-02.png)
    
    In the **Graph**, the nodes assigned to the selected profile will have their fill color and not be shaded.
    
    ![Nodes associated with profile](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/01176c5b-2d83-4368-9911-fb55fa73db9d/create-assign-03b.png)
3.  Select the nodes that you want to disassociate from the profile, then click the **Unassign** button in the **Profiles** tab.
    
    ![Unassign button in the Profiles panel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/80a511af-5fdc-4754-b16c-e4aac264117f/unassign-03.png)
    
    After doing so, the selected nodes will show as shaded rather than show the fill color for the currently selected profile.
    
    ![Nodes shaded no longer associated with profile](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/740113f5-111a-41ca-a58c-505925c9ca68/create-assign-03.png)

## Deleting a Profile

To **Delete** a profile, follow these steps:

1.  In the **Profiles** tab, use the **dropdown menu** to select as the **Current Profile** the one you want to delete.
    
    ![Select profile](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bdfbe1ad-fb12-496a-ab6f-624282daea84/delete-profiles-01.png)
    
    The bottom part of the drop-down lists all created profiles.
    
2.  Click the **Delete** button to remove it from the list of available profiles.
    
    ![Delete profile](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0325b7c8-aecc-4762-b50a-96ab4a256f2f/delete-profile-02.png)

## Additional Resources