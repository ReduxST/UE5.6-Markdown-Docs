# Material Attributes Expressions

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/material-attributes-expressions-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/material-attributes-expressions-in-unreal-engine)  
**Processed:** 2025-06-14 16:35:07

---

## Make Material Attributes

The **Make Material Attributes** node allows you to define any of the standard Material attributes found on the [Main Material Node](/documentation/en-us/unreal-engine/using-the-main-material-node-in-unreal-engine), bundle them together, and pass them along through a single output. This is useful when creating [Layered Materials](/documentation/en-us/unreal-engine/creating-layered-materials-in-unreal-engine), as it allows you to define an entire Material within a Material Function and then utilize that data in a parent Material. You can also use it in complex Material setups in which you want to define multiple Material types and blend them together, all within one Material asset.

When connecting a Make Material Attributes node to a Material, you must make sure that the Use Material Attributes option is set to true (checked) in the Material properties. This will collapse the Main Material Node down to a single input, which accepts the incoming data from a Make Material Attributes node.

![Use Material Attributes option](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/dec3b9cc-c42b-40ee-b34f-39b655f1d706/use-material-attributes.png)

Make Material Attributes is superseded by the [Set Material Attributes](/documentation/en-us/unreal-engine/material-attributes-expressions-in-unreal-engine#setmaterialattributes) node, and in most cases you should use that instead.

## Set Material Attributes

The **Set Material Attributes** expression serves the same purpose as Make Material Attributes. It allows you to define a set of Material Attributes, and pass them along as bundled data through a single wire.

Unlike the Make Material Attributes node, which displays all standard Material Attributes by default, the inputs that appear on the Set Material Attributes node are user-defined in the **Details panel**. This allows you to incorporate only the Material Attributes that you need.

![Set Material Attributes array](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9886b6ef-7b2a-4b00-a6a5-b1cced77412d/set-material-attributes.png)

For example, the Material Function shown below only requires four attributes — **Base Color, Metallic, Roughness, and Normal**. Using the Set Material Attributes expression instead of Make Material Attributes takes up less space and results in a more concise Material Graph.

In most cases, Set Material Attributes is preferred to Make Material Attributes.

The only drawback is that the node is not context sensitive, meaning the user must know which attributes they need to add to the array for various combinations of Blend Mode and Shading Model. If you are unsure, you can use the Make Material Attributes node, which contains all necessary inputs.

## Break Material Attributes

The **Break Material Attributes** expression splits up an incoming set of Material Attributes, and outputs each individual attribute through a separate pin.

This is useful when creating [Layered Materials](/documentation/en-us/unreal-engine/layering-materials-in-unreal-engine), because it allows you to access the individual attributes within a Material Layer function. This enables you choose which attributes you want to plug into the Main Material node, and gives you the ability to selectively modify the attributes with additional logic in the Material Graph.

In the example above, Break Material Attributes is used to split up the attributes from a generic chrome Material Layer Function. The Metallic, Specular, Roughness and Normal attributes are passed into the Main Material Node unchanged, but the Base Color attribute is not used. Instead, a Vector 3 parameter is added to the Roughness texture and this result is passed into the Base Color input.

## Get Material Attributes

**Get Material Attributes** performs the same task as Break Material Attributes, but offers significant workflow benefits. Instead of fully breaking apart the incoming Material Attributes, Get Material Attributes allows you to pull out only the attributes you need. Select the node and then click the **Add Element** icon in the **Details Panel** to add output pins.

![Get Material Attributes details properties](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/aebb0e8a-73a2-4d29-a1cf-6c93fb233f10/get-material-attributes-array.png)

You can use the dropdown menus to define which Material Attribute is targeted by each array element.

![Change array elements on Get Material Attributes node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/960f0cc1-6e83-49e9-b98d-e06f497e6561/get-attributes-change-outputs.png)

The Material shown below recreates the tinted chrome example from the [Break Material Attributes](/documentation/en-us/unreal-engine/material-attributes-expressions-in-unreal-engine#breakmaterialattributes) section, but uses the Get and Set Material Attributes expressions instead. Note that the graph is cleaner and requires fewer wires.

In this case, only the Roughness data is broken out of the Material Attributes. A tint parameter is then added to the Roughness map to create some surface variation and the result is passed into Base Color with a [Set Material Attributes](/documentation/en-us/unreal-engine/material-attributes-expressions-in-unreal-engine#setmaterialattributes) node. The rest of the Material Attributes simply pass through unmodified.

![Material Attributes output pin](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e2ca9164-01f6-4b2e-bcbd-e890395895f0/material-attributes-passthrough.png)

## Blend Material Attributes

The **Blend Material Attributes** expression takes two sets of Material Attributes, and blends them together using per-pixel operations defined in the Alpha input.

For example, this Material Layer Blend takes a top and bottom set of Material Attributes, and blends between them using a mask texture.

Click image to enlarge.