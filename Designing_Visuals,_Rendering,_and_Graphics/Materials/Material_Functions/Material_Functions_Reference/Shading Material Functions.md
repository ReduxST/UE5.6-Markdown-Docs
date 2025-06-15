# Shading Material Functions

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/shading-material-functions-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/shading-material-functions-in-unreal-engine)  
**Processed:** 2025-06-14 16:50:18

---

The Shading Material functions provide for specialized shading operations, such as fuzzy shading and adjusting the shape of a specular highlight.

## FuzzyShading

This function emulates a surface similar to velvet or moss, and is similar to a Fresnel calculation. Incidentally, it is also useful for shader effects such as a scanning electron microscope.

| Inputs | Description |
| --- | --- |
| **Diffuse (Vector3)** | Takes in a texture to be used as the diffuse color. |
| **Normal (Vector3)** | Takes in a normal map used to perturb the surface of the fuzzy result. |
| **CoreDarkness (Scalar)** | Value used to darken the object wherever its normals become parallel to the camera, generally toward the center. The higher the number, the darker the core. Default is 0.8. |
| **Power (Scalar)** | Controls the rate of falloff from the core to the edge. Default is 6.0. |
| **EdgeBrightness (Scalar)** | Controls how bright the surface becomes as its normals become perpendicular to the camera, generally toward the edges. |

![Fuzzy Shading](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8b14c472-92fe-48fc-8690-20155df38007/fuzzy-shading.png)

## FuzzyShadingGrass

This function is designed to provide the diffuse portion of grass shading. Similar to FuzzyShading, this function allows you to blend in a new color at the edges by first desaturating by a given percentage and then applying a custom color to the desaturated area.

| Inputs | Description |
| --- | --- |
| **EdgeDesat (Scalar)** | 0-1 number controlling how much the edges of the object should be desaturated to make way for the edge color. |
| **EdgeColor (Vector3)** | This color will be applied to the edge area. Use *EdgeDesat* to desaturate that area if too much color mixing is taking place. |
| **Diffuse (Vector3)** | Takes in a texture to be used as the diffuse color. |
| **Normal (Vector3)** | Takes in a normal map used to perturb the surface of the fuzzy result. |
| **CoreDarkness (Scalar)** | Value used to darken the object wherever its normals become parallel to the camera, generally toward the center. The higher the number, the darker the core. Default is 0.8. |
| **Power (Scalar)** | Controls the rate of falloff from the core to the edge. Default is 6.0. |
| **EdgeBrightness (Scalar)** | Controls how bright the surface becomes as its normals become perpendicular to the camera, generally toward the edges. |

![Fuzzy Shading Grass](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/71f0c059-9f3d-49a1-abdf-2560e6e27b77/fuzzy-shading-grass.png)