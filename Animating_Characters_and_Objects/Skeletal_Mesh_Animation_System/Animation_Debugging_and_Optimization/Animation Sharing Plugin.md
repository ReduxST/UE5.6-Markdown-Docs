# Animation Sharing Plugin

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/animation-sharing-plugin-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/animation-sharing-plugin-in-unreal-engine)  
**Processed:** 2025-06-14 16:07:35

---

When creating animation systems for large crowds of characters, you can use the **Animation Sharing Plugin** to significantly reduce your projects performance cost. Rather than performing individual evaluations of an [Animation Blueprint](/documentation/en-us/unreal-engine/animation-blueprints-in-unreal-engine) for each character in your level, you can share animations from a single evaluation across many characters, resulting in a system where the difference between 100 characters and 1000 characters results in a minimum increase in performance cost.

Utalizing the [Leader Pose Component system](/documentation/en-us/unreal-engine/working-with-modular-characters-in-unreal-engine), Animation Sharing utilizes a set of animation state buckets for which animation instances are evaluated. The resulting poses are then transferred to all child components that are part of the bucket. You can then implement blending and playback position randomization techniques to give your crowd a more diverse animation playback.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a0418ea5-b8ee-449f-ba06-67e76cf2e6b2/sharingdemo.gif)

The following diagram provides a high-level breakdown of how the system works with a numbered key explaining the included components:

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a43fab2c-8aad-4820-8e2d-be048675bd18/animsharingdiagram-1.png)

1.  Individual Crowd Actors (AActor)
    
2.  `UAnimationStateProcessor` instance that is part of the Animation Sharing Setup
    
3.  Runtime manager that is initialized using the Animation Sharing Setup
    
4.  States (enum named), which the user has set up
    
5.  Runtime representation of the state that takes the form of a Skeletal Mesh Component
    
6.  Master Pose Component system used to share the animation with the child Skeletal Mesh Components
    

#### Prerequisite

-   Enable the **Animation Sharing** [Plugin](/documentation/en-us/unreal-engine/working-with-plugins-in-unreal-engine). Navigate in the **Menu Bar** to **Edit** > **Plugins** and locate the Animation Sharing plugin, listed under the **Animation** section, or by using the **Search Bar**. **Enable** the Plugin and restart the editor.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f17af05c-1b88-43ea-86c6-354ed71fcad3/plugin.png)

-   A crowd Skeletal Mesh character.
    
-   A set of animations to play on the character.
    

## Set-Up Animation Sharing

After installing the Animation Sharing plugin, create an **Animation Sharing Setup** asset. To create a new asset, use (**+**) **Add** in the **Content Browser** and navigate to **Animation** > **Advanced** > **Animation Sharing Setup**.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e095110a-592e-433c-bca8-9f0dd78d5b43/createsetupasset.png)

The Animation Sharing Setup asset contains all the information that will be shared across the specified Actors.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9a348602-5d78-4475-ae88-f9853eac8777/asset.png)

Open the Animation Sharing Setup asset to access its properties in the Detail panel.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3863c557-55b6-49ea-ad8f-e3fffae9a01c/details.png)

### Skeleton Setups

Using the animation Sharing Setup asset's **Skeletal Setups** property, you can assign multiple Skeletons along with their corresponding properties to define the meshes that will share animation systems. This is useful when you have multiple Skeletons and Skeletal Meshes that will be driven by animations during animation sharing. You can add an array using (**+**) **Add** in the Skeleton Setups property.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/85898d6a-3ad8-4584-8528-3ff06e9042c9/newarray.png)

Here you can reference a list of the available properties you can access after adding a Skeleton Setups array to the asset, and a description of their functionalities:

| Property | Description |
| --- | --- |
| **Skeleton** | The Skeleton asset to be replicated. The Animation Sharing Setup is specific to the specified Skeleton. |
| **Skeletal Mesh** | The Skeletal Mesh to be replicated. This is used for debugging poses only. |
| **Animation Blueprint for Blending** | The Animation Blueprint that is a child of AnimSharingTransitionInstance. You must create and set up one of these to handle blending between states. Additionally, every time a blend is required, one of these is generated and ran to handle the transition which adds a cost. |
| **Animation Blueprint for Additive Animation** | The Animation Blueprint that is a child of AnimSharingAdditiveInstance used for additive animations. Inside your Animation Sharing Setup asset, you will also need to set Animation State to On Demand and enable the Additive option. |
| **State Processor Class** | Interface class used when determining which state an Actor is in. This needs to be set in order to add the Animation States. |
| **Animation States** | This is an array that holds all the states the Actor can be in. Each state is its own bucket. |

