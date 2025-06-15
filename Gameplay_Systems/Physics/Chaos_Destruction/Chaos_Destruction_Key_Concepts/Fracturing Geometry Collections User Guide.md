# Fracturing Geometry Collections User Guide

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/fracturing-geometry-collections-user-guide](https://dev.epicgames.com/documentation/en-us/unreal-engine/fracturing-geometry-collections-user-guide)  
**Processed:** 2025-06-14 16:24:18

---

You can find similar information in video format in the Epic Developer Community site by watching the [Fracture and Clustering](https://dev.epicgames.com/community/learning/tutorials/k84m/chaos-destruction-fracture-and-clustering) tutorials.

The **Fracture Mode** is an editor mode that contains a wide variety of tools for creating, fracturing, and manipulating **Geometry Collections**. Geometry Collections are the asset type used by Chaos Destruction for simulating real-time fracturing in Unreal Engine.

The available fracturing tools provide users with a lot of control over how the Geometry Collection is fractured. This includes the number of fractured pieces and how they relate to each other (fracture hierarchy).

Each fracture tool uses a different method, or algorithm, to generate different fracture patterns. Each method comes with a variety of options to further customize the generated pattern, including adding randomization.

In this guide you will learn to use the various fracturing tools available in the Fracture Mode.

Before learning about the Fracture Mode, you should know how to create Geometry Collections from Actors in the Level. If you are not familiar with the process, refer to the [Geometry Collections User Guide](/documentation/en-us/unreal-engine/chaos-destruction-key-concepts-in-unreal-engine).

## Fracture the Geometry Collection

Before using the fracturing tools, create a Geometry Collection from a Static Mesh Actor in your Level and select it.

![Create a Geometry Collection from a Static Mesh Actor in your Level](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2c47ad94-0dbf-4f27-8721-3bfc74675f5d/destruction-fracture-6.png)

You can now access the available fracture tools under the **Fracture** section of the **Fracture Mode** panels. Each tool can be applied to the Geometry Collection as a whole, or to selected fractured pieces (individual bones) after fracturing.

Click the image for full size.

When applying a fracture method to the Geometry Collection, a new fracture level is created. This is reflected in the Geometry Collection's **Fracture Hierarchy** window.

Click the image for full size.

A Geometry Collection's fracture hierarchy resembles a tree structure. It contains a root bone with one or more child bones which make up the fractured pieces. Each child bone can, in turn, contain its own child bones.

The levels in the fracture hierarchy represent the structure of the tree, with four levels representing a tree-like structure with three branching levels of child bones.

![A 4 level fracture hierarchy](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c0b7ea53-99cf-47f4-aaec-85cbf7a5c84d/destruction-fracture-6c.png)

You can use different fracturing tools each time you fracture the Geometry Collection, creating different fracture patterns per level in the Fracture Hierarchy.

You can select multiple bones (fractured pieces) in the Geometry Collection by holding **CTRL** and selecting them directly in the viewport. You can also use the provided [selection tools](/documentation/en-us/unreal-engine/fracture-mode-selection-tools-user-guide) to quickly select a set of bones directly.

### Reset the Geometry Collection

After fracturing the Geometry Collection, you can reset it to its original state by clicking the **Reset** button under the **Generate** section. This sets the Geometry Collection to its original state when it was created without any applied fracturing. This can be helpful when trying different fracture methods until you find the configuration that provides the desired results.

![Click the Rest button to reset the Geometry Collection to its initial state](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c9982bbf-9500-46bc-bbd7-925f184462cb/destruction-fracture-11.png) ![You can reset a Geometry Collection to its original state by clicking the Reset button](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/94fdaea5-2367-495d-9d53-5c05536537b1/destruction-fracture-reset.gif)

### View Settings

The **View Settings** help you visualize what the Geometry Collection looks like after applying any fracture operation.

![Common view options](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/340a925f-377a-4f08-8155-da2be656b4b1/destruction-fracture-8.png)

| Option | Description |
| --- | --- |
| **Explode Amount** | Displays what the Geometry Collection will look like when it fractures during gameplay. A value of 1 will separate all bones and will show what a completely fractured Geometry Collection looks like. |
| **Hide UnSelected** | Hides the bones that are not currently selected in the Geometry Collection. This helps you focus on specific bones while applying a fracture method. |
| **Fracture Level** | Defines which fracture level to visualize. Selecting All will display the bones for all fracture levels. |

Click the image for full size.

![Changing the Explode values from 0 to 1](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bfc9e7d3-8e73-42b7-a5c1-60207c87d500/destruction-fracture-explode.gif)

### Common options included with most fracture methods

All fracture tools have these **Common Fracture** options:

![Common Fracture options for all fracture methods](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/69d6b3d4-bd08-470c-9386-74fdbdc5e3c9/destruction-fracture-10.png)

| Option | Description |
| --- | --- |
| **Random Seed** | This value is used to generate the random fracturing pattern over the Geometry Collection. A -1 means a random seed value will be used every time a new fracture operation is applied. Specifying a value generates a fracture pattern tied to that seed number, which when entered will always generate that same fracture pattern. |
| **Chance to Fracture** | Sets the chance that a bone is likely to be fractured during the fracture operation where 1 is equal to 100%, meaning all bones will be fractured. 0 is equal to 0% chance of any bone being fractured. |
| **Group Fracture** | Generates a fracture pattern across all selected meshes. |
| **Draw Sites** | Draws points in the center of the bones to be cut out by the fracture pattern. |
| **Draw Diagram** | Draws the fracture pattern diagram on top of the Geometry Collection. |
| **Grout** | Defines the amount of space to leave between cut piece. |

![A fractured Geometry Collection with grout](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d6a39035-5bda-4906-a02a-19774fb57245/destruction-fracture-12.png)

Most fracture methods share these **Noise** options:

-   **Amplitude**: Defines the size of the perlin noise displacement in centimeters. A value of 0 indicates that no noise will be used when generating the fracture pattern.
    
    ![Amplitude: 0](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/790ad5be-b738-4a7a-a183-438189399f2a/destruction-fracture-13a.png)
    
    ![Amplitude: 30](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4633eb2e-cda5-451e-9161-54738d888fd5/destruction-fracture-13b.png)
    
-   **Frequency**: Defines the period of the perlin noise. Smaller values produce a smoother noise pattern, and larger ones produce a rougher noise pattern.
    
    ![Amplitude: 5, Frequency: 0](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e8b67bbe-bbb1-4984-9e43-9fbeb482bd2c/destruction-fracture-14a.png)
    
    ![Amplitude: 5, Frequency: 200](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/82c0b673-e248-4684-93e7-45277f81e132/destruction-fracture-14b.png)
    
-   **Persistence**: Defines the persistence of the perlin noise layers. For each layer (octave) after the first, the **amplitude** of the perlin noise will be scaled by this factor.
    
    ![Amplitude: 5, Persistence: 0.5](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4889222c-e019-44be-9ecf-4bf87751e6d9/destruction-fracture-15a.png)
    
    ![Amplitude: 5, Persistence: 1](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/661504bf-851b-4970-86ae-22320f0ce04d/destruction-fracture-15b.png)
    
-   **Lacunarity**: Defines the lacunarity of the perlin noise layers. For each layer (octave) after the first, the **frequency** of the perlin noise will be scaled by this factor.
    
    ![Amplitude: 5, Lacunarity: 2](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/46fea472-9872-4e2a-be92-95ad95a85492/destruction-fracture-16a.png)
    
    ![Amplitude: 5, Lacunarity: 4](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/91bd75fb-095a-4423-bc84-f4e64b3d2f87/destruction-fracture-16b.png)
    
-   **Octave Number**: Defines the number of fractal layers (octaves) of perlin noise that will be applied to the fracture pattern. Each layer is additive, with Amplitude and Frequency scaled by Persistence and Lacunarity, respectively. Smaller values (1-2) will generate smooth patterns, while larger values will generate more craggy patterns.
    
    ![Amplitude: 5, Octave Number: 1](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1c628374-1445-444f-bf5f-4bb0796249b7/destruction-fracture-17a.png)
    
    ![Amplitude: 5, Octave Number: 8](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f32469be-a6a1-4fad-8152-7af7200499e2/destruction-fracture-17b.png)
    
-   **Point Spacing**: Distance (in centimeters) between vertices on cut surfaces where noise is added. Larger spacing between vertices results in more efficient meshes with fewer triangles. However, this also results in lower overall resolution to see the shape of the added noise.
    

## Use the Fracture Tools

Each Fracture tool has its own settings that provide relevant options to achieve the desired results.

### Uniform Fracture

The **Uniform** tool uses a Voronoi algorithm to generate the fracture pattern. Enter a minimum and maximum number of Voronoi sites (or number of fractured pieces) and the algorithm will choose a random value within the range.

![You can enter a minimum and maximum number of Voronoi sites](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/48effc3a-1ba3-41c7-859f-628793108b07/destruction-fracture-18.png)

In the fractured Geometry Collections below, the one on the left has the **Min** and **Max Voronoi Sites** set to **20**. This means that the fractured Geometry Collection will have 20 fractured pieces. The example on the right has the **Min** and **Max Voronoi Sites** set to **100**.

|   |   |
| --- | --- |
| ![Min / Max Voronoi Sites: 20](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e56963ab-a2ac-4bbe-8a1c-3c94b996aba5/destruction-fracture-19a.png) | ![Min / Max Voronoi Sites: 100](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/678a29ff-3053-41ce-b4fa-89f10a916950/destruction-fracture-19b.png) |
| 20 Voronoi Sites | 100 Voronoi Sites |
| *Click image for full size.* | *Click image for full size.* |

### Cluster Fracture

The **Cluster** fracture tool is an extension of the Uniform fracture method where both use a Voronoi algorithm when generating their fracture pattern. While the Uniform Voronoi method produces a relatively even distribution of sites, the Cluster method gathers its sites together into islands of close proximity, creating a more varied fracture pattern compared to the uniform method.

![Cluster fracture tool options](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cdb7ff97-422e-4e20-a752-65cfe1cb71a7/destruction-fracture-58.png)

| Option | Description |
| --- | --- |
| **Min Num Clusters** | Defines the minimum number of Voronoi clusters that will be created. |
| **Max Num Clusters** | Defines the maximum number of Voronoi clusters that will be created. |
| **Min Sites per Cluster** | Defines the minimum number of Voronoi sites per cluster. |
| **Max Sites per Cluster** | Defines the maximum number of Voronoi sites per cluster. |
| **Min Dist from Center** | Defines the minimum cluster radius. The cluster radius offset will be added to this value. |
| **Max Dist from Center** | Defines the maximum cluster radius (in centimeters). The Cluster Radius Offset will be added to this value. |
| **Cluster Radius Offset** | Defines the radius offset of the cluster (in centimeters) that is added to the minimum and maximum distance from the center. |

The examples below use the following Cluster settings as a starting point:

| Setting | Value |
| --- | --- |
| **Min Num Clusters** | 2 |
| **Max Num Clusters** | 2 |
| **Min Sites per Cluster** | 5 |
| **Max Sites per Cluster** | 5 |
| **Min Dist from Center** | 0.1 |
| **Max Dist from Center** | 0.1 |
| **Cluster Radius Offset** | 0 |

The following have also been set under the Common Fracture settings:

-   **Draw Sites**: Enabled
-   **Draw Diagram**: Disabled

In the example below you can see the difference between setting the **Min** / **Max Number of Clusters** from **2** to **5**.

![Min / Max Num Clusters: 2](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5c469d40-abf9-4eb9-8928-e89ba797907f/destruction-fracture-20a.png)

![Min / Max Num Clusters: 5](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8f71399d-d428-42c8-aa68-d387d0cd29dd/destruction-fracture-20b.png)

In the example below you can see the difference between setting the **Min** / **Max Sites per Cluster** from **5** to **10**.

![Min / Max Sites Per Cluster: 5](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9f87d068-c340-4a4a-a16c-19c3d8d44d1d/destruction-fracture-20a.png)

![Min / Max Sites Per Cluster: 10](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f0174fa1-f0db-4cad-8fdf-6096a2eb6c5c/destruction-fracture-21b.png)

In the example below you can see the difference between setting the **Min** / **Max Distance from Center** from **0.1** to **0.2**.

![Min / Max Dist from Center: 0.1](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0c8cbce2-56e0-4d83-a23d-07a54ef14b45/destruction-fracture-20a.png)

![Min / Max Dist from Center: 0.2](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/48fe0d80-7479-4252-82ed-9d68b8c08405/destruction-fracture-22b.png)

In the example below you can see the difference between setting the **Cluster Radius Offset** from **0** to **10**.

![Cluster Radius Offset: 0](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fb196415-e8d7-4a47-9b36-0ad04a34f684/destruction-fracture-20a.png)

![Cluster Radius Offset: 10](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/49d1f2c4-bc1b-4c9a-9759-25ba88a3195c/destruction-fracture-23b.png)

### Radial Fracture

The **Radial** fracture tool creates a distribution of Voronoi sites that operate from a center point and radiate outwards. The center position is controlled by manipulating the gizmo inside the Viewport.

![Radial fracture tool gizmo](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/07572b84-927f-4841-814c-0698521ca539/destruction-fracture-24.png)

If you want to place it at a specific location, you can enter the **Center** and **Normal** rotation (1) of the center point directly in the **Radial Voronoi** options. To activate those fields, **disable** the **Use Gizmo** checkbox (2) in the **Placement Controls** section.

![Radial Voronoi options](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/00be9a06-1419-4c2f-abe7-92db21335ab9/destruction-fracture-59.png)

The Radial fracture tool comes with the following options:

-   **Center**: Defines the center location of the generated fracture pattern. This option is only available if you disable the **Use Gizmo** checkbox.
    
-   **Normal**: Defines the normal rotation of the plane used to generate the fracture pattern. This option is only available if you disable the **Use Gizmo** checkbox.
    
-   **Radius**: Defines the radius of the pattern from the center location.
    
    ![Radius: 50](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a4f04498-6493-4665-8fb1-70b91d3871c9/destruction-fracture-27a.png)
    
    ![Radius: 100](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/226e4a7f-8987-424e-b6dc-283f04b285d4/destruction-fracture-27b.png)
    
-   **Angular Steps**: Defines the number of angular steps used to generate the fracture pattern. These steps subdivide the circumference of the diagram.
    
    ![Angular Steps: 5](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/32ab5fef-ca0f-427f-83d1-5f1fe4c78ede/destruction-fracture-27a.png)
    
    ![Angular Steps: 20](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/15f15b10-1a98-4e3f-90f6-470596be6f65/destruction-fracture-28b.png)
    
-   **Radial Steps**: Defines the number of radial steps used to generate the fracture pattern. This affects the number of times the pattern is divided outwards from the center.
    
    ![Radial Steps: 5](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1de45560-1f11-4703-9909-06d864e844fb/destruction-fracture-27a.png)
    
    ![Radial Steps: 20](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/be00a75b-4b57-4ee2-ab29-faac1aa465ca/destruction-fracture-29b.png)
    
-   **Angle Offset**: Defines an angular offset (in degrees) used for every radial step.
    
    ![Angle Offset: 0](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e9a48db7-74fc-48a0-b4db-a2a22ed5b25b/destruction-fracture-27a.png)
    
    ![Angle Offset: 35](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/92a30f10-e50a-4fdd-a427-50c783426845/destruction-fracture-30b.png)
    
-   **Variability**: Defines the amount to randomly space each generated Voronoi site (in centimeters).
    
    ![Variability: 0](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f515ff64-8aa5-4940-b04a-0aca4421c2df/destruction-fracture-27a.png)
    
    ![Variability: 5](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6368ea5d-f650-4b3b-9d60-ad76e2999455/destruction-fracture-31b.png)
    

### Planar Fracture

The **Planar** fracture tool is used to create a planar cut in the Geometry Collection. As cuts are created in the Geometry Collection, the gizmo resets to the centroid of your current selection. This is helpful if you are trying to make deliberate cuts as you select different Bones in the Viewport.

You can disable the gizmo resetting to the center of your current selection by disabling **Center on Selection** under the **Placement Controls** section.

![Disable the Center on Selection checkbox under the Placement Controls section](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d8b2a28d-2999-49d9-b205-7d0466209e82/destruction-fracture-32.png)

It's important to note that the plane used for each cut extends to infinity, meaning that even if the gizmo displays the plane at a specific size, the cut will extend in the plane's direction to cut the entire Geometry Collection.

You can also forgo using the gizmo by disabling **Use Gizmo** under the **Placement Controls** section.

![Disable the Use Gizmo checkbox under the Placement Controls section](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/66293e62-8cbe-445f-a3ad-e9eaa0c6dc04/destruction-fracture-33.png)

Disabling the gizmo enables you to set a **Number of Cuts** under the **Plan Cut** section. This results in a random number of cuts to the Geometry Collection.

![You can now enter a specific Number of Cuts under the Plane Cut section](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a50b2f79-9006-49e9-9886-fba19cec4366/destruction-fracture-34.png)

In the example below you can see the difference between setting the **Number of Cuts** from **1** to **10**.

![Number of Cuts: 1](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/376949d0-0656-4bcf-ab44-4640e17a38df/destruction-fracture-35a.png)

![Number of Cuts: 10](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ec3f9d3a-47bb-40dd-b3a4-743dee61b7dd/destruction-fracture-35b.png)

You can change the placement of these cuts by changing the **Random Seed** value under the **Common Fracture** section.

![Random Seed: 20](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/00e78121-0e89-4748-ab84-dc38d2c59b0b/destruction-fracture-36a.png)

![Random Seed: 40](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ad141ae2-ac3a-4a58-8157-19a7887de796/destruction-fracture-36b.png)

### Slice Fracture

The **Slice** fracture tool is an extension of the **Planar** fracture tool with the added ability to set the number of cuts along each axis. This allows for initial cuts to be aligned into columns and rows. Slices can also have random angles and offset variations applied to them.

| Option | Description |
| --- | --- |
| **Slices X** | Defines the number of slices along the X axis. |
| **Slices Y** | Defines the number of slices along the Y axis. |
| **Slices Z** | Defines the number of slices along the Z axis. |
| **Random Angle Variation** | Defines the maximum angle (in degrees) to randomly rotate each slicing plane. |
| **Random Offset Variation** | Defines the maximum distance (in centimeters) to randomly shift each slicing plane. |

In the example below you can see the difference between setting the **Random Angle Variation** from **0** to **35**.

![Random Angle Variation: 0](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c4bef8a7-3b2a-481d-91c2-5d712d266b07/destruction-fracture-37a.png)

![Random Angle Variation: 35](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fb330764-c8e9-44e9-abac-e803fc6eb171/destruction-fracture-37b.png)

In the example below you can see the difference between setting the **Random Offset Variation** from **0** to **50**.

![Random Offset Variation: 0](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/86e76e10-d988-4d14-a62f-d76ec1251694/destruction-fracture-37a.png)

![Random Offset Variation: 50](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/62f945b9-498b-4e54-a3d4-5284d00c6c99/destruction-fracture-38b.png)

### Brick Fracture

The Brick fracture tool is considered experimental and may receive significant changes in future versions of the engine.

The **Brick** fracture tool generates a customizable brick pattern. You can specify how the bricks are arranged and their size for when the pattern is applied to the Geometry Collection.

| Option | Description |
| --- | --- |
| **Bond** | Sets the brick bond pattern that determines how the bricks are arranged in the fracture pattern. You can select from: Stretcher, Stack, English, Header, and Flemish. |
| **Brick Length** | Defines the brick length in centimeters. |
| **Brick Height** | Defines the brick height in centimeters. |
| **Brick Depth** | Defines the brick depth in centimeters. |

The Example below shows the **Stretcher** bond method applied to the Geometry Collection.

![Example of the Stretcher bond method](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2be8e4e5-bdb0-4b7f-977c-d2bd6ac92c8f/destruction-fracture-39.png)

### Mesh Fracture

The **Mesh** fracture tool uses the shape of a Static Mesh to generate the fracture pattern. This is useful if you want to create very specific pattern shapes.

Drag a **Static Mesh** into the level and place it so it intersects the Geometry Collection.

![Drag a Static Mesh into the level](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d553c2d9-1d21-436f-8362-67658c37b35a/destruction-fracture-44.png)

Click **Mesh** and go to the **Mesh Cut** section in the **Fracture** panel.

![Go to the Mesh Cut section in the Fracture panel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6c8568f7-d6e7-45cb-8ade-8dee6fc6713c/destruction-fracture-45a.png)

Click the **Cutting Actor** dropdown. Select the Static Mesh actor you dragged into the level. Alternatively, you can click the Eye-Dropper button and click on the Static Mesh in the viewport.

![Select the Static Mesh actor from the list](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/45e887cc-bc43-4e3c-935d-633d3523dbbc/destruction-fracture-45.png)

Click **Fracture** to cut the Geometry Collection in the shape of the Cutting Actor. To see the results, select the **Cutting Actor** in the **Viewport** and move it.

![Move the Cutting Actor outside of the Geometry Collection to the see the results](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/62814ede-c4fa-4aa3-8236-20049443385e/destruction-fracture-cut-mesh.gif)

The following **Cut Distributions** are available with the tool:

![Cut Distribution options available](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6e0de11a-fa0e-4618-ba24-12eda52ad226/destruction-fracture-46a.png)

| Option | Description |
| --- | --- |
| **Single Cut** | Generates a single cut at the current location of the Cutting Actor. |
| **Uniform Random** | Scatters the Cutting Actor in a uniform random distribution around the Geometry Collection's bounding box. |
| **Grid** | Arranges the Cutting Actor in a regular grid pattern across the Geometry Collection. |

The following options are available for the **Uniform Random** Cut Distribution:

![Uniform Random Cut Distribution options](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/19fdc0cd-9bff-4f9d-ab4e-206e8c6c8122/destruction-fracture-46b.png)

| Option | Description |
| --- | --- |
| **Number to Scatter** | Defines the number of Actors to randomly scatter. |
| **Min Scale Factor** | Defines the minimum scale factor to apply to the cutting meshes. A random scale will be chosen between Min and Max. |
| **Max Scale Factor** | Defines the maximum scale factor to apply to the cutting meshes. A random scale will be chosen between Min and Max. |
| **Random Orientation** | Whether to randomly vary the orientation of the cutting actors. |
| **+/- Roll Range** | Defines the range that will be used to pick a random roll (rotation in X axis) for the cutting Actors. |
| **+/- Pitch Range** | Defines the range that will be used to pick a random pitch (rotation in Y axis) for the cutting Actors. |
| **+/- Yaw Range** | Defines the range that will be used to pick a random yaw (rotation in Z axis) for the cutting Actors. |

In the example below you can see the difference between setting the **Number to Scatter** from **5** to **10**.

![Number to Scatter: 5](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8743ba38-2fa0-440e-92ee-a212c83721ce/destruction-fracture-47a.png)

![Number to Scatter: 10](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5a480991-e76a-40f6-a507-3637a5aa1270/destruction-fracture-47b.png)

In the example below you can see the difference between **enabling** and **disabling** the **Random Orientation**.

![Random Orientation: Enabled](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/323b0c59-c662-407a-adb2-c3bb23759d3d/destruction-fracture-48a.png)

![Random Orientation: Disabled](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/614ce26d-ae2f-4236-a3d7-ec8c24dfdb5f/destruction-fracture-48b.png)

The following options are available for the Grid Cut Distribution:

![Grid Distribution options](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/647261e7-aba8-48cb-a17d-2f0b0c09d936/destruction-fracture-60.png)

| Option | Description |
| --- | --- |
| **Grid Width** | Defines the number of cutting meshes to add to the X-axis of the grid. |
| **Grid Depth** | Defines the number of cutting meshes to add to the Y-axis of the grid. |
| **Grid Height** | Defines the number of cutting meshes to add to the Z-axis of the grid. |
| **Variability** | Defines the magnitude of the random displacement of the cutting Actors. |
| **Min Scale Factor** | Defines the minimum scale factor to apply to the cutting Actors. |
| **Max Scale Factor** | Defines the maximum scale factor to apply to the cutting Actors. |
| **Random Orientation** | Whether to randomly vary the orientation of the cutting Actors. |

In the example below you can see the difference between **enabling** and **disabling** the **Random Orientation**.

![Random Orientation: Enabled](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2a7ef7a7-abb0-4b04-ba5c-a29342e76879/destruction-fracture-49a.png)

![Random Orientation: Disabled](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/70d88336-34be-42b3-82e4-4b714448605e/destruction-fracture-49b.png)

### Custom Fracture

The **Custom** fracture tool is the most extensive fracturing tool included with the Fracture Mode.

![Custom fracture tool options](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a221c6ee-2998-4299-b19a-df8d86441529/destruction-fracture-61.png)

| Option | Description |
| --- | --- |
| **Pattern** | Defines the pattern used to generate the Voronoi sites. |
| **Normal Offset** | Defines the offset value used for each vertex's normal direction. |
| **Variability** | Defines the amount to randomly offset each Voronoi site in centimeters. |
| **Sites to Add** | Defines the number of Voronoi sites to add to the pattern. |
| **Skip Fraction** | Defines the fraction of points that will not be fractured (skipped). |
| **Skip Mode** | Defines the method used for skipping the points that will not be fractured. |

With this tool, the **Fracture Diagram** is considered its own entity that can be moved relative to the Geometry Collection. This is useful when looking to create more customized fracture patterns.

|   |   |
| --- | --- |
| ![The gizmo is centered](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cdf69800-a4a5-4a71-9e46-c8e8d134cb94/destruction-fracture-50a.png) | ![The gizmo is moved to a corner](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/006e095b-dbbc-4563-b507-95dca4e19474/destruction-fracture-50b.png) |
| The gizmo is centered | The gizmo is moved to a corner |
| *Click image for full size.* | *Click image for full size.* |

To better visualize the fracture diagram, you can freeze positional data for the fracture sites. Under the **Common Fracture** section, enable **Draw Sites** and disable **Draw Diagram**.

![Enable the Draw Sites checkbox and disable the Draw Diagram checkbox](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a6f60462-d51c-4efa-9837-a791a8bd9986/destruction-fracture-51.png)

In addition, under the **Live Voronoi Sites** section. set the **Pattern** to **Centered** and set the **Variability** to **40**.

![Select the Centered Pattern and set the Variability to 40](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c0b733e5-1c12-4f8a-8002-2204cbd3cc60/destruction-fracture-52.png)

Doing this enables you to move the gizmo to a desired location on the Geometry Collection. In the Fracture Mode panel under the **Custom Voronoi** section, click the **Freeze Live Sites**.

![Click the Freeze Live Sites button under the Custom Voronoi section](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e9b9e3e7-45c9-4bef-91fc-f7f350a3201f/destruction-fracture-53.png)

|   |   |
| --- | --- |
| ![The gizmo is placed at the top left corner](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a8b72e10-9572-4b99-b566-43304f2a6bf0/destruction-fracture-54a.png) | ![The gizmo is moved revealing the frozen sites](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9c3d1e1f-1814-4bfe-a613-bea612d86ab2/destruction-fracture-54b.png) |
| The gizmo is placed at the top left corner | The gizmo is moved revealing the frozen sites |
| *Click image for full size.* | *Click image for full size.* |

You can continue this process to deliberately place sites on the Geometry Collection. Once you are ready, click **Fracture** to see the results of all the sites placed on the Geometry Collection.

![The fractured Geometry Collection](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c6f742f1-b6b2-4051-b915-8963f00fba1d/destruction-fracture-55.png)

Since the fracture diagram is separate from the Geometry Collection, you can make changes to the Geometry Collection without affecting the fracture itself.

For example, if you set the **Sites to Add** to **2000**, scale down the Geometry Collection to the shape of a column and click **Fracture**, you get the fracture pattern applied to the current shape of the Geometry Collection.

![Set the Sites to Add to 2000](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/89448c03-5086-4971-8448-aa75b84ac271/destruction-fracture-56a.png) ![Scale the Geometry Collection](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f1074c38-63cd-4516-be0b-bdc832e8d3ef/destruction-fracture-56b.png)

Rescale the Geometry Collection to its original size and notice how the fracture pattern is now stretched, resembling splinters of wood.

![Rescale the Geometry Collection to its original size](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cc3606e8-6819-400a-854d-8c3975139c06/destruction-fracture-57.png)

Because the fracture diagram isn't directly tied to the Geometry Collection, when you rescale the Geometry Collection, the fracture diagram remains the same. This means that you can create unique fracture patterns that fit a stylistic choice for your project, like this one with elongated fractures.