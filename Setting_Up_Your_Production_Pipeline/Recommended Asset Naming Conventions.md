# Recommended Asset Naming Conventions

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/recommended-asset-naming-conventions-in-unreal-engine-projects](https://dev.epicgames.com/documentation/en-us/unreal-engine/recommended-asset-naming-conventions-in-unreal-engine-projects)  
**Processed:** 2025-06-14 16:45:55

---

As you develop projects in **Unreal Engine (UE)**, the list of **Assets** in your **Content Browser** will expand. This runs the risk of creating redundant variations of assets you're experimenting with, or introducing ambiguity with overly similar names. For example, it is possible for you to have a folder named "Soldier" with a Blueprint, a texture, and a model that all have the name "Soldier" in them, but no clear way to tell which is which in a simple list.

For large projects, we recommend you establish a common naming convention for individual Assets early in development. This will make it easier for you and your team to locate files and prevent potential conflicts or ambiguity. The naming convention described below reflects how Epic Games names Assets in sample projects, such as the [In-Camera VFX Production Test](/documentation/en-us/unreal-engine/in-camera-vfx-production-test-sample-project-for-unreal-engine).

```
		`[AssetTypePrefix]_[AssetName]_[Descriptor]_[OptionalVariantLetterOrNumber]`

Copy full snippet
```
\[AssetTypePrefix\]\_\[AssetName\]\_\[Descriptor\]\_\[OptionalVariantLetterOrNumber\]

-   `AssetTypePrefix` identifies the type of Asset, refer to the table below for details.
    
-   `AssetName` is the Asset's name.
    
-   `Descriptor` provides additional context for the Asset, to help identify how it is used. For example, whether a texture is a normal map or an opacity map.
    
-   `OptionalVariantLetterOrNumber` is optionally used to differentiate between multiple versions or variations of an asset.
    

Consider using this naming convention for your own project's Assets, as it will provide multiple ways for your team to locate an Asset when searching the Content Browser.

This naming convention is only a recommendation to simplify setting up your project. Your requirements will always take precedence, and it is likely that you won't use all of these Asset types in your Project.

## Recommended Asset Prefixes

This list is not exhaustive, as new features can require new Asset types. If you are using an Asset type not listed, use the existing list as a guideline for your naming convention for that Asset.

| Asset | Prefix |
| --- | --- |
| General |   |
| [HDRI](/documentation/en-us/unreal-engine/hdri-backdrop-visualization-tool-in-unreal-engine) | HDR\_ |
| [Material](/documentation/en-us/unreal-engine/unreal-engine-materials) | M\_ |
| [Material Instance](/documentation/en-us/unreal-engine/instanced-materials-in-unreal-engine) | MI\_ |
| [Physics Asset](/documentation/en-us/unreal-engine/physics-asset-editor-in-unreal-engine) | PHYS\_ |
| [Physics Material](/documentation/en-us/unreal-engine/physical-materials-in-unreal-engine) | PM\_ |
| [Post Process Material](/documentation/en-us/unreal-engine/post-process-materials-in-unreal-engine) | PPM\_ |
| [Skeletal Mesh](/documentation/en-us/unreal-engine/skeletal-mesh-assets-in-unreal-engine) | SK\_ |
| [Static Mesh](/documentation/en-us/unreal-engine/static-meshes) | SM\_ |
| [Texture](/documentation/en-us/unreal-engine/textures-in-unreal-engine) | T\_ |
| [OCIO Profile](/documentation/en-us/unreal-engine/color-management-with-opencolorio-in-unreal-engine) | OCIO\_ |
| [Blueprints](/documentation/en-us/unreal-engine/blueprints-visual-scripting-in-unreal-engine) |   |
| Actor Component | AC\_ |
| Animation Blueprint | ABP\_ |
| Blueprint Interface | BI\_ |
| Blueprint | BP\_ |
| Curve Table | CT\_ |
| Data Table | DT\_ |
| Enum | E\_ |
| Structure | F\_ |
| Widget Blueprint | WBP\_ |
| 
[Particle Effects](/documentation/en-us/unreal-engine/creating-visual-effects-in-niagara-for-unreal-engine)



 |   |
| Niagara Emitter | FXE\_ |
| Niagara System | FXS\_ |
| Niagara Function | FXF\_ |
| 

[Skeletal Mesh Animations](/documentation/en-us/unreal-engine/skeletal-mesh-animation-system-in-unreal-engine)



 |   |
| Rig | Rig\_ |
| Skeleton | SKEL\_ |
| Montages | AM\_ |
| Animation Sequence | AS\_ |
| Blend Space | BS\_ |
| [ICVFX](/documentation/en-us/unreal-engine/in-camera-vfx-in-unreal-engine) |   |
| NDisplay Configuration | NDC\_ |
| [Animation](/documentation/en-us/unreal-engine/cinematics-and-movie-making-in-unreal-engine) |   |
| Level Sequence | LS\_ |
| Sequencer Edits | EDIT\_ |
| [Media](/documentation/en-us/unreal-engine/media-framework-in-unreal-engine) |   |
| Media Source | MS\_ |
| Media Output | MO\_ |
| Media Player | MP\_ |
| Media Profile | MPR\_ |
| Other |   |
| [Level Snapshots](/documentation/en-us/unreal-engine/level-snapshots-in-unreal-engine) | SNAP\_ |
| [Remote Control Preset](/documentation/en-us/unreal-engine/remote-control-for-unreal-engine) | RCP\_ |