# Skeletal Meshes

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/skeletal-mesh-assets-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/skeletal-mesh-assets-in-unreal-engine)  
**Processed:** 2025-06-14 16:50:40

---

Characters in **Unreal Engine** are created using multiple unique assets that render the visual geometry, play animations, and construct logic that control the character's behaviors in real time. The foundational asset for characters in Unreal Engine is the **Skeletal Mesh** asset, which contains the character's visual mesh, or geometric model render of the character, and the character's [skeleton](https://dev.epicgames.com/documentation/en-us/unreal-engine/skeletons-in-unreal-engine) that contains bone data, which is used to animate the character.

A Skeletal Mesh asset is created in external **Digital Content Creation** (**DCC**) software and exported as an `.fbx` file. FBX files are then [imported into Unreal Engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/importing-skeletal-meshes-using-fbx-in-unreal-engine) projects. After importing a character into Unreal Engine, you can view and edit the components of the Skeletal Mesh asset in the [Skeletal Mesh Editors](https://dev.epicgames.com/documentation/en-us/unreal-engine/animation-editors-in-unreal-engine), such as the characters [Mesh](https://dev.epicgames.com/documentation/en-us/unreal-engine/skeletal-mesh-editor-in-unreal-engine), [Skeleton](https://dev.epicgames.com/documentation/en-us/unreal-engine/skeleton-editor-in-unreal-engine), [physics asset](https://dev.epicgames.com/documentation/en-us/unreal-engine/physics-asset-editor-in-unreal-engine) and [animation sequence](https://dev.epicgames.com/documentation/en-us/unreal-engine/animation-sequence-editor-in-unreal-engine) properties.

For more information about importing character FBX files into Unreal Engine, refer to the following documentation:

[

![Importing Skeletal Meshes Using FBX](https://dev.epicgames.com/community/api/documentation/image/62cefaf3-4ce3-4ca2-8803-8a65f0a24865?resizing_type=fit&width=640&height=640)

Importing Skeletal Meshes Using FBX

Learn how to import skeletal meshes.





](https://dev.epicgames.com/documentation/en-us/unreal-engine/importing-skeletal-meshes-using-fbx-in-unreal-engine)

FBX files imported into Unreal Engine as Skeletal Mesh assets will contain the character's model, and skeleton. The character's skeleton will be imported as an additional asset called a [Skeleton asset](https://dev.epicgames.com/documentation/en-us/unreal-engine/skeletons-in-unreal-engine), which you can view and edit in the [Skeleton Editor](https://dev.epicgames.com/documentation/en-us/unreal-engine/skeleton-editor-in-unreal-engine).

![ImageAltText](https://dev.epicgames.com/community/api/documentation/image/b3d98715-44ec-4bf5-a800-4edcb5f85c7d?resizing_type=fit&width=1920&height=1080)

![ImageAltText](https://dev.epicgames.com/community/api/documentation/image/a66c1356-1294-49fc-823e-096ae4ac2ecf?resizing_type=fit&width=1920&height=1080)

ImageAltText

ImageAltText

FBX files can also contain animations for the character, and are imported along with the character model, as [Animation Sequence assets](https://dev.epicgames.com/documentation/en-us/unreal-engine/animation-sequences-in-unreal-engine). Animation Sequences can be viewed and edited using the [Animation Sequence Editor](https://dev.epicgames.com/documentation/en-us/unreal-engine/animation-sequence-editor-in-unreal-engine). Animation Sequence assets can be dynamically played on a characters using [Character](https://dev.epicgames.com/documentation/en-us/unreal-engine/characters-in-unreal-engine) and [Animation Blueprints](https://dev.epicgames.com/documentation/en-us/unreal-engine/animation-blueprints-in-unreal-engine) at runtime, as well as used in authored cinematics using [Sequencer](https://dev.epicgames.com/documentation/en-us/unreal-engine/cinematics-and-movie-making-in-unreal-engine).

[![ImageAltText](https://dev.epicgames.com/community/api/documentation/image/0ada8a59-3d5c-4437-a3bf-b8de581e395c?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/0ada8a59-3d5c-4437-a3bf-b8de581e395c?resizing_type=fit)

After importing a character's Skeletal Mesh asset, along with its accompanying Skeleton asset and Animation Sequences, you can add the Skeletal Mesh asset directly into a level. In order to control a Skeletal Mesh asset, as a Character or other non-playable characters and objects, you must create a Character blueprint and add the Skeletal Mesh as a [Mesh component](https://dev.epicgames.com/documentation/en-us/unreal-engine/anatomy-of-a-blueprint-in-unreal-engine) to build game and animation logic to govern its behaviors and assemble its parts.

## Create a Character Blueprint

There are many ways a Character Blueprint can be built depending on your character and projects needs, here you can follow an example workflow of building a simple character blueprint to apply animations to your character in a level.

[![ImageAltText](https://dev.epicgames.com/community/api/documentation/image/a3af51fa-0b5c-4dce-9bc8-88d5730a4f5e?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/a3af51fa-0b5c-4dce-9bc8-88d5730a4f5e?resizing_type=fit)

To create a character blueprint navigate in the **Content Browser** and use (**+**) **Add** to select **Blueprint Class**.

[![ImageAltText](https://dev.epicgames.com/community/api/documentation/image/57f79945-7ae8-4acb-bba2-e5516f3d598c?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/57f79945-7ae8-4acb-bba2-e5516f3d598c?resizing_type=fit)

Then Select the Character class option and select create.

[![ImageAltText](https://dev.epicgames.com/community/api/documentation/image/62991f7f-a4a1-43e0-a797-aa42ac48a8c8?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/62991f7f-a4a1-43e0-a797-aa42ac48a8c8?resizing_type=fit)

In the **Content Bowser**, **name** and **open** your Character Blueprint asset.

[![ImageAltText](https://dev.epicgames.com/community/api/documentation/image/bb5c4077-e700-49f5-9c27-a463abe63dd3?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/bb5c4077-e700-49f5-9c27-a463abe63dd3?resizing_type=fit)

In the blueprint's **Components** panel, select the **Mesh** component, and navigate in the **Details** panel to the **Skeletal Mesh** property.

[![ImageAltText](https://dev.epicgames.com/community/api/documentation/image/6e39d593-d247-4d19-b929-74602274e6aa?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/6e39d593-d247-4d19-b929-74602274e6aa?resizing_type=fit)

Using the drop-down menu, select your **Skeletal Mesh** asset.

[![ImageAltText](https://dev.epicgames.com/community/api/documentation/image/84858710-447b-4b7b-893d-fa51df806d62?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/84858710-447b-4b7b-893d-fa51df806d62?resizing_type=fit)

Position your Skeletal Mesh in the **Viewport** panel to align with the **Arrow** and **Capsule** components..

After saving and compiling your blueprint, you can then add the Character Blueprint to your level.

[![ImageAltText](https://dev.epicgames.com/community/api/documentation/image/df44e268-f204-4207-be8e-1ff9e38a1d2a?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/df44e268-f204-4207-be8e-1ff9e38a1d2a?resizing_type=fit)

You can create gameplay controls and behaviors using the Character Blueprint's **Event Graph** and functions.

For more information about setting up a character in Unreal Engine, refer to the following documentation:

[

![Setting Up a Character](https://dev.epicgames.com/community/api/documentation/image/e94e1f40-81fe-4d28-a1d9-2797920a4324?resizing_type=fit&width=640&height=640)

Setting Up a Character

A high-level overview of how to set up a basic character or Skeletal Mesh in Unreal Engine.





](https://dev.epicgames.com/documentation/en-us/unreal-engine/setting-up-a-character-in-unreal-engine)

### Modular characters

Some characters are built using multiple skeletal meshes that represent pieces of a character, and are assembled in the level. This is common when creating characters that may change outfits or appearances, or have dynamic elements that depend on gameplay sineros, or player achievements.

[![ImageAltText](https://dev.epicgames.com/community/api/documentation/image/771ef4bb-c98d-41d0-bd30-13baac4fe7c4?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/771ef4bb-c98d-41d0-bd30-13baac4fe7c4?resizing_type=fit)

For more information about creating modular characters in Unreal Engine, see the following documentation:

[

![Working with Modular Characters](https://dev.epicgames.com/community/api/documentation/image/b41309a7-b700-45a1-98c4-7289b791a9fb?resizing_type=fit&width=640&height=640)

Working with Modular Characters

Create characters by combining multiple skeletal mesh components.





](https://dev.epicgames.com/documentation/en-us/unreal-engine/working-with-modular-characters-in-unreal-engine)

## Animating Skeletal Meshes

Animation Sequences can be played on a Skeletal Mesh's Skeleton asset. You can play animations by assigning a Character Blueprint's Mesh component's **Animation Mode** property to **Use Animation Asset** and then selecting an Animation Sequence asset in the **Anim to Play** property's drop-down menu.

After saving and compiling the blueprint, this animation will play on the character blueprint in the level.

### Animation Blueprints

Using an [animation blueprint](https://dev.epicgames.com/documentation/en-us/unreal-engine/animation-blueprints-in-unreal-engine), you can create animation logic, such as [blend spaces](https://dev.epicgames.com/documentation/en-us/unreal-engine/blend-spaces-in-unreal-engine), to play animation sequence on the character model in the level.

To create an Animation Blueprint for a Skeletal Mesh, open the content browser, and select **Add** (**+**) > **Animation** > **Animation Blueprint**, and select the skeleton asset imported with your skeletal mesh.

[![ImageAltText](https://dev.epicgames.com/community/api/documentation/image/c8288c15-aad8-4a37-ae41-745510d733aa?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/c8288c15-aad8-4a37-ae41-745510d733aa?resizing_type=fit)

You now have access to an [Anim Graph](https://dev.epicgames.com/documentation/en-us/unreal-engine/animation-workflow-guides-and-examples-in-unreal-engine) that can dynamically select Animation Sequences to play back on the character based on blueprint logic.

[![ImageAltText](https://dev.epicgames.com/community/api/documentation/image/7133c2ef-1df3-4631-87eb-e0bab42f58d5?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/7133c2ef-1df3-4631-87eb-e0bab42f58d5?resizing_type=fit)

### Animating Compatible Skeletal Meshes

Multiple Skeletal Meshes assets can be linked when they share the same or very similar skeleton structures. Skeleton compatibility can be manually set when skeletons share a similar structure using identical naming conventions.

[![ImageAltText](https://dev.epicgames.com/community/api/documentation/image/a2f30018-b66c-4f83-a1e6-76756488db8a?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/a2f30018-b66c-4f83-a1e6-76756488db8a?resizing_type=fit)

For more information about skeleton compatibility and sharing animations across multiple meshes, refer to the [Sharing Skeletons section of the Skeleton Asset](https://dev.epicgames.com/documentation/en-us/unreal-engine/skeletons-in-unreal-engine) documentation.

### Non-Skeleton Animation

In addition to Animation Sequences, you can animate the mesh of Skeletal Mesh assets using deformer animation techniques. Deformers transform the geometry of the mesh rather than the bones, to create more intricate animations, such as facial expressions, skin, clothing, or muscle movement.

For more information about animating Skeletal Meshes using deformers, see the following documentation:

[

![Morph Target Previewer](https://dev.epicgames.com/community/api/documentation/image/a834f8ed-8d52-4627-9b58-6c220ac2470b?resizing_type=fit&width=640&height=640)

Morph Target Previewer

User guide for the editing modes available in the Animation Editor.





](https://dev.epicgames.com/documentation/en-us/unreal-engine/morph-target-previewer)