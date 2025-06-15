# Using Radial Motion Blur

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/using-radial-motion-blur-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/using-radial-motion-blur-in-unreal-engine)  
**Processed:** 2025-06-14 17:00:44

---

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/aa268dc3-aaeb-436d-ad52-8ef296c414e9/perbonemotionblurtopicimage-1.png "PerBoneMotionBlurTopicImage-1.png")

The standard **Motion Blur** that Unreal Engine supports assumes that a point on an object's surface moves in a straight line from frame to frame, and then uses information from where that point was located during the previous frame to apply the blur effect.

This works well for an object moving from one position to another. However, this method produces visual errors when applied to an object that is rotating 180 degrees within a single frame, like a very quickly rotating wheel on a car. In this instance, the Motion Blur looks at a point on one side of the wheel, then assumes it traveled to the opposite side of the wheel in a straight line rather than moving around the circumference.

To help address this issue, a special **Radial Motion Blur** Material was developed and released in the free Unreal Engine **Content Examples** project. You can use this Material to make an object look as if it were rotating quickly by applying a radial instead of linear motion blur. In the example image below you can see the results of using standard Motion Blur on a rotating object (left) compared with the results of using the Radial Motion Blur Material (right).

![Motion Blur comparison](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0a1e5038-46a7-4b92-89e3-66477cc42a24/motionblurerror.png "MotionBlurError.png")

This tutorial will walk you through the process of setting up the Radial Motion Blur Material in your own projects.

## Required Setup

This tutorial requires assets found in the **Content Examples** sample project. If you do not already have this sample project, download and install it from the **Learn** tab in the Epic Games Launcher.

Click for full image.

In the Content Examples Project, you can find a working example of Radial Motion Blur in the **Materials\_Advanced** map.

Due to its complexity, it is beyond the scope of this tutorial to rebuild the base **M\_RadialMotionBlur** Material from scratch. However, if you would like to examine the base Material Graph, you can find the Material asset in the Content Browser under **Content > Example Content > Materials > Materials**.

![Radial Motion Blur base Material location](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ef56a130-5f83-48f4-8431-4c636029d723/radial-blur-base-material.png)

For the purpose of this tutorial we will rebuild the Radial Motion Blur example using the following assets in the Content Browser.

-   **SM\_Wheel** - Static Mesh
-   **SM\_Wheel\_Blur** - Static Mesh
-   **MI\_RadialMotionBlur** - Material Instance

To use the Radial Motion Blur Material in your own project, you can right-click the **MI\_RadialMotionBlur** Material Instance in the **Content Browser**, and select **Asset Actions** > **Migrate** in the context menu.

![Migrate Assets tool](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1c345804-e40c-4808-a2e3-25f7b8f1e3ba/migrating-assets.png)

The Migrate Assets tool will automatically include both MI\_RadialMotionBlur and the base RadialMotionBlur Material in the migration. For more information on this topic, see the guide on [Migrating Assets](/documentation/en-us/unreal-engine/migrating-assets-in-unreal-engine).

## Steps

1.  Make sure the Unreal Editor is closed. Inside your project folder, navigate to the **Config** folder and locate **DefaultEngine.ini**.
    
    Click image to enlarge.
    
2.  Open **DefaultEngine.ini** with a text editor, and in the **\[/Script/Engine.RendererSettings\]** section add **r.CustomDepth=3**.
    
    ![Custom Depth 3](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0fe6a8ee-750d-4dfa-b37b-bdf24bccd573/custom-depth-three.png)
3.  Radial Motion Blur requires two **Static Meshes**: The mesh that you want to apply the Radial Motion Blur to, and a "dummy" mesh that will cover it. The dummy Mesh needs to not only cover the object that will be blurred, it also needs to completely cover the space that it will sweep through while rotating, and it should wrap around that swept space as tightly as possible without intersecting with the original object's geometry.
    
    Click image to enlarge.
    
    In the example image above, the Mesh that we want to apply the blur to has its standard Material applied, while the "dummy" mesh is a hull wrapped around it, visualized with a yellow wireframe. Note that it fits closely over the Static Mesh but does not penetrate through it. You may decide to use your own Meshes, but for the purposes of this guide we will be using the assets **SM\_Wheel** and **SM\_Wheel\_Blur**, which you can find in the Content Examples project under **Content > ExampleContent > Materials > Meshes**.
    
    ![SM_Wheel Static Mesh location](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/281ded06-c79c-42c9-8b89-c5d2fe4c4b24/sm-wheel-content-browser.png)
4.  Create a new **StaticMeshActor** by dragging **SM\_Wheel** into the scene.
    
    Click image to enlarge.
    
