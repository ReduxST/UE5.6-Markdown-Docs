# Procedural Content Generation Framework Node Reference

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/procedural-content-generation-framework-node-reference-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/procedural-content-generation-framework-node-reference-in-unreal-engine)  
**Processed:** 2025-06-14 16:44:22

---

The Procedural Content Generation (PCG) Framework utilizes the Procedural Node Graph to generate procedural content both in the Editor and at Runtime. Using a format similar to the Material Editor, spatial data flows into the graph from a PCG Component in your Level and is used to generate points. The points are filtered and modified through a series of nodes, which are listed below:

## Blueprint

| Node | Description |
| --- | --- |
| 
**Execute Blueprint**

 | 

Executes a specified custom Blueprint Class with the Execute or Execute With Context method on a clean instance of a Blueprint Class deriving from `UPCGBlueprintElement`.

 |

## Control Flow

| Node | Description |
| --- | --- |
| 
**Branch**

 | 

Selects one of two outputs based on a Boolean attribute. This allows the provided data to pass to either the "Output A" or "Output B" based on a boolean value that can be overridden in the graph. Controls execution flow tthrough the graph so that depending on specific circumstances (presence or absence of something, platform running, and so on) some different parts of a graph are executed. The branch that does not have any data is culled from execution in order to perform more efficiently.

 |
| 

**Select**

 | 

Selects one of two inputs to be forwarded to a single output based on a Boolean attribute. This is used to control execution flow in the graph so that depending on specific circumstances (presence or absence of something, platform running, and so on) some different parts of a graph are executed.

Select branches (inputs) are not culled from execution at this point but may be in a future release.



 |
| 

**Select (Multi)**

 | 

Multi-input version of the Select node, which can be made to be an integer, enum, or string-based. This node is especially useful to make it more obvious in the graph when picking different data. It removes some of the "magic number" impression, or in cases where there are more than two inputs to select from.

 |
| 

**Switch**

 | 

Multi-output version of the Branch node, which can be made to pick an integer, string, or enum. This node is especially useful to make it more obvious in the graph when picking different data. It removes some of the "magic number" impression, or in cases where there are more than two inputs to select from.

 |

## Debug

| Node | Description |
| --- | --- |
| 
**Debug**

 | 

Debugs the previous node in the graph but is not transient. This works the same as enabling debug on the nodes that provide their data to this node. This is useful to have a permanent debug point in a grpah since it is not transient even though the debug parameters are.

It does not execute in non-editor builds.



 |
| 

**Sanity Check Point Data**

 | 

Validates that the input data point(s) have a value in the given range; outside of the range this node logs an error and cancels the generation. This is useful when trying to validate assumptions in a graph but shouldn't be considered a good building block in graphs.

 |
| 

**Print String**

 | 

Prints a message that outputs a prefixed message optionally to the log, node, and screen. This acts as a passthrough node in the shipping build, meaning that it will not output the prefixed message at this point. This node is useful for debugging and validating assumptions in a graph, such as on dead branches following control flow nodes.

 |

## Density

| Node | Description |
| --- | --- |
| 
**Curve Remap Density**

 | 

Remaps the density of each point in the point data to another density value according to the provided curve. This can be used to dovetail densities in some situations to have nicer gradients or do more complex processing downstream. Since this relies on a separate data object, it is more easily changed from outside of PCG.

Final Density = Curve Remap(Input Density)

 |
| 

**Density Remap**

 | 

Applies a linear transform to the point densities. Optionally, this can be set to not affect values outside the input range.

D' = (Out\_Max - Out\_Min) \* (D - In\_min) / (In\_max - In\_min) + Out\_Min

 |
| 

**Distance to Density**

 | 

Sets the point density according to the distance of each point from a reference point. This is used to compute density gradients against a target point, allowing for finer grained control.

For most intents and purposes, this node is superseded by the native Distance node that is more generalize and significantly more efficient.



 |

## Filter

| Node | Description |
| --- | --- |
| 
**Attribute Filter**

 | 

General purpose filtering on attributes and properties. It works on both Point Data and Attributes Sets. This is used to separate data to either cull points or allow separate processing to introduce variation. This filter can either be a constant, another spatial data (when the input is a spatial data, on which you can filter as-if sampling the same point or from the ToPoint version), or an Attribute Set.

 |
| 

**Attribute Filter Range**

 | 

Range-based version of the Attribute Filter where input data (Point Data or Attribute Set) is separated into what's inside the range and what's outside the range. This is used to separate data to either cull points or allow separate processing to introduce variation. This filter can either be a constant, another spatial data (when the input is a spatial data, on which you can filter as-if sampling the same point or from the ToPoint version), or an Attribute Set.

 |
| 

**Density Filter**

 | 

Filters points based on density and the provided filter ranges.

This node is fully superceded by the Attribute Filter node, but is more specialized and more efficient than it is. This node should be used when performance is a major concern or when it makes it easier to convey intent in the graph this way.



 |
| 

**Discard Points on Irregular Surface**

 | 

Tests multiple points around given source points to determine if they are on the same plane. This is an example of using a PCG Subgraph and is used in the Electric Dreams demo.

 |
| 

**Filter Data By Attribute**

 | 

Separates data (not contents) based on whether they have a specified metadata attribute, with the data having the attribute in the Inside Filter output and the rest in the Outside Filter output. This is used to prevent errors and warning on subgraph sections that rely on the existence of certain attributes that might not be guaranteed to exists in some circumstances, such as when getting data from actors in a world.

 |
| 

**Filter Data by Index**

 | 

Separates data (not contents) based on their index and the filter provided in the settings. This filter is built from a string that contains individual indices or ranges separated by commas. Negative numbers are supported similar to how Python ranges work. For example, on an array of size 10 (values between 0 and 9), the selected indices 0, 2, 4:5, 7:-1 will include the indices 0, 2, 4, 7, and 8. This is used when there are very well known parameters in your graph that precisely allows some data, but it is likely that the first or last indices will generally be the most commonly selected indices.

 |
| 

**Filter Data By Tag**

 | 

Separates data (not contents) according to their tags. You can specify a comma-separated list of Tags to filter by. This is useful when getting data from the world and building relationships between data in PCG. For example, the Get Actor Data node could return all actors with a given tag and then some of these would be inclusions and exclusions. Using the Fitler Data By Tag node then separates the data and passes it to where it woul dbe useful in the graph.

 |
