# Runtime Virtual Texturing Quick Start

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/runtimevirtual-texturing-quick-start-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/runtimevirtual-texturing-quick-start-in-unreal-engine)  
**Processed:** 2025-06-14 16:47:39

---

This guide refers to materials found in the Content Examples project available from the Epic Games Launcher under the Samples tab. While the materials are not required to do the steps below, setting up the landscape to function properly with painted landscape materials is. See the [Landscape Quick Start Guide](https://dev.epicgames.com/documentation/en-us/unreal-engine/landscape-outdoor-terrain-in-unreal-engine) before continuing, or open the Content Examples project **Landscapes** map under the **Samples** tab for use with this guide.

In this **Runtime Virtual Texturing** (RVT) quick start, we'll walk through the process of setting up and using RVT for your Landscape and non-Landscape components in your projects.

Before starting this guide, it's important to understand that Runtime Virtual Textures work best with Landscape terrains for a few reasons:

-   Complex Landscape materials cache the shading results for a performance win.
    
-   Improved quality and variation are achievable with spline and decal-type effects.
    
-   Blending of non-Landscape Actors with your Landscape is handled by the same RVT Asset.
    

After going through this guide, you'll have a better understanding of:

-   Setting up a Runtime Virtual Texture Asset and how it connects to different components.
    
-   Enabling Runtime Virtual Texturing for a Landscape Material.
    
-   Setting up a Runtime Virtual Texture Volume in your Level.
    
-   Setting up additional Actors to render to the Runtime Virtual Texture.
    

## 1 - Project Setup

Before you can use Runtime Virtual Textures, you must first enable it for your project. Follow these steps:

1.  From the main menu, select the **Edit** menu and select **Project Settings**. Under the **Engine** > **Rendering** > **Virtual Textures** category, set **Enable virtual texture support** to true.
    
    [![Under the Virtual Textures category set Enable virtual texture support to true](https://dev.epicgames.com/community/api/documentation/image/84ac1886-1115-460d-af44-9bcceb29f74c?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/84ac1886-1115-460d-af44-9bcceb29f74c?resizing_type=fit)
    
2.  **Restart** the Project.
    

## 2 - Creating a Runtime Virtual Texture Asset

The **Runtime Virtual Texture** Asset contains the configuration details for the RVT Asset assigned to a Runtime Virtual Texture Volume. The RVT Asset also works by linking Materials and other Actors in your scene that need to share data.

1.  In the **Content Drawer**, use the right-click context menu or the **+Add** button to create a **Runtime Virtual Texture** Asset from the **Textures** category.
    
    [![Create a Runtime Virtual Texture Asset from the Materials andTextures category](https://dev.epicgames.com/community/api/documentation/image/67b3f171-4e26-4766-927e-47b7f0391cc3?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/67b3f171-4e26-4766-927e-47b7f0391cc3?resizing_type=fit)
    
2.  Give the **Runtime Virtual Texture** Asset a name. For this guide, it is named `VT_Test`.
    
3.  Double-click the Asset to open the **Runtime Virtual Texture** Asset Editor where you can configure its properties.
    
    [![Double-click the Asset to open the Runtime Virtual Texture Asset Editor where you can configure its properties](https://dev.epicgames.com/community/api/documentation/image/89969dd6-f3e3-4aea-8899-92cfbae26e94?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/89969dd6-f3e3-4aea-8899-92cfbae26e94?resizing_type=fit)
    
    From this window, you can define the size, tile size, and type of Material Attributes the runtime virtual texture supports. These properties can be adjusted in real-time while working in the editor to see their changes take effect.
    
    For details and usage of these settings, see [Virtual Texture Settings](https://dev.epicgames.com/documentation/en-us/unreal-engine/virtual-texturing-settings-and-properties-in-unreal-engine) page.
    

## 3 - Creating a Runtime Virtual Texture Material

For details and usage of these settings, see [Virtual Texture Settings](https://dev.epicgames.com/documentation/en-us/unreal-engine/virtual-texturing-settings-and-properties-in-unreal-engine) page.

In this step, we'll be using a simple Landscape material for runtime virtual texturing support. In addition, we'll set up logic using some RVT-specific Material Expressions that allow for the material to fall back to its original use when virtual texturing isn't available on a supported platform.

Setting up your material to work with RVT requires that two contexts be considered:

-   Part of the material will **write to** the RVT Asset.
    
-   Part of the material will **sample from** the RVT asset and apply further logic.
    

This example landscape material, taken from the **Content Examples** project, has a simple layer blend setup for Snow, Grass, and Rock.

[![This example landscape material has a simple layer blend setup](https://dev.epicgames.com/community/api/documentation/image/8db85050-4da6-451b-a543-478319675bfc?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/8db85050-4da6-451b-a543-478319675bfc?resizing_type=fit)

Click the image for full size.

If you're not using the material from Content Examples, you can recreate it as shown above. However, keep in mind that you'll still need to properly set up the Material for use with a Landscape. Follow the [Landscape Quick Start Guide](https://dev.epicgames.com/documentation/en-us/unreal-engine/landscape-outdoor-terrain-in-unreal-engine) if you need a starting point.

The sections that follow will break down parts of this Material to demonstrate how we're writing to and sampling from the RVT Asset.

### Required Material Setup

Setting up a Landscape material for use with an RVT Asset is the same as setting up a traditional one, with one exception; **Use Material Attributes** should be enabled. This option enables us to use **Make Material Attributes** expressions to rebuild and output the material for different use cases supported.

1.  Open your existing or available Landscape material. Right-click in the graph and search for a **Make Material Attributes** expression. Add one to your graph.
    
2.  Move the wire connections from the Main Attributes node to the **Make Material Attributes** node. You should have something that looks like this:
    
    [![Move the wire connections from the Main Attributes node to the Make Material Attributes node](https://dev.epicgames.com/community/api/documentation/image/aade3b73-7535-42f5-9c10-5e7151228c8c?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/aade3b73-7535-42f5-9c10-5e7151228c8c?resizing_type=fit)
    
    Click the image for full size.
    
3.  Now, with the **Main Attributes** node selected, use the **Details** panel to enable **Use Material Attributes**.
    
    [![Use the Details panel to enable Use Material Attributes](https://dev.epicgames.com/community/api/documentation/image/eb8a32aa-21b4-476c-9073-1fbf46c4d2d2?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/eb8a32aa-21b4-476c-9073-1fbf46c4d2d2?resizing_type=fit)
    
4.  Pull off the output of the **Make Material Attributes** node and create a **Virtual Textures Feature Switch** node. This should plug it into the **No** input. Connect that to the **Material Attributes** output.
    
    [![Pull off the output of the Make Material Attributes node and create a Runtime Virtual Textures Feature Switch node](https://dev.epicgames.com/community/api/documentation/image/9a4a046f-f191-4987-8a71-243fa0e1a0c0?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/9a4a046f-f191-4987-8a71-243fa0e1a0c0?resizing_type=fit)
    

Your material should now look like this:

[![Material Setup](https://dev.epicgames.com/community/api/documentation/image/318fa09a-6fd0-4f87-a338-240038d2f2b9?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/318fa09a-6fd0-4f87-a338-240038d2f2b9?resizing_type=fit)

Click the image for full size.

### Writing to the Runtime Virtual Texture Asset

Next, the material needs to *write to* the RVT Asset through the **Runtime Virtual Texture Output** expression. This node references the RVT Asset created earlier in this guide and enables corresponding Material Attributes (such as Base Color, Roughness, and Normal) to be used as input attributes of this node.

1.  Right-click and add a **Runtime Virtual Texture Output** node to the graph.
    
    [![Right-click and add a Runtime Virtual Texture Output node to the graph](https://dev.epicgames.com/community/api/documentation/image/b9ad7508-3ec1-46b3-bffb-af51d142e144?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/b9ad7508-3ec1-46b3-bffb-af51d142e144?resizing_type=fit)
    
    Click the image for full size.
    
2.  Connect the node wires for each material attribute input that is listed on the node. For ones not used in your base material, use a constant value in its place.
    
    [![Connect the node wires for each material attribute input that is listed on the node](https://dev.epicgames.com/community/api/documentation/image/8fa2650b-15de-425f-80f1-87cc3417d72e?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/8fa2650b-15de-425f-80f1-87cc3417d72e?resizing_type=fit)
    

Your material should now look like this:

[![Runtime Virtual Texture Output Setup](https://dev.epicgames.com/community/api/documentation/image/bfb8308b-d062-402b-84af-d8e4c5281ae9?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/bfb8308b-d062-402b-84af-d8e4c5281ae9?resizing_type=fit)

Click the image for full size.

The first part of this material is where all the layer blending and logic is happening. It is all the *camera-independent* shading that can be cached to the RVT Asset. Other objects (such as splines and decals) are expected to be composited to the output of this node by the RVT System.

### Sampling from the Runtime Virtual Texture Asset

Next, the material needs to *sample from* the RVT Asset using the **Runtime Virtual Texture Sample** expression.

During this part of the graph, the RVT Asset is sampled and applies *camera-dependent* or additional shading operations here. The RVT Asset attributes are sampled and routed to the final Material output, so the less work is done during this part of the graph, the cheaper the rendering for this material will be.

1.  Right-click and add a **Runtime Virtual Texture Sample** node.
    
    [![Right-click and add a Runtime Virtual Texture Sample node](https://dev.epicgames.com/community/api/documentation/image/55bb5de1-f75e-4d0d-bbde-7c78bd61238a?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/55bb5de1-f75e-4d0d-bbde-7c78bd61238a?resizing_type=fit)
    
    Click the image for full size.
    
2.  Right-click and create another **Make Material Attributes** node. Connect the outputs of the **Runtime Virtual Texturing Sample** node to the corresponding inputs of the **Make Material Attributes** node.
    
    [![Connect the outputs of the Runtime Virtual Texturing Sample node to the corresponding inputs of the Make Material Attributes node](https://dev.epicgames.com/community/api/documentation/image/26834fa5-b8bf-437c-9950-da30ffa45fbf?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/26834fa5-b8bf-437c-9950-da30ffa45fbf?resizing_type=fit)
    
3.  Connect the output of the **Make Material Attributes** node to the **Yes** input of the **Virtual Texture Feature Switch** node.
    
    [![Connect the output of the Make Material Attributes node to the Yes input of the Virtual Texture Feature Switch node](https://dev.epicgames.com/community/api/documentation/image/e61222f3-de11-48d2-8b27-459a5cc445b2?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/e61222f3-de11-48d2-8b27-459a5cc445b2?resizing_type=fit)
    
    Click the image for full size.
    
4.  Select the **Runtime Virtual Texture Sample** node. In the **Details** panel, use the **Virtual Textures** Asset selection box to assign the RVT Asset you created earlier in this guide.
    
    [![Use the Virtual Textures Asset selection box to assign your RVT Asset you created earlier in this guide](https://dev.epicgames.com/community/api/documentation/image/bb3ee5e0-0833-4b19-b274-7b95b14d2aae?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/bb3ee5e0-0833-4b19-b274-7b95b14d2aae?resizing_type=fit)
    
5.  Connect the output of the **Virtual Texture Feature Switch** node to the input of the main **Material Attributes** node.
    
    [![Connect the output of the Virtual Texture Feature Switch node to the input of the main Material Attributes node](https://dev.epicgames.com/community/api/documentation/image/74329a53-e88f-4687-b967-e0a5fc03b8bd?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/74329a53-e88f-4687-b967-e0a5fc03b8bd?resizing_type=fit)
    
6.  **Save** and **Close** this Material.
    

Your material should now look like this:

[![Runtime Virtual Texture Sample Output](https://dev.epicgames.com/community/api/documentation/image/7bade092-8ad9-436e-a5d1-10b698be6592?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/7bade092-8ad9-436e-a5d1-10b698be6592?resizing_type=fit)

Click the image for full size.

## 4 - Placing a Runtime Virtual Texture Volume

Now that your material is set up to support runtime virtual texturing, you can move to your Level where you will place a **Runtime Virtual Texture Volume** to apply the RVT material to a surface, in this case, a landscape terrain.

1.  In the **Place Actors** panel, search for a **Runtime Virtual Texture Volume** under the **Volumes** category and drag it into the scene.
    
    [![Search for a Runtime Virtual Texture Volume under the Volumes category and drag it into the scene](https://dev.epicgames.com/community/api/documentation/image/85b6f3ce-319b-4bcd-b2c3-dc202b82bd03?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/85b6f3ce-319b-4bcd-b2c3-dc202b82bd03?resizing_type=fit)
    
    Click the image for full size.
    
2.  With the RVT Volume selected, under the **Virtual Texture** section, set the **Virtual Texture** material assignment box to use the Runtime Virtual Texture Asset created in Step 2 of this guide.
    
    [![Set the Virtual Texture material assignment box to use the Runtime Virtual Texture Asset created in Step 2 of this guide](https://dev.epicgames.com/community/api/documentation/image/7b0e8577-b2f0-44f0-8a6b-f75ba7fe97cf?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/7b0e8577-b2f0-44f0-8a6b-f75ba7fe97cf?resizing_type=fit)
    
3.  The RVT Volume is not yet properly scaled to cover the areas you want to apply the RVT material. Select the RVT Volume, and in its **Details** panel in the **Transform from Bounds** section, set the **Source Actor** to the one you want to use. In this example, **Landscape\_2** is used.
    
    [![In the Transform from Bounds section set the Source Actor to the one you want to use](https://dev.epicgames.com/community/api/documentation/image/795c62a5-779a-449e-888e-50be90029cc3?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/795c62a5-779a-449e-888e-50be90029cc3?resizing_type=fit)
    
4.  Click the **Set Bounds** button to scale the Runtime Virtual Texture Volume to the bounds of the selected Actor.
    
    [![Click the Set Bounds button to scale the Runtime Virtual Texture Volume to the bounds of the selected Actor](https://dev.epicgames.com/community/api/documentation/image/612e4458-9e91-433b-9c3c-adc7b1601ac8?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/612e4458-9e91-433b-9c3c-adc7b1601ac8?resizing_type=fit)
    
    Any Actor sampling from or writing to the Runtime Virtual Texture must be within the RVT Volume's bounds.
    
5.  Select the scene Actor (Landscape\_2) and in the **Details** panel under the **Virtual Texture** section, click the **Add Element** icon next to **Draw in Virtual Textures**.
    
    [![Click the Add Element icon next to Draw in Virtual Textures](https://dev.epicgames.com/community/api/documentation/image/97f8019d-993c-4810-b754-069e3536bbe1?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/97f8019d-993c-4810-b754-069e3536bbe1?resizing_type=fit)
    
    Use the Asset assignment dropdown to select your **Runtime Virtual Texture Asset**.
    
    [![click the Add Element icon next to Draw in Virtual Textures](https://dev.epicgames.com/community/api/documentation/image/0e75de73-16b6-4868-a2fd-e13b9e7f9488?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/0e75de73-16b6-4868-a2fd-e13b9e7f9488?resizing_type=fit)
    

With the Runtime Virtual Texture Volume placed and scaled around the landscape terrain and the Runtime Virtual Texture Asset assigned to the landscape, the terrain material should immediately become visible. If something is not set up correctly, the landscape will render black.

## 5 - Rendering Actors to a Runtime Virtual Texture

With your landscape's material set up, other scene Actors can be set up to render into the runtime virtual texture, such as the road spline following the terrain. Any Actors that are set up to output to a runtime virtual texture and are within the placed RVT Volume will be captured and rendered as part of the Runtime Virtual Texture Asset applied to the landscape.

The spline in this section of the guide is a Landscape Spline that is already set up in Content Examples. The steps shown here can be applied to other scene Actors and their Materials to achieve the same effect.

1.  Navigate to the **Modes** dropdown menu, select **Landscape**.
    
    [![Navigate to the Modes dropdown menu and select Landscape](https://dev.epicgames.com/community/api/documentation/image/0d9f9cad-515f-4726-a8d0-8f0f6a0de1f5?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/0d9f9cad-515f-4726-a8d0-8f0f6a0de1f5?resizing_type=fit)
    
2.  On the **Landscape** toolbar, click on **Splines**.
    
    [![Click on Splines](https://dev.epicgames.com/community/api/documentation/image/bb53f885-4de4-4399-bd11-ce80bc7002de?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/bb53f885-4de4-4399-bd11-ce80bc7002de?resizing_type=fit)
    
3.  In the Level Viewport, select any part of the spline. In the level **Details** panel, click the **Segments** button to select all segments that make up this spline.
    
    [![Click the Segments button to select all segments that make up this spline](https://dev.epicgames.com/community/api/documentation/image/c91cc611-5208-4017-b520-35f79fd75921?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/c91cc611-5208-4017-b520-35f79fd75921?resizing_type=fit)
    
4.  Under the **Landscape Spline Meshes** category, expand the **Spline Meshes** array. The Static Mesh **SM\_Street** should be assigned. Double-click on it to open the Static Mesh Editor.
    
    [![The Static Mesh SM_Street should be assigned and double-click on it to open the Static Mesh Editor](https://dev.epicgames.com/community/api/documentation/image/d9f2bf4d-9c70-49f4-a8c9-6948b54b9757?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/d9f2bf4d-9c70-49f4-a8c9-6948b54b9757?resizing_type=fit)
    
    Under its **Material Slots**, double-click on Element 0 **M\_Street** material to open it in the Material Editor.
    
    [![Double-click on Element 0 M_Street material to open it in the Material Editor](https://dev.epicgames.com/community/api/documentation/image/b24a66a1-e70a-4d7a-adfc-1ffc2bc58548?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/b24a66a1-e70a-4d7a-adfc-1ffc2bc58548?resizing_type=fit)
    
    For this Static Mesh and Material assigned, Element 0 was chosen because it is the parent Material used for slots 0 and 1, with Element 1 being a child Material Instance of Element 0. Keep in mind that any Material that is to be rendered to the RVT Asset needs to be set up to render into a runtime virtual texture using the steps that follow.
    
5.  In the material graph, right-click and add a **Runtime Virtual Texture Output** node. Connect the **Color** and **Roughness** node outputs to the **BaseColor** and **Roughness** inputs on the Runtime Virtual Texture Output node.
    
    [![Connect the Color and Roughness node outputs to the BaseColor and Roughness inputs on the Runtime Virtual Texture Output node](https://dev.epicgames.com/community/api/documentation/image/5ed1ce4a-28a0-48f1-8aa7-72a6abd9ecb5?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/5ed1ce4a-28a0-48f1-8aa7-72a6abd9ecb5?resizing_type=fit)
    
6.  **Save and Close** for both the Material and Static Mesh Editors.
    
7.  In the Level Viewport, select any part of the Landscape Spline. In the **Details** panel, click the **Segments** button to select all attached spline segments.
    
    [![Click the Segments button to select all attached spline segments in the details panel](https://dev.epicgames.com/community/api/documentation/image/2768a0e6-e849-4636-a202-e1fdbcb2dd9d?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/2768a0e6-e849-4636-a202-e1fdbcb2dd9d?resizing_type=fit)
    
8.  With the spline segments still selected, scroll down in the **Details** panel to the **Virtual Texture** section, and click the **Add Elements (+)** icon. Select your **Runtime Virtual Texture Asset** from the assignment dropdown.
    
    [![Select your Runtime Virtual Texture Asset from the assignment dropdown](https://dev.epicgames.com/community/api/documentation/image/d2d021fc-c98d-49bc-801a-402487333ea4?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/d2d021fc-c98d-49bc-801a-402487333ea4?resizing_type=fit)
    
9.  The primitive (or landscape spline in this demonstration) is now rendered into the RVT. However, the primitive is still visible. If you don't want the primitive to be visible in the main pass and to only have it rendered to the RVT, place the Level Viewport back into **Select** mode using the **Modes** dropdown and select the **Runtime Virtual Texture Volume** placed in the Level. Under the **Virtual Texture** section's advanced properties, enable **Hide Primitives**.
    
    [![Enable Hide Primitives under the Virtual Texture section's advanced properties](https://dev.epicgames.com/community/api/documentation/image/9ff33941-edca-4716-8242-466cec0cae18?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/9ff33941-edca-4716-8242-466cec0cae18?resizing_type=fit)
    

In the Level Viewport when in Game View, the Landscape Spline should be rendered into the Runtime Virtual Texture Asset and applied to the terrain's surface, and the spline primitive should no longer be visible.

![Without Runtime Virtual Texturing](https://dev.epicgames.com/community/api/documentation/image/64b345ba-a2b3-41f3-9caf-deef8f0c1acc?resizing_type=fit&width=1920&height=1080)

![With Runtime Virtual Texturing](https://dev.epicgames.com/community/api/documentation/image/37477f1d-fa95-4197-81f1-c0e925cec1f2?resizing_type=fit&width=1920&height=1080)

Without Runtime Virtual Texturing

With Runtime Virtual Texturing

Here's a closer look at the spline material being applied to the surface of the landscape using RVT.

![Without Runtime Virtual Texturing](https://dev.epicgames.com/community/api/documentation/image/a246e975-c76f-4aad-acd4-23115480cfe6?resizing_type=fit&width=1920&height=1080)

![With Runtime Virtual Texturing](https://dev.epicgames.com/community/api/documentation/image/72385f9b-d94f-43da-b6c6-d58ef6f11648?resizing_type=fit&width=1920&height=1080)

Without Runtime Virtual Texturing

With Runtime Virtual Texturing

## 6 - On Your Own!

Now that you've worked through this guide and set up a Landscape material to use a Runtime Virtual Texture, you can start to explore applying your own Actor's materials to be rendered to the RVT. Use some of the suggestions below to get started:

-   Add another Static Mesh to the RVT that can be applied like a decal. Look at how you can use a Static Mesh Plane with a masked material to add decal-like details to your terrain.
    
-   Use Foliage instances to paint meshes that can render to the RVT to create unique variations to your terrain.
    
-   Use multiple Runtime Virtual Texture Assets to manage different types of Actors, and how they render to your Runtime Virtual Texture Volume.
    
-   Use the **Translucency Sort Priority** to set the layer order for how Actors are rendered to the RVT. For example, 0 would be the bottom layer and higher values would stack on top of each other.