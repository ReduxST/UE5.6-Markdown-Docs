# Working with Modular Characters

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/working-with-modular-characters-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/working-with-modular-characters-in-unreal-engine)  
**Processed:** 2025-06-14 17:04:50

---

When creating characters in **Unreal Engine** whose appearance can be customized by a player or a game system, such as different outfits or models, you'll want to consider constructing your characters using a **Modular Character blueprint**.

Using a Modular Character blueprint, you can construct a character at runtime using multiple [Skeletal Mesh assets](/documentation/en-us/unreal-engine/skeletal-mesh-assets-in-unreal-engine) that are able to be swapped using blueprint logic, rather than importing a single Skeletal Mesh model for the full character. Using a Modular Character blueprint is a more flexible option when creating characters with a modular appearance and performs more efficiently than swapping an entire mesh.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f620cd80-ca33-4cb1-8026-7c7a9c2318f4/overview.png)

## Modular Character Set-Up Methods

When creating Modular Character systems in Unreal Engine, you can select from a few different set-up methods, that each cater to different project needs and scopes. The following are brief descriptions of each method, along with its strengths and weaknesses.

-   [Set Leader Pose Component](/documentation/en-us/unreal-engine/working-with-modular-characters-in-unreal-engine#leaderposecomponet) constructs the character by parenting skeletal mesh objects to a parent skeletal mesh object, and runs the animations exclusively on the parent. This offers the quickest set-up time but does not support isolated animation playback or physics rendering, and can carry an expensive Render Thread performance cost. The Set Leader Pose is a good starting point for setting up your first Modular Character in Unreal Engine.
    
-   [Copy Pose from Mesh](/documentation/en-us/unreal-engine/working-with-modular-characters-in-unreal-engine#copyposefrommesh) offers a middle ground solution, that you can use to build physics simulation on each of the Skeletal Mesh objects that comprise the character, in addition to optional isolated animation playback, but is the most expensive for your projects computational processes on both the Game Thread and the Render Thread.
    
-   [Merging Skeletal Mesh](/documentation/en-us/unreal-engine/working-with-modular-characters-in-unreal-engine#skeletalmeshmerge) objects at runtime provides the most comprehensive solution with relatively low performance costs on both the Game Thread and the Render Thread, by combining multiple skeletal mesh objects to render a character whole at runtime. This method however, requires the most set-up and comes at the cost of not being able to utilize a character's morph targets.
    

Here you can reference a chart to illustrate each methods strengths, weaknesses and performance costs:

|   | Leader Pose Component | Copy Pose from Mesh | Skeletal Mesh Merge |
| --- | --- | --- | --- |
| **Setup Cost** | Min | Medium | High |
| **Game Thread Cost** | Min | High | Medium |
| **Render Thread Cost** | High | High | Low |
| **Physics** | No | **AnimDynamics** or **RigidBody** | Yes |
| **Morph Target** | Yes | Yes | No |

#### Prerequisites

-   You will need a group of Skeletal Mesh assets that assemble into a full character. If you do not have a set, you can use the [City Sample Crowds](https://www.fab.com/listings/903037e9-e1ac-4f41-96e8-1683c6fa7ad4) asset pack in **Fab**.

## Leader Pose Component

One method of creating a Modular Character in Unreal Engine, is the **Leader Pose Component** system. The Leader Pose Component Blueprint callable function enables you to set Skinned Mesh Component Objects as children to a Leader Skinned Mesh Component Object. For example, you can define the Torso as the Leader Pose Component, assign an animation to the Torso, then add Feet, Legs, Hands and a Head as children which will follow the animation assigned to the Torso.

When using the Leader Pose Component, child mesh objects do not use any **Bone Transform Buffer** and won't run any animations independently, child meshes can only run animations played on the Leader Pose Component's Bone Transform Buffer. This system creates a lightweight, but limited attachment system.

In the following section, you can follow an example workflow of how to create a modular character using the Leader Pose Component system in Unreal Engine.

### Set Up Leader Pose Component

After importing your Skeletal Mesh assets into your Unreal Engine project, create a new character blueprint, using **Add** (**+**) in the **Content Browser**, and select **Blueprint Class**. In the **Pick Parent Class** window, select the **Character** class option.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e15b2e68-e76e-4a20-828b-f7d0b56c49fa/cb.png)

**Name** and **open** the blueprint.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/65e912a7-c22f-4b43-b45e-5f63264439ef/nameandopen.png)

In the **Components** panel select the mesh component, then in the **Details** panel, define a Skeletal Mesh using the **Skeletal Mesh Asset** property. It is recommended to select a foundational component of the character, such as a head, that will not change based on your game's structure.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d8afff91-38d7-4f94-9ffb-71aeff3e175c/selecthead.png)

If you expect to change all visible components of a character, you can create an empty Skeletal Mesh object as the root skeletal mesh, and use this object as your foundational asset. An empty Skeletal Mesh object may contain a very small amount of geometry that is not visible at runtime, that the other visible meshes can be oriented around.

Adjust the foundational mesh's placement in the **Viewport** panel.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b8bc15ec-9051-41e3-b97e-4bee86b80dad/viewport.png)

In the Components panel, **right-click** the mesh, and select **Duplicate** from the options menu.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/09baa303-e91a-44db-9444-b4acda9a2be5/duplicate.png)

In the **Components** panel select the duplicated mesh component and then in the **Details** panel navigate to the **Mesh** section and select another segment of the modular character in the **Skeletal Mesh Asset** property. In this workflow example the head component was swapped for the torso for the duplicated mesh component.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/54b1c66e-0355-4f35-a0b4-2ae64d529459/selecttorso.png)

