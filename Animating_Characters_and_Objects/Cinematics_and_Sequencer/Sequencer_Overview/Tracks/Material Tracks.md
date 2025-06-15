# Material Tracks

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/animate-materials-in-unreal-engine-cinematic](https://dev.epicgames.com/documentation/en-us/unreal-engine/animate-materials-in-unreal-engine-cinematic)  
**Processed:** 2025-06-14 16:05:59

---

In **Sequencer**, you can change and animate **Materials** on your **Actors** in a variety of ways. Change which Material is currently applied to an Actor using the **Material Switcher Track**, animate [Material Parameters](/documentation/en-us/unreal-engine/instanced-materials-in-unreal-engine#materialparameterization) using the **Material Parameter Track**, or animate several Materials at once using the **Material Parameter Collection Track**.

This page provides information about the variety of ways you can animate Materials on your Actors in Sequencer.

#### Prerequisites

-   You have an understanding of [Sequencer](/documentation/en-us/unreal-engine/how-to-make-movies-in-unreal-engine) and its [Interface](/documentation/en-us/unreal-engine/sequencer-cinematic-editor-unreal-engine).
-   You have a basic understanding of creating [Materials](/documentation/en-us/unreal-engine/unreal-engine-materials), [Material Parameters](/documentation/en-us/unreal-engine/instanced-materials-in-unreal-engine#materialparameterization), and [Material Parameter Collections](/documentation/en-us/unreal-engine/using-material-parameter-collections-in-unreal-engine).

## Switch Materials

To switch an Actor's Material with a different one during playback of your sequence, use the **Material Switch Track**. This track can be useful if you have already created preset Material Instances and want to immediately switch between them.

To switch Materials on your Actor, first add the Mesh Component Track of the Actor in Sequencer. Click **Add Track (+)** and select the **Mesh Component**.

![add mesh component](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/599aa6c2-eecf-43b6-b819-446bbd27905d/switcher1.png)

Next, add the Material Switcher Track for this Component by clicking **Add Track (+)** on the **Component Track** and adding a **Material Element Switcher**. The element numbers correspond to the **Material Elements** currently assigned to the mesh. To change more than one material, add switchers for all necessary elements.

![add material element switcher](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4aa83eed-f6a6-4efe-8bb9-e8416841211c/switcher2.png)

Once the tracks are added, you can [keyframe](/documentation/en-us/unreal-engine/creating-animation-keyframes-in-unreal-engine) them to set materials you want to apply at a specific time. To change the assigned material, click the dropdown menu on the Material Switcher Track and select a different material.

![material switcher change material](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5fd82df6-ecea-4b53-b6e2-f4e10210711b/switcher3.png)

You can now scrub or play your sequence and observe the material switching.

![material switcher](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a75c8047-3bde-41f0-a589-bfaca830691b/switcher4.gif)

## Animate Material Parameters

To animate specific [Material Parameters](/documentation/en-us/unreal-engine/instanced-materials-in-unreal-engine#materialparameterization) over time within a material, use the **Material Parameter Track**.

Similar to switching Materials, you must first add the Mesh Component Track of the Actor in Sequencer. Click **Add Track (+)** on the Actor Track and select the **Mesh Component**.

![add mesh component](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/033e7650-d47f-4798-bdd0-50ad8c58eeae/switcher1.png)

Next, add the Material Parameter Track for this Component by clicking **Add Track (+)** on the **Component Track** and adding a **Material Parameter Element**. The element numbers correspond to the **Material Elements** currently assigned to the mesh. To animate parameters on more than one material, add Material Parameter Tracks for all necessary elements.

![add material elements](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/16f4da20-6d22-492a-bbfe-28a98aedb429/param1.png)

Once the element track is added, add a specific Material Parameter to animate. Click **Add Parameter (+)** on the **Material Element Track** then select a parameter. Add as many parameter tracks as needed for your element.

![add parameters](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/02bcb4f3-2fb1-4bba-af1d-22612d9fd9f8/param2.png)

Depending on the type of parameter added, Sequencer will interface with it using compatible [Property Tracks](/documentation/en-us/unreal-engine/cinematic-transform-and-property-tracks-in-unreal-engine#propertytracks). For example, adding a **Vector Parameter** will create a [Color Track](/documentation/en-us/unreal-engine/cinematic-transform-and-property-tracks-in-unreal-engine#color)

Once the parameter tracks are added, you can [keyframe](/documentation/en-us/unreal-engine/creating-animation-keyframes-in-unreal-engine) them normally to animate the parameters. Afterward, scrub or play your sequence to observe the effects of the parameter changing.

![animate material parameter](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/dc2a9e34-5171-4725-ab13-a65539ee781c/param3.gif)

As you can with usual section usage, Material Parameter Sections can be [blended](/documentation/en-us/unreal-engine/creating-animation-keyframes-in-unreal-engine#blending) with one another by overlapping their sections. This can be useful to blend between different preset material states, rather than directly animating them.

![blend material parameter section](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c5525de7-b0e9-4c00-aecb-690472577c8b/param4.gif)

## Animate Material Parameter Collections

Sequencer also contains the **Material Parameter Collection Track** for animating [Material Parameter Collections](/documentation/en-us/unreal-engine/using-material-parameter-collections-in-unreal-engine). Use it to directly animate any material where the collection is referenced, so Sequencer can affect multiple materials at the same time.

To create a Material Parameter Collection track, click **Add Track (+)** in **Sequencer** and select your **Material Parameter Collection Asset** from the **Material Parameter Collection Track** menu.

![create material parameter collection track](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2a5ede3f-b8fa-4c9f-b999-2fb49b45afe3/createtrack.png)

You can then add individual parameters from this collection by clicking **Add Parameter (+)** on the track and selecting a parameter. The parameters listed here are based on the parameters created in the collection asset. Once a parameter is selected, its corresponding track is created with a keyframe set at your current time along the timeline.

![add material parameter collection parameter](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a3888e69-757a-45e8-8100-e7658b12f444/createparam.png)

Due to the arbitrary nature of Material Parameter Collections and how they are set up within each Material's graph, there are a variety of ways the Material Parameter Collection Track can affect your scene. In this example, a vector parameter is used to control additional color tinting on the character. Changing this parameter affects all child instances of this material.

![material parameter collection material setup](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6978ab8b-d8cf-4781-b594-3761cad04690/materialsetup.png)

Once the parameter tracks are added, you can [keyframe](/documentation/en-us/unreal-engine/creating-animation-keyframes-in-unreal-engine) them as usual to animate the parameters. Afterward, scrub or play your sequence to observe the effects of your animated parameter collection.

![animate material parameter collection](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/554e3acb-e4f0-46c7-8452-369a7f05f140/collection.gif)