| 

**Filter Data By Type**

 | 

Separates data (not contents) based on their type, as dictated by the Target Type. Note that it is possible to have the Outside Filter pin show up in the settings. This node is used in the graph as a way of automatically filtering but there are other instances where it might be useful to determine behavior in the graph based on the data types provided. This would be allowed here in conjunction with the Count Data node.

 |
| 

**Point Filter**

 | 

Applies a per-point filter on the In point data. The filter can be either a constant, spatial data (on which you can filter as-if sampling the same point or from the ToPoint version), or an Attribute Set.

 |
| 

**Point Filter Range**

 | 

Applies a range-based filter on point data.

 |
| 

**Self Pruning**

 | 

Removes intersections between points in the same point data, prioritizing data based on the settings (Large to Small, etc.). Points with a similar radius can be randomly selected using randomized pruning to prevent patterns from emerging.

 |

## Generic

| Node | Description |
| --- | --- |
| 
**Add Tags**

 | 

Adds tags on the provided data based on comma-separated lists of tags. This is used to improve data tracking in more complex graphs in conjunction with the Filter Data By Tag node.

 |
| 

**Apply On Actor**

 | 

Sets properties on an actor, driven by the properties provided in an Attribute Set. It can also be used to call parameter-less functions on an actor, after properties are set (if any are). If no actor is provided, then this is applied on the owner of the PCG component ( this is a PCG Partition actor in a partitioned graph). This has similar usage to the Spawned Actor Property Override Descriptions in the Spawn Actor node. This Apply On Actor node should be used carefully since changes on an actor are not revertable by PCG. An example utilizing this node is to push some data computed from PCG onto some actors that might or might not be created from PCG in a flexible manner, such as automating some data update process directly from PCG.

 |
| 

**Delete Tags**

 | 

Removes tags from the input data, either for all mathces against a comma-separated list or if a tag is not in the provided list. This node can be used to normalize tags on data to process downstream and is more of an organizational node. However, it could be used as a way to mark data as being processed in a workflow where the same processing could be done multiple times.

 |
| 

**Gather**

 | 

Takes all inputs and generates a single collection holding all the input data. Used mainly for organization.

Contains a **Dependency Only** pin to sequence execution in cases where it is important (such as World Ray Hit Query vs. content spawned in a given graph). Note that all data provided to this pin will not be passed to the output.

 |
| 

**Get Data Count**

 | 

Returns an Attribute Set containing the number of data passed to the input pin. Note that this does not ignore empty point data. This can be used in conjunction with logical operations or as a boolean directly in the branching nodes to do some processing only when needed.

 |
| 

**Get Entries Count**

 | 

Returns the number of entries in an Attribute Set. This is useful when used in conjunction with the Get Attribute Set From Index and Loop nodes to have fine-grained control on what happens in a subgraph.

 |
| 

**Get Loop Index**

 | 

Returns an attribute set containing the current loop index if this is executed inside of a loop subgraph. This returns only the index of the direct subgraph and does not go up the graph hierarchy to find the nearest loop. This can be used to compute per-iteration data for recursive patterns or for logging purposes.

 |
| 

**Proxy**

 | 

Placeholder node replacement that allows dynamic override during execution of the graph. A Prototype (default value) can be set to show the proper node pines, but the node being run can be driven through parameter overrides. This is especially usefull to allow some per-instance controls from pre-built nodes, such as exposing specific noise types.

 |
| 

**Replace Tags**

 | 

Replaces tags on the input data by their matching counterpart. This node supports replacing tags in either 1:1, N:1, or N:N relationships using comma-separated lists.

 |
| 

**Sort Attributes**

 | 

Sorts the input data (Point Data and Attribute Set) by a specified attribute in ascending or descending order. This node can be used to order data in such a way to make it predictable for downstream nodes. For example, you could order some values by priority then act on this downstream.

 |
| 

**Sort Points**

 | 

Alias for Sort Attributes.

 |

## Helpers

| Node | Description |
| --- | --- |
| 
**Spatial Data Bounds To Point**

 | 

Computes the bounds and returns a single point representing the bounds of a spatial data. This is useful for display purposes or to have a simpler representation of data that can be merged with another of the same type.

 |

## Hierarchical Generation

| Node | Description |
| --- | --- |
| 
**Grid Size**

 | 

Specifies at which grid size to execute downstream nodes. Used with [Hierarchical Generation](building-virtual-worlds/procedural-generation/pcg-development-guides/using-pcg-generation-modes).

 |

## Input Output

| Node | Description |
| --- | --- |
| 
**Data Table Row to Attribute Set**

 | 

Extracts a single row from a data table to an Attribute Set. This is a single-row access to a data table in a less flexible manner than what the Load Data Table enable, but can still be useful.

 |
| 

**Load Alembic File**

 | 

Loads an Alembic file into PCG point data. This node is used to import and process an Alembic file to a Point Data format. While there are more than just points in Alembic files, the other types are not currently supported by this node. This node is not intended to be run in a graph being iterated on. Instead, use EUW that does this conversion and stores Alembic to a PCG asset once in order to make this more efficient.

Requires the **Procedural Content Generation (PCG) External Data Interop** plugin.

 |
| 

**Load Data Table**

 | 

Loads a UDataTable into PCG point data. This node can either import the table as Point Data or as an Attribute Set. This is extremely useful to make PCG data-driven without having to look at the PCG graph. Changes in the Data Table are propagated to PCG when the file is saved.

 |
| 

**Load PCG Data Asset**

 | 

Loads, either synchronously or asynchronously, a PCG Data Asset object and passes its data downstream in the graph.

 |

## Metadata

| Node | Description |
| --- | --- |
| 
**Add Attribute**

 | 

Adds an attribute to point data or an attribute set.

 |
| 

**Attribute Noise**

 | 

Computes new values for a target attribute for each point in a set of point data. This works with Point Data and Attribute Sets. The value will depend on the selected input attribute, **Mode**, **Noise Min**, and **Noise Max**. This is useful to add variation on contiuous parameters.

 |
| 

**Attribute Partition**

 | 

