# Datasmith Import Process

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/datasmith-import-process-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/datasmith-import-process-in-unreal-engine)  
**Processed:** 2025-06-14 16:18:54

---

The following sections provide details about specific issues that Datasmith handles during the scene conversion. Understanding these issues can help you understand the results that Datasmith produces, and to work with your content in the Unreal Editor.

You can download the two projects used in this page from Sketchfab:

-   ["Richard's Art Gallery - Audio Tour"](https://skfb.ly/YHEN) by shinymagic is licensed under [Creative Commons Attribution](http://creativecommons.org/licenses/by/4.0/).
-   ["Vintage fan"](https://skfb.ly/6WXsR) by Noah is licensed under [Creative Commons Attribution](http://creativecommons.org/licenses/by/4.0/).

## Units and Scale

In Unreal Engine, all distances are always measured in centimeters. However, other 3D design applications typically offer a choice of units of measurement. If you use a different unit of measurement in your source application, Datasmith automatically takes care of adjusting the scale of your scene so that your geometry appears at exactly the same real-world size in the Unreal Engine, and at the right locations in 3D space. You don't have to change anything about the way you work in your source application.

For example, if you use inches as the unit of measurement in your source application, an object that is ten units long in your original scene becomes 25.4 world units long in the Unreal Engine.

|   |   |
| --- | --- |
| ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6ef7863c-c99d-4b7c-b965-382ea0eb7201/datasmith-units-1.png) | ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0979fcd7-3b4b-44c5-9a78-38fe472c661a/datasmith-units-2.png) |
| Source | After import |

When a scene hierarchy contains parents with non-uniform scales and custom pivot transforms that are compensated for at the level of individual objects, the complexity of the coordinate system conversions can make the results in Unreal Engine not match your initial scene. If you encounter this problem, you may be able to solve it by returning to your original scene and simplifying the transforms in your scene hierarchy.

## Names and Labels

Datasmith detects naming information about the geometry in your source application, and reuses this information as much as possible for the Assets and Actors that it creates. The exact process is a little different for each different application or file format, and the results in the Unreal Engine may be slightly different from your source application, but the ultimate goal is to make it possible for you to find and manage your content after import.

For Static Meshes, you'll see that the name of the Asset in the Content Browser, the filename of the Asset on disk, and the name of the Actor in the Level are often different.

-   **Content Browser label -** Datasmith generates the label for each Static Mesh Asset in the Content Browser based on the naming information it finds in your source file, if any. Some supported applications and file formats allow multiple objects to exist with the same name. If this is the case in your scene, you may find that several Assets in the Content Browser end up with the same label.
    
-   **Filename -** However, the file name of each Asset on disk needs to be unique. Therefore, Datasmith names each Asset file using a unique identifier that it extracts from the source application.
    
-   **Actor name -** Each time Datasmith places an Actor into a Level, it tries to give that Actor exactly the same name the corresponding object had in your source file, if any. If it can't find a unique name, it reuses the same label from the Content Browser to name the Actor. If another Actor already exists in the Level with that name, Datasmith makes the Actor name unique by incrementing a numeric suffix.
    

Note that there is a distinction between the *labels* that you see for Static Mesh Assets in the Content Browser, and the *names* of the files Datasmith generates for those Assets on disk. This should be transparent for most purposes while you're working in the Editor. However, if you want to use Blueprint or Python scripting to work with your Assets or your Datasmith Scene, you may need to be aware of this distinction.

## Triangle Facing Direction

In order to achieve the best possible performance at runtime, Unreal Engine culls any triangles that it doesn't expect to be visible. This avoids spending any GPU cycles to render those triangles. In particular, the Engine assumes that all objects have a thickness. Any triangles that face away from the camera are assumed to be the back side of that object, and will be hidden from view by the front side of the object. This is called *back-face culling*, and it's an optimization technique that is used extensively in 3D rendering.

However, some design applications do not make the same distinction between the front and back faces of a surface, and may render surfaces regardless of which side you view them from. When working in your design tool, you may not always be aware of the facing direction of a given surface. This can lead to the surface normal, which is the direction perpendicular to the surface, pointing inward, or away from the direction that you need the surface to be viewed from. This may lead you to create planar, single-walled geometry without any thickness at all.

After you import your scene, this may cause some parts of your scene to be invisible when viewed from certain angles in the Unreal Engine. It may even look as if those parts of your model were not imported; however, the likelihood is that their surface normals are pointing away from the camera you're using to view the scene. If you rotate around the model, you may find that those surfaces suddenly appear.

