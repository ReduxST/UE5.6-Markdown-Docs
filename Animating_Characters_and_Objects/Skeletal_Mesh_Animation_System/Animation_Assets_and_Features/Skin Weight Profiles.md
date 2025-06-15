# Skin Weight Profiles

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/skin-weight-profiles-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/skin-weight-profiles-in-unreal-engine)  
**Processed:** 2025-06-14 16:50:55

---

The **Skin Weight Profile (SWP)** system enables you the ability to replace, a subset of, the original Skin Weights (SW) stored as part of a **Skeletal Mesh**. While the use-cases for this system may vary, one possible use-case is to improve visual fidelity in situations or on certain platforms that disable any dynamic character parts.

For example in the video below, a character with a coat may have its dynamic parts disabled in order to improve performance on lower-end platforms. When the foot is raised, this leads to undesirable clipping. Using Skin Weight Profiles, you can achieve a suitable alternative to using more expensive dynamics and mitigate the amount of clipping.

Below you can also see the difference between using dynamic cloth, copy pose without Skin Weight Profiles, and running with Skin Weight Profiles.

|   |   |   |
| --- | --- | --- |
| ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/edcf87de-dc5b-4fd3-8181-4ff0b70a677b/cloth.gif) | ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a64abaa4-71b9-4c26-b75d-827819b3760f/copypose.gif) | ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9f8872cf-588d-4d45-bc55-7c3cf919aace/profile.gif) |
| Cloth | Copy Pose | Profile |

## Setup

When working with Skin Weight Profiles, they have to be imported and set up in the **Editor** in order to be able to use them at runtime.

### Importing a Profile

You can import a profile inside the **Skeletal Mesh Editor** and you will need to provide an FBX file containing the different Skin Weights, a name for the profile, and optionally an LOD index.

1.  Inside the **Asset Details** panel for a **Skeletal Mesh**, click the **Add (+)** button under **Skin Weights** and select **Import Skin Weight Profile**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4e0f18f5-fe30-4f45-a545-d80f0e092b70/importskinweight_01.png)
2.  Select an FBX file containing Skin Weight data to import and click **Open**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/53f0d448-f718-4563-a0c6-1e2e7a3a1083/importskinweight_02.png)
3.  Enter a **Profile Name** (and optionally an LOD index) and click **Import**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8443fef6-2c60-45df-aa03-60ce3babe328/importskinweight_03.png)
    
    Your new Skin Weight Profile will be added as an array element inside the **Asset Details** panel.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6582be16-a093-40cb-8b1f-262c9a219226/importskinweight_05.png)

### Importing Specific LOD Data

If you have **Skeletal Mesh** LODs that use custom LODs, meaning they were imported separately and not generated in-Engine, you will need to import a matching file containing the different Skin Weights. These files can also be imported as part of a pre-existing SWP as illustrated below.

For your existing SWP, select which LOD you want to import weights for.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b925e40d-7c15-486e-af2d-bfb459409e3d/skinweightlod_01.png)

After you select an FBX file containing Skin Weight data, it will show up under the **Source Files** section of the profile.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9b8ed4a8-1446-4ad8-9b9d-d312af765fc7/skinweightlod_02.png)

### Importing a Profile for a Specific LOD

If you want (or need) to override the original Skin Weight at a specific LOD level, you can do so during the import process by specifying which LOD index the imported file contains data for.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/32d00626-08bb-4e5f-bb42-355f44caf6b1/importlodindex.png)

### Reimporting a Profile

If you update any of the source data for the Skin Weight Profile, you can reimport the files. If the stored file path does not exist any more, you will be prompted for a new file location.

To do so, click the **Reimport** icon for the SWP you wish to reimport.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2b6e271d-813b-4643-82f3-2dfa1ca81879/reimportswp.png)

If you have multiple LODs, you can select which LOD you wish to reimport a SWP for from the reimport menu.

#### Reimporting with a Different File

Inside the **Skeletal Mesh Editor**, you can reimport Skin Weights from a different file by clicking the ellipse (...) icon and choosing a new file.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/13d0bdb9-b6a0-4e03-b6f4-0df8978ddccd/reimportdifferentswp.png)

### Removing a Profile

You can remove a Profile, or a LOD within a Profile, inside the **Skeletal Mesh Editor** by clicking the **Remove Profile** button.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a6eca2f1-c2af-49de-919a-530613b02c50/removeprofile.png)

You can remove an entire SWP or LOD within a profile from the remove option.

### Previewing a Profile

You can preview what the different Skin Weights for a specific SWP look like inside the [Animation Editors](/documentation/en-us/unreal-engine/animation-editors-in-unreal-engine) in the Viewport, or during a Play in Editor session.

You can set a specific SWP for a Skinned Mesh component (or child class), by selecting it in the Viewport and selecting the desired profile to preview.

