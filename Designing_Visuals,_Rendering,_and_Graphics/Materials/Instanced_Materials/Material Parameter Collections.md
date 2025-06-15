# Material Parameter Collections

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/using-material-parameter-collections-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/using-material-parameter-collections-in-unreal-engine)  
**Processed:** 2025-06-14 16:59:49

---

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a48052f4-3c85-49a8-b43f-e2ee94c87664/globalparams1.jpg)

A **MaterialParameterCollection** is an asset that stores an arbitrary set of [scalar and vector parameters](/documentation/en-us/unreal-engine/creating-and-using-material-instances-in-unreal-engine) which you can reference in an Material. It is a powerful tool that artists can use to pass global data into multiple Materials at once. You can also use Material Parameter Collections to drive per-level effects, such as snow amount, destruction amount, wetness, and so on, which would otherwise require setting individual parameter values within many different Material Instances in your Level.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f7402073-920c-4e79-95c6-552fe83076af/globalparams1.png) ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e731c7a3-fccd-4543-bde9-63f5537d3820/globalparams2.png)

In the example above, global parameters stored in a Material Parameter Collection are used to control the following aspects of the scene.

-   The flower morph states along with the speed and strength of the wind.
-   The player's position is tracked and fed into the foliage. That position information is used to move the flowers and grass away from the player as they walk nearby.
-   The sun angle and color is also tracked and used to correctly colorize the water crests and limit the effect to only times when light shines directly through the wave crests (when the player is looking toward the sun).
-   The coloration of effect across the time of day and overall diffuse lighting color for the water are also being controlled.

## Creating and Editing Material Parameter Collections

MaterialParameterCollections are a discrete asset type created in the [Content Browser](/documentation/en-us/unreal-engine/content-browser-in-unreal-engine). Use the following steps to create a MaterialParameterCollection and add a parameter.

1.  **Right-click** in the Content Browser, and expand the **Material** subcategory in the Create Advanced Asset section. Select **MaterialParameterCollection** in the context menu.
    
    ![Create new MaterialParameterCollection](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/86ee2fcb-1fc3-4b36-bbfb-b102b5d07209/create-mpc.png)
2.  Rename the MaterialParameterCollection asset to describe the types of parameters it will contain. This example uses the name **MPC\_GlobalParams**. **Double-click** the asset to edit the MaterialParameterCollection.
    
    ![Rename Material Parameter Collection](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cfef1bd5-fda7-4962-a2a8-cec71af1ec29/rename-mpc.png)
3.  A new window opens displaying the **Scalar** and **Vector Parameters** contained within the MaterialParameterCollection.
    
    ![Open Material Parameter Collection](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c02d8535-66bc-4b79-94a6-9e7886d88701/mpc-details-panel.png)
4.  To add parameters to the collection, click the **Add Element** (+) icon in either the Scalar or Vector Parameter section. For this example, add a **Scalar Parameter**. Name it **GlobalEmissivePower** and change the default value to **1.0**.
    
    ![Add Scalar Parameter to MPC](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f9072ed1-2b70-4284-b242-1e98d39db92c/add-scalar-param.png)
5.  Add any additional Scalar or Vector Parameters as needed. A single Material Parameter Collection can hold up to 1024 Scalar Parameters and 1024 Vector Parameters.
    

## Using Material Parameter Collections in Materials

You can now use the parameters in your MaterialParameterCollection to define the attributes in your Materials. One of the main benefits of Material Parameter Collections is that the parameter values are stored in a separate asset from the Materials themselves. This means you can reference a Material Parameter Collection in as many Materials as you want, and when you change the values in the Material Parameter Collection, it automatically affects every Material that references it.

Use the following steps to reference your Material Parameter Collection in a base Material.

1.  **Right-click** in the Content Browser and click **Material** in the Create Basic Asset section of the context menu. Give the Material a descriptive name.
    
    ![Create new Material](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f042dcf4-1b8c-44b5-b281-90c74acf43ca/create-material.png)
2.  In the Content Browser you should now have a Material, as well as the MaterialParameterCollection you created in the previous section. **Double-click** the **Material** to open it in the Material Editor.
    
    ![Material and MPC in Content Browser](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/99827e3d-ff09-48a0-b95c-d36c581c7448/mpc-and-material-assets.png)
3.  This Material will be a simple emissive surface that uses a Fresnel expression to make the Material glow slightly brighter around the edges. Add the following Material Expression nodes to your Material Graph.
    
    | Material Expression Type | Name | Default Value |
    | --- | --- | --- |
    | Vector Parameter | Base Color | 1,0,0,0 |
    | Vector Parameter | Emissive Color | 0.1,0.01,0.14,0 |
    | Multiply - x2 | n/a | n/a |
    | Fresnel | n/a | n/a |
    
    Connect the Material Expressions as shown in the image below.
    
    ![Emissive starting Material Graph](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b3bde554-0ee4-4b27-a09b-5b0f0c0d7136/emissive-starting-graph.png)
4.  Select the **Fresnel** node in the Material Graph. In the Details Panel set the **Exponent** to **6** and the **Base Reflect Fraction** to **0.1**. These properties control the falloff of the rim lighting effect. Experiment with a higher or lower **Exponent** to influence how much of the surface is affected by the Fresnel node.
    
    ![Fresnel Material Expression properties](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cf81c358-c584-45e7-bd17-456d2c663861/fresnel-settings.png)
5.  **Right-click** in the Material Graph and search for "collection" and add a **CollectionParameter** to your graph. This node is used to bring infromation from your MaterialParameterCollection into the Material Graph.
    
    ![Unspecified Collection Parameter](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3daa1ebb-b80e-4571-8ba3-ad33a6a43283/collection-parameter.png)
