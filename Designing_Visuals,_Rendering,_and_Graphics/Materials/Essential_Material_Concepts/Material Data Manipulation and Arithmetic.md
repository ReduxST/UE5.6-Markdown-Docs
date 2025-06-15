# Material Data Manipulation and Arithmetic

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/material-data-manipulation-and-arithmetic-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/material-data-manipulation-and-arithmetic-in-unreal-engine)  
**Processed:** 2025-06-14 16:35:09

---

The [Material Data Types](/documentation/en-us/unreal-engine/material-data-types-in-unreal-engine) page introduced the four ways data is represented in the Material Editor. To create Materials effectively it is necessary not only to know these data types, but also how to manipulate data and control the way information travels through your Material Graph.

Two topics are discussed in this document.

1.  [Manipulating data types](/documentation/en-us/unreal-engine/material-data-manipulation-and-arithmetic-in-unreal-engine#manipulatingdatatypes): How to combine floats into a multi-channel vector, and conversely, how to isolate information out of a larger data type.
2.  [Material Graph arithmetic](/documentation/en-us/unreal-engine/material-data-manipulation-and-arithmetic-in-unreal-engine#materialgrapharithmetic): Rules and processes for performing arithmetic operations in a Material with different data types.

## Manipulating Data Types

Just because a piece of information originates as one data type does not mean it needs to stay that way. For example, you can combine or **Append** two Scalar Parameters (floats) into a two-channel vector (float2) in order to pass them into an input that requires two-channel data. Conversely, you can use a **ComponentMask** to retrieve a specific subset of channels out of a larger vector.

The Material Expressions documented in this section provide ways to combine and separate data to control the way information flows through your Material Graph.

### AppendVector

An AppendVector Material Expression combines the data in **Input A** with the data in **Input B**, and outputs a multi-channel vector (float2, float3, or float4). In this example, two Constants are appended together to output a float2: **(1, 2)**.

![AppendVector Node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d5d67ebb-41e2-4f6b-b1be-14309dc5ed79/append-node.png)

#### Example Use Case

The Append node is often useful when you want the ability to modify two values independently of one another, but need to pass them into an input that requires multi-channel data. The graph below gives artists a way to control the Tiling or **UV scale** of a texture in a Material Instance, but only uniformly.

![UV Tiling controls uniform](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/aa6c8b32-d29b-4dec-9a43-3ae148b512c2/tiling-uniform.png)

The shortcoming in this example is that the Material Graph only contains one parameter, but UV Coordinates have two channels. With this solution you cannot control the width and height of the texture independently.

You can solve this by using an **AppendVector**. Create a separate Scalar Parameter for each axis and then pass them into the Append node. The Append node combines the two parameters into a float2, which is then multiplied by the Texture Coordinates.

![UV tiling controls two-channel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d66d30cc-34f2-4d93-9e94-09fa71dfc567/append-vector.png)

Since **Tiling X** and **Tiling Y** are parameterized separately, you can now control the width and height of the texture independently.

#### Append Order

The AppendVector expression combines data in the order it is attached to the node. The data in Input B is always appended to the end of the data in Input A. Consider the two images below.

 ![Append order initial](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ce11d3bf-2b35-440e-8df5-a16eb8039603/append-order-01.png) ![Append order reversed](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8f3ef04b-2c39-4635-ade5-631b235b3cd0/append-order-02.png)

-   In the first slide, the appended result is **(0.05, 0.2, 0.8)**, or light blue as the node preview shows.
-   In the second slide, the appended result is **(0.8, 0.05, 0.2)**, or pink as the node preview shows.

### AppendMany

**AppendMany** is a [Material Function](/documentation/en-us/unreal-engine/unreal-engine-material-functions-overview) that works the same way as the AppendVector expression, but can combine up to four separate float/scalar values into a multi-channel vector.

![AppendMany Material Function](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6ea0ecf5-3da3-4554-877d-05fc547ced71/append-many.png)

One added benefit of the AppendMany function is that it provides three different output pins. This gives you access to some or all of the appended channels, depending on what you need for a given situation.

The AppendMany node only accepts float/scalar values on its inputs. If you pass a float2, float3, or float4 into the AppendMany node, all but the first value is discarded.

### Component Mask

The **Component Mask** Material Expression serves the opposite purpose to the Append nodes documented above. Instead of combining data, a ComponentMask provides a way to separate data into its component parts or channels.

A Component Mask functions like a gate. For any data connected to its input, you can choose exactly which channels are allowed to pass through the output. The image below shows a Constant4Vector containing values of (0, 1, 0.7, 0.5). When you select the Mask node in the graph, four check-boxes are displayed in the Details Panel.

![Component Mask Details Panel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1c27e412-f9ee-4046-bc41-120cbfa53727/component-mask-properties.png)

These check-boxes determine which channels the node will output. Currently none are checked, so the Mask node will not output any information. If you attempt to plug it into a downstream input, the node will display an error.

![Component Mask Details Panel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/92793756-66e3-4b0e-955f-202ee73656ab/component-mask-error.png)

These checkboxes give you a way to filter out information and only use the channels that you need.

Suppose you wanted to use the value in the **A channel** to control the opacity of a Material. You would enable the A channel by checking the box, then connect the output pin of the Mask to the **Opacity Input**.

![Component Mask example](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2f8a33b9-59c7-4079-b52a-894a0b891b44/component-mask-opacity.png)

The ComponentMask discards the R, G, and B channels because they are unchecked, and outputs only the value in the A channel — in this case 0.5.

## Material Graph Arithmetic

The second main way of manipulating data in a Material Graph is through mathematical operations. All common arithmetic operations are available in the Material Editor.

![Arithmetic Material expressions](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c3bf6d92-a33c-4bc4-9955-9af443e35e42/arithmetic-nodes.png)

The four arithmetic Material Expressions. Read more on the Math Material Expressions page.

The basic purpose of the arithmetic nodes should be relatively self-evident. For example, if you plug constant values of **0.3** and **0.2** into an **Add** node, the Add node calculates **0.3 + 0.2** and outputs a value of **0.5**. Arithmetic between two constant values is simple and straightforward.

![Simple addition operation](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8aabaa20-76fd-4358-a86f-f5d6a2ad3366/simple-add-graph.png)

However, as demonstrated on the data types page, information does not always travel through the Material Graph as individual float values. Because of this, it is important to understand the rules and processes for performing arithmetic between various data types in a Material. There are two major areas of concern.

1.  Not all data types are compatible with one another for arithmetic operations.
2.  Arithmetic operations work differently depending on the data types involved.

### Compatible and Incompatible Data Types

The example above showed a simple addition operation between two float values, or 0.3 + 0.2 = 0.5. This operation works because both values are the same kind of data. What happens if a different data type is passed into one of the inputs? These three points summarize compatibility between data types:

-   Arithmetic between **equivalent data types** is always valid. For example, **float2 + float2** returns a new float2.
    
-   Arithmetic between a float and any larger float is valid. For example, **float + float3** returns a new **float3**.
    
-   Arithmetic between two inequivalent data types is invalid. For example, **float2 + float3** is invalid and returns an error.
    

In other words, arithmetic across two different data types is possible, but only if one of the data types is a float. In the graph below, the operation **0.3 + (1,2)** is valid. The float is added to both values in the float2, and the result is a new float2 with values of **1.3, 2.3)**.

![Float1 plus float2](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fcb99061-2f72-4e9d-bb09-a2c15aee680b/float1-float2-add.png)

However, arithmetic between inequivalent float2, float3, or float4 data returns an error.

![Float3 plus float2 error](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ba47d123-b7d2-4eb0-8123-082f8838eea6/float2-float3-error.png)

The table below summarizes data type compatibility for Material Graph arithmetic.

| Data Type | Compatible Data Types for Arithmetic |
| --- | --- |
| Float | Any |
| Float2 | Float, Float2 |
| Float3 | Float, Float3 |
| Float4 | Float, Float4 |

### Arithmetic Rules Between Data Types

It's also necessary to understand how arithmetic calculations are performed between different data types. The two scenarios below demonstrate how arithmetic works when one or both of the data types are larger than a float.

#### Arithmetic Between Equivalent Data Types

When arithmetic occurs between equivalent data types (float2 + float2 for example) each value in Input A is operated on by the corresponding value in Input B. The example below shows addition between two **Constant2Vector** Expressions.

![Addition between two Float2 variables](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ed1605d1-c51a-4430-94f6-969b07a41962/float2-float2-add.png)

Written out in long form, there are two separate addition operations. The first values in each node are added together: **(1 + 2)**. Then the second values in each node are added **(3 + 3)**. The result is a new float2: **(2, 6)**.

The chart below shows an arithmetic example for each of the four data types.

| Input A, Input B | Input Data | Math Notation | Resulting Data |
| --- | --- | --- | --- |
| Float, Float | (4) / (2) | 4 / 2 = 2 | 8 |
| Float2, Float2 | (1, 3) + (2, 3) | (1 + 2), (3 + 3) | (3, 6) |
| Float3, Float3 | (3, 2, 0.5) \* (2, 1, 2) | (3 x 2), (2 x 1), (0.5 x 2) | (6, 2, 1) |
| Float4, Float4 | (2, 2, 2, 3) - (1, 1, 2, 2,) | (2 - 1), (2 - 1), (2 - 2), (3 - 2) | (1, 1, 0, 1) |

#### Arithmetic Between a Float and a Vector

When arithmetic occurs between a float and any larger data type, the float is used repeatedly for each separate calculation. In the image below a **Constant** and a **Constant3Vector** are multiplied together.

![Multiplication between a Float and a Float3](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/58ef379f-a321-4fc5-873c-4b0430e4252b/float-float3-mult.png)

As shown in the illustration, the value in the Constant is multiplied by each value in the Constant3Vector. There are three separate multiplication expressions: **(2 *3), (2* 1)**, and **(2 \*2)**. The product is a float3: **(6, 2, 4)**.

Whether the float is in Input A or Input B has no bearing on multiplication and addition, but of course matters for division and subtraction.

![Subtraction operation](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3e1b9121-9b84-4907-b033-40771314c9fc/float3-sub-float1.png)

In the image above, the value in the Constant (2) is subtracted from each value in the Constant3Vector (6, 4, 3). Written out in math notation: (6 - 2), (4 - 2), (3 - 2). The resulting float3 is **(4, 2, 1)**.

If you were to reverse the input order, the results would be different.

![Subtraction with inputs reversed](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d959bd6f-99b9-4bd2-8174-c408a041b49c/subtraction-reversed.png)

Since the float is now the top number in the subtraction node, each arithmetic operation is inverted: **(2 - 6), (2 - 4), (2 - 3)**. The resulting float3 is **(-4, -2, -1)**.

## Conclusion

The concepts and techniques on this page are a key component in most of the Material Graph logic you will use to create Materials. The reference pages linked below can help you increase your understanding of math and data manipulation operations in the Material Editor.

-   [Math Material Expressions](/documentation/en-us/unreal-engine/math-material-expressions-in-unreal-engine)
-   [Vector Operation Expressions](/documentation/en-us/unreal-engine/vector-operation-material-expressions-in-unreal-engine)