Define the skeleton and skeletal mesh assets you wish to share animations across using the respective **Skeleton** and **Skeletal Mesh** properties.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/96290af3-74f9-4bae-bf83-b2ef8cf3817e/defineskel.png)

### Animation State Enumeration

In order to select poses for the crowd character, you will need to create an **Enumeration asset** that will select Animation States in the Animation Sharing Setup asset. Create an Enumeration asset by navigating in the **Content Browser** to (**+**) **Add**, and selecting **Blueprints** > **Enumeration**.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8b142234-2081-487f-bdd9-bba954876aa1/createnewenum.png)

**Name** and **open** the Enumeration asset.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f5e78992-92e0-45d2-a202-846f738e4715/enumasset.png)

Then assign Enums for each of your crowds animation states using the (**+**) **Add Enumerator** button and typing the definitions in the **Display Name** properties. In this workflow two Enums are created for an `Idle` and `Run` animation.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0fde93a4-d5cd-4dab-953d-b95e23360e2f/enumassignments.png)

### Animation Sharing Character Blueprint

Create a character blueprint that will represent your crowd-character. Navigate in the content browser to (**+**) **Add** and select **Blueprint Class** \> **Character**.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b751482c-dbea-4431-b926-03f7c29416f3/createbp.png)

**Name** and **open** your Crowd Character Blueprint.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fe0381f4-36dc-4ddf-afb7-b8bb0de3ab2f/crowdbp.png)

Assign the Character's Mesh using the drop-down in the **Skeletal Mesh Asset** Property.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7c0aac1f-7bb7-4bef-8021-3cc4082a66ab/assignmesh.png)

In the Character Blueprint's **Event Graph**, you can build the logic that will set the Enumeration Asset's state based on a variable or gameplay state. In the workflow example a key press function, **Keyboard Event 5**, is used to change the Enum state.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2f5fdb17-e7b7-423a-b1af-ea90dc12b494/keyevent.png)

Then in the **Event Begin Play** node's logic, create a **Get Animation Sharing Manager** node. Next create a **Register Actor** and connect the Sharing Manager's **Return Value** pin to the Register Actor node's **Target** pin. Create a **Self** reference variable and connect it to the **In Actor** pin. Finally, set the character's skeleton as the **Sharing Skeleton**.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/19ab2679-bbb4-407c-999f-ce71e70beceb/sharingcharbp.png)

### Animation Sharing State Processor

The `AnimationSharingStateProcessor` class is a specialized Blueprint class that you can use to set the Animation Sharing Setup assets Animation State to control what animation should be played using your **Enumeration** asset.

To create a new `AnimationSharingStateProcessor` blueprint, navigate in the **Content Browser**, use (**+**) **Add** and select **Blueprint Class**.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8bc469d5-d7c8-4168-9891-e3e5cfb27ea3/createbp.png)

Use the **Search Bar** to locate and select the `AnimationSharingStateProcessor` class, and then the **Select** button.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8ba80d10-21c5-45fe-9447-c3f25a80af1b/createclassbp.png)

**Name** the blueprint and open it in the [Blueprint Editor](/documentation/en-us/unreal-engine/user-interface-reference-for-the-blueprints-visual-scripting-editor-in-unreal-engine).

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c73a682f-9a98-4036-92e9-a0a23350acf0/proccessorasset.png)

The Animation Sharing State Processor Blueprint should only be used for prototyping. Runtime performance will be greatly improved by using the native implementation as opposed to the Blueprint implementation.

In the Blueprint's **Class Defaults** panel, select the **Animation State Enum** drop down menu, and select your **Enumeration** asset.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5ce1ab05-5e6b-4f35-a04c-66dfb16adb5a/createnewenum.png)

After adding your Enumeration asset, you can use the Animation Sharing State Processor blueprint's two **Override Functions** to reference and drive the animation selection across your crowd of characters.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/464a231e-17b9-4dd9-8a7c-48e611a53494/overides.png)

