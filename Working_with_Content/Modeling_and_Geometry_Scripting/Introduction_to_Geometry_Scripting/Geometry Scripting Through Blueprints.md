# Geometry Scripting Through Blueprints

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/geometry-scripting-through-blueprints-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/geometry-scripting-through-blueprints-in-unreal-engine)  
**Processed:** 2025-06-14 16:25:36

---

Geometry Scripting provides Blueprint and Python functions for creating custom modeling tools and workflows. This guide covers the fundamentals of using Geometry Scripting through Blueprints. The steps below go through generating a procedural mesh tool for level design, similar to the geometry tools created for the [Lyra sample project](/documentation/en-us/unreal-engine/lyra-geometry-tools-in-unreal-engine).

This guide shows you how to:

-   Generate procedural geometry for quick level blocking.
-   Use boolean operations to cut out a mesh dynamically.
-   Create a Static Mesh bake function.

The tool you develop is a small example of procedural mesh generation and tools you can create with Geometry Scripting. An advanced example is the **Procedural Content Generation Framework**, which uses Geometry Scripting as a base. To learn more about this toolset, see [Procedural Content Generation Overview](/documentation/en-us/unreal-engine/procedural-content-generation-overview).

Additional workflows you can create besides procedural generation include:

-   [Assigning multiple materials to assets](https://dev.epicgames.com/community/learning/tutorials/L6K/unreal-engine-ue5-0-geometry-script-assigning-materials-to-mesh-areas) .
-   [Applying mesh booleans with Python](https://dev.epicgames.com/community/learning/tutorials/D9x/unreal-engine-ue5-0-geometry-script-mesh-booleans-in-python).
-   [Generating Blocking Volumes based on convex hulls.](https://dev.epicgames.com/community/learning/tutorials/OO2/unreal-engine-ue5-0-geometry-script-convex-hull-blocking-volume-tool)

## Prerequisite Knowledge

To understand and use the content on this page, you must:

-   Have a fundamental understanding of [Blueprints](/documentation/en-us/unreal-engine/introduction-to-blueprints-visual-scripting-in-unreal-engine).
-   Be familiar with the introductory topic of [Geometry Scripting](/documentation/en-us/unreal-engine/geometry-scripting-users-guide-in-unreal-engine), specifically the new object types introduced.

This guide uses the [Third Person template](/documentation/en-us/unreal-engine/third-person-template-in-unreal-engine). However, you can use any project to follow along.

## Enabling Plugin

Using Geometry Scripting requires having the associated plugin enabled.

To enable the plugin or verify that it is already enabled, follow these steps:

1.  In the **[menu bar](/documentation/en-us/unreal-engine/level-editor-in-unreal-engine#menubar)**, select **Edit** > **Plugins**.
    
2.  In the search bar, type "geometry script".
    
    ![Enable Geometry Scripting Plugin](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/63cad38d-766f-4f92-8e59-d4a96797dc29/enable-plugin.png)
3.  Enable **Geometry Script** plugin, and select **Yes** in the dialog popup.
4.  Restart the engine.

## Creating a Blueprint Class

To get started, you must ensure you have the correct Blueprint class. Since the goal is to create a procedural mesh for level design, use the **GeneratedDynamicMeshActor** class.

To select a Blueprint class, follow these steps:

1.  In the **Content Browser**, right-click and select **Blueprint Class**.
2.  Search for and select **GeneratedDynamicMeshActor**.
    
    ![Generated Dynamic Mesh Actor Class](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f8e2cf57-f0d5-4e35-ac94-7632694a2a68/generated-dynamic-mesh-actor.png)
3.  Name the Blueprint **BP\_ProceduralGen**.

If you do not see **GeneratedDynamicMeshActor** as an option, the Geometry Scripting plugin is not enabled.

### Event Setup

After creating the class, you must set up the specific event to populate the Dynamic Mesh you will use for building your tool.

To create the event, follow these steps:

1.  In the Content Browser, double-click the Blueprint class.
2.  Open the **Event Graph**.
3.  Right-click in the graph, and type "generated mesh" to filter the available nodes, then select **Event on Rebuild Generated Mesh**. This event triggers every time you update the parameters of the Dynamic Mesh–causing the mesh to be rebuilt.
    
    ![Event Rebuild Generated Mesh](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5be7a635-d8f9-4f56-b045-ab031382320c/event-rebuild-generated-mesh.png)
4.  Promote the **Target Mesh** output to a local variable by right-clicking its pin and selecting **Promote to Variable**.
    
    ![Promote Pin to Variable](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e1afa1bf-a40a-497e-887a-17f01df1e25c/promote-target-mesh.png)
5.  Name the variable **DynamicMesh**, set the type to **Dynamic Mesh**, and keep it private. This variable represents the Dynamic Mesh you edit.

## Building Geometry

With the Blueprint class and event created, you can begin adding geometry scripting functions. The goal in this guide is to generate block-out shapes that you can transform and cut out. For that, you need first create the mesh you want to edit.

To create a mesh, follow these steps:

1.  Drag off the **DynamicMesh** variable's execution pin, then search and select the **Append Box** node. This adds a box primitive to the Dynamic Mesh.
2.  Connect the out pin of the **DynamicMesh** variable to the **Target Mesh** input pin.
    
    ![Dynamic Mesh Variable](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e9111f49-8d33-4397-89d5-a1c2ccd2fb31/append-box.png)

With these first few nodes, you have created a procedural mesh. You can test it by compiling and dragging the Blueprint into your Level. To learn what other shapes you can instantly make, see the [Primitive Generation](/documentation/404) section of the Geometry Scripting Reference document.

### Adding Transformation Widget

In order to be able to dynamically adjust the transformation of your mesh, you can add interactive controls.

To add interactive controls, follow these steps:

1.  Create a new public variable called **BoxSize** and set the type to Vector.
    
    ![BoxSize Variable](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a7ba8537-afdb-47c1-b4ce-9399ad6d331e/box-size-variable.png)
2.  In the **Details** panel of this variable, enable **Instance Editable** and **Show 3D widget**. Set the **Default Value** to 200, 200, 200. Enabling the 3D widget creates a manipulator for interactively controlling the X, Y, and Z transforms.
    
    ![Variable Details Panel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/914a56eb-acc0-4664-bb55-5de47581b594/box-size-detail-panel.png)
3.  Drag out the variable and select **Get BoxSize**.
4.  Right-click the variable and select **Split Struct Pin**. The X, Y, and Z values of the variable will drive the dimensions of the box.
5.  Connect the corresponding X, Y, and Z values to the respective dimension values of **Append Box**.
    
    ![Widget Size Values](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9d7b44b4-7b6e-4d51-bba7-c9ee4508b181/connect-box-size-variable.png)
6.  **Compile** (Ctrl + Alt) and **Save** (Ctrl + S).

You can now generate a cube mesh and dynamically adjust the dimensions. Each adjustment with the widget generates a new dynamic mesh of the set size versus scaling the mesh.

![Dynamic Mesh](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6be9062d-f41b-41a9-a54c-c44ab9547dc6/dynamic-mesh-widget.gif)

For the widget to appear you must be in **Selection Mode**.

## Editing with Booleans

Boolean operations subtract or add mesh pairs. These are helpful for quickly adding detail and displacement effects to your mesh. To create the second mesh for the boolean function, you can allocate a temporary mesh from a mesh pool. The temporary mesh avoids unnecessary geometry in the editor, which puts less strain on computing processing.

To create a boolean operation, follow these steps:

1.  Right-click the graph, then search and select **Get Compute Mesh Pool**. This allocates a temporary mesh to perform a boolean operation.
2.  Pin **Append Box's** execution pin to **Get Compute Mesh Pool**.
3.  Drag out the **Return Value** pin, then search and select **Request and Release Mesh**. Connect the execution pins.
4.  Drag out the **Mesh** pin, then search and select **Append Cylinder**. This node adds a cylinder mesh that you will use to subtract from the box mesh.
5.  Promote the output **Target Mesh** to a variable called **BoolMesh**. Set the type to **Dynamic Mesh** and leave it private.
    
    ![Bool Mesh Variable](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b7807c6e-a027-411e-bedf-3bc355add746/bool-mesh-variable-5-5.png)
6.  Drag out the execution pin of **BoolMesh**, then search and select **Apply Mesh Boolean**. You will use this node to apply the boolean operation to your mesh.
7.  Drag out and connect the **DynamicMesh** variable to the **Target Mesh** input of **Apply Mesh Boolean**.
8.  Connect **BoolMesh** to the **Tool Mesh** pin of **Apply Mesh Boolean**. **Tool Mesh** represents the mesh you want to do the boolean with. This parameter is why you added the **Append Cylinder** node.
    
    ![Apply Mesh Boolean Node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f46a4b67-a647-4326-8fdd-a9499aa33a46/apply-mesh-boolean.png)
9.  Set the Operation type in the Apply Mesh Boolean node to **Subtract**.
10.  **Compile** (Ctrl + Alt) and **Save** (Ctrl + S).

When you compile and view the Blueprint in the Level Editor, you might not see the boolean effect because it's too small. To see the effect, you can manually set the size of the boolean mesh or dynamically adjust it using widgets.

### Adding Widgets

Just as you created a widget for the box primitive, you can do the same for the boolean mesh and location.

To create a widget, follow these steps:

1.  Under the **Variables** panel, create a public variable for the location of the boolean mesh, name it **BoolLocation**, and set the type to **Vector**.
    
2.  In the **Details** panel, enable **Instance Editable** and **Show 3D widget**.
    
3.  Right-click the **Transform** pin of the **Append Cylinder** node, select **Split Struct Pin**, then connect the **BoolLocation** variable to the **Transform Location**.
    
    ![Bool Location Variable](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9701ac65-8d08-4f7b-83d2-006ce11c8640/bool-location-variable-5-5.png)
4.  Create another public variable, name it **BoolSize**, and set the type to Vector. You can use this to adjust the size of the boolean mesh.
5.  In the **Details** panel, enable **Instance Editable** and **Show 3D widget**, then set the **Default Value** to 1, 1, and 5.
6.  Drag the variable into the graph and select **Get Bool Size**.
7.  Right-click the pin and select **Split Struct Pin**.
8.  Connect the **Bool Size** pins to the corresponding **Transform Scale** pins of the **Append Cylinder** node.
    
    ![Bool Size Variable](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e2ee75f9-323d-4806-8bfa-f90adbb89bf8/bool-size-variable-5-5.png)
9.  **Compile** (Ctrl + Alt) and **Save** (Ctrl + S).

You now have a mesh you can dynamically transform into different shapes.

![Dynamic Boolean Editing](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/794724b4-bc04-47cb-8ef7-8b1534bcb122/dynamic-boolean-editing-widgets.gif)

## Bake to Static Mesh Function

Now that you have your dynamically generated mesh, you can apply it to existing static meshes for quick level design. To do so, you can create a bake function and expose it to the Level Editor's **Details** panel.

To create the function, follow these steps:

1.  Create a new function called **Bake Static Mesh**.
    
    ![Bake Static Mesh Function](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0f15cfac-94d4-46a3-b0f3-de5afde97db7/bake-static-mesh-function.png)
2.  In the **Details** panel of the function, enable **Call in Editor** to activate the event from the Level Editor.
    
    ![Enable Call in Editor ](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2d2b58c3-c354-4271-974f-e75ed92b9012/call-editor-function.png)
3.  Drag off the function's execution pin, then search for and select **Get Dynamic Mesh**. The function pulls the dynamic mesh currently in use.
4.  Drag off the **Get Dynamic Mesh** execution pin, then search for and select **Copy Mesh to Static Mesh**. Also, connect the **Return Value** to **From Dynamic Mesh**. When the function executes, the dynamic mesh is baked to the selected static mesh.
    
    ![Copy Mesh to Static Mesh Function](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3e0711cd-833b-46f1-aa91-fb5b0d0b959a/copy-mesh-to-static-mesh.png)
5.  To select the static mesh you want to bake, you must expose the parameter to the editor. Create a public variable, call it **TargetMesh**, and set the type to **Static Mesh**.
6.  Drag the variable into the graph and select **Get TargetMesh**.
7.  Right-click the variable pin and select **Convert to Validated Get**. This conversion sets up the function to only run the code if you have a mesh selected.
8.  Connect **Target Mesh** pin to **To Static Mesh Asset**.
    
    ![Bake Static Mesh Graph](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b2d3f5d6-10a9-4db5-b8ca-32c95d2cba14/bake-static-mesh-graph.png)
    
    Finale Bake Script.
    
9.  **Compile** and **Save**.
10.  A **Bake to Static Mesh** button now appears in the Level Editor's **Details** panel. Before using the button, update the **Target Mesh** to the static mesh you want to bake.
    
    ![Bake Static Mesh Button](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bddea7c1-b1d6-4ce2-bead-a0b87e6280af/bake-static-mesh-button.png)

## Reviewing End Results

With the Bake Static Mesh function and procedural mesh script, you can use a dynamic mesh to update the static meshes in your level continually.

Final procedural mesh script. Click to expand.

## On Your Own

Using what you learned, try making the following adjustments:

-   Change the box mesh to a sphere.
-   Add a second boolean mesh for extra modeling control.
-   Use the **Create New Static Mesh Asset From Mesh** node to bake the dynamic mesh to a new static mesh instead of an existing one.