# Map Check Errors

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/map-check-errors-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/map-check-errors-in-unreal-engine)  
**Processed:** 2025-06-14 16:34:59

---

Unreal Engine provides a mechanism for alerting you to potential problems in the form of map check errors and warnings instead of having to hunt down issues manually without knowing what is causing the problem or how to fix it. These errors are an automated way to find out where problems lie and allows you to get them fixed before they have a serious impact on your game.

## Performing a Map Check

Map check errors and warnings are displayed following performing a build all of a map and can also be performed separately using the *Map Check* option in the [Level Editor Toolbar](/documentation/en-us/unreal-engine/level-editor-toolbar-in-unreal-engine)'s Build menu.

## Errors

Errors are critical problems that can potentially cause execution failure. These need to be fixed before proceeding.

### Lighting

**\[LightActor\] has same light GUID as \[LightActor\] (Duplicate and replace the orig with the new one)**

Duplicate and replace the original with the new one.

## Warnings

Warnings are issues which, while not critical, can cause your game to not function properly or with sub-optimal performance. These should be addressed but are not showstoppers.

### Actor

**\[Actor\] : Large Actor casts a shadow and will cause an extreme performance hit unless bUseBooleanEnvironmentShadowing is set to true**

A large Actor has been set to cast shadows - this will cause extreme performance issues and should have bUseBooleanEnvironmentShadowing set to true.

**\[Volume\] causes damage, but has no damagetype defined.**

This warning is caused when there is a volume that is set to cause damage but does not have a damage type defined. A damage type is important because it tells the game code how to handle a Actor's reaction to taking damage. This can be solved by going to the Actor's Property Window->Physics Volume and setting the 'DamageType' property.

**\[Actor\] : Brush has non-coplanar polygons**

This warning is caused when there is a brush in the level that has non-coplanar polygons. This is usually caused by using brush editing tools in geometry mode in extreme ways and can cause missing polygons in the level. This warning can be resolved by deleting the brush and recreating it.

**\[Actor\] in same location as \[Another Actor\]**

This warning is caused when there is an Actor that is in the same exact location as another Actor. This warning is usually the result of an accidental duplication or paste operation. It can be fixed by deleting one of the Actors, or disregarded if the placement was intentional.

**\[Actor\] has invalid DrawScale/ DrawScale3D**

This warning is caused when either DrawScale, DrawScale3D X, DrawScale3D Y, or DrawScale 3D Z is equal to zero. Meaning that the Actor will not be shown because it is being scaled to zero on one of its axis. To solve this problem, change any DrawScale's that are zero to be non-zero by selecting the Actor and changing its drawscale at the bottom of the main UnrealEd window.

**\[Actor\] is obsolete and must be removed!**

This warning is caused when there is an instance of an Actor in a level that has been marked deprecated. This is usually because an Actor was marked deprecated after the level was created, but the map was never updated. This can be fixed by simply deleting the Actor.

**\[Actor\] bStatic true, but has Physics set to something other than PHYS\_None!**

This warning is caused when an Actor has its bStatic flag set to true but its Physics is set to PHYS\_None. Since bStatic means that the Actor will not be moving, having Physics set to PHYS\_None is contradictory. Actors set with the bStatic flag are also not ticked(updated). This error can be solved by going to the Actor's properties and changing its Physics to PHYS\_None.

**\[Actor\] : Volume Actor has NULL collision component - please delete**

The specified volume Actor has a NULL collision component and should probably be deleted.

**\[Actor\] : Volume Actor has a collision component with 0 radius - please delete**

The specified volume Actor has a zero radius for its collision component and should probably be deleted.

**\[Actor\] (LOD \[Index\]) has hand-painted vertex colors that no longer match the original StaticMesh \[StaticMesh\]**

It looks like the original mesh was changed since this instance's vertex colors were painted down - this may need a refresh.

**\[Actor\] has collision enabled but StaticMesh \[StaticMeshName\] has no simple or complex collision.**

You want to either set Collision Enabled to No Collision on the Actor, or add collision to the mesh (by adding simple collision shapes, and/or enabling collision on sections)

**Actor casts dynamic shadows and has a BoundsScale greater than 1! This will have a large performance hit**

Serious performance warning... either reduce BoundsScale to be less than or equal to 1 or remove dynamic shadows...

**\[ActorName\] has WorldTrace blocked. It will be considered to be world geometry**

### BSP Brush

**\[Brush Actor\] : Brush has zero polygons - please delete!**

This warning indicates that you have a brush in the level that does not have any polygons associated with it. The brush should be deleted as it is not doing anything useful.

**Run 'Clean BSP Materials' to clear \[count\] references**

This warning indicates that there are material references on brush faces that are not contributing to the BSP, and that applying the Tools->'Clean BSP Materials' operation can clean up these references.

**\[Actor\] : Brush has NULL BrushComponent property - please delete!**

This warning is caused when there is a Brush with a "None" ConstraintInstance component. It is usually found in older maps where duplication was used to create a Brush and can be fixed by deleting the Brush causing the warning and creating a new one.

**\[Brush\] : Brush is planar**

Planar brush used - please note that this may not work well with collision.

### Camera

**Camera has AspectRatio=0 - please set this to something non-zero**

### Class

**\[ \]::\[ \] is obsolete and must be removed (Class is abstract)**

**\[ \]::\[ \] is obsolete and must be removed (Class is deprecated)**

### Foliage

**Foliage instances for a missing Static Mesh have been removed.**

**Foliage in this map is missing \[MissingCount\] cluster component(s) for Static Mesh \[MeshName\]. Opening the Foliage tool will fix this problem.**

### Landscape

**\[LandscapeComponent\] : Fixed up deleted layer weightmap**

**\[LandscapeComponent\] : Fixed up incorrect layer weightmap texture index**