Splites the input data (Point Data or Attribute Set, or other spatial data to be converted to Point Data if required) in a partition according to the attributes selected. All elements with the same values for each of the selected attributes ends up in the same output data. This is helpful to separate data going into a Loop node if there is processing to be done in a certain situation for the same attribute value, such as sampling points on a mesh using the Mesh Sampler and propagating these points through a Copy Points on the "right" points.

 |
| 

**Attribute Rename**

 | 

Renames an existing attribute. This node is used when downstream processing needs specific attributes to exist. This is useful to pass data down to subgraphs.

 |
| 

**Attribute Select**

 | 

Computes the **Min**, **Max**, or **Median** on a selected **Axis**. Note that this is analogous to computing a dot product with an axis.

 |
| 

**Attribute String Op**

 | 

Performs String-related attribute operations, such as appending strings. This node is used in conjunction with the Print String node and the Create Target Actor nodes.

 |
| 

**Break Transform Attribute**

 | 

Breaks down a Transform attribute into its components: **Translation**, **Rotation**, and **Scale**.

 |
| 

**Break Vector Attribute**

 | 

Breaks down a Vector attribute into its components: **X**, **Y**, **Z**, and **W**.

 |
| 

**Copy Attribute**

 | 

Copies an attribute either from the **Attribute** pin or from the input itself, to a new point data. This node is useful in the sense that it allows you to move some values to other attributes, performance more complex operations and ultimately write back to the original attribute, if needed.

 |
| 

**Create Attribute**

 | 

Creates an Attribute Set with a single attribute.

 |
| 

**Delete Attributes**

 | 

Filters (keep or remove) comma-separated attributes from an Attribute Set or Spatial Data. This node is used to remove attributes that aren't useful downstream. In some caeses, it might worthwhile to do so to not pollute output data with temporary attributes, but also because some operations are more costly on a per-attribute basis, such as Copy Points, and depends on the settings being used.

 |
| 

**Density Noise**

 | 

Alias for Attribute Noise.

 |
| 

**Filter Attributes by Name**

 | 

Filters (keep or remove) comma-separated attributes from an Attribute Set or Spatial Data. This is an alias for Delete Attributes.

 |
| 

**Get Attribute from Point Index**

 | 

Retrieves a single point from point data and its attributes in a separate Attribute Set. This node is often used inside of loops on partitioned data to retrieve the common attribute value easily.

 |
| 

**Make Transform Attribute**

 | 

Creates a Transform attribute from three provided attributes: **Translation**, **Rotation**, and **Scale**.

 |
| 

**Make Vector Attribute**

 | 

Creates a Vector attribute from two to four attributes based on **Output Type**.

 |
| 

**Match And Set Attributes**

 | 

Selects an entry in the provided Attribute Set table (Match Data) and copies its values to the input data (Point Data or Attribute Set). This supercedes the Point Match and Set node.

Selection is driven by matching an attribute (Match Attributes) on the input data (Input Attribute) with an attribute on the Match Data (Match Attribute) so that values are copied only from an entry in the Match Data if their values coincide.

When data is not matching an attribute, all entries in the Match Data are considered valid matches. Additionally, there is an option to keep or discard entries that do not match anything from the Match Data.

In cases where there are multiple potential matches in the Match Data, it is possible to weight them (Match Weight Attribute) or one will be selected randomly. It is possible to correlate a \[0 - 1\] value from the input data to the normalized weight from the Match Data using the Use Input Weight Attribute and Input Weight Attribute fields. This allows to drive random selection from a previously computed spatial noise.

Finally, when matching attributes, it is possible to match against the nearest value if there are no equal values to it. It is also possible to have a maximum distance threshold at which to match or not, but this is limited to continuous value types that have a reasonable distance metric.

Note that the distance on vectors is the euclidean distance in engine units, the distance on rotators is in degrees, and distance on quaternions is in radians.

Any attributes used during the match operation are not propagated to the output data, so the matching attribute and/or the weight attributes from the Match Data will not be copied to the output.

This node is very flexible to inject data onto points and attribute sets and allows to build complex data sets by its ability to match values. It is a cornerstone in data-driven graphs where a node could load a list of data-tables or data-assets, then copy the proper data to points in a single operation easily.

 |
| 

**Merge Attributes**

 | 

Merges multiple attribute sets (in order of connection) together. Attributes that are not common are set to their respective default value (as of attribute creation) in the entries that did not have these attributes.

 |
| 

**Point Match and Set**

 | 

Using the **Match And Set Type** option, finds a match for each point based on the selection criteria, then applies the value to an attribute.

A common use case is to select meshes to be used downstream in a **Static Mesh Spawner node** with the **By Attribute** selector.

 |
| 

**Transfer Attribute**

 | 

Sets an attribute from an object of the same type (spatial to spatial or points to points) with the same data set size. This is useful if some processing is done on the same data set but only a subset of the attributes needs to persist, or when there is a 1:1 relationship that exists in the data.

 |

### Attribute Bitwise Op

| Node | Description |
| --- | --- |
| 
**And**

 | 

Computes the result of the bitwise AND between two attributes.

 |
| 

**Not**

 | 

Computes the result of the bitwise NOT between two attributes.

 |
| 

**Or**

 | 

Computes the result of the bitwise OR between two attributes.

 |
| 

**Xor**

 | 

Computes the result of the bitwise XOR (Exclusive OR) between two attributes.

 |

### Attribute Boolean Op

| Node | Description |
| --- | --- |
| 
**And**

 | 

Computes the result of the boolean AND between two attributes.

 |
| 

**Not**

 | 

Computes the result of the boolean NOT between two attributes.

 |
| 

**Or**

 | 

Computes the result of the boolean OR between two attributes.

 |
| 

**Xor**

 | 

Computes the result of the boolean XOR (Exclusive OR) between two attributes.

 |

### Attribute Compare Op

| Node | Description |
| --- | --- |
| 
**Equal**

 | 

Writes the comparison Equal To result between two attributes to a boolean attribute.

 |
| 

**Greater**

 | 

Writes the comparison Greater Than result between two attributes to a boolean attribute.

 |
| 

**Greater or Equal**

 | 

Writes the comparison Greater Than Or Equal To result between two attributes to a boolean attribute.

 |
| 

**Less**

 | 

Writes the comparison Less Than result between two attributes to a boolean attribute.

 |
| 

**Less or Equal**

 | 

Writes the comparison Less Than or Equal To result between two attributes to a boolean attribute.

 |
| 

**Not Equal**

 | 

