# Alembic for Grooms Specification

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/using-alembic-for-grooms-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/using-alembic-for-grooms-in-unreal-engine)  
**Processed:** 2025-06-14 16:58:16

---

The Hair Rendering and Simulation features are intended to provide a minimally viable implementation of strand-based hair importing, rendering, and simulation. This update does not provide a hair grooming solution. Hair shaping, or grooming, will need to be performed in an external DCC tool such as Maya by using their XGen tool or the plugin [Shave and a Haircut](https://www.unrealengine.com/en-US/programs/shave-and-a-haircut). Other tools like [Ornatrix](https://ephere.com/plugins/autodesk/max/ornatrix/), [Yeti](https://peregrinelabs.com/yeti/), or [Houdini](https://www.sidefx.com/docs/houdini/fur/workflow.html) can be used as well.

This document outlines an informal schema for Alembic files in an attempt to standardize the import of hair groom and guide hair information into Unreal Engine for use with the [Hair Rendering and Simulation](/documentation/en-us/unreal-engine/hair-rendering-and-simulation-in-unreal-engine) features. The intent is that as you generate Hair Grooms, conforming to this schema allows Unreal Engine to import those grooms directly. Upon import, attributes that are supported by UE4 for both rendering and physics will be mapped to those attributes in the Alembic file.

## Goals

1.  Define a groom-specific, informal, Alembic metadata schema to facilitate importing of hair into Unreal Engine.
2.  Examine the attributes that are supported by Unreal Engine for hair, and map those attributes onto Alembic.

### Curves

The general shape of the hair is read from the standard Alembic Curve schema:

```
`Alembic::AbcGeom::ICurves`
Copy full snippet
```
Alembic::AbcGeom::ICurves

### Width

Groom attributes exported using this specification enables the importer to retrieve and use them when building the groom. However, the width attribute does have a special behavior. For example, in a DCC application like Maya, width values are exported directly on the curves so there's no need to export a custom `groom_width` attribute; the importer will convert Maya's width values into the `groom_width` attribute. It is worth noting that if the `groom_width` attribute is present in your groom, it will not be overwritten during import. If no `groom_width` attribute is specified, or one couldn't be converted from width values, the builder in Unreal Engine falls back to using a value of 1 centimeter for the width value.

The curve width can be stored per-ICurve using:

```
`(GeometryScope::kConstantScope)`
Copy full snippet
```
(GeometryScope::kConstantScope)

Or it can be stored per-curve using:

```
`(GeometryScope::kUniformScope)`
Copy full snippet
```
(GeometryScope::kUniformScope)

Or it can be stored per-cv using:

```
`(GeometryScope::kVertexScope)`
Copy full snippet
```
(GeometryScope::kVertexScope)

Note that the importer supports `kUniformScope`, but this has not been tested.

## Naming Conventions

Property names must be lowercase with no spaces or special characters.

All properties must start with the following prefix:

```
`groom_<attr>`
Copy full snippet
```
groom\_<attr>

For example, `groom_id`, `groom_color`, or `groom_width` are all using the proper naming conventions.

## Scoping and Precedence

Properties in this document have an assigned scope. The scope controls at which *level* the groom property can be defined.

The available scopes are:

| Scope | Description |
| --- | --- |
| **Constant** | These parameters have a single value for all curves with an `AbcGeom::ICurves` Object. |
| **Uniform** | These parameters have a value per-curve in an `AbcGeom::ICurves` Object. |
| **Vertex** | These parameters have a value per-curve per-cv. |

### General Properties

This section outlines properties that apply to the groom as a whole. These properties should be added to the topmost node: IXForm or ICurves.

| Name | Type | Optional | Description | Value |
| --- | --- | --- | --- | --- |
| `groom_version_major` | int16 | No | Used to identify which **major** version of the groom schema this file conforms to. | 1 |
| `groom_version_minor` | int16 | No | Used to Identify which **minor** version of the schema this file conforms to. | 5 |
| `groom_tool` | string | Yes | The name and version of the tool that generated this file. Useful for debugging and tracking down issues. |   |
| `groom_properties` | string | Yes | String describing the parameters used to generate this groom. These are tool-specific options, used for debugging. |   |

### Geometry Parameters

All geometry parameters are optional but have internal behavior to fall back on if they are not present with your exported groom.

| Name | Type | Scope | Optional | Description | Range |
| --- | --- | --- | --- | --- | --- |
| `groom_ guide` | int8/16/32 | Constant/Uniform | Yes | Guides are generated from the imported strands and decimation settings. | 0 = Not a guide / 1 = Guide |
| `groom_group_id` | int32 | Constant/Uniform | Yes | All strands will be grouped together. | \[0, INT\_MAX\] |
| `groom_root_uv` | float32/64\[2\] | Uniform | Yes | 
Root UVs are computed by projecting the root of the strand onto a sphere.

This attribute is optional. If not specified, a root UV is automatically generated in the engine using a spherical mapping.



 | \[-FLOAT\_MAX, FLOAT\_MAX\] |
| `groom_id` | int32 | Uniform | Yes | Strands won't have IDs. This is intended for use in debugging and with `groom_closest_guides` attribute. | \[0, INT\_MAX\] |
| `groom_color` | float32/64\[3\] | Vertex | Yes | Falls back to black. | \[0, FLOAT\_MAX\] |
| `groom_closest_guides` | int32\[3\] | Uniform | Yes | Intended for specialized use where the interpolation data is computed outside of Unreal Engine. | \[0, INT\_MAX\] |
| `groom_guide_weights` | float32\[3\] | Uniform | Yes | Intended for specialized use where the interpolation data is computed outside of Unreal Engine. | \[0, FLOAT\_MAX\] |