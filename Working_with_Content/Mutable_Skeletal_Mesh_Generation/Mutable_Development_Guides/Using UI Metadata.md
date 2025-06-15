# Using UI Metadata

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/using-ui-metadata-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/using-ui-metadata-in-unreal-engine)  
**Processed:** 2025-06-14 17:02:23

---

You can use the following document to learn about how to use UI Metadata with Mutable Characters.

## UI Metadata

All parameter and state nodes have a **UI** section section of properties in the **Details** panel. In this section, you can specify extra information for each parameter and parameter option. This information is available in-game. UI metadata is commonly used to help generate the in-game UI.

![UI section of details panel of parameter nodes in mutable character blueprint](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/16bd4d2d-5aba-4d00-8ade-a798cc129938/image_0.png)

Here you can reference a list of the properties found in this section, with a description of their functionality:

| Property | Description |
| --- | --- |
| **Minimum & Maximum Values** | In these properties you can set two numerical scalar values that can be used as the minimum and maximum values for the node. |
| **Editor Gameplay Tags** | 
This is an **Editor Only** variable, which means that it is not available in-game.

Using this property you can add tags to parameters and parameter options. Then, from the **Preview Instance** tab, you can filter parameter options that contain any or all the specified tags.

![gameplay tag filter property](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/aee2c13d-613f-4bd8-8cdd-a4237f704c5f/image_1.png)

 |
| **Object Friendly & UI Section Names** | Here you can set object friendly and UI Section names. |
| **UI Order** | Here you can set an order for the UI element using an integer value. |
| **UI Thumbnail** | Here you can set a UI Thumbnail image. |
| **Editor UIThumbnail Object** | 

This is an **Editor Only** variable, which means that it is not available in-game.

You can use this property to set a thumbnail for a parameter option in the **Instance Properties** tab when the `UI Thumbnails` property is also enabled. You can set any type of asset that has a UE thumbnail.

![ui thumbnails property](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6af6304e-2269-4d13-85e5-fbd28c40b887/image_2.png)

 |
| **Extra Information** | 

This option is a Map that you can use to add extra String information with a specifier.

![extra information property](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/743c8c16-e143-4c67-841d-e36ebf7eb010/image_3.png)

 |
| **Extra Assets** | 

This option is similar to the **Extra Information** property that you can use to add extra asset information with a specifier.

![extra information property](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a5165301-982f-4cfe-b114-540ff5e5fbff/image_4.png)

 |

## UI Metadata API

The UI Metadata is stored inside the CO, which you can access using the following methods:

-   **GetParameterUIMetadata**: This method returns the UI Metadata of the specified parameter.
    
-   **GetIntParameterOptionUIMetadata**: This method returns the UI Metadata of the specified parameter option.
    
-   **GetStateUIMetadata**: This method returns the UI Metadata of the specified state.
    

![ui metadata api methods](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/64908def-282b-46f5-9df7-60ff52f75e88/image_5.png)

## UI Metadata with Table Nodes

Parameters generated through a **Table** node can contain metadata as well. You can add metadata to these assets by adding a new variable to the **Data Table Structure** using the **Mutable Param UI Metadata** data type. Then, from the **Table** node’s **Properties** tab, you can specify which column of the Data Table will be used as UI Metadata for each parameter option.

![options ui metadata column property](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/dfbee9aa-0c5c-4491-bf83-e83aa13fcb41/image_6.png)

## Example of Usage

The perfect example to see how the UI Metadata works is the **Preview Instance** tab of the Customizable Object and Customizable Object Instance Editors.

In the editor, you can set the **Maximum Value** and **Minimum Value** options to determine the boundaries of the float parameters. In the following example, the value of the middle point changes depending on the Maximum and Minimum values.

![minimum and maximum value properties](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ca33e987-d2b7-45bd-b49f-ca0b1e6372df/image_7.png)

You can organize the parameters of the **Preview Instance** tab by specifying a **UI Section** for each parameter. After recompiling the Customizable Object and enabling the **UI Sections** property of the **Preview Instance**, all the parameters will be organized in their corresponding sections. Parameters that do not have a section specified will be assigned to a section called **Miscellaneous**.

![preview instance panel properties](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c2ab3ad2-c1c3-401b-9308-6e7f0d1c8d3d/image_8.png)

Another way to organize the parameters of the **Preview Instance** is by setting a value to the **UI Order** option. This setting organizes parameters by this value from low to high.

If you specify a Texture to the **UI Thumbnail** option or an UAsset to the **UI Thumbnail Editor** option, each parameter option will have a thumbnail next to the option name.

If there is a value in both options, the thumbnail that is shown is the Texture2D set to the **UI Thumbnail** option.

Finally, the Editor UI also has an example of how to use the `Extra Assets` map. If you add a new map entrance to a float parameter with the **Key** `SliderImage` and a UTexture2D asset, the slider of the float parameter will set that texture to the widget's background.

![extra assets property](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/79607298-5248-4c60-9555-39aaaa14289a/image_9.png)