Writes the comparison Not Equal result between two attributes to a boolean attribute.

 |

### Attribute Maths Op

| Node | Description |
| --- | --- |
| 
**Abs**

 | 

Computes the value of the Absolute Value mathematical operation. Converts an input attribute value into a positive value and writes the result to an attribute.

 |
| 

**Add**

 | 

Computes the value of the Add mathematical operation. Takes two input values, adds them together, and writes the result to an attribute.

 |
| 

**Ceil**

 | 

Computes the value of the Ceiling mathematical operation. Takes an input value and rounds it up to the next integer.

 |
| 

**Clamp**

 | 

Computes the value of the Clamp mathematical operation. Takes in input values and constrains them to a specific range.

 |
| 

**Clamp Max**

 | 

Provides a maximum value for the Clamp mathematical operation.

 |
| 

**Clamp Min**

 | 

Provides a minimum value for the Clamp mathematical operation.

 |
| 

**Divide**

 | 

Computes the value of the Divide mathematical operation. Takes in two inputs, divides the first input by the second, and writes the result to an attribute.

 |
| 

**Floor**

 | 

Computes the value of the Floor mathematical operation. Takes in an input value, rounds it down to the nearest integer, and writes the result to an attribute.

 |
| 

**Frac**

 | 

Computes the value of the Frac mathematical operation. Takes in an input value and returns the fractional portion of that value.

For example, for an input value X, the result is X minus the Floor of X. The output value ranges from zero to one, inclusive on the low end, exclusive on the high end.

 |
| 

**Lerp**

 | 

Computes the value of the Linear Interpolate mathematical operation. This expression draws a line between two points and uses a third Ratio value to determine the value of a point along that line. It then writes this value to an attribute.

 |
| 

**Max**

 | 

Computes the value of the Max mathematical operation on attribute(s) and writes the result to an attribute. This operation takes in two input values and outputs the higher of the two.

 |
| 

**Min**

 | 

Computes the value of the Min mathematical operation on attribute(s) and writes the result to an attribute. This operation takes in two input values and outputs the lower of the two.

 |
| 

**Modulo**

 | 

Computes the value of the Modulo mathematical operation. Takes in two input values and divides the first by the second. It then returns the remainder and writes that as an attribute.

 |
| 

**Multiply**

 | 

Computes the value of the Multiply mathematical operation. Takes in two input values, multiplies them, and writes the result to an attribute.

 |
| 

**One Minus**

 | 

Computes the value of the One Minus mathematical operation on an attribute and writes the result to an attribute. This expression takes in an input value X and outputs 1-X and writes the result as an attribute.

 |
| 

**Pow**

 | 

Computes the value of the Power mathematical operation. This expression takes in two values: a base and an exponent. It raises the base value to the exponent power and outputs the result as an attribute.

 |
| 

**Round**

 | 

Computes the value of the Round mathematical operation and writes the result to an attribute. This expression takes in an input value and rounds it to the nearest whole number.

 |
| 

**Set**

 | 

Sets the output attribute to the value of the provided attributes.

 |
| 

**Sign**

 | 

Computes the value of the Sign mathematical operation and writes the result to an attribute. Evaluates an input value and indicates whether it is positive, negative, or exactly zero.

-   If the input is negative, this node outputs -1.
    
-   If the input is exactly 0, this node outputs 0.
    
-   If the input is positive, this node outputs 1.
    

 |
| 

**Sqrt**

 | 

Computes the value of the Square Root mathematical operation on an input and writes the result to an attribute.

 |
| 

**Subtract**

 | 

Computes the value of the Subtract mathematical operation. This expression takes in two inputs and subtracts the second input from the first.

 |
| 

**Truncate**

 | 

Computes the value of the Truncate mathematical operation and writes the result to an attribute. This expression truncates a value by discarding the fractional part while leaving the whole number. For example, a value of 1.4 is truncated to 1.

 |

### Attribute Reduce Op

| Node | Description |
| --- | --- |
| 
**Average**

 | 

Gathers ensemble information on which the graph could operate on. For example, you could find the average position to use as a good pivot to scale against for all points in a Point Data.

 |
| 

**Max**

 | 

Gathers ensemble information on which the graph could operate on. For example, you could find the average position to use as a good pivot to scale against for all points in a Point Data.

 |
| 

**Min**

 | 

Gathers ensemble information on which the graph could operate on. For example, you could find the average position to use as a good pivot to scale against for all points in a Point Data.

 |

### Attribute Rotator Op

| Node | Description |
| --- | --- |
| 
**Combine**

 | 

Combines two rotation values and writes the result as an attribute, combining first A, then B.

 |
| 

**Inverse Transform Rotation**

 | 

Transforms a Rotator by the inverse of the supplied transform.

 |
| 

**Invert**

 | 

Finds the inverse of a provided Rotator and writes the result as an attribute.

 |
| 

**Lerp**

 | 

Linearly interpolates between two Rotator inputs **A** and **B** based on the **Ratio**. This applies 100 percent of A when Ratio is 0 and 100 percent of B when Ratio is 1.

 |
| 

**Normalize**

 | 

Clamps an angle to a range of -180 to 180 and writes the result as an attribute.

 |
| 

**Transform Rotation**

 | 

Transforms a rotation by a given Transform. This node takes a rotation as input and applies the given transform.

 |

### Attribute Transform Op

| Node | Description |
| --- | --- |
| 
**Compose**

 | 

Composes two Transforms in order: A *B. Order is important when composing Transforms. A* B yields a Transform that first applies A, then B to any subsequent transformation.The result is written to an attribute.

 |
| 

**Invert**

 | 

Inverts the input Transform and writes the new Transform as an attribute.

 |
| 

**Lerp**

 | 

Linearly interpolates between two Transform inputs **A** and **B** based on the **Ratio**. This applies 100 percent of A when Ratio is 0 and 100 percent of B when Ratio is 1.

 |

### Attribute Trig Op

| Node | Description |
| --- | --- |
| 
**Acos**

 | 

Returns the inverse cosine (arccos) of an input and writes the result to an attribute.

 |
| 

**Asin**

 | 

Returns the inverse sine (arcsin) of an input and writes the result to an attribute.

 |
| 

**Atan**

 | 

Returns the inverse tangent (arctan) of an input and writes the result to an attribute.

 |
| 

