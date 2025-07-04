# Versioning of Assets and Packages

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/versioning-of-assets-and-packages-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/versioning-of-assets-and-packages-in-unreal-engine)  
**Processed:** 2025-06-14 17:02:51

---

**Unreal Engine (UE)** has multiple versioning systems that define and ensure compatibility between the Engine and the code and data it consumes. Versioning can be used not only to detect incompatible code or data, but also to manage custom serialization and data conversion. We will break UE versioning into three main systems: **Engine Version**, **Serialization Version**, and **Build ID**.

## Engine Version

The **Engine Version** is the highest-level and most user-visible form of versioning within UE. This part of the Engine's versioning system ensures backward compatibility and protects against data loss by controlling the saving and loading of Assets. The Engine Version appears in the **About Unreal Editor** section of the **Help** menu within the Editor.

![The About Unreal Editor dialogue box displays the current version of the Unreal Editor as well as the current changelist.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/75d33a05-1fa9-4ffc-b5ab-00bbca6c942f/about-unreal-editor.png "About Unreal Editor")

*The Engine Version, as displayed in the Editor.*

The actual Engine Version contains five components: major version, minor version, and patch version, followed by the changelist and the name of the branch from which it was built. In code, these five components exist in the `FEngineVersion` class and its parent class, `FEngineVersionBase`.

| Component | Type | Example Value (see screenshot above) |
| --- | --- | --- |
| Major Version | `uint16` | 5 |
| Minor Version | `uint16` | 0 |
| Patch Version | `uint16` | 3 |
| Changelist Number | `uint32` | 20979098 |
| Branch Name | `FString` | +++UE5+Release-5.0 |

The individual numerical components do not decrease in value over time, except when a higher-order value increases. This means that any two Engine Versions can be compared, component by component, to determine whether they are identical, or which is newer. In addition, a licensee-created changelist will always be considered newer than an Epic changelist, provided that the major version, minor version, and patch version values all match. The branch name is not used for compatibility checks, and exists primarily for display purposes.

Incompatible Engine Versions will cause the Engine to fail to load Assets. In some cases, this will cause an operation to fail in an obvious way, but note that Assets saved in a newer version of the Engine will simply not show up in the Content Browser, and any references to them will be treated as null. Saving the referencing Asset can be dangerous, as the now-null reference will be saved in the process, effectively losing that information without notifying the user.

### Assets and Packages

Assets contain the Engine Version of the Editor used to save them. By checking this value at load time, the Engine gracefully handles properties that have been added to, or removed from, serialized data via code changes. A removed field found during deserialization (such as while loading an Asset) will be unrecognized and ignored, while a newly-added field will be missing from the serialized data, but will hold its default value. Upon serializing the Asset's data to save it to disk, data for removed fields will have already been discarded, and data for newly-added fields will exist and be serialized along with all other properties. The end result of this is that, as data structures are changed over time, the serialized representations of those structures will smoothly discard obsolete fields while adding in new ones. For this reason, serialized data from any given version of the Engine will be legible only to the same or newer versions. This rule prevents data loss errors that would arise from older versions of the Engine discarding newer properties and then serializing data back to an on-disk format.

Engine Versions with Changelist 0 are considered compatible with all other Engine Versions. This facilitates engine development by engineers, but should not be used to save Assets to disk. Instead, content creators should use a distributed, binary build of the Editor, so that they can work with Assets that carry accurate Engine Version data and take advantage of the protections against data loss that it provides.

### Coding with Engine Version

The `FEngineVersion` class provides access to Engine Version information in your projects. It is recommended that these functions be called when you need to display your Engine Version or check for compatibility.

| Function Name | Static/Instance | Effect |
| --- | --- | --- |
| `Current` | Static | Gets the build's Engine Version. Typically used for display purposes rather than actual compatibility checks. |
| `CompatibleWith` | Static | Gets the earliest (lowest) Engine Version that the current build is compatible with. Intended for compatibility checks, such as those involving Assets, Modules, and network data. |
| `IsCompatibleWith` | Instance | Indicates whether or not the current Engine Version is compatible with the `FEngineVersionBase` input parameter you supply. |