6.  Select the **Collection Parameter** node in the Material Graph. In the Details Panel, use the **Collection** drop-down menu to select the **MPC\_GlobalParameters** collection you created earlier.
    
    ![Select Material parameter Collection](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fed5949a-71c0-42ff-8213-2d1ca624f4d9/select-parameter-collection.png)
7.  Use the **Parameter Name** drop-down menu to select the **EmissivePower** parameter.
    
    ![Select Emissive Power parameter](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/550b5e8a-1f9b-4804-bb23-2adfc1e04094/select-parameter.png)
8.  Connect the **'EmissivePower'** node to the open **B** input on the Multiply node as pictured below.
    
    ![Select Emissive Power parameter](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2002a155-e89e-4628-98ec-a55d57f9c1cd/final-mpc-graph.png)
9.  Click **Save** in the Material Editor Toolbar to compile and save the Material. After saving the asset you can close the Material Editor.
    
    ![Save Material Asset](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/be0306fb-c5e6-4616-a071-a2cd5d021837/save-and-compile.png)

## Testing the Material Parameter Collection

To demonstrate the Material Collection Parameter's usefulness in controlling the attributes of multiple Materials, you can create one or more Material Instances and apply them to different objects in the scene.

1.  **Right-click** your base Material and choose **Create Material Instance** from the context menu.
    
    ![Create a Material Instance](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ff42d4b0-b368-4e66-a3a6-9a5a402200b8/create-material-instance.png)
2.  Apply the base Material and the Material Instance to two different objects in your level. You can change the Base Color and Emissive Color parameters in the Material Instance so you can tell the two apart.
    
    ![Apply Materials to objects in level](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/83e2ccc6-eb5a-4861-81ef-aa7914d2d8d6/apply-materials-in-level.png)
3.  Now when you open the Material Parameter Collection and change the **EmissivePower** value, the new value will immediately propagate to both the base Material and the Material Instance.
    

## Updating Material Parameters Collections Through Blueprints

You can also interact with Material Parameter Collections through Blueprints. This is an extremely powerful tool, as it means players can manipulate the appearance of a Material during game play. The example below demonstrates how to change the **EmissivePower** of the two Materials in response to a keystroke. At runtime, pressing the **B** key will make the emissive value brighter, and pressing the **D** key will make it dimmer. Releasing either key sets the parameter back to its original value of **1**.

1.  In the toolbar above the main Editor viewport, expand the **Blueprints** drop-down menu, and select **Open Level Blueprint** from the list.
    
    ![Open Level Blueprint](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1dbfdcba-1586-42be-9b53-df334d45041b/open-level-blueprint.png)
2.  **Right-click** in the Level Blueprint and search for **keyboard event**. Add a **B** Keyboard Event from the context menu. Repeat this action and add a **D** Keyboard Event.
    
    ![B and D Keyboard Event nodes](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5e15e761-6dc9-420d-af15-cb0ccb55af22/keyboard-event-nodes.png)
3.  **Right-click** in the Level Blueprint and add a **Set Scalar Parameter Value** node to the Blueprint. Use the **Collection** drop-down menu to reference your **\*MPC\_GlobalParams** Material Parameter Collection.
    
    ![Collection drop-down menu](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1ffd83c8-70c0-4d40-9c96-e7187b4197bd/collection-drop-down.png)
    
    Use the **Parameter** drop-down to reference the **EmissivePower** Parameter.
    
    ![Emissive Power Parameter](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ef34ee28-52de-4fc1-814a-1e2d5b51c219/emissive-power-variable.png)
4.  Duplicate the **Set Scalar Parameter Value Node** twice, so you have three copies in your Blueprint. Wire up the nodes so your Blueprint Graph looks like the image below. The **Pressed** output on the **B and D** Keyboard Event nodes should connect to the input on the first and third **Set Scalar Parameter Value** nodes. The **Released** outputs on both Keyboard Event nodes should connect to input on the second **Set Scalar Parameter Value** node.
    
    ![Blueprint Graph completed](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/16efb841-eaed-488e-9a4b-d8206b983c5c/blueprint-wired.png)
5.  The final step is to set a **Parameter Value** for the **EmissivePower** in response to each Keyboard Event. In this example, when the **B** key is pressed, the **EmissivePower** increases to **50**. When the **D** key is pressed the **Emissive Power** decreases to **0.05**. When both keys are released, the Parameter is set to its original value of **1**.
    
    ![EmissivePower values](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5ba09745-e0f8-49ff-aa92-ef70cbe442bf/emissive-power-values.png)
6.  Click **Compile** in Blueprint Editor toolbar to compile the Level Blueprint. You can now test the changes in-game.
    
7.  Click the **Play in Editor** icon in the Editor toolbar, and test the Blueprint by pressing and releasing the **B** and **D** keys. The results are shown in the video below.
    

## Limitations and Performance Characteristics

A Material can reference, at most, two different MaterialParameterCollections. One is typically used for game-wide values while the other can be used for level specific parameters. A collection can have up to 1024 scalar parameters and 1024 vector parameters.

Modifying the number of parameters in a collection will cause a recompile of all Materials that reference that collection. If you need to add numerous parameters, it can be faster to add a lot of parameters up front in an empty map.

If you rename a parameter, any Materials referencing that parameter will continue to work as expected. However, any Blueprint referencing that parameter will now be broken. You must reassign the ParameterName of the Blueprint function which operates on the collection to fix this.

Updating values in a MaterialParameterCollection is much more efficient than setting many different parameters on various Material instances.