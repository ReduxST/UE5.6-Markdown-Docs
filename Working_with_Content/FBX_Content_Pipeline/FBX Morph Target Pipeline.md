# FBX Morph Target Pipeline

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/fbx-morph-target-pipeline-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/fbx-morph-target-pipeline-in-unreal-engine)  
**Processed:** 2025-06-14 16:23:27

---

A **Morph Target** is a snapshot of vertex locations for a specific mesh that have been deformed in some way. For instance, you can take a character model, reshape their face to create a facial expression, and then save that edited version as a Morph Target. In Unreal, you can blend the Morph Target to cause the character's face to make that expression. Morph Targets can be imported into Unreal via FBX, and will be encapsulated within an Animation Sequence.

This makes it very easy to import complex Morph Target animations into Unreal, since you can have any number of Morph Targets driving a single animation. For instance, you could use Morph Targets in your animation package to animate a character speaking some dialog. This animation may use any number of Morph Targets to capture the full motion of the face. However, when imported, the result will appear to be just a single Animation Sequence. You still have access to the animation data for each Morph Target via [**Curves**](/documentation/en-us/unreal-engine/animation-curves-in-unreal-engine).

Morph Target support in the FBX import pipeline provides an easy method for getting morph targets for skeletal meshes from 3D applications into Unreal for use in games. The pipeline allows for any number of morph targets for any number of Skeletal Meshes to be imported within a single file.

This page is a technical overview of using the FBX content pipeline to import morph targets into Unreal.

The Unreal Engine FBX import pipeline uses **FBX 2020.2**. Using a different version during export may result in incompatibilities.

This page includes information on both Autodesk Maya and Autodesk 3ds Max, please choose your preferred content creation tool below and the information relevant only to the chosen tool will be displayed:

Autodesk Maya Autodesk 3ds Max

## Naming

When importing morph targets into Unreal using the FBX format, the individual morph targets will be named according to the names of the blend shapes or morphs in the 3D application.

\* The name will be the name of the blendshape added to the name of the blendshape node, i.e. `[BlendShapeNode]_[BlendShape]`.

\* The name will be the name of the channel in the Morpher modifier.

## Setting Up Morph Targets

Setting up morph targets in Maya to be exported to FBX requires the use of blend shapes. The steps below provide a brief explanation of the steps necessary to set up a morph target for export. Refer to the help files of the application for more detailed information.

1.  Start with the base mesh.
    
    ![maya_setup_1.png](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6ba02dd0-6d3b-482c-9a87-1a1b6ba53c90/maya_setup_1.png)
2.  Duplicate the mesh that will be modified to create the target pose. In this case, it is the head. Create the target pose. For this example, the target pose is the character winking.
    
    ![maya_setup_2.png](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3a71a251-054f-4fde-8517-40e3b557e945/maya_setup_2.png)
3.  Select the target mesh and then the base mesh in that order.
    
    ![maya_setup_3.png](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b85199a6-e585-493b-a906-f1b79e83f3b0/maya_setup_3.png)
4.  In the **Create Deformers** menu of the **Animation** menu set, select **Blend Shape**. The target mesh can be deleted after this step if desired.
    
    ![maya_setup_4.jpg](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f5b60f7c-11f6-4316-beff-65c98aacdc0d/maya_setup_4.jpg)
5.  The blend shape node is now visible in the base mesh's properties. These are the names that will be used in Unreal. You can change the names of the blendshape node and the blendshape here.
    
    ![maya_setup_5.png](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/100b717f-f707-4ece-b159-8acc04985e21/maya_setup_5.png)
6.  Adjusting the blendshape's weight up to 1.0 causes the base mesh to interpolate toward the target pose.
    
    ![maya_setup_6.png](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b6dd4606-fc89-4955-82e6-fb17357fa2c8/maya_setup_6.png)

Setting up morph targets in 3dsMax to be exported to FBX requires the use of the Morpher modifier. The steps below provide a brief explanation of the steps necessary to set up a morph target for export. Refer to the help files of the application for more detailed information.

1.  Start with the base mesh.
    
    ![max_setup_1.jpg](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8f4de27c-1747-472c-b566-d6d66190c673/max_setup_1.jpg)
2.  Duplicate the mesh that will be modified to create the target pose. In this case, it is the head. Create the target pose. For this example, the target pose is the character winking.
    
    ![max_setup_2.jpg](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/56f7161c-06bf-4754-a23b-1d3d57890e9f/max_setup_2.jpg)
3.  Add a **Morpher** modifier to the base mesh. It needs to be before the **Skin** modifier in the stack.
    
    ![max_setup_3.jpg](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/74db94ea-ba1d-4420-8c41-07ae5dab73cd/max_setup_3.jpg)
4.  With the morph channel you want to populate selected, press the ![max_pick_button.jpg](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5d982248-4732-4578-84de-6ba141fca41f/max_pick_button.jpg) in the **Morpher** modifier's properties rollout or **right-click** on the channel and choose *Pick Object From Scene*.
    
    ![max_setup_4.jpg](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d66a5a32-a367-414b-8b05-c28fb236ba00/max_setup_4.jpg)