Compatibility is possible if the current Engine Version is the same or newer than the Engine Version being checked. For example, any 4.19 Editor build will be compatible with any 4.18 Asset, but a 4.18 Editor build will not be compatible with an Asset saved in a 4.19 build. The exception to this is that two Engine Versions are always considered compatible if either has a Changelist component of 0. This is done to support the live development environment, as code-based builds of the Engine that were not synced via Unreal Game Sync are marked as Changelist 0, creating a more permissive environment with regard to version checks. When cooking a build, however, these Assets will cause warnings, so working with "Changelist 0" Assets is not recommended.

To disable warnings that appear during cooking a build with "Changelist 0" Assets, add `ZeroEngineVersionWarning=0` in the `[Core.System]` section of your project's `DefaultEngine.ini` file.

### Updating the Engine Version

The Engine Version of a build is controlled by the values defined within the `/Build/Build.version` file in the Engine. This file can be updated by editing it manually, by running the `UpdateLocalVersion` commandlet, or by syncing with [Unreal Game Sync](/documentation/en-us/unreal-engine/unreal-game-sync-ugs-for-unreal-engine). The following fields are read from the `/Build/Build.version` file:

| Field Name | Notes |
| --- | --- |
| `MajorVersion` | Controls the major version of the Engine. |
| `MinorVersion` | Controls the minor version of the Engine. |
| `PatchVersion` | Controls the patch version of the Engine. |
| `Changelist` | Defined manually. Can be updated manually, or by build systems using the `UpdateLocalVersion` **AutomationTool** command. This will use the depot path name of the build, replacing slashes with pluses. |
| `CompatibleChangelist` | This is the lowest (or earliest) value of Changelist that will be considered compatible with this Engine Version. It is often zero, such as for local builds of the Engine, but Epic's publicly-released binary builds, or binary builds distributed internally, will have nonzero values and will therefore be incompatible with locally-compiled versions. |
| `IsLicenseeVersion` | Should be 0 for locally-compiled builds synced from source control, but will be set to 1 by build systems through the `UpdateLocalVersion` AutomationTool command. Setting this to 1 is appropriate for promoted builds and will enable tighter version checking, although Hot Reload will be disabled. |
| `IsPromotedBuild` | Indicates that this is a promoted build. Default value is "1". |
| `BranchName` | A string used to describe the branch from which the build was compiled. Used for display purposes, or to uniquely identify a build. Does not affect compatibility checks. |
| `BuildId` | When compiling, the Engine and Modules are all tagged with this value. The Engine will consider any Module without this value to be incompatible. It is recommended that this be left blank, which will cause a new, unique value to be generated on each compile. See the **Build ID** section below for more information. |

### UpdateLocalVersion Commandlet

The `UpdateLocalVersion` commandlet is useful for cases where manually editing the `Build/Build.version` file is not desired, such as when compiling on a dedicated build machine. The `/Build/BatchFiles/RunUAT.bat` file can be used to launch the `UpdateLocalVersion` commandlet as follows:

```
	`RunUAT.bat UpdateLocalVersion [-CL=INT] [-CompatibleCL=INT] [-Build=STRING] [-SkipHeader] [-Licensee] [-Promoted=BOOL] [-Branch=STRING]`

Copy full snippet
```
RunUAT.bat UpdateLocalVersion \[-CL=INT\] \[-CompatibleCL=INT\] \[-Build=STRING\] \[-SkipHeader\] \[-Licensee\] \[-Promoted=BOOL\] \[-Branch=STRING\]

These parameters are interpreted as follows:

| Parameter | Type (Default Value) | Interpretation |
| --- | --- | --- |
| `CL` | Integer (0) | Controls the `Changelist` field in `Build.version`. |
| `CompatibleCL` | Integer (0) | Controls the `CompatibleChangelist` field in `Build.version`. |
| `Build` | String (empty) | Replaces the build version string in the engine by updating the `BUILD_VERSION` macro in source code. |
| `SkipHeader` | Bool (false) | If present, the Engine's header files will not be updated. |
| `Licensee` | Bool (false) | Controls the `IsLicensee` field in `Build.version`. If this parameter is present, will be treated as true. |
| `Promoted` | Bool (false) | Controls the `IsPromotedBuild` field in `Build.version`. Any non-zero integer value for this parameter will be considered `true` and will write `1` to the field. |
| `Branch` | String (empty) | Controls the `BranchName` field in `Build.version`. |

## Object Version

UObject-derived classes are subject to compatibility checks based on Engine Version, but they also have a separate, two-part versioning system, **Object Version**, which features both an Engine-level version and any number of custom, Object-level versions. Object serialization is often customized to improve performance (such as Assets containing a lot of bulk data), implement data format changes (such as performing unit conversions), or to save space (such as by writing Object data to disk in a compressed format). Implementing custom serialization requires overriding the `UObject` function, `Serialize`, changing the data format depending on your project's needs, and including checks based on the Object Version in the new code. Doing this will enable you to maintain backward compatibility across serialization changes, while preventing data loss, in the same way that Engine Version does.

### Engine-Level Serialization and Versioning

At the Engine level, a global enumerated type, `EUnrealEngineObjectUE5Version`, is used to version custom serializer functions. Whenever a custom serializer is changed, a new entry should be added into `EUnrealEngineObjectUE5Version`. Since this enumerated type is modified by Epic in official Unreal Engine releases, a parallel global enumerated type, `EUnrealEngineObjectLicenseeUEVersion`, exists for licensees to add their own Engine-level versioning. All future packages saved will have the incremented values of both enumerated types saved into the package, and serializing (and deserializing) code can perform logic with these values to determine how to read or write data.

The Engine will automatically check these version values against itself, and will fail to load any package with a version number higher than that of the Engine.

This method is not ideal for developers who have multiple teams working on different areas of the Engine. It is impossible to update the version enumeration in multiple places, and reordering the constants when merging will corrupt or invalidate Assets saved with those version numbers. Object-level serialization is recommended for developers with multiple teams writing custom serialization code.

### Object-Level Serialization and Versioning

To support parallel development (especially when using different branches), the Engine provides Object-level versioning via `FGuid`\-based custom versions. The `FGuid` structure contains an integer version number, which can be increased over time like any other version number would (generally implemented as a custom enumerated type), but also contains a global unique identifier (GUID) which makes it possible to have as many different, parallel custom versions as your team needs. Keeping a separate custom version for each system or branch makes it easy to update the custom version in one branch without causing conflicts when merging code from other branches.

To register a new `FGuid`, create a global object of type `FCustomVersionRegistration` with your GUID and current version number. For example, the following line of code creates the `AnimGraphVer` `FGuid` in `Engine/Source/Runtime/AnimGraphRuntime/Private/AnimationCustomVersion.cpp`:

```
	`const FGuid FAnimationCustomVersion::GUID(0x2EB5FDBD, 0x01AC4D10, 0x8136F38F, 0x3393A5DA); 	// Register the custom version with core 	FCustomVersionRegistration GRegisterAnimationCustomVersion(FAnimationCustomVersion::GUID, FAnimationCustomVersion::LatestVersion, TEXT("AnimGraphVer"));`

