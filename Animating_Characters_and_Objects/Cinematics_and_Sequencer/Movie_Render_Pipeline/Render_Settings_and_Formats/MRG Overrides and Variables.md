# MRG Overrides and Variables

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/mrg-overrides-and-variables-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/mrg-overrides-and-variables-in-unreal-engine)  
**Processed:** 2025-06-14 16:37:21

---

## Settings Override

Each node has its own set of applicable parameters.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9865b2fb-fae2-4db0-8d53-fb091676c550/image_0.png)

To change or override the default settings just enable the checkbox and update the new desired values. Keeping in line with how the rest of the engine works, overridden parameters have a return arrow next to them that resets the parameter back to the class-default.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2723f00b-dc4d-4e18-89dc-2ab1f0e09160/image_1.png)

Full nodes can easily be overwritten and redeclared in the render graph. Remember how the evaluation of the graph flows back from the Output to the Input , or right to left. This means that whole nodes can be redeclared further down the graph.

In this simple example, we have the default Warm Up settings node. If we evaluate the graph we can see its end effect.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d2dc756a-dcec-4578-b247-686a8e3ed5e2/image_2.png)

Now if we add a second Warmup Settings node downstream and set some different values we see that those have been fully redeclared in the Graph Evaluation debug.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8eff0818-0e45-4fe9-89df-533c7bbdc695/image_3.png)

This also works "per chain".

This works with Subgraphs as well. In this example the default Warm Up node is in the subgraph. When we evaluate the graph we see that the parent graph is inheriting the warm up settings from the subgraph.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f2a6eecf-7397-4893-b7e7-bc431e52ca74/image_4.png)

But we can override that down stream.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/92dab3c1-7946-41c1-9c28-409788b264ed/image_5.png)

You can even re-declare collection membership per chain.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8daa1e4d-a438-4663-ab27-70d7eaa6ce5c/image_6.png)

You can also create new collections, change the renderer and re-declare modifiers making this notion of graph flow evaluation incredibly editable and flexible.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8388cd37-6a3b-402e-b3d7-cd2db4874f48/image_7.png)

## Exposing Parameters and Variables

Right clicking over a node will show you what is available to expose as a variable.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2fc63fdf-6de4-445d-a59a-d7d67d8a80f3/image_8.png)

When a property is selected its pin is exposed.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/aaf723bd-2e79-4513-ba19-b9889e38b3c9/image_9.png)

If you hover over the pin it will tell you the data type.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/46e996b0-ef34-4f26-8066-30a29e78a354/image_10.png)

You can create your own variable by hitting the plus icon under the Variables sections in the Members tab. Then set the name of the variable as well as the type and default value.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fdf1fd20-bded-4e16-a0eb-9d3aa2d9e7fb/image_11.png)

Then just drag the variable into the graph and connect it to the applicable pin.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/84ae1198-bb37-498c-ad9b-2595ba431fb0/image_12.png)

Alternatively you can Right Mouse Click over the desired pin and select Promote to Variable.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/35541a46-329a-4b22-b63e-5b8a5961304b/image_13.png)

A variable of the correct data type will be created and connected for you. You can then edit the name and the default values in the details panel.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/471247b9-ae21-49d6-b944-baee18da76fd/image_14.png)

Once you have an exposed variable these parameters can now be set on the job level in Movie Render Queue if desired when the graph is assigned.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/653bcced-2cdc-42a5-8409-0a7f43ae4424/image_15.png)

Just like with the graph nodes to override the parameter on the MRQ job level just enable the checkbox and set the desired parameter setting.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5c5a5ae7-8477-44b9-8865-03d3c6fd1025/image_16.png)