**Atan 2**

 | 

Returns the inverse tangent (arctan2) of 2 inputs (B/A) and writes the result to an attribute.

 |
| 

**Cos**

 | 

Returns the cosine (cos) of an input and writes the result to an attribute.

 |
| 

**Deg to Rad**

 | 

Returns a radians value based on the input in degrees and writes the result to an attribute.

 |
| 

**Rad to Deg**

 | 

Returns a degrees value based on the input in radians and writes the result to an attribute.

 |
| 

**Sin**

 | 

Returns the sine (sin) of an input and writes the result to an attribute.

 |
| 

**Tan**

 | 

Returns the tangent (tan) of an input and writes the result to an attribute.

 |

### Attribute Vector Op

| Node | Description |
| --- | --- |
| 
**Cross**

 | 

Outputs the Cross Product of two input vectors.

 |
| 

**Distance**

 | 

Calculates the distance between two Vector inputs.

 |
| 

**Dot**

 | 

Returns the Dot Product of two input Vectors.

 |
| 

**Inverse Transform Direction**

 | 

Transforms a direction Vector by the inverse of the input Transform, but does not change its length. The result is written to an attribute.

 |
| 

**Inverse Transform Location**

 | 

Transforms a location by the inverse of the input Transform. The result is written to an attribute.

 |
| 

**Length**

 | 

Returns the length of a Vector stored in an input vector.

 |
| 

**Normalize**

 | 

Outputs a normalized copy of the Vector, ensuring it is safe to do so based on the length. Returns a zero vector if vector length is too small to safely normalize.

 |
| 

**Rotate Around Axis**

 | 

Calculates and returns the result of Vector A rotated by Angle (Deg) around Axis.

 |
| 

**Transform Direction**

 | 

Transforms an input direction Vector by the supplied transform. Does not change its length.The result is written to an attribute.

 |
| 

**Transform Rotation**

 | 

Transforms a rotator or quaternion by the input Transform. The result is written to an attribute.

 |

### Attribute Rotator Op

| Node | Description |
| --- | --- |
| 
**Make Rot from Angles**

 | 

Returns a Rotator attribute created using inout Roll, Pitch, and Yaw values.

 |
| 

**Make Rot from Axis**

 | 

Returns a Rotator using a reference frame created from the Forward, Right, and Up axis.

 |
| 

**Make Rot from X**

 | 

Returns a Rotator attribute created using only an X axis. The Y and Z axis are unspecified but will be orthonormal.

 |
| 

**Make Rot from XY**

 | 

Returns a Rotator attribute created using X and Y axes. The X axis remains fixed and the Y axis may change minimally to enforce orthogonality. Also computes the Z value.

 |
| 

**Make Rot from XZ**

 | 

Returns a Rotator attribute created using X and Z axes. The X axis remains fixed and the Z axis may change minimally to enforce orthogonality. Also computes the Y value.

 |
| 

**Make Rot from Y**

 | 

Returns a Rotator attribute created using only an Y axis. The X and Z axis are unspecified but will be orthonormal.

 |
| 

**Make Rot from YX**

 | 

Returns a Rotator attribute created using Y and X axes. The Y axis remains fixed and the X axis may change minimally to enforce orthogonality. Also computes the Z value.

 |
| 

**Make Rot from YZ**

 | 

Returns a Rotator attribute created using Y and Z axes. The Y axis remains fixed and the Z axis may change minimally to enforce orthogonality. Also computes the X value.

 |
| 

**Make Rot from Z**

 | 

Returns a Rotator attribute created using only a Z axis. The X andY axis are unspecified but will be orthonormal.

 |
| 

**Make Rot from ZX**

 | 

Returns a Rotator attribute created using Z and X axes. The Z axis remains fixed and the X axis may change minimally to enforce orthogonality. Also computes the Y value.

 |
| 

**Make Rot from ZY**

 | 

Returns a Rotator attribute created using Z and Y axes. The Z axis remains fixed and the Y axis may change minimally to enforce orthogonality. Also computes the X value.

 |

## Param

| Node | Description |
| --- | --- |
| 
**Get Actor Property**

 | 

Retrieves the contents of a property from the actor holding the PCG component (or higher in the object hierarchy).

By default, it looks at actor-level properties (useful for Blueprint variables), but it can look at component properties as well using the **Select Component** option.

This property can hold a "flat" struct (such as one with no arrays) or be an array of a valid supported type. In the case of an array, then the output will be an Attribute Set with multiple entries.

This node is useful to retrieve data from actors in the world (self or otherwise) to allow for per-instance control in the graph, using the same interface as the Get Actor Data. This could, for example, hold a list of static meshes to spawn material sand more.

 |
| 

**Get Property From Object Path**

 | 

Retrieves the contents of a property from the actor holding the PCG component (or higher in the object hierarchy). This is similar to the Get Actor Property node except that it can take actor references (soft object paths) through an Attribute Set. This node is useful in data-driven use cases where a data table could hold references to actors and could easily retrieve properties from these as needed without having to rely on actor selection.

 |
| 

**Point To Attribute Set**

 | 

Converts a Point Data to Attribute Set by dropping all of the point properties and keeping only the point attributes. If the input Point Data has no attribute, then no Attribute Set will be output. This node can be useful as an optimization in either processing or memory in certain cases, or to homogenize data types across the graph.

 |

## Point Ops

| Node | Description |
| --- | --- |
| 
**Apply Scale to Bounds**

 | 

For each point in the input Point Data(s), the bounds min and max is multiplied by their scale and the scale will be reset to 1, but preserving negative values.

 |
| 

**Bounds Modifier**

 | 

Modifies the bounds property on points in the provided point data. This node is used to affect the bounds in the input Point Data in a simple way, which might be useful prior to a Self Pruning node or Intersections or Differences for example to tweak the final result.

 |
| 

**Build Rotation From Up Vector**

 |  |
| 

**Combine Points**

 | 

For each input Point Data, outputs a new Point Data containing a single point that encompasses all points in its respective Point Data. This allows recomputing Point Data and setting a specific transform. This node is used as an optimization or higherlevel view on some data in some instances.

 |
| 

**Duplicate Point**

 | 

For each point, duplicate the point and move it along an axis defined by the Direction, and apply a transform on the new point. Repeat the process the number of times Iterations indicates. If "Direction applied in relative space" is selected, the axis of displacement is picked from the new point iteratively. This node is used to lay down a lot of points quickly, and to build fractal-like patterns.

 |