**Fixed up shared weightmap texture for layer \[Layer\] in component \[Component\] (shares with \[Name\])**

**Landscape (\[ProxyName\]) has overlapping render components at location (\[X,Y\])**

### Level

**Duplicate level info**

Two WorldInfos somehow exist...

**Map should have KillZ set.**

This warning is caused when the map's KillZ in the WorldInfo properties is set to the default value. All maps should specify a KillZ appropriate for the level so that players cannot simply fall forever until they reach the playable world bounds.

### Lighting

**\[Actor\] : Light Actor has NULL LightComponent property - please delete!**

This warning is caused when there is a Light Actor with a "None" LightComponent. It is usually found in older maps where duplication was used to create the Actor and can be fixed by deleting the Actor causing the warning and creating a new one.

**Maps need lighting rebuilt**

This warning is caused when lighting has been invalidated by moving or modifying a light Actor. This can cause problems because the rendered lighting in the level is not accurately representing the current state of lights in the level. This error can be solved by going to the Build menu and rebuilding lighting for a map.

**Component is a static type but has invalid lightmap settings! Indirect lighting will be black. Common causes are lightmap resolution of 0, LightmapCoordinateIndex out of bounds.**

### Navigation

**Paths need to be rebuilt**

### Particle System

**\[Actor\] : Emitter Actor has NULL ParticleSystemComponent property - please delete!**

This warning is caused when there is an Emitter Actor with a "None" ParticleSystemComponent. It is usually found in older maps where duplication was used to create the Actor and can be fixed by deleting the Actor causing the warning and creating a new one.

**PSysComp has an empty parameter Actor reference at index \[Index\] (\[Actor\])**

Param.Actor should not be NULL.

**PSysComp has an empty parameter material reference at index \[Index\] (\[Actor\])**

Param.Material should not be NULL.

### Skeletal Mesh

**\[Actor\] : SkeletalMeshActor has no PhysicsAsset assigned.**

In order for a SkeletalMesh to have an accurate bounding box, it needs to have a PhysicsAsset assigned in its SkeletalMeshComponent. An incorrect or inaccurate bounding box can lead to the mesh vanishing when its origin is not in view, or to poor shadow resolution because the bounding box is too big.

**\[Actor\] : Skeletal Mesh Actor has NULL SkeletalMeshComponent property**

The specified SkeletalMeshActor has a NULL SkeletalMeshComponent.

**\[Actor\] : Skeletal Mesh Actor has NULL SkeletalMesh property**

The specified SkeletalMeshActor has a NULL SkeletalMesh.

### Sound

**\[Actor\] : Ambient sound Actor has NULL AudioComponent property - please delete!**

This warning is caused when there is an Ambient sound Actor with a "None" AudioComponent. It is usually found in older maps where duplication was used to create an Actor and can be fixed by deleting the Actor causing the warning and creating a new one.

**Ambient sound Actor's AudioComponent has a NULL SoundCue property!**

This warning is caused when there is a AmbientSound Actor with a NULL SoundCue property. This is a problem because the Actor will not actually be playing any sounds. This can be fixed by first choosing a sound cue in the generic browser and then going to the Actor's Property Window->Audio Category->Audio Component and setting the 'SoundCue' property.

### Static Mesh

**\[Static Mesh Actor\] : Static Mesh Actor has NULL StaticMesh property**

This warning is caused when there is a Static Mesh Actor in a level with a NULL StaticMesh property. This can be a problem because the Actor exists and is using memory, but does not have a Static Mesh to actually draw. This warning is usually the result of creating a StaticMesh Actor without first selecting a StaticMesh in the generic browser. This warning can be fixed by first selecting a Static Mesh in the generic browser and then going to the StaticMesh Actor's Property Window->StaticMeshActor Category->StaticMeshComponent->StaticMeshComponent Category to set the 'StaticMesh' Property.

**\[Actor\] : Static Mesh Actor has NULL StaticMeshComponent property - please delete!**

This warning is caused when there is a Static Mesh Actor with a "None" StaticMeshComponent component. It is usually found in older maps where duplication was used to create the Actor and can be fixed by deleting the Actor causing the warning and creating a new one.

**\[StaticMesh\] has simple collision but is being scaled non-uniformly - collision creation will fail**

Simple collision cannot be used with non-uniform scale. Please either fix the scale or the collision type.

**More overridden materials \[Count\] on Static Mesh component than are referenced \[Count\] in source mesh \[StaticMesh\]**

**\[Count\] element(s) with zero triangles in Static Mesh \[StaticMesh\]**

### Volume

**LevelGridVolumes are only allowed in the persistent level**

This warning is caused when a LevelGridVolume is placed in a streaming level. These types of volumes are only allowed in the persistent level. This problem can be fixed by moving the LevelGridVolume to the persistent level.

**LevelStreamingVolume is not in the persistent level - please delete**

This warning is caused when there is a level streaming volume that does not exist in the persistent level. This can be problematic because the volume will not be considered when checking to see if a streaming level should be loaded or unloaded. You can fix this problem by deleting the level streaming volume and recreating it.

**No levels are associated with streaming volume.**

This warning is caused when there are no levels associated with a LevelStreamingVolume, making it non-functional. This problem can be fixed by associating one or more streaming levels with the offending LevelStreamingVolume.

### Uncategorized

**Filename \[Filename\] is too long - this may interfere with cooking for consoles. Unreal filenames should be no longer than \[Length\] characters.**

Please rename the file to be within the length specified.

**\[ObjectName\] : Externally referenced**

## Infos

Infos are issues which do not need to be addressed by the user but may be useful to know.

### Actors

**\[Actor\] : Repaired painted vertex colors**

Painted vertex colors were repaired on this Actor.