If your character's mesh components were exported properly the mesh should snap into the correct position in the **Viewport** panel. If this does not occur, you will need to manually align the mesh components.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/12755d8c-8a1c-45b2-b530-4edb93200d6a/addtorso.png)

**Rename** the duplicate component to match the corresponding mesh component.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b39f44e3-3cb8-4faf-ac41-b6b34535113f/rename.png)

Repeat this process from the foundational mesh component, until all mesh components have been added to the blueprint and your character has all of its pieces.

![ImageAltText](Fullbody.png)(convert:false)

After all mesh components have been added to the character blueprint and are correctly aligned in the **Viewport** panel, open the blueprint's **Construction Script** panel. From the **Construction Script** node, create a **Set Leader Pose Component** node.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/55fdfdf3-6bfd-4ca4-8891-17231aa25b56/createleadernode.png)

Drag instances of each mesh component, contained within your blueprint, into the graph.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2b623d36-8e4d-402d-9cb3-609ab522be2d/dragdrop.gif)

Connect the foundational mesh component to the Set Leader Pose Component node's **New leader Bone Component** input pin.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/52f3aa9e-b6e8-48d7-aef5-ba15c027766c/connectleader.png)

Connect the remaining mesh components to the Set Leader Pose Component node's **Target** input pin.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8035bad5-2343-44ed-93d8-af5453264494/connecttargets.png)

After saving and compiling your character blueprint, your modular character is now assembled and can be added, animated and controlled in your project.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a7df0380-c47d-44ce-94e8-15f101455f79/moddemo.gif)

It is important to know that characters using the Leader Pose Component node reduces the performance cost of the character on the **Game Thread**, but it does not reduce the render cost of the character on the **Render Thread**. The character will still render the same number of Components separately, with additional draw calls for each additional section the Component contains.

It is also important to know that any child mesh object of the Leader Bone has to be a subset with the exact matching structure. You cannot have any other extra joints or skip any joints. Since there is no Bone Buffer data for extra joints, any extra or skipped joints will be rendered using the reference pose.

Child Mesh objects contained within a Modular Character blueprint cannot run unique animations, or simulate physics independently from the Leader Pose component.

## Copy Pose From Mesh

Another method to assemble modular characters in Unreal Engine is the **Copy Pose from Mesh** system. Copy Pose From Mesh is an **AnimGraph** node you can use within the Animation Blueprint of the child meshes that enables you to copy the animation pose from another Skeletal Mesh Component. Copy Pose From Mesh will only copy matching bones, and everything else will use the reference pose.

### Set Up Copy Pose Component

After importing your Skeletal Mesh assets into your Unreal Engine project, create a character blueprint and add each mesh component to the blueprint.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cca10245-edaa-4eb6-92d3-c31c553b27ca/createcopyposechar.png)

Create an Animation Blueprint for the foundational mesh component and assign it in the Mesh Component's **Details** panel, by setting the **Animation Mode** property to **Use Animation Blueprint**, and then selecting your main animation blueprint using the **Anim Class** property.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7606a284-5fec-42f1-910e-f03c9fd69908/assignabp.png)

In this workflow example, the modular character mesh uses the template mannequin's Skeleton asset, and can be assigned to use the `ThirdPerson_AnimBP` animation blueprint found in the [Third Person Template project](/documentation/en-us/unreal-engine/third-person-template-in-unreal-engine).

