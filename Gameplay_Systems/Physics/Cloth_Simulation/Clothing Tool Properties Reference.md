# Clothing Tool Properties Reference

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/clothing-tool-in-unreal-engine---properties-reference](https://dev.epicgames.com/documentation/en-us/unreal-engine/clothing-tool-in-unreal-engine---properties-reference)  
**Processed:** 2025-06-14 16:13:45

---

The **Cloth Paint Tools** have many options and properties that you can use to make very specific clothing simulations. Below you'll find the details about the menu options you can use when creating your clothing assets and details about the Cloth Paint panel that you will use when selecting different painting tools to paint cloth values for your render mesh.

## Clothing Asset Creation Menus

In this section, you'll find the details about the properties and settings you can use when creating and applying your clothing assets to your render mesh.

### Section Selection

The **Section Selection** menu is available by right-clicking a selected section. It enables you to select the different material elements of your render mesh to create and apply a clothing asset. In this menu, you can identify the LOD and a material section of your mesh that you've selected, create a cloth asset for your render mesh and its LODs, apply the clothing asset to the selected section, and remove it later if needed.

![The context menu which opens when right-clicking a selected section](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f050943e-8b56-4e9e-889c-0180b46da86c/section-selection-context-menu-properties.png)

| Property | Description |
| --- | --- |
| **LOD Section Selection** | The name of the LOD level used and the Section to create a Cloth Asset for. |
| **Apply Clothing Asset** | Select a clothing asset to apply to the selected section. |
| **Remove Clothing Asset** | Remove the currently assigned clothing asset. |
| **Create Clothing Asset from Section** | 
Create a new clothing asset using the selected section as a simulation mesh.

![Create a new clothing asset using the selected section](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/142d7a81-a22c-4571-8992-086079b1449f/create-cloth-section.png)

-   Basics
    -   **Asset Name**: The name entered for the cloth section asset.
    -   **Remove from Mesh**: Whether or not to leave this section behind (if driving a mesh with itself). Enable this is driving a high-poly mesh with a low-poly mesh.
-   Collision
    -   **Physics Asset**: Physics Asset to extract collisions from. Note that this will export Sphere and Sphylls, but does support up to 32 convex faces (or 5 boxes).



 |
| **Create Clothing Asset from LOD Section** | 

Create a clothing simulation mesh from the selected section and add its LOD to an existing clothing asset.

![Create a clothing simulation mesh from the selected section and add its LOD to an existing clothing asset](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ce1e03c2-b099-4c7c-800e-bf1fcd1f0365/create-cloth-lod-section.png)

-   Target
    -   **Remap Parameters**: If reimporting, this will map the old LOD parameters to the new LOD mesh. If adding a new LOD, this will map the parameters from the preceding LOD.
    -   **Target Asset**: This is the target asset when importing LODs.
    -   **LOD Index**
        -   **Replace LOD**: Replace the simulation mesh in LOD0 of your selected clothing asset with this section.
        -   **Add LOD**: Use the selected section to add a new LOD.
-   Basic
    -   **Remove from Mesh**: Whether or not to leave this section behind (if driving a mesh with itself). Enable this if driving a high-poly mesh with a low-poly one.



 |
| **Generate section # up to LOD #** | Generated LODs will use section # up to LOD #, and ignore it for lower quality LODs |

## Clothing Panel

The **Clothing** panel houses all the clothing data, masks, configuration parameters for how your cloth reacts, and the tools you'll use when painting your cloth values.

![The clothing panel with main parameter categories expanded](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a0acdafe-fcd7-4a72-8bd2-078bab0cfb57/clothing-panel-properties.png)

### Clothing Data

The **Clothing Data** category displays your currently created clothing assets that are assigned to a render mesh,enables you to copy clothing data from an existing skeletal mesh, and lets you select from the available LODs created for your mesh to adjust parameter values.

![The properties in the clothing data section of the clothing panel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bf134e56-13b0-4469-89f9-6efa1680f267/clothing-data-properties.png)

| Property | Description |
| --- | --- |
| **Name** | The name of the cloth asset created for a LOD section of your physical mesh. |
| **Copy Clothing from SkeletalMesh** | Enables you to select a skeletal mesh from which to copy clothing data. |
| **Level of Detail (LOD) Selection** | Enables you to select a Level of Detail (LOD) mesh to set parameters, paint values, or copy values to. |

### Masks

The **Masks** category displays any created parameter sets for painted cloth values. These can be assigned a Target value for use with your clothing asset.

![The properties in the mask section of the clothing panel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/57840654-a2b6-4456-86dd-18dda5cf62a3/mask-properties.png)

| Property | Description |
| --- | --- |
| **Name** | 
The name given to the mask along with its target setting for this parameter set.

Context Menu Settings

-   Set Target
    -   **None**: The target has not been set for this parameter set.
    -   **Max Distance**: This is the maximum distance the clothing simulation particle can move from its animated position.
    -   **Backstop Distance**: This is the distance offset from the Max Distance used to limit the movement of the cloth simulation particles.
    -   **Backstop Radius**: This is a radius that when intersected with the Max Distance will prevent any cloth simulation particle from moving into that area.
-   Actions
    -   **Move Up**: Moves the Mask up one slot in the list.
    -   **Move Down**: Move the Mask down one slot in the list.
    -   **Delete**: Deletes the Mask from the list.
    -   **Apply**: Applies the Mask to the physical mesh.



 |
| **Plus (+)** | Adds a new Mask to the available list of Mask parameters. |

### Config

The **Config** properties enable you to adjust how your cloth reacts so that it can simulate different types of material, such as burlap, rubber, leather, and much more.

![Clothing panel configuration properties](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7ec49aad-0817-498c-a0a2-dd6876fcb68a/clothing-config-properties.png)

| Property | Description |
| --- | --- |
| **Physics Asset** | The Physics Asset to extract collisions from when building a simulation. |
| **Wind Method** | 
How wind should be processed; Accurate uses drag and lift to make the cloth react differently, Legacy applies similar forces to all clothing without drag and lift (similar to APEX).

-   **Legacy**: Use the Legacy wind mode, where accelerations are modified directly by the simulation with no regard to drag or lift.



 |
| **Vertical Constraint Config** | 

Constraint data for vertical constraints.

-   **Stiffness**: How stiff this constraint is between the nodes. This affects how closely it will follow the desired position.
-   **Stiffness Multiplier**: This is a multiplier affecting the **Stiffness** value used.
-   **Stretch Limit**: The hard limit on how far this constraint can stretch.
-   **Compression Limit**: The hard limit on how far this constraint can compress.



 |
| **Horizontal Constraint Config** | 

Constraint data for horizontal constraints.

-   **Stiffness**: How stiff this constraint is between the nodes. This affects how closely it will follow the desired position.
-   **Stiffness Multiplier**: This is a multiplier affecting the **Stiffness** value used.
-   **Stretch Limit**: The hard limit on how far this constraint can stretch.
-   **Compression Limit**: The hard limit on how far this constraint can compress.



 |
| **Bend Constraint Config** | 

Constraint data for bend constraints.

-   **Stiffness**: How stiff this constraint is between the nodes. This affects how closely it will follow the desired position.
-   **Stiffness Multiplier**: This is a multiplier affecting the **Stiffness** value used.
-   **Stretch Limit**: The hard limit on how far this constraint can stretch.
-   **Compression Limit**: The hard limit on how far this constraint can compress.



 |
| **Shear Constraint Config** | 

Constraint data for shear constraints.

-   **Stiffness**: How stiff this constraint is between the nodes. This affects how closely it will follow the desired position.
-   **Stiffness Multiplier**: This is a multiplier affecting the **Stiffness** value used.
-   **Stretch Limit**: The hard limit on how far this constraint can stretch.
-   **Compression Limit**: The hard limit on how far this constraint can compress.



 |
| **Self Collision Radius** | The size of self-collision spheres centered on each vertice. |
| **Self Collision Stiffness** | The stiffness of the spring force that will resolve self-collisions. |
| **Self Collision Cull State** | The scale to use for the radius of the culling checks for self-collisions. Any other self-collision body within the radius of this check will be culled. This helps performance with higher resolution meshes by reducing the number of colliding bodies within the cloth. Reducing this will harm performance. |
| **Damping** | The damping of particle motion per-axis. |
| **Friction** | The friction of the surface when colliding. |
| **Wind Drag Coefficient** | The drag coefficient for wind calculations, where higher values mean wind has a more lateral effect on cloth. |
| **Wind Lift Coefficient** | The lift coefficient for wind calculations, where higher values make cloth rise easier in the wind. |
| **Linear Drag** | The drag applied to linear particle movement per-axis. |
| **Angular Drag** | The drag to angular particle movement, where higher values should limit material bending (per-axis). |
| **Linear Inertia Scale** | The scale for linear particle inertia, or how much movement should translate to linear motion (per-axis). |
| **Angular Inertia Scale** | The scale for angular particle inertia, or how much movement should translate to angular motion (per-axis). |
| **Centrifugal Inertia Scale** | The scale for centrifugal particle inertia, or how much movement should translate to angular motion (per-axis). |
| **Solver Frequency** | The frequency of the position solver, where lower values will lead to stretchier, bouncier cloth. |
| **Stiffness Frequency** | The frequency for stiffness calculations, where lower values will degrade stiffness of constraints. |
| **Gravity Scale** | The scale of gravity effect on the cloth particle simulation. |
| **Gravity Override** | The direct gravity override value |
| **Tether Stiffness** | The scale for stiffness of particle tethers between each other. |
| **Tether Limit** | The scale for the limit of particle tethers (how far they can separate). |
| **Collision Thickness** | The "thickness" of the simulated cloth, which is used to adjust collisions. |
| **Anim Drive Spring Thickness** | Default spring thickness if an anim drive is in use. |
| **Anim Drive Damper Thickness** | Default damper thickness if an anim drive is in use. |

### Import

The **Import** option displays the file path of any [imported APEX files](/documentation/en-us/unreal-engine/clothing-tool-in-unreal-engine---properties-reference#clothingdata).

![The field where an imported clothing asset's original path is displayed in the clothing panel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1f68360b-be00-4737-93b4-985e1ce9284d/import.png)

| Property | Description |
| --- | --- |
| **Imported File Path** | If this asset was imported from a file, this will be the original path. |

### Cloth Painting

The **Cloth Painting** section enables you to select between your different tools, such as brush, gradient, smooth, and fill.

Before these properties can be populated, you must first select a clothing asset from your [Clothing Data](/documentation/en-us/unreal-engine/clothing-tool-in-unreal-engine---properties-reference#clothingdata) window and then click the **Activate Paint Tools** button in the toolbar.

![The activate cloth pain button in the toolbar](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/859989f8-ccbe-4fb3-80e7-5dfc9856262c/activate-cloth-paint.png)

The type of tool to use when painting cloth values.

-   [Brush](/documentation/en-us/unreal-engine/clothing-tool-in-unreal-engine---properties-reference#brush)
-   [Gradient](/documentation/en-us/unreal-engine/clothing-tool-in-unreal-engine---properties-reference#gradient)
-   [Smooth](/documentation/en-us/unreal-engine/clothing-tool-in-unreal-engine---properties-reference#smooth)
-   [Fill](/documentation/en-us/unreal-engine/clothing-tool-in-unreal-engine---properties-reference#fill)

#### Brush

The **Brush** tool enables you to paint a radius and strength value on your cloth as you drag across cloth asset.

![The brush cloth painting properties](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ffd343c8-35b5-4086-90ff-0599ed3d8c84/cloth-painting-brush.png)

| Property | Description |
| --- | --- |
| View |   |
| **View Min** | When painting float/1D values, this is considered the zero or black point for painted values. |
| **View Max** | When painting float/1D values, this is considered the one or white point for painted values. |
| **Autoview Range** | When set, the view min and max values will be calculated from the values present in the currently editable mask. |
| Advanced Rollout |   |
| **Flip Normal** | Whether to flip normals on the mesh preview. |
| **Cull Backface** | Whether to cull back-facing triangles when rendering the mesh preview. |
| **Opacity** | The opacity value of the mesh preview enables you to see through the mesh. |
| Visualization |   |
| **Vertex Preview Size** | Size of vertex points drawn when mesh painting is active. |
| Tool Settings |   |
| **Paint Value** | The value to paint onto the mesh for this parameter. |
| Brush |   |
| **Radius** | The radius of the Brush used for painting. |
| **Strength** | The strength of the brush (0.0 - 1.0). |
| **Falloff** | The amount of fall off to apply (0.0 - 1.0). |
| **Enable Brush Flow** | Enables "flow" painting where the paint is continually applied from the brush every tick. |
| **Ignore back-facing** | Whether back-facing triangles should be ignored when painting. |

#### Gradient

The **Gradient** tool enables you to paint a gradual blend between a set of cloth values that are selected.

![The gradient cloth painting properties](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b75b559c-d966-44ac-92e6-5ade13597e99/cloth-painting-gradient.png)

| Property | Description |
| --- | --- |
| View |   |
| **View Min** | When painting float/1D values, this is considered the zero or black point for painted values. |
| **View Max** | When painting float/1D values, this is considered the one or white point for painted values. |
| **Autoview Range** | When set, the view min and max values will be calculated from the values present in the currently editable mask. |
| Advanced Rollout |   |
| **Flip Normal** | Whether to flip normals on the mesh preview. |
| **Cull Backface** | Whether to cull back-facing triangles when rendering the mesh preview. |
| **Opacity** | The opacity value of the mesh preview enables you to see through the mesh. |
| Visualization |   |
| **Vertex Preview Size** | Size of vertex points drawn when mesh painting is active. |
| Tool Settings |   |
| **Gradient Start Value** | The value of the gradient at the start points. |
| **Gradient End Value** | The value of the gradient at the end points. |
| **Use Regular Brush** | Enables the painting of selected points using a brush rather than a point. |
| Brush |   |
| **Radius** | The radius of the Brush used for painting. |
| **Strength** | The strength of the brush (0.0 - 1.0). |
| **Falloff** | The amount of falloff to apply (0.0 - 1.0). |
| **Enable Brush Flow** | Enables "flow" painting where the paint is continually applied from the brush every tick. |
| **Ignore back-facing** | Whether back-facing triangles should be ignored when painting. |

#### Smooth

The **Smooth** tool enables you to blur or soften the contrast between painted cloth values.

![The smooth cloth painting properties](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2b5bcd22-6c26-44ba-b966-ec5c3fd88e0a/cloth-painting-smooth.png)

| Property | Description |
| --- | --- |
| View |   |
| **View Min** | When painting float/1D values, this is considered the zero or black point for painted values. |
| **View Max** | When painting float/1D values, this is considered the one or white point for painted values. |
| **Autoview Range** | When set, the view min and max values will be calculated from the values present in the currently editable mask. |
| Advanced Rollout |   |
| **Flip Normal** | Whether to flip normals on the mesh preview. |
| **Cull Backface** | Whether to cull back-facing triangles when rendering the mesh preview. |
| **Opacity** | The opacity value of the mesh preview enables you to see through the mesh. |
| Visualization |   |
| **Vertex Preview Size** | Size of vertex points drawn when mesh painting is active. |
| Tool Settings |   |
| **Strength** | The strength of the smoothing (blurring) effect when painting. |
| Brush |   |
| **Radius** | The radius of the Brush used for painting. |
| **Strength** | The strength of the brush (0.0 - 1.0). |
| **Falloff** | The amount of falloff to apply (0.0 - 1.0). |
| **Enable Brush Flow** | Enables "flow" painting where the paint is continually applied from the brush every tick. |
| **Ignore back-facing** | Whether back-facing triangles should be ignored when painting. |

#### Fill

The **Fill** tool enables you to replace areas with similar values with another value.

![The fill cloth painting properties](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4b2cc1b5-f64f-4500-8e1a-12ded1b22aab/cloth-painting-fill.png)

| Property | Description |
| --- | --- |
| View |   |
| **View Min** | When painting float/1D values, this is considered the zero or black point for painted values. |
| **View Max** | When painting float/1D values, this is considered the one or white point for painted values. |
| **Autoview Range** | When set, the view min and max values will be calculated from the values present in the currently editable mask. |
| Advanced Rollout |   |
| **Flip Normal** | Whether to flip normals on the mesh preview. |
| **Cull Backface** | Whether to cull back-facing triangles when rendering the mesh preview. |
| **Opacity** | The opacity value of the mesh preview enables you to see through the mesh. |
| Visualization |   |
| **Vertex Preview Size** | Size of vertex points drawn when mesh painting is active. |
| Tool Settings |   |
| **Threshold** | Threshold for fill operation that will keep filling until sampled vertices aren't within this range of the original vertex. |
| **Fill Value** | The value to fill all select vertices to. |
| Brush |   |
| **Radius** | The radius of the Brush used for painting. |
| **Strength** | The strength of the brush (0.0 - 1.0). |
| **Falloff** | The amount of falloff to apply (0.0 - 1.0). |
| **Enable Brush Flow** | Enables "flow" painting where the paint is continually applied from the brush every tick. |
| **Ignore back-facing** | Whether back-facing triangles should be ignored when painting. |