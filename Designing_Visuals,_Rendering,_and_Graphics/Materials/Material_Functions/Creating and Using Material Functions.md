# Creating and Using Material Functions

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/creating-and-using-material-functions-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/creating-and-using-material-functions-in-unreal-engine)  
**Processed:** 2025-06-14 16:17:10

---

## Creating Material Functions

Use the following steps to create a new Material Function:

1.  Right-click in the **Content Browser**. In the context menu under the Create Advanced Asset section, open the **Materials** sub-menu and select **Material Function** from the list.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cb0dc9d2-61ff-490e-b236-58a731eabc2e/create-material-function.png)
2.  Rename the Material Function after it appears in the Content Browser. Your name should be as descriptive as possible so that when someone looks at it they can easily understand what it does. This example ses the name **Custom\_Fresnel**. You can re-name your Material Function by selecting it in the **Content Browser**, pressing **F2** on the keyboard, and typing a new name.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8ec7ea88-6594-4235-b6c6-05d12157234d/custom-fresnel.png)

## Editing Material Functions

After you create a new Material Function, you need to open it in the Material Editor to begin constructing the Material Expression network. You can also open existing Material Functions if you would like to change their behavior. There are two ways to open a Material Function for editing:

1.  Double-click a Material Function asset in the **Content Browser** to open it in a separate Material Editor tab. You can then edit the Material Expression network within the Material Function to modify its behavior
    
    ![Cheap Contrast Material Function asset](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0922f870-68e6-4f3f-9385-98aed34c38a9/cheap-contrast-content-browser.png)
2.  Double-click a Material Function node within an existing Material, and the Material Function will open in a new Material Editor Tab.
    
    ![Cheap contrast Material Function Call node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/abe8a374-7bd7-4f20-afd5-bf474e3a864b/cheap-contrast-node.png)

When double-clicked, the Material Function opens in a new tab of the Material Editor, showing the Material Expression network contained within the function. You can then edit the graph to your liking.

![Cheap contrast material graph](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cca0f27d-947e-4dc5-8987-a02aae8ec045/cheap-contrast-material-graph.png)

It is important to note that any changes made and saved to a Material Function will propagate to all instances of that Material Function moving forward. For example, if you made a change to the internal network of a Radial Gradient Material Function, all existing instances of that function would receive the update, as well as all new instances moving forward.

For this reason, unless you are certain that your change needs to propagate throughout all other instances of the function, it may be wise to **make a copy of an existing function** in the Content Browser (right-click and choose Duplicate from the context menu) rather than editing the original material function.

Once you make changes to a function you must click the **Apply** button to propagate the changes to the function asset and any Materials using the function. Once done, be sure to save your asset in the Content Browser.

![Apply changes](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0a67326f-510d-481c-b2c4-07fe8e518586/apply-changes.png)

## Publishing Your New Function

In order to use your Material Function , you need to make sure that it shows up within the **Material Function Library** in the Material Editor Palette. In order to do this, you must set the **Expose to Library** property to true.

1.  Deselect all nodes within your function by clicking in the background of the Material Graph. This will display the function's base properties in the **Details** panel.
    
    ![Expose to library](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7bb76ae6-6180-4c03-9bcd-0936c694d46c/expose-to-library.png)
2.  Add a description. This is critical, as putting a description here will cause that description to appear as a tooltip when users mouse over the function in the Material Function Library as well as in Material Editor. Adding descriptions to your Input and Output nodes is certainly good practice, but if you had to choose only one place to comment in your expression, this is by far the most important one.
    
    ![Function description](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e2fb965c-79a9-411d-b951-6af30b64d9d3/function-description.png)
3.  **Library Categories Text** lets you choose which category your Material Function will appear in. You can add additional categories by clicking **Insert**, and typing a new category name. However, it is wise to be as concise as possible and not add any more categories than are absolutely needed.
    
    ![Function categories](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8a1120a9-10cb-4d41-87a9-3a2dc9c561cf/categories.png)

## Using Material Functions

### From Material Palette

Once you have created your Material Function and published it to the library, you can use it in an existing Material by dragging it directly from the Material Editor Palette. In addition to user-created Material Functions, the Palette contains all the default Material Functions included with the engine.

![Material Function library](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1b280ded-3fac-4b27-8583-198ef6cf99b6/mf-library-palette.png)

Default Material Functions are sorted into a wide range of categories. User-created Material Functions are placed in the **Misc** category by default, but you can change their categorization in the Details panel properties for the function. Drag a Material Function into your Material Graph, and a Material Function Call node is created, containing the various inputs and outputs defined by the input and output nodes within the function.

![Drag Material Function from Palette](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/268759f8-f37f-4850-b3ed-27f37bf3ca9a/drag-from-palette.png)

You can also add Material Functions to your Material by **right-clicking** in the Material Editor and searching for them in the context menu.

### Unspecified Function Node

A third way to use Material Functions is by placing an **Unspecified Function** node in your Material Graph, and then assigning a Material Function to it in the Details panel.

1.  Hold the **F key** and **left-click** in the Material Graph to place an Unspecified Function node.
    
    ![Unspecified Function node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8074ef92-36a2-4dfb-84ef-07cc8d972d9c/unspecified-function.png)
2.  Assign a Material Function to the Unspecified Function node in the **Details** panel. You can search for a Material Function in the dropdown menu in the Details Panel, or you can select a Material Function asset in the **Content Browser** and click the **Use Selected Asset from Content Browser** button.
    
    ![Use selected asset from Content Browser](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/192defd2-ea88-462d-ac14-ac1663ef0b9d/use-selected-asset.png)
3.  The Unspecified Function node is replaced by the selected Material Function – Blend Angle Corrected Normals in this example.
    
    ![Blend angle corrected normals node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/406ea4c3-a799-492b-86dc-b18e170050c0/blend-angle-corrected.png)