| 

**Extents Modifier**

 | 

Modifies the extent of each point in the point data by manipulating the bounds.

 |
| 

**Split Points**

 | 

For each point, create two points split in "Before Split" and "After Split" where the bounds are split along the specified "Split Axis" and "Split Position". For example, if the Split Position is 0.5, each point is cut in its middle and each half is a different output. This can be used to do more complex point assemblies by supporting subdivision.

 |
| 

**Transform Points**

 | 

Changes the points transforms (either in place or to an attribute with **Apply to Attribute**) using basic random rules. Each component of the transform (translation, rotation, scale) can be set to Absolute instead of relative to allow for more control.

It contains the following options:

**Uniform Scale**: Scales point data to the same X, Y, Z ratio.

**Recompute Seed**: Forces the points seed to be updated according to their new world position.

**Example**: use a Transform Points node with Absolute Rotation and rotation Z being 0 will make certain that the points are pointing in Z up.This makes sure the points are upwards after sampling from the landscape.

This node is useful in generating spatial variation with control on the input Point Data. It is a staple of graphs generating natural looking data.

 |

## Sampler

| Node | Description |
| --- | --- |
| 
**Copy Points**

 | 

Copies an instance of all points in the **Source per point in the Target** input. There are multiple options for inheriting spatial properties, but **Attribute Inheritance** has the most impact on the performance of this node. You can use this node to perform nested loop copies so you can have one source with two targets with two outputs, or two sources with two target with four outputs. This node is often used to instantiate Point Data generated in local space (namely in PCG assemblies/assets). Prior to post processing at their world position.

 |
| 

**Mesh Sampler**

 | 

Samples points on a specified static mesh. Note that this operation is costly.

Requires the **PCG Geometry Script Interop** plugin and the **Geometry Script** plugin.

 |
| 

**Texture Sampler**

 | 

Samples the UV of a texture at each point. Given a texture input, using the "Planar From Texture Data" texture mapping method transforms the UV coordinates based on the Get Texture Data node and samples the teture onto the point inputs. If the texture mapping method is "Use Explicit Points UV Coordinates" the UV coordinates are 0-1, with additional options to determine which attribute is being used for UV as well as address the texture to wrap using advanced tiling, or clamp it to 0-1.

 |
| 

**Select Points**

 | 

Selects a subset of points from the input Point Data using a probability that a given point will be selected or not. In practice, this means that if you take a ratio of 0.5, you will have approximately half the input points, but have no guarantee on whether it is going to be exactly half or not. Since the decision to select a point or not is done independently, this follows a normal distribution.

 |
| 

**Spline Sampler**

 | 

Samples points using the spline as the source material. Sampling on the spline means directly on the spline curve, while the **Horizontal**, **Vertical** and **Volume** options sample on the spline volume (driven by the radius of the control points in the Y/Z axes).

Sampling inside the spline requires the spline to be closed.

 |
| 

**Surface Sampler**

 | 

Samples points on a Surface data, in a regular grid pattern. This node contains the following options:

-   **Point Extents**: Defines the basic grid cell size on the surface.
    
-   **Looseness**: Defines cell size to allow for variation. In practice, the cell size is point extents \* (1 + Looseness).
    
-   **Points Per Square Meter**: Computes the ratio of kept cells. This property limits overcrowding when your grid is large.
    

 |
| 

**Volume Sampler**

 | 

Samples the provided spatial data on a regular 3D grid. This exhibits 'voxel-like' behavior and could potentially be costly for large data or high densities.

 |

## Spatial

| Node | Description |
| --- | --- |
| 
**Attribute Set To Point**

 | 

Converts an Attribute Set to Data Point by creating one default point per entry in the Attribute Set. The resulting Point Data has the same attributes as the original Attribute Set.

 |
| 

**Create Points**

 | 

Creates a point data containing points from a static description of points. This node is normally used to create a single point to seed another process that would require some world position or similar.

 |
| 

**Create Points Grid**

 | 

Creates a point data containing a simple grid of points defined by the settings. This node is used in local space mode couples with the Copy Points node to create grids around multiple sources.

 |
| 

**Create Spline**

 | 

Creates a Spline from the input point data. Contains options to create the following:

-   Create Component or Create Data Only
    
-   Closed or Linear Splines
    
-   Apply custom in and out tangents from Attribute names.
    

 |
| 

**Create Surface From Spline**

 | 

Creates an implicit surface from a **closed** spline. This surface can then be used like other surfaces in the Surface Sampler, Difference, Intersection, and so on.

At this point in time, this relies on a discretization of the spline and as such, might not work for very large splines. If that is the case, consider sampling your spline first, then creating a new spline (using the Create Spline node) before using this node.



 |
| 

**Cull Points Outside Actor Bounds**

 | 

Culls point from the input Point Data based on the current component (partition actor or original) bounds with additional control for bounds expansion. This can be used to make sure input data is relevant to the current processing while allowing some overlap if required.

 |
| 

**Difference**

 | 

Outputs the result of the difference of each source against the union of the differences. This node has the following options:

**Density Function**: Controls which density function is used after the operation is complete. Contains the following options:

-   **Minimum**: Final density is equal to the density of the source minus the max density of all the differences.
    
-   **Clamped Subtraction**: Final density is equal to the density of the source minus the sum density of all the differences. This value is clamped between 0 and 1.
    
-   **Binary**: Final density is equal to 0 if the density of the difference is greater than zero. Otherwise the final density is equal to the density of the source.
    

**Mode**: Controls behavior of difference in the presence of concrete spatial data vs continuous data (other types, more akin to distribution functions). Note that in some cases where we want to select a concrete element, this should be set to Discrete otherwise the resulting density function could not be flat. Contains the following options:

-   **Inferred**: Discrete if either the source or the differences are points, and continuous otherwise.
    
-   **Continuous**: Does not collapse the Density function.
    
-   **Discrete**: Collapses the density function, meaning it converts the data to point data.
    

 |
| 

**Distance**

 | 

For each point in the first input, calculates the distance to the nearest point in the second input and automatically ignores self when computing the distance from one point data set to the same point data set. Optionally, can output the distance vector as an attribute. This node is used to simulate distance fields or create distance-based gradients in a Point Data. This can be used to tweak the scale of trees on the edges of forests or ones that are too close to a stream.

 |