5.  In the **Details Panel** for this StaticMeshActor, click the **Create Blueprint from Selection** button to create a new Blueprint based on this Actor. Name the Blueprint **BP\_StaticMesh\_MotionBlur** and save it to your **Blueprints** folder. The Static Mes is converted to a Blueprint Actor type and the **Blueprint Editor** will automatically open.
    
    Click image to enlarge.
    
6.  In the **Blueprint Editor**, locate the **Components Panel** and select the **StaticMeshComponent** for your Mesh. Then, in the **Details Panel**, expand the **Advanced** section under **Rendering**. Set **Render Custom Depth Pass** to True, then set **Custom Depth Stencil Value** to 5.
    
    Click for full image.
    
7.  In the **Components Panel**, click the **Add Component** button. Select **Static Mesh** in the drop-down list to add a new StaticMeshComponent as a child of the base Mesh. Re-name this Mesh "**MotionBlur Mesh**".
    
    ![Add Static Mesh component](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/db2d172f-8b89-4f1b-a279-923678129872/add-static-mesh-component.png)
8.  In the **Details Panel**, set the Static Mesh for your MotionBlur Mesh to **SM\_Wheel\_Blur**. Rotate it **90°** on the x-axis so that it fits over the base Mesh. In the Materials section, ensure that it has the **MI\_RadialMotionBlur** Material Instance applied.
    
    Click for full image.
    

## Result

With the **MI\_RadialMotionBlur** Material Instance applied, your base Mesh should now appear as if it is rotating very quickly. The image below demonstrates a normal, stationary Static Mesh (left), versus a Mesh with the RadialMotionBlur applied to a dummy Mesh surrounding the base Mesh (right).

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/90172817-f4ba-4ec4-95a8-3cf368d6e445/motionblur_finalresult.png)

Note that you do not need to rotate your base Mesh or Actor in order to achieve this effect. Instead, the RadialMotionBlur Material itself creates the illusion that the object is rotating. You can adjust the effect using the **Angle** and **RimRadius** parameters that are found in the **MI\_RadialMotionBlur** Material Instance.

![Radial Blur aterial Instance](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/00ac9054-172a-4543-85d4-406416c9afc1/radial-blur-material-instance.png)

The following two image sequences show how the visuals of the Radial Blur are affected when you adjust the **Angle** and **RimRadius** Material inputs.

          ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1119fb22-0da2-4baa-a854-deeef21d7106/perbonemb_001.png) ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7b61c5a2-ee23-4c6b-87e9-837a1bbf9135/perbonemb_002.png) ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9cfb7402-d913-4de9-a641-adf0d2e9bc7e/perbonemb_003.png) ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6b299cfe-b33c-4628-a57d-924852a099cc/perbonemb_004.png) ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/95e8200b-245b-4e29-95fc-c08b0662059c/perbonemb_005.png) ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2cdeb945-4a6a-4b4f-bb01-c0ebdd8dc564/perbonemb_006.png) ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/643208c9-5b33-4622-be67-38d76baf512b/perbonemb_007.png) ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a4b41811-ad07-4e8a-bd16-f723f29ee0d8/perbonemb_008.png) ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ddd35506-1a2f-4fe6-a4c0-2406e4c472c1/perbonemb_009.png) ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d839f03d-3e22-4d4d-862b-02a47b0763de/radialblur_10-2.png) ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/dbc0c3e3-4c41-457b-944f-81fe0b513317/radialblur_11-2.png)

This Angle parameter is used to control the intensity of the Radial Blur. The higher it is, the faster the object will look like it is rotating.    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1567630e-562a-46af-91ef-095fa964d5cb/rimradius_0.png) ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2fb57b87-447c-4c4f-a32a-78038922e238/rimradius_20.png) ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0d585e7f-17b8-44de-936e-d7c597b9749d/rimradius_25.png) ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1b34dd4a-57bf-4741-b9d9-fc1d9b3ce2d4/rimradius_30.png) ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ccd35235-7025-4d3a-9b63-c3275968e3a1/rimradius_42.png)

The RimRadius parameter is used to limit what will be blurred by the Radial Blur. You should set the RimRadius to match the radius of the mesh that is used for the Radial Blur.

You can reuse this new Actor type that you've created to make all kinds of objects that use the Radial Motion Blur effect. Change the Static Mesh used for both the base Mesh and the dummy Mesh, and ensure that the dummy Mesh uses a Material Instance of the RadialMotionBlur Material. Remember that the dummy mesh should fit as closely as possible to the area that would be swept by the base mesh when it rotates.

![Radial Motion Blur on multiple shapes](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bd5b6c17-f1db-42d2-bd03-6cbb7d3a7267/motionblur_othershapes.png)

Finally, if you want different objects to have different settings, create new Material Instances based on the **RadialMotionBlur** Material and give them the desired settings accordingly. For more information about how to create Material Instances, see the guide on [Creating and Using Material Instances](/documentation/en-us/unreal-engine/creating-and-using-material-instances-in-unreal-engine).