After assigning this animation blueprint, the foundation mesh, in this case the characters head, will begin to animate leaving the remaining mesh components to output their reference pose.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2e0de22f-3fc2-4e1e-84e6-b614196582b5/headanimating.gif)

Now create an Animation Blueprint asset that will drive the animation pose for each of the remaining child mesh components of the modular character. Create this asset using (**+**) **Add** in the **Content Browser**, and selecting **Animation** > **Animation Blueprint**. Then assign your modular character's Skeleton asset. In this workflow example the mannequin character's skeleton is used.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6a0ea60b-f272-44b1-bf43-aa6ab93efd8a/createabp.png)

**Name** and **open** the Animation Blueprint.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fb690ad8-572a-441b-b445-bfd67f0193fb/childabp.png)

Within the Animation Blueprint, create a reference variable to the foundational mesh component. To create a reference variable, first add a new variable in the **My Blueprint** panel's **Variables** section called `Source Mesh Component` using (**+**) **Add**, and then select **Skeletal Mesh Component** > **Object Reference**.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d63a3d61-0b2d-422b-9301-282667139fc1/createmeshvar.png)

Then in the Animation Blueprint's **Event Graph**, create a **Cast to Blueprint** node to link the Animation Blueprint to your character's blueprint. Create a **Try Get Pawn Owner** node and connect its **Return Value** to the Cast to Blueprint node's **Object** input pin. Dragging off the Cast to Blueprint Node's **output** pin, create a **Get Mesh** node. Finally create a **Set Variable** node for your mesh variable and connect the Get Mesh node's **output** pin to the Set Variable node's **input** pin.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6fd2fcdc-0f05-41db-aa5d-e1ac8caab97a/casttobp.png)

In the **AnimGraph**, create a **Copy Pose From Mesh** node. Add your reference variable to the graph and connect it to the Copy Pose From Mesh node's **Source Mesh Component** input pin. Finally connect the Copy Pose From Mesh node's output pose to the **Output Pose** node.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cd0135c9-2506-4e04-a7f7-8a94a0370821/copyposeanimgraph.png)

In your character blueprint, set each child mesh component to use the new animation blueprint to run on each of your child mesh components. To set the animation blueprint, select each child mesh component in the **Components** panel, and then set the **Animation Mode** property to **Use Animation Blueprint** and the **Anim Class** property to your child mesh animation blueprint.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7cd2eb97-0b33-4fad-8b0f-dfc3077532c0/setchildabp.gif)

When using Copy Pose From Mesh to synchronize animations across multiple mesh components, you will want to make sure that the Skeletal Mesh Component you are coping from has already ticked, otherwise you will copy the last frame's animation. To ensure the foundational mesh has ticked, you can parent the child mesh components to the foundational mesh component by dragging each child mesh object onto the foundational mesh component in the **Comments** panel in the character blueprint.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/85ed7db7-3e34-4118-ad7e-b7b99f7c76a9/parentmeshobjects.gif)

You could also set this relationship in code by setting the foundational mesh's tick as a prerequisite for the child mesh evaluation. See the [Tick Dependency](/documentation/en-us/unreal-engine/actor-ticking-in-unreal-engine#tickdependency) documentation for more information.

When building modular characters using the Copy Pose from Mesh method, you have access to a full animation graph for each of the mesh components, which enables you more dynamic control of isolating animation playback. Additionally you are able to build light physics simulations for each mesh component independently, using the [RigidBody](/documentation/en-us/unreal-engine/animation-blueprint-rigid-body-in-unreal-engine) or [AnimDynamics](/documentation/en-us/unreal-engine/animation-blueprint-animdynamics-in-unreal-engine) nodes.

It is important to note however, that using Copy Pose From Mesh is a more performance expensive process than using the Leader Pose Component system because an animation graph evaluation must run on each child.

## Skeletal Mesh Merge

When creating modular characters within Unreal Engine, you can also merge multiple meshes at runtime into a single Skeletal Mesh using the Merge Meshes blueprint function node. While this method has a high initial performance cost of creating the Skeletal Mesh, the recurring rendering cost is lower than other methods since you are rendering a single Skeletal Mesh instead of multiple meshes.

For example, if you have a character composed of three Components (head, body and legs) and you have 50 characters on screen, this would result in 50 draw calls. Without Skeletal Mesh Merge, each Component has its own draw call resulting in three calls per character or a total of 150 draw calls.

