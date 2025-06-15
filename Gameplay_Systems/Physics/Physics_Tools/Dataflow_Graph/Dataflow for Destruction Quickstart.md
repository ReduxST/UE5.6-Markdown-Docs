# Dataflow for Destruction Quickstart

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/dataflow-for-destruction-quickstart](https://dev.epicgames.com/documentation/en-us/unreal-engine/dataflow-for-destruction-quickstart)  
**Processed:** 2025-06-14 16:18:36

---

This quick start guide will teach you how to fracture a static mesh and destroy it by using Unreal’s [Dataflow graph system](/documentation/en-us/unreal-engine/dataflow-overview), instead of the traditional workflow which uses the Fracture mode in the editor.

Before reading this guide, please read the [Destruction Quick Start](/documentation/en-us/unreal-engine/destruction-quick-start) guide to learn how to destroy a static mesh using the traditional workflow. This guide will follow the same steps, but use Dataflow instead of the Fracture mode.

## 1 - Required Setup

1.  Create a new project and select the **Games** category and the **First Person** template. Enter your project's name and click **Create**.
    
    Click for full view.
    
2.  In the editor, click **File > New Level**. Select the **Basic** template and click **Create**. Save the level.
    
    ![Create a new level and use the Basic template](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5efccac4-34c8-4c14-a5ac-759221841e9f/destruction-setup-4.png)

### Section Results

In this section, you created a new project and set it up so you can add a static mesh which can be fractured in the next section of this guide.

## 2 - Creating the Geometry Collection

In this section you will create a Geometry Collection from a static mesh actor.

1.  Add a static mesh to the level which you'll use to create a fractured mesh. In this example, I'm using the **Chaos Primitive Box** included in the [Content Examples](https://www.fab.com/listings/0281d63e-71f7-4e07-a344-5fa721ac4d35) project available on Fab.
    
    Click for full view.
    
2.  Click the **Mode** dropdown and select **Fracture**.
    
    ![Click the Mode dropdown and select Fracture](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5f9772c7-7aca-442a-9892-22514547ce1d/dataflow-destruction-quickstart-2.png)
3.  Go to the **Generate** section and click **New** to create a new **Geometry Collection**.
    
    Click for full view.
    
4.  The **Select Path** window will open.
    
    -   (1) Select the **directory location** where the Geometry Collection will be saved.
    -   (2) Enter the **name** of the asset.
    -   (3) Click the **Dataflow** dropdown.
    
    ![Enter the directory location, name of the asset and click the Dataflow dropdown](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9cfdf98a-5c9a-42d2-9cc7-ba31679fb4df/dataflow-destruction-quickstart-4.png)
5.  Click **DataFlowAsset** under the **Create New Asset** category.
    
    ![Click DataFlowAsset under the Create New Asset category](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1012fd15-4045-4a65-9835-0794bf540783/dataflow-destruction-quickstart-5.png)
    
    -   (1) Select the directory location where the asset will be saved.
    -   (2) Enter the asset name.
    -   (3) Click Save.
    
    ![Select the directory location, asset name and click Save](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/36edf2ff-40b8-48c1-907d-f0271eed9c3c/dataflow-destruction-quickstart-6.png)
6.  Click **Create Geometry Collection** to create the **Geometry Collection** and a **Dataflow** asset.
    
    ![Click Create Geometry Collection](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/74d5c280-77e6-4754-a3fa-b7dac8df95ae/dataflow-destruction-quickstart-7.png) ![A Geometry Collection and Dataflow asset are created](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/06b42603-e1c3-479d-a6c5-21a036f62103/dataflow-destruction-quickstart-8.png)
7.  Click **Selection Mode > Selection** to go back to the **Selection** mode in the editor.
    
    -   Double click the **Geometry Collection** asset in the **Content Browser** to open it.
    -   In the **Geometry Collection** window you will see a **Dataflow Graph** panel where you can enter the Dataflow nodes to fracture the Geometry Collection.
    
    ![Click Selection Mode - Selection](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c0a1156f-de9d-461b-b0d0-7fc4911f7ab3/dataflow-destruction-quickstart-9.png)
    
    Click for full view.
    

### Section Results

In this section you learned how to create a Geometry Collection with a Dataflow asset associated with the collection.

In the next section you will learn how to fracture the Geometry Collection by creating a Dataflow node graph.

## 3 - Fracturing the Geometry Collection

1.  Right click on the **Dataflow** graph and search for then select **Static Mesh To Collection**.
    
    -   With the node selected, go to the **Asset Details** panel and scroll down to the **Asset** section.
    -   Click the **Static Mesh** dropdown and select the static mesh to convert to a Geometry Collection.
    
    ![Right click on the Dataflow graph and search for then select Static Mesh To Collection. Select the Static Mesh asset](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6bed8596-4328-47df-9741-97132dec3c75/dataflow-destruction-quickstart-11.png)
2.  Drag from the **Collection** pin of the **Static Mesh to Collection** node and search for then select **Bounding Box**.
    
    ![Add a Bounding Box node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/405b176f-fcbe-4069-ac36-753ec99008c0/dataflow-destruction-quickstart-12.png)
3.  Drag from the **Bounding Box** pin of the **Bounding Box** node and search for then select **Uniform Scatter Points**.
    
    -   Go to the **Scatter** section and enter **10** for the **Min** and **Max Number of Points**.
    
    ![Add a Uniform Scatter Points node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e507e381-04fc-4768-91b4-12f52d615852/dataflow-destruction-quickstart-13.png)
4.  Drag from the **Collection** pin of the **Static Mesh to Collection** node and search for then select **Voronoi Fracture**.
    
    -   Connect the **Points** pin from the **Uniform Scatter Points** node to the **Points** pin of the **Voronoi Fracture** node.
    
    ![Search for then select Voronoi Fracture](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/94f0b24e-53c5-4d32-9619-e71c98ee0190/dataflow-destruction-quickstart-14.png)
5.  Drag from the **Bounding Box** pin of the **Bounding Box** node and search for then select **Uniform Scatter Points**.
    
    -   Go to the **Scatter** section and enter **25** for the **Min** and **Max Number of Points**.
    -   Enter a **Random Seed** number.
    
    ![Add a Uniform Scatter Points node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/66323d0a-69b3-4066-bbc7-b0d93a631876/dataflow-destruction-quickstart-15.png)
6.  Drag from the **Collection** pin of the **Voronoi Fracture** node and search for then select **Voronoi Fracture**.
    
    -   Connect the **Points** pin of the **Uniform Scatter Point** node to the **Points** pin of the **Voronoi Fracture** node.
    
    ![Search for then select Voronoi Fracture](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7ea3cf9a-37d7-4b60-81e2-12c86e03e3b5/dataflow-destruction-quickstart-16.png)
7.  Drag from the **Collection** pin of the **Voronoi Fracture** node and search for then select **Auto Cluster**. Connect the **Transform Selection** pin of the **Voronoi Fracture** node to the **Transform Selection** pin of the **Auto Cluster** node.
    
    ![Add an Auto Cluster node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/635de593-ddf1-4704-b8bc-fbedf486270b/dataflow-destruction-quickstart-17.png)
8.  Drag from the **Collection** pin of the **Auto Cluster** node and search for then select **Geometry Collection Terminal**.
    
    -   Connect the **Material Instances** and **Instanced Meshes** pins from the **Static Mesh to Collection** node to the **Material Instances** and **Instanced Meshes** pins of the **Geometry Collection Terminal** node.
    
    ![Add a Geometry Collection Terminal node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5be843a4-7f5e-43d3-bf20-b1974aa6fb5f/dataflow-destruction-quickstart-18.png)
    
    Click for full view.
    
9.  Go to the **Damage** section and expand the **Damage Threshold** array.
    
    -   Enter **5000**, **500**, and **50** for the **damage amounts**.
    
    ![Enter 5000, 500, and 50 for the damage amounts](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cd5df979-8a8d-4908-b9b1-6dae0108b2f2/dataflow-destruction-quickstart-20.png)
10.  Drag the **Geometry Collection** from the **Content Browser** into the level and move it above the ground.
    
    -   Click the **Play Mode** options button and select **Simulate** or **Selected Viewport** to see the results.
    
    ![Click Simulate](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/85e64a42-0341-46f1-8eee-702fb5192ac4/dataflow-destruction-quickstart-21.png)
11.  Below you can see the Geometry Collection fracturing when it hits the ground.
    
    ![The Geometry Collection fractures when it hits the ground](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/25b9ee31-1cd6-4606-95b6-3a4724171da7/dataflow-destruction-quickstart-drop.gif)

### Section Results

In this section you learned how to fracture the Geometry Collection by creating a Dataflow node graph.

In the next section you will learn how to destroy the Geometry Collection by shooting it.

## 4 - Destroying the Geometry Collection by shooting it

In this section you will use the **First Person Rifle** Blueprint that comes with the template to shoot and destroy the Geometry Collection you created.

You will modify the projectile Blueprint to apply an external strain to the Geometry Collection and trigger the fracture.

1.  In the **Content Browser** go to **FirstPerson > Blueprints** and drag **BP\_Pickup\_Rifle** to the level. During gameplay you can pick up the rifle and shoot by using the left mouse button.
    
    ![Drag BP_Pickup_Rifle to the level](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/153da227-0c19-4b6a-be42-0c79499afc39/dataflow-destruction-quickstart-22.png)
2.  In the same folder, double-click **BP\_FirstPersonProjectile** to open it. In the **Event Graph**, select all the nodes except Event Hit and **delete** them.
    
    ![Open the BP_FirstPersonProjectile Blueprint and delete all the nodes except Event Hit](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ac6d5b39-e8f6-46e2-b1bc-a45455980a3e/dataflow-destruction-quickstart-23.png)
3.  Drag from the **Other Comp** pin of the **Event Hit** node and search for then select **Cast to Geometry Collection Component**.
    
    ![Add a Cast to Geometry Collection Component node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3b1263e0-ac47-4f46-94f8-6aa8f4e2128e/dataflow-destruction-quickstart-24.png)
4.  Drag from the **As Geometry Collection Component** pin of the **Geometry Collection Component** node and search for then select **Apply External Strain**.
    
    ![Add an Apply External Strain node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/590d5179-089b-4206-8ffe-118c123fe6e8/dataflow-destruction-quickstart-25.png)
5.  Drag from the **Hit** pin of the **Event Hit** node and search for then select **Break Hit**.
    
    -   Connect the **Location** and **Hit Item** pins of the **Break Hit Result** node to the **Location** and **Item Index** pins of the **Apply External Strain** node.
    -   Set the **Radius** to **100**, the **Propagation Depth** and **Propagation Factor** to **1**, and **Strain** to **50000**.
    
    ![Break the Hit results and connect the Location and Hit Item to the Apply External Strain node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4058dfed-36b9-4cde-8e65-ca4f8b974f5a/dataflow-destruction-quickstart-26.png)
6.  Drag from the **Apply External Strain** node and search for then select **Apply Linear Velocity**.
    
    -   Connect the **Hit Item** pin of the **Break Hit Result** node to the **Item Index** pin of the **Apply Linear Velocity** node.
    
    ![Add an Apply Linear Velocity node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/723a298a-cb0b-47ab-8e60-4aedfc31db46/dataflow-destruction-quickstart-27.png)
7.  Right click in the **Event Graph** and search for then select **Get Actor Forward Vector**.
    
    -   Drag from the **Return Value** pin of the **Get Actor Forward Vector** node and search for then select **multiply**.
    -   Connect the **Multiply** node to the **Linear Velocity** pin of the **Apply Linear Velocity** node.
    
    ![Add a Get Actor Forward Vector node and a multiply node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8782204d-118d-4624-8c9c-eb25a501e20b/dataflow-destruction-quickstart-28.png)
8.  Create a **Float** variable and name it **Linear Velocity**. Set its **default value** to **500**.
    
    ![Create a Float variable and name it Linear Velocity with a default value of 500](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4b00c75f-5e7e-4c3f-ace7-802a7695e289/dataflow-destruction-quickstart-29.png)
9.  Connect the **Linear Velocity** variable to the **Multiply** node.
    
    -   **Compile** and **Save**.
    
    Click for full view.
    
10.  Press **Play** and move to the rifle to pick it up. Use the left mouse button to shoot a projectile at the Geometry Collection and destroy it
    
    ![The projectile applies external strain to teh Geometry Collection on hit, fracturing it](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a7c30437-1d21-462c-ad8d-a5f2de32f61b/dataflow-destruction-quickstart-shoot.gif)

### Section Results

In this section you learned how to apply an external strain to the Geometry Collection when the projectile hits it.

## 5 - Modifying the Dataflow Graph

### Fracturing a Different Static Mesh

You can quickly change the static mesh used by the Dataflow graph to see how other meshes look when fractured the same way.

Select the **Static Mesh to Collection** node and change the **Static Mesh** in the **Asset** section.

### Changing the Point Pattern

You can change the scatter point pattern used by the fracture node by replacing the Uniform Scatter Points node with another pattern.

### Changing the Fracture Pattern

You can also experiment with different fracture patterns by replacing the fracture node used in the Dataflow graph.

### Section Results

In this section you learned how you can quickly modify the fractured Geometry Collection by changing the static mesh, point patterns, or fracture patterns in the Dataflow graph.

## 5 - On Your Own!

Now that you know how to generate and destroy Geometry Collections using Dataflow, try experimenting with different nodes and parameters to see how your results change.