| 

**Find Convex Hull 2D**

 | 

Computes a 2D convex from the input Point Data using the location only (not bounds) of each point. This node can be used in conjunction with the Create Spline node to create a spline that encompasses all the points and that in turn can also be passed into the Create Surface From Spline node.

 |
| 

**Get Actor Data**

 | 

General version of the Get … Data nodes. Reads data from an Actor using the Actor Filter and the Mode.

It contains the following options:

**Actor Filter**: Determines which Actors to consider when fetching Actor data.

**Include Children**: Determines whether to consider any child Actors of the input.

**Mode**: Contains the following options:

-   **Parse Actor Components**: Builds PCG data from the components on the Actor.
    
-   **Get Single Point**: Return one point data containing one point per actor with its transform and local bounds. Use MergeSinglePointData option if you need to.
    
-   **Get Data from PCG Component**: Returns the result of another actor's PCG execution. Note that only data passed to the Output node is stored on the PCG component and only some types are supported (Point Data & Attribute Set), and will be queried accordingly. PCG will make sure that the execution of the remote actor will be done before continuing execution. Note that it needs the data to be already generated (or currently generating) and can't be on the same actor as the component it executes.
    
-   **Get Data from PCG component or Parse Actor components**: Returns PCG output first, if present. Then parses Actors, if needed.
    

Extra options when getting PCG Data:

-   **Expected Pins**: If you get PCG Data, you can also provide a list of expected pins that matches the output node of the PCG Graph that generated the data.
    
-   **Get Data On All Grids:**Get data from every grid size on the target components.
    
    -   **Allowed Grids:** If not using Get Data On All Grids, select the set of grid sizes which data can be pulled from.
        
    -   **Components Must Overlap Self:** Only get data from components which overlap with the bounds of your source component. This is an optional optimization to avoid getting data that is probably not relevant to your component.
        

This node is the most common way to access data from PCG, especially in root graphs.

 |
| 

**Get Bounds**

 | 

Creates an attribute set containing the world space bounds (min & max) of any given Spatial data. Note that this is more general than the Combine Points node as it will return bounds for more types. This node can be used as a higher-level construct to do larger scale processing in a graph.

 |
| 

**Get Landscape Data**

 | 

Specialization of the **Get Actor Data** node that returns appropriately typed and constructed Landscape data.

 |
| 

**Get PCG Component Data**

 | 

Specialization of the Get Actor Data node that returns only the generated output from selected actor PCG components.

 |
| 

**Get Points Count**

 | 

Returns the number of points in the provided input Point Data. This creates a single Attribute Set, regardless of the number of inputs and one entry in that Attribute Set per input Point Data.

 |
| 

**Get Primitive Data**

 | 

Specialization of the **Get Actor Data** node that returns appropriately typed and filtered Primitive data.

 |
| 

**Get Spline Data**

 | 

Specialization of the **Get Actor Data** node that returns appropriately typed and filtered Spline data.

 |
| 

**Get Texture Data**

 | 

Loads a texture to a surface data. Note that this requires a GPU to execute for most compressed texture types. This supprots sampling of compressed textures, UTexture2DArrays with an index to select the desired UTexture2d, sampling CPU-avaialble Textures which can be created using the Availability property on any UTextures, and Point Fitlering instead of of only Bilinear filtering. This node also allows editor-only option to force CPU sampling. This creates a duplicate of the target texture that is CPU-visible and uncompressed and samples that instead. It avoids compression artifacts from GPU sampling.

 |
| 

**Get Volume Data**

 | 

Specialization of the **Get Actor Data** node that returns appropriately typed and filtered Volume data.

 |
| 

**Inner Intersection**

 | 

Computes the inner intersection between all data provided to the node, regardless of their pins.

**Example**: Input contains \[A, B, C\]

**Result**: A ∩ B ∩ C

 |
| 

**Intersection**

 | 

Computes an outer intersection for each data provided in the **Primary Source** pin, where the result is one intersection per data on the primary source pin against the union of data on each other **Source** pins.

**Example**: Primary Source contains \[A, B\] Source 1 contains \[C, D\] Source 2 contains \[E\].

**Result**: A ∩ (C ∪ D) ∩ E, B ∩ (C ∪ D) ∩ E

 |
| 

**Make Concrete**

 | 

Collapses composite data types (intersection, difference, union) unto Point Data. For already concrete data, has no effect. This node isn’t normally used directly but is a conversion step into specific nodes.

 |
| 

**Merge Points**

 | 

Combines multiple input point data into a single point data. Attributes are merged and non-common attributes are defaulted as needed.

 |
| 

**Mutate Seed**

 | 

Mutates the seed of every point in the input Point Data(s) according to its position, previous seed, this node’s seed and the component’s seed. This node is useful to separate random behavior after doing some operations that are duplicating points but might not otherwise affect the seed.

 |
| 

**Normal To Density**

 | 

Computes point data density based on the point normal and the provided settings (**Normal**, **Offset**, **Strength**, **Density Mode**) which is similar to a dot product, with additional flexibility. This node is often used to affect in some way some of the points that are most closely aligned with a specific axis (making some trees taller) or least aligned (removing trees on steep inclines).

 |
| 

**Point Neighborhood**

 | 

Computes neighborhood-based values and sets them on the input Point Data, according to a search distance (in engine units). The values include distance to center, average neighborhood center, average density and average color. This node can be used to smoothen out density or values across points, which is often useful for natural procedural processes.

 |
| 

**Point From Mesh**

 | 

Builds a point data containing one point with the bounds of the provided static mesh and a reference to that mesh. This is useful when selection of the potential mesh is done upfront and then moving these bounds to the points (often through a partition node + Loop node + Point From Mesh combination) prior to doing intersection tests or self pruning.

 |
| 

**Projection**

 | 

Creates a projection data from a source data to project onto a target. Note that if there are no special projection representations for that source data to that target data, then it converts the data to points. This node is very often used to re-project points on surfaces after some manipulation in the graph. For example, it will often follow a Copy Points node to replace the points in a proper position in their environment.

 |
| 

**Spatial Noise**

 | 