1.  Click the **Character** button, then under **Animation**, select your desired SWP under the **Skin Weight Profile** section.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cd9eedc5-96c8-404c-97ae-46619bb13ece/previewskinweight_01.png)
    
    Debug information will be displayed in the Viewport when selecting a SWP to preview.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a8be0140-1818-40b7-874f-169a8e2600c7/previewskinweight_02.png)
    
    You can also preview Skin Weights inside the Main Level Editor Viewport through the **Details** panel and the **Skin Weights Profile** setting.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7de7220d-ee9e-4544-8538-d31f041cf39e/previewskinweight_04.png)

## Runtime Blueprint Exposed API

At runtime, you can set up a SWP for a Skinned Mesh component (or any child-class) using the provided ([Blueprint](/documentation/en-us/unreal-engine/blueprints-visual-scripting-in-unreal-engine) exposed) API.

| Name | Blueprint Node | Description |
| --- | --- | --- |
| **Set Skin Weight Profile** | ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fb8504ab-6e0e-4d6f-b910-fceedeea8bb5/setskinweightprofile.png) | This will set the specific SWP according to the provided name (if it exists). |
| **Clear Skin Weight Profile** | ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2980ab6a-c708-4797-8725-26d354665a17/clearskinweightprofile.png) | This will clear any previously set SWP. |
| **Unload Skin Weight Profile** | ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3ed01cf0-047a-4d54-b615-ae5a5b295487/unloadskinweightprofile.png) | This forcefully unloads deletes the Skin Weight Buffer for the provided name. |
| **Get Current Skin Weight Profile** | ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d4a850e7-15a1-4689-bb57-294c414aee1c/getcurrentskinweight.png) | Returns the name of the currently set SWP, 'None' otherwise. |
| **Is Using Skin Weight Profile** | ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8b6e9280-f0a5-4a5a-af9c-6ca0004ec5ca/isusingskinweightprofile.png) | Returns whether or not a profile is set. |

## Scalability

The system has the ability to load the default-set SWP at runtime, this can be performed using two paths: Static or Dynamic Paths.

### Static Path

Using the **Static** path, during serialization of the Skeletal Mesh data, the system will check whether or not a default profile has been set, and if so it will be loaded. It will take the original Skin Weight buffer and overwrite its data with that of the default profile. This means that whenever a default SWP is loaded using the Static path, no more changes can be applied afterward, and the original data will be lost until the Skeletal Mesh is reloaded.

If the user tries to change to the Dynamic path or try and set a SWP manually the system will cause an error.

### Dynamic Path

The **Dynamic** path, just like with the Static path, during serialization the default profile will be loaded. However, instead of overriding the original Skin Weight buffer, it will create a new one. Whenever any subsystem requests the buffer, it will return the override rather than the original. The benefit of this system is that it can be toggled at runtime, which is what sets it apart from the Static path.

### Default Profiles

You can assign a default SWP profile inside the **Details** panel of the **Skeletal Mesh Editor** as well as override the original Skin Weights on a per-platform or LODIndex basis.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7284fa3d-a421-410d-89f2-d5c37e614fc2/defaultprofiles_02.png)

In the image above, one SWP is assigned as the override for **Desktop** and another SWP is set for **Mobile**.

When assigning a SWP as the default profile, any additional profiles will be unable to be assigned as the default.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5d6648bd-981d-42fd-af6c-74b449563a63/defaultprofiles_01.png)

When a default profile is assigned, any LOD below the LOD index set under **Default Profile from LODIndex** will override the Skin Weights of the Skeletal Mesh with Skin Weights from the profile.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7a3c0494-97bf-47cb-891f-ab1f7df42aef/defaultprofiles_03.png)

## Console Commands at Runtime

The following console commands can be used at runtime while previewing the SWP system:

| Name | Description |
| --- | --- |
| **a.SkinWeightProfile.LoadByDefaultMode** | 
Enables/disables run-time optimization to override the original skin weights with a profile designated as the default to replace it. Can be used to optimize memory for specific platforms or devices.

-   **0**: Static disabled.
-   **1**: Static enabled.
-   **2**: Dynamic disabled.
-   **3**: Dynamic enabled.



 |
| **a.SkinWeightProfile.DefaultLODOverride** | 

Override LOD index from which on the default Skin Weight Profile should override the Skeletal Mesh's default Skin Weights.

-   **\-1**: Disabled.
-   **0**: LOD index 0.
-   **N**: LOD index N (where N is the LOD to load).



 |
| **a.SkinWeightProfile.AllowedFromLOD** | 

Override LOD index from which on the Skin Weight Profile can be applied.

-   **\-1**: Disabled.
-   **0**: LOD index 0.
-   **N**: LOD index N (where N is the LOD to load).



 |