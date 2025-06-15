# Destruction Quick Start

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/destruction-quick-start](https://dev.epicgames.com/documentation/en-us/unreal-engine/destruction-quick-start)  
**Processed:** 2025-06-14 16:20:01

---

You can find similar information in video format in the Developer Community site by watching the [Chaos Destruction Overview](https://dev.epicgames.com/community/learning/tutorials/BbX7/chaos-destruction-overview) tutorial.

## 1 - Required Setup

1.  Create a new project and select the **Games** category and the **First Person** template. Enter your project's name and click **Create**.
    
    Click for full view.
    
2.  In the editor, click **File > New Level**. Select the **Basic** template and click **Create**. Save the level.
    
    ![Create a new level and select the Basic template](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/92dd7100-ae99-4e72-b86e-7f8970f66002/destruction-setup-4.png)

### Section Results

In this section, you created a new project and set it up so you can add a Static Mesh which can be fractured in the next section of this guide.

## 2 - Creating the Geometry Collection

Destruction within the Chaos system starts with a new kind of asset called a **Geometry Collection**. These assets can be built from one or more Static Meshes, including those gathered together in Blueprints or even nested Blueprints.

Once you have a Geometry Collection, you can break it apart using the **Fracture Mode** and define the settings that determine how it breaks apart.

In this section you will create a Geometry Collection from a Static Mesh actor.

1.  Add a Static Mesh to the level which you'll use to create a fractured mesh. In this example, I'm using the Chaos Primitive Box included in the [Content Examples](https://www.fab.com/listings/0281d63e-71f7-4e07-a344-5fa721ac4d35) project available in Fab.
    
    Click for full view.
    
2.  Click the **Mode** dropdown and select **Fracture**.
    
    ![Select the Fracture mode from the Select Mode dropdown](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/be52d3d0-33a0-4ad9-8ce6-80538ec12c4b/destruction-quickstart-2.png)
    
    This will open the **Fracture Mode** windows that contain all the tools for fracturing your mesh. Alternatively, you can press **Shift-6** to switch to the Fracture Mode.
    
    Click for full view.
    
3.  Go to the **Generate** section and click **New** to create a new **Geometry Collection**. This new asset type will be saved in the **Content Browser** and will be used to create your fractured mesh.
    
    ![Click New to create a new Geometry Collection](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/93027ed4-3e83-4b4b-b40e-d326f36f4842/destruction-quickstart-3.png)
    1.  Select the **directory location** where the Geometry Collection will be saved.
        
    2.  Enter the name for the Geometry Collection asset.
        
    3.  Click **Create Geometry Collection**.
        
        ![Select the directory location, enter a name for your asset and click Create Geometry Collection](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/30519194-5e03-4cff-b2f9-4e00765f27d4/destruction-quickstart-4.png)
    4.  Click **Save All** in the **Content Browser** to save the new Geometry Collection asset.
        
        ![Click Save All in the Content Browser to save the new Geometry Collection asset](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e2048898-c434-46f6-a06e-b3c681f064a0/destruction-quickstart-4b.png)
4.  The Static Mesh will be replaced with the Geometry Collection in the level. In the **Fracture Hierarchy** window you will see that the Geometry Collection has a single node in the hierarchy.
    
    This means that the Geometry Collection is composed of only one piece (single node). As you fracture your Geometry Collection, you will see each fractured piece represented as a separate leaf (child) node in the hierarchy. This hierarchy represents how the entire object was fractured, from a single solid piece to individual pieces that can break off as strain is applied.
    
    ![The Static Mesh will be replaced with the Geometry Collection in the level](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9cca7979-7754-4b90-9a54-7c7bf3821f41/destruction-quickstart-5.png)
    
    Click for full view.
    

### Section Results

In this section you learned how to create a Geometry Collection from a Static Mesh actor. You also learned how to enable the Fracture Mode in the editor and view a Geometry Collection's Fracture Hierarchy.

In the next section you will learn how to fracture the Geometry Collection.

## 3 - Fracturing the Geometry Collection

There are several different types of fracture methods available. Combining the different techniques may lead to more interesting-looking destruction. You will have to experiment with the different options and settings to achieve your desired results.

In this guide you will learn about the standard **Uniform Voronoi** method. With this method you define a minimum and maximum number of sites to create cell volumes for fracturing.

1.  Go to the **Fracture** section and click the **Uniform** fracture button.
    
    ![Click the Uniform fracture button](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cfc21321-5b3c-4da1-93d7-0895099f7636/destruction-quickstart-7.png)
2.  Leave the default settings as they appear and click **Fracture**.
    
    ![Click Fracture](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/df69e336-9983-4148-9a9f-8e251d37b71e/destruction-quickstart-8.png)
3.  The Geometry Collection is now fractured and you can see the newly created nodes (fractured pieces) in the **Fracture Hierarchy** window. For this example, you created 20 nodes.
    
    Click for full view.
    
4.  You can see the current fracture hierarchy by going to the **Level Statistics** window. In this example, Level 0 has 1 piece, and Level 1 has 20 pieces. If you continue to further fracture the Geometry Collection, the new structure will be reflected in this window.
    
    Click for full view.
    
5.  You can preview how the Geometry Collection will fracture by changing the value of the **Explode Amount** field inside the **Fracture** window.
    
    Click for full view.
    
6.  In the example below, you can see the results of changing the value from 0 to 1 in the field.
    
    ![Change the Explode Amount to preview how the Geometry Collection will fracture](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/74846f11-14e9-4e8b-b4bb-44efde883fc0/destruction-quickstart-explosion.gif)
7.  Select the **Geometry Collection** and move it above the ground. Click the **Play Mode options** button and select **Simulate** or **Selected Viewport** to see the results.
    
    ![Click Simulate from the Play Modes option menu](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a4469ea1-7859-4841-aa09-03de847b6be8/destruction-quickstart-12.png)
8.  Below you can see the result of the performed steps.
    
    ![The box falls to the ground and fractures on impact](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9935fa9b-3527-4077-a332-1a36118ea0fc/destruction-quickstart-fall.gif)

### Section Results

In this section you learned how to use the **Fracture Mode** to fracture a Geometry Collection by using the standard Uniform Voronoi method.

In the next section you will learn how you can destroy the Geometry Collection by shooting it.

## 4 - Destroying the Geometry Collection by shooting it

In this section you will use the First Person Rifle Blueprint that comes with the template to shoot and destroy the Geometry Collection you created.

The fractured pieces of a Geometry Collection break apart when enough strain is applied to its **Connection Graph** (how the fractured pieces are connected to one another).

The most common way to apply strain to a Geometry Collection is by using a [Physics Field](/documentation/en-us/unreal-engine/physics-fields-in-unreal-engine). In this example, you will use a pre-built **Master Field** that comes with Unreal Engine by default. You will spawn this Field at the projectile's impact location, and the Field will cause the Geometry Collection's pieces to break apart.

1.  In the **Content Browser** go to **FirstPerson > Blueprints** and drag **BP\_Rifle** to the level. During gameplay you can pick up the rifle and shoot by using the left mouse button.
    
    Click for full view.
    
2.  In the same folder, double-click **BP\_FirstPersonProjectile** to open it. In the **Event Graph**, select all the nodes except **Event Hit** and delete them.
    
    Click for full view.
    
3.  Drag from the **Event Hit** node and search for then select **Spawn Actor from Class**.
    
    ![Drag from the Event Hit node and search for then select Spawn Actor from Class](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8404f4d3-489b-493f-b814-fdbef511246d/destruction-quickstart-15.png)
    1.  Click the **Class** dropdown of the **Spawn Actor** node and search for then select **FS\_MasterField**.
        
        ![Click the Class dropdown of the Spawn Actor node and search for then select FS_MasterField](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7efab3a8-ec4b-4932-8bc2-324af13dc7b6/destruction-quickstart-16.png)
    2.  Drag from the **Spawn Transform** pin of the **Spawn Actor** node and select **Make Transform**.
        
        ![Drag from the Spawn Transform pin of the Spawn Actor node and select Make Transform](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c9ff849c-f5fa-46f0-80ec-a9d1673525b4/destruction-quickstart-17.png)
    3.  Connect the **Hit Location** pin of the **Event Hit** node to the **Location** pin of the **Make Transform** node.
        
        ![Connect the Hit Location pin of the Event Hit node to the Location pin of the Make Transform node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/90bc8e89-177f-4edf-9f9e-63c4aeca449d/destruction-quickstart-18.png)
4.  Drag from the **Return Value** pin of the **Spawn Actor** node and search for then select **Set Activation Type**.
    
    ![Drag from the Return Value pin of the Spawn Actor node and search for then select Set Activation Type](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/dde5f6fb-f4d1-45df-9316-03134be8f684/destruction-quickstart-19.png)
    1.  Connect the **Spawn Actor** node to the **Activation Type** node.
        
    2.  Click the **Activation Type** dropdown and select **Trigger**. This will set the Master Field to activate when triggered.
        
        ![Click the Activation Type dropdown and select Trigger](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/50fbb296-ed2a-401d-8efb-3139d4c9aa98/destruction-quickstart-20.png)
5.  Drag from the **Return Value** pin of the **Spawn Actor** node and search for then select **CE Trigger**.
    
    ![Drag from the Return Value pin of the Spawn Actor node and search for then select CE Trigger](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cd553755-41e8-475a-bd01-2ea2ff407a69/destruction-quickstart-21.png)
6.  Connect the **Activation Type** node to the **CE Trigger** node. The **CE Trigger** node immediately activates the Master Field.
    
    Click for full view.
    
7.  Drag from the **CE Trigger** node and search for then select **Delay**.
    
    ![Drag from the CE Trigger node and search for then select Delay](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7af6bad7-6ce9-4217-8cb6-e9035480b138/destruction-quickstart-23.png)
8.  Drag from the **Delay** node and search for then select **Destroy Actor**. This will destroy the projectile after a brief delay on impact.
    
    ![Drag from the Delay node and search for then select Destroy Actor](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/63ba0a96-443f-4c29-95ce-0a0aca5cbffd/destruction-quickstart-24.png)
9.  Your complited Blueprint Script should look as following:
    
    Click for full view.
    
10.  Go back to **Fracture Mode** and select the Geometry Collection. Press **Shift-B** to toggle the bone colors of the Geometry Collection so you can see the box materials.
    
    ![Press shift B to toggle the bone colors](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c9397e55-27cb-4ea9-b5ed-aa29d81b59af/destruction-quickstart-26.png)
11.  Press **Play** and move to the rifle to pick it up. Use the left mouse button to shoot a projectile at the Geometry Collection and destroy it
    
    ![Use the left mouse button to shoot a projectile at the Geometry Collection and destroy it](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1d0d33fa-9d0e-4635-99e2-683eead98ce9/destruction-quickstart-shoot.gif)

### Section Results

In this section you learned how to spawn a Physics Field that applies strain to a Geometry Collection, causing it to break apart.

## 5 - On Your Own!

Now that you know how to create and fracture a Geometry Collection, you can take what you've learned and apply it to more complex examples.

Here are some additional examples you might want to try:

-   Use several Static Meshes to create a more complex Geometry Collection.
-   Create more fracture levels and use different fracturing methods to create more interesting destruction patterns.
-   Build a more complex structure by combining several Geometry Collections and destroy them by shooting them.

![Geometry Collection with different types of fracture methods](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6750a9dd-9383-4389-b964-3feafddacac2/destruction-quickstart-27.png)

## Next Steps

You can learn more about the Fracture Mode and the Destruction system by reading the Key Concepts documentation or watching the [Chaos Destruction video tutorials](/documentation/en-us/unreal-engine/physics-fields-in-unreal-engine) in the Developer Community site.