-   You can use the **Process Actor State** function to reference your Sharing Animation Character's blueprint and reference your Enum asset state.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0152ce53-39e0-4733-a334-f12e4cc4215e/processstatefuntion.png)

-   Using the **Get Animation State Enum**, to interface with a native implementation of the Animation Sharing State Processor, in order to return the Enum class.

After creating your Animation Sharing State Processor blueprint, you can assign it In the Animation Sharing Setup asset's **State Processor Class** property.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d4a27993-8005-417b-a4de-8aac2c29467b/setprocessorclass.png)

### Animation States

Once you assign an Animation Sharing State Processor blueprint to your Animation Sharing Setup asset, you can create an animation state array using (**+**) **Add** in the **Animation States** property and selecting your Enum values from the **State** properties drop-down menu.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/46764856-8731-4608-a384-a6a0d927c240/createstates.png)

For each Animation State array, add an **Animation Setups** array using (**+**) **Add**, in order to define the animation sequence to play.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e9803834-eb9a-457c-a806-72a25c0051b7/assignseq.png)

Here you can reference a list of the Animation State array properties and a description of their functionality:

| Property | Description |
| --- | --- |
| **State** | Define which Enumeration State will activate the Animation State array using the drop-down menu. The available options are inherited based on the assigned **Animation State Processor**'s **Animation State Enum** property. |
| **Animation Setups** | 
Here you can set the Animation States properties, such as the animation sequence to play, and the randomization applied. The following properties are available for each **Animation Setups** array added to your **Animation States** property:

-   **Anim Sequence**: Set the **Animation Sequence** to play when this animation state is active.
-   **Anim Blueprint**: Set the Animation Sharing [Animation Blueprint](/documentation/en-us/unreal-engine/animation-sharing-plugin-in-unreal-engine#animationblueprintsetup) to playback the **Animation Sequence** when this animation state is active.
-   **Num Randomized Instances**: Set the number of random animation playback instances to generate when this animation state is active. A random instance will generate a unique **start time offset**, to diversify the look of the crowd. Using (**+**) **Add**, you can set this property on a per-platform basis.
-   **Enabled**: When enabled, this animation state will be activatable. Using (**+**) **Add**, you can set this property on a per-platform basis.



 |
| **On Demand** | When enabled, this state is classified as **on-demand**, which means you can kick off a unique animation when needed. This spins up a unique instance per on-demand animation. When reaching the maximum value, it will snap to the nearest animation. |
| **Additive** | When enabled, the state is an **additive** animation state. **On-demand** must also be enabled and you will need an [Additive Animation Blueprint](/documentation/en-us/unreal-engine/animation-sharing-plugin-in-unreal-engine#animsharingadditiveinstance) to handle blending. |
| **Blend Time** | Here you can set the duration of blending when blending to the state. |
| **Maximum Number Of Concurrent Instances** | The number of instances that will be created for the state (platform-specific). |
| **Requires Curves** | When enabled, this animation state requires curves or morph targets to function correctly for follower components. |

### Scalability Settings

You can use the **Scalability Setting** section of properties in the Animation Sharing Setup asset to define how the animation sharing works across a large number of actors.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f77d4cb1-1b3f-495e-867a-ce92e8ec14bf/scalesettings.png)

Here you can reference a list of the **Scalability Settings** properties and a description of their functionality:

| Property | Description |
| --- | --- |
| **Use Blend Transitions** | When enabled, the animation will play a blend to transition from one state to another. |
| **Blend Significance Value** | Here you can set a significance value tied to whether or not a transition should be blended. A value of 0 will result in no significance considered, a value of 1 will consider the significance first. |
| **Maximum Number Concurrent Blends** | Here you can set the number of blends that can be running at the same time. Each animation that is over this limit will snap to the nearest one. |
| **Tick Significance Value** | Here you can set a value that will be used with the [Significance Manager](/documentation/en-us/unreal-engine/significance-manager-in-unreal-engine). Anything over the specified value will not be ticked. |

### Animation Blueprint Setup

You will need to set up an Animation Blueprint to handle the blending between the Animation States by referencing the current active pose, `From Component` and the pose being fed to the Animation Sharing system, `To Component`. This requires a special class of Animation Blueprint called an **Anim Sharing Transition Instance**. To create an Animation Blueprint, navigate in the **Content Browser**, select **Animation** > **Animation Blueprint**.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b6c52ec1-b62e-4719-ba4e-2a1395964662/createanimbp.png)