For example, in the following scene (on the left), the ceiling and the ends of the pipes appear to be missing, even though the geometry was imported correctly. Enabling the **Two Sided** option for the Materials makes the surfaces appear (see below for details).

![Single sided](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5976091f-abb8-4202-b2a0-26fc68c13945/datasmith-two-sided-off.png)

![Two Sided](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c2cea8d9-83cc-4307-b260-a6f3d622deee/datasmith-two-sided-on.png)

The best way to deal with this situation is in your source application. Keep the following suggestions in mind:

-   We highly recommend modeling all objects with thickness whenever they need to be seen from all sides, and making sure that the normals face outward.
    
-   If you know that your object will only need to be viewed from one side, you can fix the missing mesh by flipping the normal of the surface in your source application and re-importing the scene. This leaves the surface as one-sided, but at least inverts the facing direction of the surface so that it appears correctly when viewed in the Unreal Engine from the direction you need.
    
-   Some modeling applications, such as Rhino, 3ds Max, Cinema 4D and SketchUp, offer viewport modes that make it easier to find back-facing triangles. See the documentation for your modeling tool for details.
    

However, if you want to fix the problem in the Unreal Editor without going back to your source scene, you could also consider the following options:

-   You can flip the orientation of the triangles in the Static Mesh Editor so that they face the other direction. See [Modeling Mode Overview](/documentation/en-us/unreal-engine/modeling-mode-in-unreal-engine). However, the same problem will still remain if those triangles are visible from the other side. This may be a good solution for something like a ceiling that will only be seen from the inside, but not for an interior wall that can be seen from both sides. Keep in mind that if you ever modify this piece of geometry in your source scene and re-import your Datasmith Scene Asset, you'll lose the changes you made in the Static Mesh Editor. So if you have to go back and modify your geometry for another reason, make sure to go back and fix the orientation of the faces in SketchUp at the same time.
    
-   You can make the Material two-sided in the Material Editor. This makes the Engine render the surface when it is seen from either side. Although this sounds at first like a good solution, it tends to produce visual artifacts when used with **Static** or **Stationary** lighting, as both sides of the surface will use the same space in the lightmap texture. If your Material is a Material Instance, look in the **Details** panel of the Material Editor for **General > Material Property Overrides > Two Sided**. Or, you can find this property in the **Details** panel of the **Material Editor**.
    
    Click for full image.
    
-   You may have an issue not with the visibility of the face itself, but only with light coming through the object — such as a ceiling that does not correctly block light from a directional light overhead. To address this, configure the Static Mesh Actor so that it casts shadows from both sides. Look in the **Details** panel for the **Lighting > Shadow Two Sided** setting.
    
    Click for full image.
    

Unreal Engine offers multiple ways to light your scene. The method that offers the best runtime performance, and typically the smoothest, most realistic spread of indirect illumination, is *baked* lighting. To use this approach in Unreal Engine, you give the lights in your scene a **Mobility** setting of either **Static** or **Stationary**, then use a tool in the Unreal Editor called [Lightmass](/documentation/en-us/unreal-engine/lightmass-basics-in-unreal-engine) to build the lighting for the scene. This calculates the light that hits each object in the scene from those Static and Stationary lights, and stores it in a special kind of texture, called a *lightmap*. At runtime, this lighting information is applied from each object's lightmap texture to its surface.

In order for this system to work, every vertex in a Static Mesh needs to be mapped to a unique coordinate in the 2D space of its lightmap texture. This mapping is called a UV set or UV channel. Moreover, this 2D coordinate space needs to be laid out in such a way that no two triangles in the mesh overlap each other in the 2D texture space. If two triangles in the mesh are mapped the same area of the 2D texture, then Lightmass won't be able to store a unique pattern of light and shadow for each of those triangles. This causes odd lighting artifacts at runtime.

To ensure that all your Static Meshes are ready to receive static lighting, Datasmith automatically invokes the Unreal Editor's automatic UV unwrapping system for each Static Mesh it imports. This process adds two new UV sets to each Static Mesh:

-   One is a simple unwrapping of the triangles that make up the mesh into a flat representation in 2D space. This breaks the mesh into multiple smaller "islands" that each represent a connected section of the mesh surface.
    
-   The islands in the first lightmap are then rearranged and resized to fit into a layout that avoids any overlap, and that minimizes wasted space around the islands. This is the final layout that will be used for the object's lightmap when you build the lighting for your Level.
    

