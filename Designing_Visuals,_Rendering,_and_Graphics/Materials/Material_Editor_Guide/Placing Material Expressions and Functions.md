# Placing Material Expressions and Functions

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/placing-material-expressions-and-functions-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/placing-material-expressions-and-functions-in-unreal-engine)  
**Processed:** 2025-06-14 16:43:22

---

**Material Expressions** and **Material Functions** are the building blocks used to create fully functional Materials in Unreal Engine. Each Expression or Function is a self-contained node in the Material graph. These nodes run small snippets of HLSL code on their inputs and output the results.

This page demonstrates the various ways to insert Material Expressions and Functions into your Material graph.

## Material Expressions

Each **Material Expression** node contains a small set of HLSL instructions to perform a very specific task in the Material. Materials are built by combining Expressions and Functions to achieve a desired visual result.

For example, if you want to change the scale of a texture on your mesh, you can use a **Multiply** node. By multiplying a **Constant** value by the **Texture Coordinates** of a Material, you can manipulate the scale of the texture.

![When the multiplication value is changed from 1 to 3, the texture is tiled three times across the surface instead of once.](https://dev.epicgames.com/community/api/documentation/image/f044e94d-6e75-4d1c-a7c3-15fa8a2afb3e?resizing_type=fit&width=1920&height=1080)![When the multiplication value is changed from 1 to 3, the texture is tiled three times across the surface instead of once.](https://dev.epicgames.com/community/api/documentation/image/6ab3de07-ee66-4b8b-af3a-377d13290425?resizing_type=fit&width=1920&height=1080)

**When the multiplication value is changed from 1 to 3, the texture is tiled three times across the surface instead of once.**

This is a simple, but versatile piece of **Material logic**. When small node networks like this are combined you can ultimately create very sophisticated surface effects.

## Differences Between Expressions and Functions

The main difference between Material Expressions and Functions is that Material Expressions are created directly in the source code of the engine, while Material Functions exist as editable assets in the Content Browser.

#### Material Expressions

Material Expressions are static pieces of code that can only do what they are programmed to do. A **Multiply** node is programmed to multiply two values together. The only way you could alter its utility is to change it in the source code. There were four Material Expressions in the earlier example:

[![Four material expressions](https://dev.epicgames.com/community/api/documentation/image/3388f56f-880e-42eb-8a91-93602ea515ca?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/3388f56f-880e-42eb-8a91-93602ea515ca?resizing_type=fit)

1.  **Constant** — Holds a single numeric (float) value.
    
2.  **Multiply** — Multiplies input A and input B and outputs the product.
    
3.  **Texture Coordinates** — Outputs the UV texture coordinates of the Material in the form of a two-channel vector value.
    
4.  **Texture Sample** — References an image texture and outputs the color value(s) of the texture.
    

#### Material Functions

Material Functions are more dynamic because you can configure them to perform any type of calculation you want. You can [create and edit Material Functions](https://dev.epicgames.com/documentation/en-us/unreal-engine/creating-and-using-material-functions-in-unreal-engine) without having to make source code changes.

If you double-click a Material Function node, the **Material Function Editor** opens. Within a Material Function you will find a self-contained node graph made up of Material Expressions.

[![Camera Depth Fade](https://dev.epicgames.com/community/api/documentation/image/df73e3a2-6cf9-40c1-90e9-3e66c446b1e0?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/df73e3a2-6cf9-40c1-90e9-3e66c446b1e0?resizing_type=fit)

*A CameraDepthFade Material Function contains the Material graph pictured to the right.*

Material Functions are one way to condense complicated Material logic into a single, easy to read node that can be used across multiple Materials. Functions are an excellent way to package repetitive Material graphs so that they can be shared and reused by other team members.

## Placing Material Expressions

There are four ways to insert Material Expressions into the Material graph.

1.  [Drag and drop from the Palette](https://dev.epicgames.com/documentation/en-us/unreal-engine/placing-material-expressions-and-functions-in-unreal-engine#drag-and-drop-from-the-palette)
    
2.  [Right-click context menu](https://dev.epicgames.com/documentation/en-us/unreal-engine/placing-material-expressions-and-functions-in-unreal-engine#right-click-context-menu)
    
3.  [Drag from an input or output pin](https://dev.epicgames.com/documentation/en-us/unreal-engine/placing-material-expressions-and-functions-in-unreal-engine#drag-from-an-input-or-output-pin)
    
4.  [Keyboard shortcuts](https://dev.epicgames.com/documentation/en-us/unreal-engine/placing-material-expressions-and-functions-in-unreal-engine#keyboard-shortcuts)
    

### Drag and Drop from the Palette

The Palette is a collapsible sidebar panel on the right side of the Material Editor window. Click on **Palette** to expand the panel if it is not visible.

[![Expand Material palette](https://dev.epicgames.com/community/api/documentation/image/7115c389-54cf-4adb-949d-781429d23f20?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/7115c389-54cf-4adb-949d-781429d23f20?resizing_type=fit)

To keep the Palette visible at all times, click the **pin icon**.

[![Pin Palette](https://dev.epicgames.com/community/api/documentation/image/e0b5946b-f184-4598-9f78-53f93109285a?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/e0b5946b-f184-4598-9f78-53f93109285a?resizing_type=fit)

Click the pin again to unpin the Palette. When unpinned, the Palette collapses after every action.

#### Searching the Palette

The Palette contains a list of all Material Expressions and Material Functions available in UE5. These are sorted into categories according to their general purpose.

[![Material palette categories](https://dev.epicgames.com/community/api/documentation/image/441e48bf-e4e2-4667-b4f6-9c351cec65bd?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/441e48bf-e4e2-4667-b4f6-9c351cec65bd?resizing_type=fit)

You can search the Palette by typing a query in the search bar. The search filter updates progressively as you type and automatically highlights the closest match.

[![Palette search](https://dev.epicgames.com/community/api/documentation/image/9511aa02-db4f-4cb8-9bd2-e37628d60be8?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/9511aa02-db4f-4cb8-9bd2-e37628d60be8?resizing_type=fit)

The **Category menu** lets you filter which node types are visible in the Palette.

[![Palette search filters](https://dev.epicgames.com/community/api/documentation/image/468f5db8-cc46-420c-8353-d785df8cbdc6?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/468f5db8-cc46-420c-8353-d785df8cbdc6?resizing_type=fit)

-   Select **Expressions** to only show only Material Expressions in the palette.
    
-   Select **Functions** to show only Material Functions and hide Expressions.
    
-   **All** Material Expressions and Functions are visible by default.
    

#### Inserting Expressions and Functions from the Palette

You can drag any Material Expression or Function from the palette directly into your Material graph.

1.  **Left-click** the name of a Material Expression in the palette and drag it into the Material graph with the **left mouse button** held down.
    
    [![Drag and drop expression](https://dev.epicgames.com/community/api/documentation/image/a674675a-5046-40cc-9238-ae5797c9bf47?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/a674675a-5046-40cc-9238-ae5797c9bf47?resizing_type=fit)
    
2.  **Release the left mouse button** and the Material Expression is inserted at the pointer.
    
    [![Node in graph](https://dev.epicgames.com/community/api/documentation/image/3454cf8d-a8e1-4224-8c83-36663446bb76?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/3454cf8d-a8e1-4224-8c83-36663446bb76?resizing_type=fit)
    

### Right-Click Context Menu

You can also add Material nodes to your graph from the **right-click menu**. Like the Palette, the right-click menu contains a categorized list of all Material Expressions and Functions. The right-click menu has a search bar, but does not have a way to filter out Expressions or Functions.

1.  **Right-click** anywhere in the background of the Material graph.
    
    [![Drag and drop expression](https://dev.epicgames.com/community/api/documentation/image/0faf7629-dfec-4e9c-a6ae-9074e51794b0?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/0faf7629-dfec-4e9c-a6ae-9074e51794b0?resizing_type=fit)
    
2.  Browse the categories, or type a query into the search bar to find an Expression or Function.
    
3.  **Left-click** the name of a Material Expression or Function to place it in your graph.
    
    [![Blend Overlay function](https://dev.epicgames.com/community/api/documentation/image/5aa94c74-8681-4a26-a777-b520db240f17?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/5aa94c74-8681-4a26-a777-b520db240f17?resizing_type=fit)
    

You can also press the **Enter** key to insert whichever Material Expression is currently highlighted in blue. Use the up and down arrows to select from the list, or refine your search terms.

### Drag From An Input or Output Pin

A second way to access the context menu is to **left-click** and drag a wire from any input or output pin on an existing node in your graph. Release the left mouse button anywhere in the graph and the context menu appears. Use the search bar or browse the categories to find and spawn a node. One advantage to this method is that the Material Expression or Function is already wired correctly when it spawns, saving you a step.

### Keyboard Shortcuts

There are a number of Keyboard shortcuts that you can use to quickly insert commonly used Material Expressions. To insert a Material Expression **hold down a keyboard shortcut** and **left-click** anywhere in the Material graph.

This table shows the default Material Expression keyboard shortcuts.

| Keyboard Shortcut Key | Material Expression |
| --- | --- |
| 
A

 | 

Add Material Expression

 |
| 

B

 | 

Bump Offset Material Expression

 |
| 

1

 | 

Constant Material Expression

 |
| 

2

 | 

Constant2Vector Material Expression

 |
| 

3

 | 

Constant3Vector Material Expression

 |
| 

4

 | 

Constant4Vector Material Expression

 |
| 

D

 | 

Divide Material Expression

 |
| 

I

 | 

If Material Expression

 |
| 

L

 | 

Linear Interpolate Material Expression

 |
| 

F

 | 

Material Function Material Expression

 |
| 

M

 | 

Multiply Expression

 |
| 

N

 | 

Normalize Expression

 |
| 

O

 | 

One Minus Expression

 |
| 

P

 | 

Panner Expression

 |
| 

E

 | 

Power Expression

 |
| 

R

 | 

Reflection Vector WS Expression

 |
| 

S

 | 

Scalar Parameter Expression

 |
| 

S

 | 

Texture Sample Expression

 |
| 

U

 | 

Texture Coordinate Expression

 |
| 

V

 | 

Vector Parameter Expression

 |

You can change the Material Expression keyboard shortcuts by going to **Edit > Editor Preferences > Keyboard Shortcuts > Material Editor Spawn Nodes**.

## Placing Material Functions

In most cases you will use the same methods as above to place Material Functions in your graph. The **Palette** and **right-click menu** work the same for Material Functions as they do for Expressions.

There is one additional way to place Material Functions in your graph.

### Placing Material Functions from Content Browser

One thing that is exclusive to Material Functions is that you can also drag and drop them from the **Content Browser** into your Material.

Find the Material Function you want to use in the Content Browser, then **left-click and drag** the asset into the Material graph. You can access the Content Browser from the **Content Drawer** at the bottom of the Material Editor, or from the main UE5 Editor window.

To find Material Functions in the Content Browser, you need to look in the **Engine** folder, which is not visible by default.

To display the **Engine** folder, click the **Settings** icon on the right side of the Content Browser, and check **Show Engine Content**.

[![Show Engine content](https://dev.epicgames.com/community/api/documentation/image/47915e2a-3430-41c3-929d-6b9b922dc494?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/47915e2a-3430-41c3-929d-6b9b922dc494?resizing_type=fit)

Material Functions are found in the Content Browser at the path **All > Engine > Content > Functions**.

[![Included Material functions](https://dev.epicgames.com/community/api/documentation/image/38eb8f74-120d-4b20-b389-774f2b1a700f?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/38eb8f74-120d-4b20-b389-774f2b1a700f?resizing_type=fit)

## Connecting Material Nodes

Use the following steps to connect any two nodes in your Material graph.

1.  Left-click and drag a wire from an input or output pin on the first node.
    
    [![Connecting Material Expressions](https://dev.epicgames.com/community/api/documentation/image/f60565c3-3672-4200-8002-fe9d3509caf5?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/f60565c3-3672-4200-8002-fe9d3509caf5?resizing_type=fit)
    
2.  Release the left mouse button over a pin on the second node.
    

To delete a connection, hold the **Alt** key and click the wire between two nodes. You can also left-click the wire and press **Delete**.

You can move an existing wire from one pin to another. **Ctrl+Click** the connection you want to move and drag it to a different input or output.

## Conclusion

Material Expressions and Functions are the primary building blocks of UE5 Materials. The engine includes hundreds of Material nodes, each designed to hold a specific type of data or execute a set of HLSL instructions. You will most likely find yourself using a small number of nodes very frequently. For example, the Material Expressions with [keyboard shortcuts documented above](https://dev.epicgames.com/documentation/en-us/unreal-engine/placing-material-expressions-and-functions-in-unreal-engine#keyboard-shortcuts) are all fundamental to Material creation in UE5.

Material Expressions and Functions usually have tooltips to summarize their purpose, and most are documented on the Materials reference pages.

-   [Material Expressions Reference](https://dev.epicgames.com/documentation/en-us/unreal-engine/unreal-engine-material-expressions-reference)
    
-   [Material Functions Reference](https://dev.epicgames.com/documentation/en-us/unreal-engine/unreal-engine-material-functions-reference)
    

Since Material Expressions are often pure HLSL code, you can also read the official [Microsoft HLSL documentatio](https://docs.microsoft.com/en-us/windows/win32/direct3dhlsl/dx-graphics-hlsl)n for technical background information.

### Continue Reading

-   [Using the Main Material Node](https://dev.epicgames.com/documentation/en-us/unreal-engine/using-the-main-material-node-in-unreal-engine)
    
-   [Previewing and Applying your Materials](https://dev.epicgames.com/documentation/en-us/unreal-engine/previewing-and-applying-your-materials-in-unreal-engine)