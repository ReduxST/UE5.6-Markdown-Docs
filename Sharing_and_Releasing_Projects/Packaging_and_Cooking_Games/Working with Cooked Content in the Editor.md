# Working with Cooked Content in the Editor

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/working-with-cooked-content-in-the-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/working-with-cooked-content-in-the-unreal-engine)  
**Processed:** 2025-06-14 17:04:41

---

You can use **cooked content** in the your **Project**, but there are additional requirements and limitations when working with cooked content in the **Unreal Editor**.

This document currently only applies to content for the Windows platform.

## Required Configuration

Add the following options to your project's `DefaultEngine.ini` file:

```
		`[/Script/UnrealEd.CookerSettings] 		cook.AllowCookedDataInEditorBuilds=True 		s.AllowUnversionedContentInEditor=1`

Copy full snippet
```
\[/Script/UnrealEd.CookerSettings\] cook.AllowCookedDataInEditorBuilds=True s.AllowUnversionedContentInEditor=1

The first option corresponds to the **Allow Cooked Content in the Editor** option in the **Project Settings**, while the second option can currently only be set through the config file.

![The Allow Cooked Content in the Editor setting in the Project Settings window](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/120c3461-f429-4b87-bfb2-ab2ff19ae864/allow-cooked-content-setting.png)

## Cooking Content for Use in the Editor

When you set the config option `s.AllowUnversionedContentInEditor=1`, no further action is required to be able to use cooked content.

You can find cooked content in your project in the following folder:

```
		`Saved\Cooked\WindowsNoEditor\(ProjectName)\Content\`

Copy full snippet
```
Saved\\Cooked\\WindowsNoEditor\\(ProjectName)\\Content\\

In contrast to uncooked content, cooked content will consist of more than one file per Asset. Usually, an Asset will be split up into separate files, `.uasset` and possibly `.uexp` and `.ubulk` files. All of these need to be copied to your project's content folder for the cooked content to work.

## Behavior of Cooked Content in the Editor

Once you have versioned and cooked your Assets, you can drop them into your content folder and they will show up in the **Content Browser** as expected.

Cooked Assets will be read-only, and it is not possible to open editors for these Assets. For example, you can't view a cooked **Material** in the **Material editor**, nor open a cooked mesh in the **Static Mesh editor**.

Take special care when the cooked content has references to other content. To preserve any references, you must maintain the same folder structure the cooked content was originally in, and cooked Assets cannot be moved or renamed once cooked. The editor may not handle the additional `.uexp`/`.ubulk` files properly in some cases. For example, when deleting a cooked Asset through the content browser, its `.uexp`/`.ubulk` files might not be deleted.

There is currently no exhaustive list of which Asset types are supported, and the following listing is not implying that types listed as working are officially supported.

The following Asset types are regularly tested and should work when cooked:

-   Textures
-   Materials
-   Static Meshes
-   Sound waves
-   Cascade Particles
-   Animation Sequences
-   Skeletal Meshes
-   Level Sequences
-   AnimBPs
-   BP\_Enums

There are known issues with the following assets:

-   Niagara
-   Blueprints

Everything not listed might or might not work. Proceed carefully if using other Asset types.