Then, Datasmith automatically sets up the Static Mesh Asset to use the second generated UV for storing and applying lightmaps.

If you use 3ds Max, and you have already set up UV channels that you want to use for your lightmaps, refer to the [Datasmith for 3ds Max](/documentation/en-us/unreal-engine/using-datasmith-with-3ds-max-in-unreal-engine) guide.

## Collisions and Physics

By default, Datasmith doesn't set up any physics for the Static Mesh Assets it creates. You can set up physics for your Static Meshes in the Unreal Editor after you import; for details, see [Setting up Collisions With Static Meshes](/documentation/en-us/unreal-engine/setting-up-collisions-with-static-meshes-in-unreal-engine), or [Setting up Collisions With Static Meshes in Blueprint and Python](/documentation/en-us/unreal-engine/setting-up-collisions-with-static-meshes-in-blueprints-and-python-in-unreal-engine).

If you're working with 3ds Max, you can model your own custom geometry in 3ds Max, and have the Datasmith importer automatically assign that geometry to the Static Mesh Assets it creates. For details, refer to the [Datasmith for 3ds Max](/documentation/en-us/unreal-engine/using-datasmith-with-3ds-max-in-unreal-engine#customcollisionshapes) page.

## Lights

Datasmith imports light sources from file formats that support them, converting them automatically into the most appropriate type of light supported by Unreal Engine: typically, a [Point Light](/documentation/en-us/unreal-engine/point-lights-in-unreal-engine), [Spot Light](/documentation/en-us/unreal-engine/spot-lights-in-unreal-engine), [Rectangular Area Light](/documentation/en-us/unreal-engine/rectangular-area-lights-in-unreal-engine), or [Directional Light](/documentation/en-us/unreal-engine/directional-lights-in-unreal-engine).

### Area, Plane, and Volume Lights

Some applications, such as 3ds Max and Cinema 4D, support lights that are emitted from 2D shapes or 3D volumes. These types of lights do not have an exact counterpart in the Unreal Engine. This includes mental ray area lights, V-Ray and Corona plane, disc, dome and sphere lights, and so on. When Datasmith imports one of these area lights, it mimics the light's behavior using a special, custom-written Blueprint class called **DatasmithAreaLightMesh**.

![Area light off](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/05ba9c58-8988-42b9-912e-d7ba9350f056/5-0-070-light-off.png)

![Area light on](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7ee937f4-e3a0-4861-9bf7-c47cbfa3dc73/5-0-070-light-on.png)

This Blueprint essentially pairs an auto-generated emissive surface with an auto-generated Rect Light, Point Light, or Spot Light:

-   The job of the emissive surface is to represent the visible, physical extents of the light in the Level's 3D space, and in reflections from other surfaces.
-   The job of the Rect Light, Point Light, or Spot Light is to emit the actual light out into the scene.

You can control the shape, size, color, and intensity of the emissive glow, and the properties of the Light Actor. Select the **DatasmithAreaLightMesh** Actor in the **Level Viewport** or **World Outliner**, and use the settings in the **Light** category of the **Details** panel. For example:

Click for full image.

Some settings, such as **Color** and **Intensity**, affect both the emissive glow and the Light Actor.

The result of this setup is a light that has a visible presence in the scene, and that illuminates surrounding objects. However, unlike in offline renders you might do in your source application, if your **DatasmithAreaLightMesh** uses a Spot Light or a Point Light, the actual light the DatasmithAreaLightMesh emits into the Level is cast from a single point rather than from the whole surface.

The emissive surface does not currently cast any light out into the scene, regardless of whether you bake your lighting using Lightmass or whether you use dynamic lighting. Only the Point Light or Spot Light Component actually illuminates the surrounding objects in the Level.

## Materials

The Datasmith import process creates a new Material Asset in the Unreal Engine Project to represent each different set of geometry surface properties it recognizes in the scene it imports. Although the goal of the scene transformation is to carry over surface properties with the best possible fidelity, you'll likely need to tweak these Materials after import. You can double-click any Material Asset to edit it.

Most of the Material Assets that you'll find in the **Materials** folder are Material Instances. That means that when you edit the Material Instance, you'll see a pre-set list of settings that are determined by its parent or "master" Material. In the Content Browser you can see whether a material is a Material Instance.

Click for full image.

