# Using Shape Grammar With PCG

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/using-shape-grammar-with-pcg-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/using-shape-grammar-with-pcg-in-unreal-engine)  
**Processed:** 2025-06-14 17:00:50

---

Unreal Engine’s **Procedural Content Generation Framework** provides technical artists and designers with a powerful set of tools for creating procedural content. In the context of procedural content generation, a **Shape Grammar** is a set of rules that defines how content should be generated and structured. In a grammar, user-defined symbols called **Modules** represent assets and are combined together in a string to create more complex structures.

A fence generator created using shape grammar.

## Important Concepts and Terms

-   **Modules**: User-defined symbols that represent assets. These can be letters or words. Modules are stored as an Attribute or can be hardcoded into a node
-   **Syntax**: The symbols and methods for combining modules in a string to form rules.

## Prerequisites

This documentation builds on concepts and information presented in the [Procedural Content Generation Overview](/documentation/en-us/unreal-engine/procedural-content-generation-overview).

## Grammar Syntax

PCG Grammar follows a specific syntax to combine modules using the following symbols:

-   You can use Modules by themselves or combine them with other modules. Here are some examples using modules with the symbols `A` and `B`:
    -   `A` means to place the module with the symbol `A`.
    -   `A, B` means to place modules `A` and `B` together.
    -   `*` means to place a module as many times as possible. For example, `A*` means to place module `A` as many times as possible.
    -   `+` means to place a module at least one time and then as many times as possible. For example, `A+` means to place module `A` at least once and then as many times as possible.
-   You can encapsulate Modules using square brackets `[]` to create module combinations:
    -   `[A, B]` combines modules `A` and `B`, and is placed together.
    -   `[A, B]*` means to place `A` and `B` together as many times as possible.
    -   `[A, B]+` means to place `A` and `B` together once and then as many times as possible.
    -   `[A, B]2` means to place `A` and `B` together twice.
-   Module combinations can be randomized using curly brackets and integers to assign probability:
    -   `<A, B, C>` means to place module `A` if there is enough room, otherwise place module `B`, and then module `C`.

For example, the fence generator shown in the image above uses grammar rules to determine where to place a gate, fence sections, and posts along a spline. It uses the following modules:

| **Symbol** | **Rule** |
| --- | --- |
| `A` | Place a regular fence section. |
| `G` | Place a gate. |
| `P` | Place a fence post. |
| `BL` | Place a fence with a large broken section. |
| `BS` | Place a fence with a small broken section. |

It uses the grammar `{[A,P]:2,[BL,P]:1,[BS,P]:1}*,[G,P], {[A,P]:2,[BL,P]:1,[BS,P]:1}*`

The syntax translates to the following:

| **Syntax** | **Meaning** |
| --- | --- |
| `{[A,P]:2,[BL,P]:1,[BS,P]:1}*` | Randomly chooses between placing a fence section with a post, a large broken fence section with a post, or a small broken fence section with a post using the weighted values shown in the syntax. Fill until placing the gate at the midpoint of the spline. |
| `[G,P]` | Places a gate and a fence post. |
| `{[A,P]:2,[BL,P]:1,[BS,P]:1}*` | Randomly chooses between placing a fence section with a post, a large broken fence section with a post, or a small broken fence section with a post using the weighted values shown in the syntax. Fill until reaching the end of the spline. |

## PCG Grammar Nodes

PCG Grammar uses several graph nodes that define the grammar and shape of your system.

### Subdivision Nodes

#### Spline To Segment

The **Spline to Segment** node breaks a spline into segments of point data. Each segment is defined by two connected control points.

This node has the following options:

| **Option** | **Description** |
| --- | --- |
| **Extract Tangents** | Extracts the tangent between the previous segment and the next segment. |
| **Extract Angles** | Extracts the angle between the previous segment and the next segment. The angle will be zero at the extremity for non-closed splines. |
| **Extract Connectivity Info** | Sets the index of the previous and next segment to keep information on connectivity. |
| **Extract Clockwise Info** | Outputs a global attribute that tracks if the spline points are clockwise or counter clockwise. |