5.  In the viewport, click on the target mesh.
    
    ![max_setup_5.jpg](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2a00c207-f2d4-4006-92f5-8908ee0cedeb/max_setup_5.jpg)
6.  The morph channel is now populated and displays the name of the target mesh. This is the name that will be given to the morph target in Unreal. You can change it in the **Channel Parameters** section of the **Morpher** modifier's rollout.
    
    ![max_setup_6.jpg](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/62415051-1973-4107-8b19-553fd71069d0/max_setup_6.jpg)
7.  Adjusting the channel's weight up to 100.0 causes the base mesh to interpolate toward the target pose.
    
    ![max_setup_7.jpg](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e3f5384a-3bbe-4f1f-a2bf-283c0a48b4ab/max_setup_7.jpg)

## Exporting Morph Targets

1.  Select the base mesh(es) and joints to be exported in the viewport.
    
    ![maya_export_1.png](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b4a04a4a-1521-48a5-83ad-0449f3418b7f/maya_export_1.png)
2.  In the *File* menu, choose *Export Selection* (or *Export All* if you want to export everything in the scene regardless of selection).
    
    ![maya_export_2.jpg](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5d11e884-3989-48e3-beea-acf50e6ee979/maya_export_2.jpg)
3.  Choose the location and name for the FBX file to export the morph target to and set the appropriate options in the **FBX Export** dialog. For the purposes of exporting morph targets, you must enable the **Animations** checkbox and all of the **Deformed Models** options.
    
    ![maya_export_3.jpg](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6c292a95-3cda-4700-9477-9cb37aea344b/maya_export_3.jpg)
4.  Click the ![maya_export_button.jpg](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a380b7f5-15de-445a-a06b-6b68bb3a88b0/maya_export_button.jpg) button to create the FBX file containing the morph target(s).
    

1.  Select the base mesh(es) and bones to be exported in the viewport.
    
    ![max_export_1.jpg](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/31fd0b09-2828-492d-aa1d-e8ac3d8110a7/max_export_1.jpg)
2.  In the *File* menu, choose *Export Selected* (or *Export All* if you want to export everything in the scene regardless of selection).
    
    ![max_export_2.jpg](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/eed514ce-721e-4993-8c9d-f606fea0b253/max_export_2.jpg)
3.  Choose the location and name for the FBX file to export the morph target to and click the ![max_save_button.jpg](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6cc7694f-8a9a-44db-8844-5c69da5e9651/max_save_button.jpg)button.
    
    ![max_export_3.jpg](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/038c5520-e3d9-4da9-846e-de8dc2703274/max_export_3.jpg)
4.  Set the appropriate options in the **FBX Export** dialog. For the purposes of exporting morph targets, you must enable the **Animations** checkbox and all of the **Deformations** options.
    
    ![max_export_4.jpg](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d6ac25f3-974b-450f-8aba-3f849b471c52/max_export_4.jpg)
5.  Click the ![max_ok_button.jpg](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a997a418-22d1-4609-852d-6ae6ea3fe1be/max_ok_button.jpg) button to create the FBX file containing the morph target(s).
    

## Importing Morph Targets

The FBX morph target import pipeline allows for importing both a *SkeletalMesh* and morph target all at once. If you import and add morph targets to an existing Skeleton with morph targets already applied, the existing ones will be overridden.

**Skeletal Mesh with Morph Targets**

1.  Click the **Import** button in the **Content Browser**. Navigate to and select the FBX file you want to import in the file browser that opens. **Note:** you may want to select ![import_fbxformat.jpg](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3599668a-e11f-44b3-80cc-76cdb999c2c9/import_fbxformat.jpg) in the dropdown to filter out unwanted files.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9ff225e5-ecf4-45d5-9888-f4fa418b1b2f/import_file.jpg)
2.  Choose the appropriate settings in the **Import** dialog. Make sure that *Import Morph Targets* is enabled. **Note:** The name of the imported mesh will follow the default [**Naming Rules**](/documentation/en-us/unreal-engine/fbx-import-options-reference-in-unreal-engine#namingconventions). See the [**FBX Import Dialog**](/documentation/en-us/unreal-engine/fbx-import-options-reference-in-unreal-engine) section for complete details of all of the settings.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c74fb885-265c-4884-8c4b-6a854c5354a2/importmorphtargets.png)
3.  Click the **OK** button to import the mesh and LODs. The resulting mesh, morph target (MorphTargetSet), material(s), and texture(s) will be displayed in the **Content Browser** if the process was successful. You can see the MorphTargetSet that was created to hold the morph target was named after the root bone of the skeleton by default.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7e2c9c3d-412a-46f6-93c6-ab6d01feac4a/importedcharacter.png)
    
    By viewing the imported mesh in Persona and using the **Morph Target Previewer** tab, you can adjust the strength of the imported morph target and see that it is working as expected.
    

The effect of **Morph Targets** is often subtle, but the control it offers the animator and the believability it adds to a character cannot be overstated.