When using `FSkeletalMeshMerge`, your main mesh component must contain a full skeleton with all of the character's animations because the merged mesh will only use the Skeleton that's set to the main mesh component. Even if you have extra joints for certain body parts, a successful mesh merge requires that you still have to have all the animations contained and running on the main mesh component.

It is also important to note that a merged mesh only run one animation at once and transferring [Morph Targets](/documentation/en-us/unreal-engine/morph-target-previewer) to the merged mesh is not supported. However, you can create a workaround to apply Morph Targets to a merged skeletal mesh by looking at `FSkeletalMeshMerge::GenerateLODModel`. After a merged mesh has been created at runtime, you can apply Morph Targets by calculating the `FMorphTargetDelta` between your base mesh and any morphs.

Additionally when using `FSkeletalMeshMerge` you will likely need to tailor build your content with this method in mind from the start. It is recommended that you use one common [Material](/documentation/en-us/unreal-engine/unreal-engine-materials) for your merged characters and decide on an **atlas** for your [Textures](/documentation/en-us/unreal-engine/textures-in-unreal-engine). This way textures can be cut and applied at runtime to create a more dynamic system for rendering your merged characters as one mesh.

### Set-Up Skeletal Mesh Merging

After importing your Skeletal Mesh assets into your Unreal Engine project, enable the **Skeletal Merging** [plugin](/documentation/en-us/unreal-engine/working-with-plugins-in-unreal-engine). To enable the plugin, navigate in the **Menu Bar** to **Edit > Plugins** and locate the Skeletal Merge plugin, listed under the **Other** section**,** or by using the **Search Bar**. After enabling the Plugin, restart the editor.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ff453d69-4976-4401-a551-7f574c81b63d/plugin.png)

After restarting the Editor, you create a character blueprint with an empty Skeletal Mesh component using (**+**) **Add** in the **Content Browser**.

Then add a **Skeletal Mesh Merge Parameters** variable to your character blueprint. To create this variable navigate in the **My Blueprint**'s panel to the **Variables** section, use (**+**) **Add** to create a new variable and define the variable type as a `Skeletal Mesh Merge Parameters` variable.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/117ad901-5fa8-471e-90a4-fa8f8457ae78/mergeparamvar.png)

**Save** and compile the **Blueprint**.

Select the Skeletal Mesh Merge Param variable in the My Blueprint panel, to open the variable **Details** panel. Define the character's skeleton using the **Skeleton** property.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/06c00057-d3fe-4c47-b853-7e3e779f382f/assignskel.png)

Now you can define the Meshes you wish to merge, using (**+**) **Add** in the **Meshes to Merge** property. Create an array for each mesh your character contains, and define the respective meshes.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/183250af-2814-4192-9c84-4c2e7bcb059d/definemeshes.png)

In the Character Blueprints Event Graph you can now create a mesh merge node from the Event Begin Play node to merge meshes defined by the Skeletal Mesh Merge Parameter variable.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/75d05f08-2406-4232-9842-db201fe0d37f/mergemeshnode.png)

You can then replace the empty skeletal mesh component with the generated merged mesh, using a Set Skeletal Mesh Asset node. Set the existing mesh node as the Target and the generated merged mesh as the New Mesh. You can then play an animation on the empty mesh object that will be played on the new merged mesh.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/acd67b23-081d-4b10-985a-00e47d9d5a00/mergemeshbp.png)

You can now add your Merged Mesh Blueprint to a level and observe the whole skeletal mesh playing animations in real time.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5fec625f-d88a-4239-a859-d1c8ea9f68ac/meshmergedemo.gif)

If your merged mesh does not align to the capsule component correctly you can adjust its positioning by moving the empty skeletal mesh component in the character blueprint's **Viewport** panel.

### Skeletal Mesh Merge Parameter Reference

Here you can reference a list of the Skeletal Mesh Merge Parameter variable's properties and a description of their functionality:

| Property | Description |
| --- | --- |
| **Mesh Section Mappings** | This is an optional array to map sections from the source meshes to merged section entries. |
| **UVTransforms Per Mesh** | This is an optional array used to transform the UVs in each mesh. |
| **Meshes to Merge** | These are the Skeletal Meshes that will be merged together. |
| **Strip Top LODs** | The number of top LODs to remove from input meshes. |
| **Needs Cpu Access** | Whether or not the resulting mesh needs to be accessed by the CPU for any reason (For example, spawning particle effects). |
| **Skeleton Before** | Whether to update the Skeleton before the merge or after (Skeleton must also be provided). |
| **Skeleton** | This is the Skeleton that will be used for the merged mesh. You can leave this empty to generate Skeleton for the merged mesh to use. |