#### Duplicate Cross-Section

The **Duplicate Cross-Section** node duplicates a spline along an extrusion vector following the rules of the selected grammar.

This node has the following options:

| **Option** | **Description** |
| --- | --- |
| **Extrude Vector as Attribute** | Determines if the extrude vector is taken from the input spline as an attribute or fixed in the settings. |
| **Extrude Vector** | Defines the extrude vector. |
| **Module Info as Input** | Takes in module info as an input, if checked. |
| **Modules Info** | Defines an array of modules to use for subdivision. |
| **Seed Attribute** | Defines the attribute that is used to drive seed selection. Uses the Seed, if no attribute is provided. |
| **Seed** | Defines the seed value used to drive random generation. |
| **Extra Outputs Attribute** | Defines the specific names of the output attributes. |
| **Grammar As Attribute** | Reads the grammar as an input attribute rather than directly from the settings, if checked. |
| **Grammar String** | Defines the grammar string used for generation. |

#### Subdivide Segment

The **Subdivide Segment** node subdivides segments based on the selected grammar and module information.

This node has the following options:

| **Option** | **Description** |
| --- | --- |
| **Subdivision Axis** | Defines the subdivide direction in point local space.This dropdown menu contains options to use the X, Y, or Z axis. |
| **Flip Axis as Attribute** | Uses an attribute to define whether the axis should be flipped, if checked. |
| **Should Flip Axis** | Defines whether the axis should be flipped, if checked. |
| **Accept Incomplete Subdivision** | Determines if it is valid if a grammar does not fill the segment. Can be used to address the “Spline has an incomplete subdivision” warning message. |
| **Seed Attribute** | Defines the attribute that is used to drive seed selection. Uses the Seed, if no attribute is provided. |
| **Seed** | Defines the seed value used to drive random generation. |
| **Extra Outputs Attribute** | Defines the specific names of the output attributes. |
| **Grammar As Attribute** | Reads the grammar as an input attribute rather than directly from the settings, if checked. |
| **Grammar String** | Defines the grammar string used for generation. |

#### Subdivide Spline

The **Subdivide Spline** node subdivides a spline based on the selected grammar and module information. Modules are placed so that both ends fall on the spline.

Tight corners might be underestimated and produce incorrect results.

This node has the following options:

| **Option** | **Description** |
| --- | --- |
| **Accept Incomplete Subdivision** | Determines if it is valid if a grammar does not fill the segment. Use this to address the “Spline has an incomplete subdivision” warning message. |
| **Module Height as Attribute** | Defines the module Z height using an attribute. |
| **Module Height** | Defines the module Z height. |
| **Module Info as Input** | Takes in module info as an input, if checked. |
| **Seed Attribute** | Defines the attribute that is used to drive seed selection. Uses the Seed, if no attribute is provided. |
| **Seed** | Defines the seed value used to drive random generation. |
| **Extra Outputs Attribute** | Defines the specific names of the output attributes. |
| **Grammar As Attribute** | Reads the grammar as an input attribute rather than directly from the settings, if checked. |
| **Grammar String** | Defines the grammar string used for generation. |

### Shape Definition Nodes

Shape definition nodes define the contours of your generated shapes.

#### Clean Spline

The **Clean Spline** node removes any extraneous control points from linear splines based on a user defined threshold. These points can be either too close in proximity (co-location) or be unnecessary to defining the spline (collinear).

This node has the following options:

| **Option** | **Description** |
| --- | --- |
| **Fuse Colocated Control Points** | Fuses control points that share the same location within a defined distance threshold. |
| **Colocation Distance Threshold** | Defines the distance threshold for fusing colocated control points. |
| **Use Spline Local Space** | Uses spline local space for distance calculations, if checked. |
| **Fuse Mode** | 
Controls how two colocated control points are fused. This dropdown contains the following options:

-   **Keep First**: Fuses the points at the location of the first point.
-   **Keep Second**: Fuses the points at the location of the second point.
-   **Merge**: Merges the points at a location halfway between the first and second points.
-   **Auto**: Uses the best solution. Fuses post most often at the location of the second point but will use the location of the first point if it would alter the length of the spline.



 |
| **Remove Collinear Control Points** | Removes unnecessary points along linear sections of the spline that have no effect on the final result. |
| **Collinear Angle Threshold** | Defines the angle threshold used to determine if points are collinear. |
| **Use Radians** | Uses radians instead of degrees when checking the angle threshold, if checked. |

#### Spline Direction

The **Spline Direction** node reverses the order of the control points, and their arrive and leave tangents.

This node has the following options:

| **Option** | **Description** |
| --- | --- |
| **Operation** | 
Defines the operation the node will perform. This dropdown contains the following options:

-   **Reverse**: Reverses the spline points regardless of their initial orientation.
-   **Force Clockwise**: Reverses the spline points if they are counter clockwise.
-   **Force Counter Clockwise**: Reverses the spline points if they are clockwise.



 |

This can be a destructive operation with spline components, as some of the user data that defines the spline’s curves may be lost in the process.

#### Primitive Cross-Section

The **Primitive Cross-Section** node assists with transforming a set of primitive cross-sections into a spline. This node requires the **Procedural Content Generation Framework (PCG) Geometry Script Interop** plugin.

This node is currently Experimental.

This node has the following options:

| **Option** | **Description** |
| --- | --- |
| **Slice Direction** | Defines the direction that slices will occur. Begins at the minimum vertex along the defined direction vector. |
| **Extrusion Vector Attribute** | Defines the name of the attribute that is populated with each cross-section extrusion vector. This vector contains length and direction data. |
| **Minimum Coplanar Vertices** | Defines the number of vertices that must be coplanar to be considered a tier feature. |
| **Tier Merging Threshold** | Defines the distance in centimeters from the previous tier that a new tier will be culled. |
| **Min Area Culling Threshold** | Defines the minimum that a new tier must have or it will be culled. |
| **Remove Redundant Sections** | Removes unnecessary tiers if it will not affect the contour of the cross-section. |
| M**ax Mesh Vertex Count** | Defines a max vertex count to avoid creating overly complex meshes. |

### Generic Grammar Nodes

#### Select Grammar

The **Select Grammar** Node selects a grammar string based on a user defined key value and a set of criteria. For each point in a point data, the node compares each criteria in sequential order until the criteria is satisfied or a select criteria is found.

This node has the following options:

| **Option** | **Description** |
| --- | --- |
| **Key as Attribute** | Selects the key using an attribute. If Key as Attribute is unchecked, a single key defined using the **Key** option is used. |
| **Key Attribute** | Defines the attribute to use as the key. This option is set to **None** if **Key as Attribute** is unchecked. |
| **Compared Value Attribute** | Defines the attribute to compare to the key value. Evaluates each value numerically. The default value is `$ScaledLocalBounds.X`, which is the size of the bounds of the point scaled by the point scale on the X axis. |
| **Criteria as Input** | Defines the criteria to compare against using an attribute input. |
| **Criteria** | Selects and defines the comparison criteria that is used to compare the key and compare value attributes. |
| **Copy Key for Unselected Grammar** | Passes through the key value for a given point, if no grammar is selected. |
| **Output Grammar Attribute** | Defines the name of the attribute that the selected grammar is written to. |
| **Remap Criteria Attribute Names** | Defines the specific attribute names that are expected for the comparison criteria, if checked. Available only when Criteria **as Input** is checked. |

#### Print Grammar

The **Print Grammar** node outputs a more detailed description of the current grammar string to the log. This is a utility node that helps validate grammar strings by breaking them down into a more readable format to show how the string is being interpreted.

This node has the following options:

| **Option** | **Description** |
| --- | --- |
| **Grammar** | Defines the grammar that will be validated in detail and output to the log. |