Copy full snippet
```
const FGuid FAnimationCustomVersion::GUID(0x2EB5FDBD, 0x01AC4D10, 0x8136F38F, 0x3393A5DA); // Register the custom version with core FCustomVersionRegistration GRegisterAnimationCustomVersion(FAnimationCustomVersion::GUID, FAnimationCustomVersion::LatestVersion, TEXT("AnimGraphVer"));

At the Object level, each UObject-derived class can choose to serialize one or more `FGuid` structures in its `Serialize` by calling the `FArchive` function, `UsingCustomVersion`. Custom code can then perform logic based on the version number from any registered `FGuid` to determine what data to read or write. Because the version number associated with any `FGuid` registered this way is assumed never to decrease, this also enables the Engine to ensure that Assets from a new version are not loaded, protecting against data loss while preserving backward compatibility in the same manner as Engine Version.

### Custom Serialization Function

Objects can override the `UObject` function called `Serialize` to control the exact data representation they have on disk. This function both reads and writes data, using the `FArchive` class, meaning you only have to lay out your data format once. The following `FArchive` functions are useful when writing version-based logic in serialization code:

| Function Name | Usage |
| --- | --- |
| `UEVer` | Returns the (Epic) Engine-level version number. This value will match up to an entry in `EUnrealEngineObjectUE5Version`. |
| `LicenseeUEVer` | Returns the (licensee) Engine-level version number. This value will match up to an entry in `EUnrealEngineObjectLicenseeUEVersion`. |
| `CustomVer` | Returns the Object-level custom version number for the current Object, based on the `FGuid` provided. This function will return -1 if `UsingCustomVersion` (see below) was not called with this `FGuid` when the Object was saved. |
| `UsingCustomVersion` | Registers an `FGuid` with the Object to track its custom version number. |

### Object Version Code Examples

Wheeled vehicles in the PhysXVehicles Plugin (included with the Engine) use both Engine Object Version and Custom Version to maintain backward compatibility with Assets built prior to certain changes to physics code.

Here, a Custom Version is used to set a variable that will change how the offset to the physics spring object representing the wheel's suspension will be calculated later. The specific Custom Version value used is taken from an enumerated type that was created by the team that maintains physics code.

```
	`void UWheeledVehicleMovementComponent::Serialize(FArchive& Ar) 	{ 		Super::Serialize(Ar); 		Ar.UsingCustomVersion(FFrameworkObjectVersion::GUID); 		if (Ar.CustomVer(FFrameworkObjectVersion::GUID) < FFrameworkObjectVersion::WheelOffsetIsFromWheel) 		{ 			bDeprecatedSpringOffsetMode = true; 		} 	}`

Copy full snippet
```
void UWheeledVehicleMovementComponent::Serialize(FArchive& Ar) { Super::Serialize(Ar); Ar.UsingCustomVersion(FFrameworkObjectVersion::GUID); if (Ar.CustomVer(FFrameworkObjectVersion::GUID) < FFrameworkObjectVersion::WheelOffsetIsFromWheel) { bDeprecatedSpringOffsetMode = true; } }

In the following example, unit conversion is performed in response to a physics change that caused angular velocity to be measured in revolutions per second rather than radians per second. Since these angular velocities were stored as floating-point values (without units), old Assets now require load-time conversion. In this case, we will only modify the angular velocity variable when loading the Asset. Any Asset of this type that we save will already have its angular velocity in revolutions per second, and will be saved with the current Engine version number, avoiding the need to run conversion code the next time that Asset is loaded.

```
	`void FConstraintInstance::PostSerialize(const FArchive& Ar) 	{ 	#if WITH_EDITORONLY_DATA 		// ... 		if (Ar.IsLoading() && Ar.UEVer() < VER_UE_FIXUP_MOTOR_UNITS) 		{ 			AngularVelocityTarget *= 1.f / (2.f * PI); 		} 		// ... 	#endif 	}`

Copy full snippet
```
void FConstraintInstance::PostSerialize(const FArchive& Ar) { #if WITH\_EDITORONLY\_DATA // ... if (Ar.IsLoading() && Ar.UEVer() < VER\_UE\_FIXUP\_MOTOR\_UNITS) { AngularVelocityTarget \*= 1.f / (2.f \* PI); } // ... #endif }

Changing the `UEVer` function call to `LicenseeUEVer` will change the code to use the licensee's version number, rather than the official Epic version number. This is recommended for non-Epic users who maintain their own version of Unreal Engine.

## Versioning of Binaries

Read the [Versioning of Binaries](/documentation/en-us/unreal-engine/how-to-version-binaries-in-unreal-engine) reference page to learn more.