Constructs a spatially-consistent noise pattern (such as Perlin noise) and writes it to a specified attribute. This node can be used in conjunction with the Match and Set Attributes with the input-driven weights to have spatial-noise applied to selection. In general, this node is useful to obtain more natural looking distributions.

 |
| 

**To Point**

 | 

Casts the data to a point data if it is already one or discretizes the spatial data to point data.

 |
| 

**Union**

 | 

Creates a logical union between data, from a distribution function perspective. Result depends on the density function option chosen.

**Density Function**: Controls which density function is used after the operation is complete. Contains the following options:

-   **Maximum**: Final density is equal to the max density of the source.
    
-   **Clamped Addition**: Final density is equal to the sum of the densities in all the differences. This value is clamped between 0 and 1.
    
-   **Binary**: Final density is equal to 1 if any density of the source is greater than zero. Note that this is rarely useful except in the context of a binary difference.
    

 |
| 

**World Ray Hit Query**

 | 

Creates a surface-like data that performs ray casts in the physics world. It can pass data to any node that expects a surface data.

By default, the size and orientation of the rays is driven by the source component's actor properties (most likely a volume), but the ray properties can be overridden. It contains the following options:

**Apply Metadata From Landscape**: Gets the landscape layer values if the raycast hits the landscape. Note that there is a small performance cost involved with this.

**Ignore PCG Hits**: Ignores all PCG generated assets. Is useful when there is no ordering enforced vs other nodes creating data in the world (or other graphs).

Optionally, can return the physical material and the actor hit.

The Filtering elements are used for finer-grained control to ignore or keep only some of the hits.

 |
| 

**World Volumetric Query**

 | 

Creates a volume-like data that gathers points from the physics world. It can pass data to any node that expects a surface data.

The Search for overlap check controls whether overlaps are returned as points or only queries overlapping nothing (subject to filtering) are returned.

Can also optionally return the actor "found" in that volume.

 |

## Spawner

| Node | Description |
| --- | --- |
| 
**Create Target Actor**

 | 

Creates an empty actor from a template that can be used as a target for writing PCG artifacts to, such as the Static Mesh Spawner.

 |
| 

**Point from Player Pawn**

 | 

Creates a point at the current player pawn location. Used during runtime generation.

 |
| 

**Spawn Actor**

 | 

Spawns either the contents of an actor or an actor per point in the provided input data. The actor is driven by the template actor class or the instanced templated actor or by attribute depending on the settings.

It contains the following options:

**Template Actor Class**: List of available Actors in your project.

**Option**:

-   **Collapse Actors**: Gathers some of the actor components (Static Mesh Components and PCG Components) and acts collapsed inside of the target actor.
    
-   **Merge PCG only**: Spawns one actor per point If the spawned actor has a PCG component, its inputs are bundled into a single graph execution.
    
-   **No Merging**: Spawns one actor per point.
    

In the No Merging case, it is possible to set properties to the actors from attributes on the points through the ‘Spawned Actor Property Override Descriptions’.

**Attach** mode:

-   **Not attached:** No engine-aware relationship will exist between the original actor (owner of the PCG component) and the created actor.
    
-   **Attached:** The created target actor will be attached as a child to the actor owning the PCG component. Note that this has an impact on streaming of said created actor in World Partition enabled maps, e.g. this actor will be streamed in with the parent.
    
-   **In Folder:** No engine-aware relationship will exist but the actor(s) will be placed in a folder named according to the actor owning the PCG component for easier visualization in the Scene Outliner. Will not impact streaming.
    

This node can be used to create partition-like actors and gather artifacts (visual and otherwise) on actors that can be properly streamed in on play.

 |
| 

**Static Mesh Spawner**

 | 

Spawn one static mesh per point in the provided point data.

Static Mesh options are added to the Mesh Entries array and selected using each entry's **Weight**. This is done by taking the sum of all the weight values and converting them to a percentage for each entry. For example, if there are four entries in the array that each have a value of 1, the value of the sum is 4. Each entry's weight is then divided by the sum and converted to a percentage. This means each entry has a 25% chance of spawning.

Selection of the static mesh is done using variations based on the selected **Mesh Selector Type** option.

It contains the following options:

-   **PCG Mesh Selector Weighted**: Selects an entry based on the total weight of entries.
    
-   **PCG Mesh Selector By Attribute**: Selects an entry based on an attribute present on the mesh.
    
-   **PCG Mesh Selector Weighted By Category**: Selects a category by looking up an Attribute on the point, then selects an entry based on weight.
    

Selected mesh will be written to an attribute on the output Point Data, as well as the bounds of the selected mesh will be pushed to the point bounds.

For each Mesh Property Override created, an attribute can be selected to be applied to a Property Target on the ISM’s Template Descriptor when it will be generated.

 |

## Subgraph

| Node | Description |
| --- | --- |
| 
**Loop**

 | 

Executes another graph as a subgraph, once per data in the loop pins. Non-loop pins are passed as-is. Pin properties are set up on the input & output nodes in each graph. The usage of the pins will drive their behavior when executed in a Loop. Feedback pins have a special behavior such that they should be paired with another of the same name in the output. During execution, the first iteration will receive the data on the feedback pin from the calling graph, but subsequent iterations will get the data from the previous iteration. This node is extremely important to simplify local processing on the same kind of data, for example by allowing sampling on a single mesh (with the Mesh Sampler node) then copying that data only on the relevant data. It is also used to build data sets that have interdependencies on them (sequences of selection & exclusions) and the like.

 |
| 

**Subgraph**

 | 

Executes another graph as a subgraph. Note that a graph can call itself recursively; the graph will execute until this Subgraph node is culled from execution (because of Control Flow nodes) or when it has no input data. Subgraph nodes are a major element in reducing graph complexity and maximizing reuse. They also enable recursivity which can be useful in some circumstances.

 |

## Uncategorized

| Node | Description |
| --- | --- |
| 
**Add Comment**

 | 

Visual aid to categorize and organize a graph. This is not an actual node.

 |
| 

**Add Reroute Node**

 | 

Graph organizational tool to add control points on edges, making them look nicer in the graph.

 |
| 

**Add Named Reroute Declaration Node**

 | 

Named reroute nodes are akin to reroute nodes but they do not have visual edges. They are used to remove otherwise very long edges or spaghetti edges across large graphs. They can be renamed and be consumed (usage) at multiple places but they can be defined only at a single place in a graph (definition).

 |