For more information about what Material Instances are and how to work with them, see [Instanced Materials](/documentation/en-us/unreal-engine/instanced-materials-in-unreal-engine) and [Creating and Using Material Instances](/documentation/en-us/unreal-engine/creating-and-using-material-instances-in-unreal-engine).

Each Material Instance also has a Parent Material: a different kind of Material Asset that contains a node graph similar to a Blueprint. This graph determines the actual operations that are carried out on the GPU when the Unreal Engine needs to render a surface that has the Parent Material or any of its Material Instances applied. The way the Parent Material's graph is constructed also controls the settings that are exposed in its Material Instances, and how those settings are used.

Datasmith assigns your Material Instances different Parent Materials depending on your source application, according to the following principles:

-   In most cases, Datasmith assigns each Material Instance a pre-existing Parent Material that is included as part of the Datasmith plugin. Typically, the pre-defined settings exposed by these Parent Materials are very similar to the material authoring settings that are available in your source application.
    
    You can freely edit these exposed settings in each Material Instance that Datasmith creates in your Project. Each different Parent Material offered by Datasmith offers a different set of properties:
    
    -   **Datasmith\_Color -** This Parent Material is used for solid colors and textured surfaces, mostly when importing CAD models. See [The Datasmith Color Material](/documentation/en-us/unreal-engine/datasmith-import-process-in-unreal-engine#thedatasmithcolormaterial) below.
    -   **SketchUpMaster -** This Parent Material is used for all surfaces imported from SketchUp. See the [SketchUp Pro](/documentation/en-us/unreal-engine/using-datasmith-with-sketchup-pro-in-unreal-engine) interop guide.
    -   **RevitMaster -** This Parent Material is used for all surfaces imported from Revit. See the [Revit](/documentation/en-us/unreal-engine/using-datasmith-with-revit-in-unreal-engine) interop guide.
-   If you're importing content from 3ds Max or Rhino, you may find that Datasmith also creates new Parent Materials in your Project, inside the `Materials/Master` folder. 3ds Max offers a much richer Material authoring workflow than most other source applications, and one that is conceptually similar to Unreal Engine Material graphs. Therefore, Datasmith is typically able to create new Master Materials that are very close to the custom Materials you have in 3ds Max, rather than having to reuse pre-set Parent Materials that have a pre-set graph and a pre-set list of exposed settings. In this case, Datasmith typically still creates Material Instances for those custom Parent Materials. It then applies those Material Instances to your Static Mesh Assets and to the Static Mesh Actors in your scene. In most cases, modifying the properties of the Material Instances should be enough to give you a good level of control over the rendered results. For some types of 3ds Max Materials, Datasmith may skip creating the Material Instances. In this case, it simply assigns the new Parent Material to your Static Mesh Assets and Actors.
    

If you want to alter the actual Material graph that a Material Instance uses to determine how to shade the surface based on those properties, you need to duplicate the Parent Material and modify the properties in your duplicate. For details on this process, see [Modifying a Datasmith Master Material](/documentation/en-us/unreal-engine/modifying-a-datasmith-master-material-in-unreal-engine).

Another option, instead of working with the Materials created by Datasmith, is always to completely replace the Material created by Datasmith with another physically based Material. This could be a Material that you create yourself in Unreal Editor, or from a third-party.

### The Datasmith Color Material

Many computer-aided design (CAD) applications use simple surface colors to shade geometry. Datasmith typically brings these sufaces into Unreal as Instances of the **Datasmith\_Color** Material.

-   The color of this Material is typically pre-set to exactly match a color from your source scene. When you use these Materials in the Unreal Engine, pay particular attention to the brightness of the color values. Design tools sometimes allow very bright surface colors — even including solid white — that are not often found in nature. You may need to tone these values down substantially in order for your lighting to look realistic.
    
-   Datasmith is typically able to respect the opacity of your source materials. If a surface color in your source scene is set to be semi-transparent, such as a glass panel, Datasmith brings its opacity into the **Alpha** channel of the Color setting. If you want to use the Alpha channel to make a previously non-transparent Material become semi-transparent in the Unreal Editor, you'll also have to change the Material's blending mode. In the **General** section, expand the **Material Property Overrides** group, check the **Blend Mode** option, and set its value to **Translucent**. 
    
-   The Datasmith\_Color parent Material also allows you to use three different kinds of texture maps: a diffuse map that provides the base color of the surface (overriding the Color setting), a normal map that provides fine surface details, and a transparency map that allows different parts of the same surface to have different opacity values. Datasmith may use these texture map settings if it can export those kinds of texture maps from your source application. If you have a Datasmith\_Color Instance with a  flat color, and you want to use texture maps like these in order to increase the realism of your surface, you might want to activate these settings and assign Texture Assets to them. When you enable one of the Map settings, you're offered a new setting under Texture Parameter Values where you can set the Texture you want to use.
    
    However, you might be better off learning how to create your own Material from scratch, so that you can take advantage of other physically based properties of the Unreal Engine renderer that are not exposed by the Datasmith\_Color parent Material, such as the Roughness and Metallic properties. See [Physically Based Materials](/documentation/en-us/unreal-engine/physically-based-materials-in-unreal-engine).
    

## Animations

If your source scene contains objects with animated 3D transforms — objects whose translation, rotation, and/or scale values change over time — Datasmith can import those animations into your Unreal Engine project. It creates a new Level Sequence that contains a track for each animated object in the scene, and saves this Level Sequence into the **Animations** folder next to your Datasmith Scene Asset. You can use this Level Sequence to play back the animation in the Unreal Editor or in the Unreal Engine at runtime.

For example, in this 3ds Max scene, the sections of this garage door are animated to move along a spline, and at the same time the camera is animated to rotate around the object.

After import, you can double-click the Level Sequence Asset in the **Content Browser** to open it up in the Sequencer UI and play back the animation.

For example, in this video, the Level Viewport is set to show the view from the camera in the Datasmith scene, so the animated result looks the same as the original in 3ds Max.

There are some important things to note about this workflow:

-   Datasmith does not import any animation curves. Instead, for each frame in the original source animation, it bakes a keyframe for each animated object that contains that object's current transform.
    
-   Datasmith does not handle animations on sub-objects, mesh deformations, object properties, or skeletal rig animations. It only handles animations that change the overall translation, rotation, or scale of a scene object in 3D space.
    

For more about Level Sequences and how to work in the Sequencer UI, see the documentation on the [Sequencer Editor](/documentation/en-us/unreal-engine/real-time-compositing-with-sequencer-in-unreal-engine).

Support for importing animations is currently limited to scenes imported from 3ds Max, Cinema 4D, VRED, Deltagen, and glTF files. (For instructions on how to include animations from a 3ds Max scene in your exported Datasmith file, see [Exporting Datasmith Files from 3ds Max](/documentation/en-us/unreal-engine/exporting-datasmith-files-from-3ds-max-to-unreal-engine).)

### Rendering Camera Animations

If your source scene contains an animated camera, the Level Sequence that Datasmith creates will contain a track for the corresponding CineCameraActor in your Unreal Engine Level. This track contains keyframes that store the 3D transforms of that camera as it moves and rotates in 3D space. If you select that CineCameraActor in the **World Outliner** and play the Level Sequence in the Unreal Editor, you'll see that the camera's preview window in the Level Viewport plays back the animation from that camera's point of view.

However, if you need to render the Level Sequence to a movie file or image sequence on disk from the animated camera's point of view, you need to first add a **Camera Cut** track to the Level Sequence, and add your animated camera to that Camera Cut track.

1.  Double-click your Level Sequence to open it in the Sequencer UI.
    
2.  Click the **\+ Track** button, then select **Camera Cut Track** from the menu.
    
    Click for full image.
    
3.  Click the **\+ Camera** button on the new **Camera Cuts** track, and select the camera whose point of view you want to use. If you want to use a camera that is already animated in the Level Sequence, you can select it from the **Existing Binding** list.
    
    Click for full image.
    
    When your Level Sequence contains many animated tracks, it may be hard to find the camera you want in the **Existing Binding** list. If so, you can select your camera from the **New Binding** list instead, or to drag your CineCameraActor from the **World Outliner** to the new **Camera Cuts** track in the Sequencer UI.
    
4.  Your CineCameraActor is represented in the Camera Cuts track by a block in the timeline. If necessary, drag the left and right boundaries of this block to line up with the start and end of the animation.
    
    Click for full image.
    
5.  Next time you render the Level Sequence, it will render each frame from the point of view of the camera in the Camera Cuts track.
    

You can add multiple different CineCameraActors to the Camera Cuts track to make the render switch back and forth between them automatically at different times.

For more information, see also [Working with Camera Cuts](/documentation/en-us/unreal-engine/cinematic-camera-cut-track-in-unreal-engine) and [Take Recorder](/documentation/en-us/unreal-engine/take-recorder-in-unreal-engine).

### Using Animations In Multiple Levels

Every Level Sequence contains references to Actors within a single specific Level. When you use Datasmith to import a scene that contains animation, the Level Sequence will contain references to the animated Actors in the Level that you have open at the time you import your scene.

If you later drop the same Datasmith Scene Asset into a different Level, the Level Sequence won't be able to find the same Actors in that new Level. The track names show up in red in the Sequencer, and playing the sequence with the new Level open has no effect. You have a few options to fix this:

-   You can update the Level Sequence to point to the copies of the Actors in the new Level.
    
    With your new Level open, click the General Settings icon in the Sequencer Toolbar, and choose **Fix Actor References** from the menu.
    
    Click for full image.
    
    The Actor tracks should return to their usual color. Then, save your change to the Level Sequence.
    
    The Level Sequence can only work with one level at a time. When you assign it to the new level, it will no longer work with the old one.
    
-   You can duplicate the Level Sequence Asset in the Content Browser before you fix its Actor references as described above. That way, you'll have one Level Sequence that works in the original Level you imported your content into, and another that works in your new Level.
    
    If you reimport your Datasmith Scene Asset, only the original Level Sequence is updated with changes to the animation in the source scene. You may need to recreate your duplicate and fix its Actor references again.
    
-   If you need the same imported Level Sequence animation to work within multiple Levels, consider using *sublevels*. You can import your Datasmith scene into an empty Level, then add that Level as a sublevel inside each of the Levels that you need to play the animation. For more information on what sublevels are and how to use them, see [Managing Multiple Levels](/documentation/en-us/unreal-engine/managing-multiple-levels-in-unreal-engine).
    

### Animation Timing and Frame Accuracy

Playing back a complex animation that contains many tracks and keyframes can sometimes result in hitches and "pops" as the playback adjusts for inconsistencies between the frame rate of the animation and the number of frames per second being rendered by the Unreal Engine. To avoid this and ensure the smoothest possible playback, Datasmith always enables the **Lock to Display Rate at Runtime** property on the Level Sequences that it creates.

You'll find this setting in the **Sequencer** UI here:

Click for full image.

This should improve the smoothness of your animations. However, you should be aware that it constrains the maximum frame rate of the Engine to the frame rate of your animation. If you need the Engine to run at a greater frame rate, this may not be an appropriate solution. For example, if your animation clip was authored in your source application at 24 or 30 frames per second, but you need your animation to play back in VR at 90 frames per second, constraining the Engine's frame rate to the animation's frame rate may not be a good solution for you. In cases like these, you may need to disable this option on your Level Sequence Assets.

## Layers

If your source application offers the ability to organize your content into layers, or some similar content, Datasmith preserves that organization in the Unreal Editor. You can use the **Layers** window (**Window > Layers**) to show and hide layers, or to quickly find and select all objects in a layer.

However, the Unreal Editor doesn't support *nested* layers. If your source scene uses nested layers, Datasmith automatically flattens the hierarchy of layers into a single list.

For more about how to work with Layers in the Unreal Editor, see [Layers Panel](/documentation/en-us/unreal-engine/layers-panel-in-unreal-engine).

## Metadata

For some kinds of source file formats, Datasmith imports metadata about the geometry objects in your scene that you set in your source application. You can access this metadata in the Unreal Editor using Blueprint and Python scripts. For details on this system, see [Using Datasmith Metadata](/documentation/en-us/unreal-engine/using-datasmith-metadata-in-unreal-engine).

### Technical Application-Specific Metadata

Some third-party applications and file formats provide access to technical metadata values about individual scene objects, such as their unique IDs, object classes, or other application-specific data. Datasmith imports this kind of technical data into Component Tags that it assigns to the Static Mesh Component that represents each object's geometry in the Level.

You can access the metadata from the Details Panel.

1.  Select the Actor whose Component Tags you want to view in the **Level Viewport** or in the **World Outliner**.
    
2.  In the **Details** panel, select the Static Mesh Component assigned to the Actor.
    
3.  Scroll down in the **Details** panel to find the **Tags > Component Tags** list.
    

Click for full image.

This kind of technical information is typically specific to the source application that created the object. Therefore, it is kept separate from the Datasmith Metadata described in the previous section. Datasmith Metadata, by contrast, is typically intended to represent "real-world" information about individual scene objects, such as their BIM data, construction properties, cost, or manufacturer; or, it may represent custom user-defined properties that have a specific meaning in your production workflow.