Select the Character's Skeleton, define the `AnimSharingTransitionInstance` as the animation blueprint's class, and then select **Create**.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3eddfcdd-df42-44c4-9395-89ef35160cb2/asignclassanimbp.png)

**Name** and open the asset.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cef164a9-8612-40bb-a021-5e424a4ad7f9/instanceasset.png)

In the Sharing Transition Animation Blueprint's AnimGraph, right-click and search for a **From Component** transition variable. Then create and connect its output to a **Copy Pose From Mesh** node. Create and connect the Copy Pose From Mesh node's output to a **Blend Poses by bool** node's **True Pose** input pin.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/10109edc-712e-42b1-b581-b445fe7bcc18/fromcomponent.png)

Right-click in the graph and search for a **To Component** transition variable. Then create and connect its output to a **Copy Pose From Mesh** node. Connect the Copy Pose From Mesh node's output to the **Blend Poses by bool** node's **False Pose** input pin.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3ed14352-8582-4d3e-b73a-f9a8b2307321/tocomponent.png)

Right-click in the graph and search for a **Blend Bool** transition variable and connect it to the Blend Poses by Bool node's Active Value input pin. Then, right-click in the graph to search for and create a **Blend Time** variable to reference the **Blend Time** property in the Animation Sharing Setup asset, and connect it to the **True** and **False Blend Time** pins. Then connect the Blend Poses by Bool node's output to the **Output Pose** node.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cfc67448-fb18-4abb-9de4-42edda98f9d4/fulltransgraph.png)

Now add the Sharing Transition State Animation Blueprint to the Animation Sharing Setup asset.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c2ddd58d-6084-42ff-a443-165f03217838/addtrandgraph.png)

You can now transition animation playback when sharing animations across multiple characters.

#### Anim Sharing Additive Instance

When using additive animations, you will need to set up an Animation Blueprint to handle the shared Additive Animations. This requires a special class of Animation Blueprint called an `AnimSharingAdditiveInstance` class.

In order to mark your animations as additive, you will need to enable the **On Demand** and **Additive** properties in your Animation Sharing Setup asset on each additive animation's Animation State array.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ce674482-8761-4cd8-9590-f320c85be06e/markadditive.png)

To create an Additive Animation Sharing Animation Blueprint, navigate in the **Content Browser**, select **Animation** > **Animation Blueprint**.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/130eaa75-7b3c-4df7-8298-a0042a5142f9/createanimbp.png)

Select the Character's Skeleton, define the `AnimSharingAdditiveInstance` as the animation blueprint's class and then select **Create**.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/10e9138f-83ca-41ef-bea5-5f2d2cc60c95/additiveinstanceclass.png)

**Name** and **open** the asset.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c90e9899-ed66-40a6-95b0-ae4f6ddd79f5/additiveasset.png)

In the Addictive Animation Blueprint's **AnimGraph**, right-click and create a **Base Component** additive variable. From the Base Component variable, create and connect a **Copy Pose From Mesh** node, and connect its output to an **Apply Space Additive** node.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/951173f1-5a66-4232-8d05-351f7e91d18c/basecomponent.png)

Right-click in the AnimGraph and create a **Sequence Player** node. Select the Sequence Player node and expose its Sequence property as a pin in the graph, by navigating in the **Details** panel and selecting **Expose Pin** in the **Sequence** property.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/52a8253b-cdbb-4ac9-9916-cbc02e8b86ac/exposepin.png)

Right-click in the AnimGraph and create an **Additive Animation** additive variable, and connect it to the Sequence Player node's **Sequence** pin. Then connect the Sequence Player node's output to the Apply Mesh Space Additive node's **Additive** pin. Finally, connect the Apply Mesh Space Additive node's output to the **Output Pose** node.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c8beaa57-ae44-40df-80e4-c54e13d48cdb/additivefullgraph.png)

You can now add The Additive Animation Blueprint to the Animation Sharing Setup asset.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ac504954-be48-47bf-a2e6-025d70baf78f/addadditivegraph.png)

You can now blend the shared animation as an additive animation.

#### Anim Sharing State Instance

You can use the **Anim Sharing State Instance** Animation Blueprint class to run shared animations across your characters. With the Anim Sharing State Animation Blueprint you can add AnimBP behavior to expose two properties by default:

-   **Animation to Play**
    
-   **Permutation Time Offset**.
    

To create an Anim Sharing Animation Blueprint, create a new Animation Blueprint asset using (+) Add in the Content Browser, and select Animation > Animation Blueprint.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f4db7856-a390-4d6f-bd84-5e79e5c31a70/createanimbp.png)

Select your skeleton asset, select the `AnimSharingStateInstance` class from the drop-down menu and then select **Create**.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e91c048a-706c-4689-a46d-eb0461efee06/animinstance.png)

**Name** and open the animation blueprint.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/953cf2e7-3d30-46a9-8c12-9b7cb97d1417/instanceasset.png)

In the AnimGraph, right-click to create a **Sequence Player** node. In the Sequence Player node's **Details** panel, expose the **Sequence** and **Start Position** properties as pins to the graph, by selecting **Expose as Pin** in the pin type drop-down menu. Right-click in the graph to create and connect an **Animation to Play** animation sharing variable to the sequence player node's **Sequence** pin.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/87b11147-46ae-4690-8ae7-e16bd291f3db/animationtoplay.png)

Right-click in the graph to create a **Permutation Time Offset** animation sharing variable, and connect it to the Sequence Player node's **Start Position** pin. Finally, connect the Sequence Player node's output to the **Output Pose** node.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5df4623e-82bf-411a-b0b4-16e481d2dfcb/stateinstancegraphfull.png)

The Animation Sharing Instance Graph's native implementation, exposes `GetInstancedActors` which returns all `AActor(s)` that are currently being driven by this state. This ensures all present [Notifies](/documentation/en-us/unreal-engine/animation-notifies-in-unreal-engine) are handled correctly and propagated to the unique instances.

This is achieved by overriding HandleNotify and handling it accordingly.

In the Animation Sharing Setup assets, in each Animation State you wish to randomize an animation playback offset, assign the Animation Sharing Animation Blueprint in the Blueprint property. Then set a value in the **Num Randomized Instances** property.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bebfd00c-4869-49e3-9ec7-c10ebc4c1340/sharingbp.png)

### Animation Sharing Manager

In order for Animation Sharing to be executed at runtime, you must create an **Animation Sharing Manager** node that points to your **Animation Sharing Setup** asset within the Character or Level blueprint. After creating the Animation Sharing Manager node, define your Animation Sharing Setup asset using the drop-down menu in the graph. In this workflow example, the Create Animation Sharing Manager node is added to the Level blueprint.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/256e296d-d4e2-48c0-adaf-687a66f8c1e9/createanimsharman.png)

Here you can reference additional functions you can call that target the Animation Sharing Manager node and a description of their functionality:

| Function | Description |
| --- | --- |
| **Animation Sharing Enabled** | Returns whether or not Animation Sharing is enabled. |
| **Get Animation Sharing Manager** | Returns the Animation Sharing Manager (or null if none has been set up). |
| **Register Actor** | Registers an Actor with the Animation Sharing Manager, according to the specified Sharing Skeleton. |

You can now add the crowd character to the level and observe its animation playback as animation states are changed.

## Animation Sharing Debugging

During **Play in Editor** (**PIE**) simulation, you can enable some helpful viewport debug rendering to illustrate how the Animation Sharing plugin works and how it is selecting animations.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7597fe15-b170-4171-b4a2-a35b7d9d8f4c/sharingdebugdemo.gif)

Here you can reference a list of console commands you can use to debug your Animation Sharing system in Unreal Engine:

| Command | Description |
| --- | --- |
| `a.Sharing.ToggleVisibility` | Toggles the visibility of the Leader Pose Components. The Debug render will be located at the level's origin point (0, 0, 0). Characters sharing animations will be rendered in **green** when they are using an active pose, and **blue** when they are blending. **Red** poses are inactive poses. The **magenta** line will point to the active pose the character is sharing. |
| `a.Sharing.ScalibilityPlatform` | Controls which platform should be used when retrieving per-platform scalability settings. |
| `a.Sharing.Enabled` | Toggles whether or not the Animation Sharing system is activated. `0` will disable the system, `1` will enable the system. |
| `a.Sharing.DebugStates` | Toggle the number of Animation States visible in the debug render. Value added to the command will set that number of debug states to render. |