# Dynamic Asset Selection

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/dynamic-asset-selection-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/dynamic-asset-selection-in-unreal-engine)  
**Processed:** 2025-06-14 16:21:20

---

You can use a combination of **Proxy**, **Proxy Table** and **Chooser Table** assets to build dynamic asset selection logic, to drive animations based on variables in your project. For example, you can use Proxy and Proxy Table assets to select what kind of animation set should be loaded and used for your character, such as different weapon sets. Alternatively, you can use Chooser Tables to dynamically select individual animation assets, such as different hit reactions based on the location your character is hit, using contextual variables from your project.

You can use the following document to learn more about setting up a dynamic animation selection system in Unreal Engine.

Though this documentation focusses on using Choosers and Proxy Tables to select animation related assets such as Animation Sequences, Montages, or AnimInstance classes, the system itself is generic and can be used to select any type of Asset, Object, or Class.

#### Prerequisites

-   Enable the **Chooser** plugin. Navigate in the **Menu Bar** to **Edit** > **Plugins** and locate **Chooser** in the **Animation** section, or use the **Search Bar**. Enable the plugin and restart the editor.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ce6bbd1b-20dd-4a54-b341-a641172705aa/image_0.png)

-   Your project contains a set of animations you wish to dynamically select based on contextual situation at runtime. This could be unique cosmetic animation sets, relevant gameplay animations such as contextual animation sineros, or animation sets relevant to equipable items like weapons.
    
-   Your project contains a functional Animation Blueprint, that you can build dynamic Animation selection logic in.
    

## Set Up an Animation Selection System

Here you can read about how to set up an animation chooser system in your project to dynamically select hit reaction animation playback based on context in your project at runtime.

### Create a Proxy Asset

A [Proxy Asset](/documentation/en-us/unreal-engine/dynamic-asset-selection-in-unreal-engine#proxyasset) is used to store the contextual information of which [Proxy Table](/documentation/en-us/unreal-engine/dynamic-asset-selection-in-unreal-engine#proxytable) asset is active, and other relevant variables.

To create a Proxy Asset, use (**+**) **Add** in the **Content Browser** and navigate to **Miscellaneous** > **Proxy Asset**.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/10b54d73-38c2-466b-aca2-2c04d41160ee/image_1.png)

Create a Proxy Asset for each animation set you wish to dynamically select animations from to drive the character, such as an idle, walk, or run set.

After creating the Proxy Assets, open each to access their settings.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5ad7bac5-b0d8-4c64-a50e-a8f304acb157/image_2.png)

For each Proxy Asset, set the **Type** property to the animation asset type you are using, in this case `AnimSequenceBase`.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/20ddd507-c917-48be-b010-77b8449a72c4/image_3.png)

Set the **Context Data** property to the **Animation Blueprint** option by adding a new **Index** array using (**+**) **Add**, selecting **Context Object Type Class** option.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/944ad717-460c-4dfd-85cf-4744fc09d522/image_4.png)

Expand the **Index** array's settings and set the **Class** property to use your Animation Blueprint, in this case `ABP_Manny`. Then ensure the **Direction** property is set to **Read**.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2450de91-58b1-4835-bcce-627c1c1253cd/image_5.png)

### Animation Blueprint Set Up

After setting up your Proxy Asset, you must create a variable in your character's animation blueprint in order to store the active proxy table during runtime. To create this variable, open your characters Animation Blueprint and create a new Variable in the **My Blueprint** panel using (**+**) **Add**. Then set the Variable type to a **Proxy Table Object Reference**. After creating the variable, **save** and **compile** your Animation Blueprint.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ad51c580-ade8-48a3-8b66-00ce03a21744/image_6.png)

The Proxy Table variable will be used in your animation graph by an Evaluate Proxy node, to determine the active Proxy Table at runtime.

### Create Proxy Table Assets

A **Proxy Table** asset is used to store the animation assets sets, that can be dynamically selected at runtime. For example, one Proxy Table may store a character's Idle animations while another may store its Walking or Running animation set.

To create a Proxy Table asset, use (**+**) **Add** in the **Content Browser** and navigate to **Miscellaneous** > **Proxy Table**.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ae3a51e1-7438-4cc3-b1d5-f8e9fe35ebce/image_7.png)

Create a Proxy Table asset for every contextual situation that a different animation set would be needed, such as locomotion animation sets for unarmed characters and characters holding a pistol or rifle.

After creating a Proxy Table asset, open the asset to access the Proxy Table's values.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4ac182f9-7dd7-4d52-91bd-a953b505e56c/image_8.png)

In the ProxyTable, add an entry for each **Proxy Asset** using (**+**) **Add Row** and selecting asset. You can then assign the associated animation asset from the set using the Value Column.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4440b311-6c14-46a7-a46f-9be5b3077503/image_9.png)

In the following workflow example, a `ProxyTable_Unarmed` asset is assigned an `Unarmed_Idle` and an `Unarmed_Walk` animations to the respective `ProxyAsset_Idle` and `ProxyAsset_Walk` rows. Then in a `ProxyTable_Pistol` asset, the same Proxy Asset rows are assigned with a `Pistol_Idle` and `Pistol_Walk` animations respectively.

| ProxyTable\_Unarmed | ProxyTable\_Pistol |
| --- | --- |
| ![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a94cd880-46bc-4df4-95c2-cceacd1a5b80/unarmed.png) | ![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1a538b93-873f-41e7-886e-b412f6941e8e/pistol.png) |

The Value column can also contain a **Class** reference, a **Chooser Asset**, or a **Lookup Proxy** for more dynamic animation selection systems.

### Using Proxy Tables at Runtime

You can use Proxy Table assets at runtime using an [Animation Node function](/documentation/en-us/unreal-engine/animation-blueprint-node-functions-in-unreal-engine) on a Sequence Player node. To create a new function to select a Proxy Table asset, select the Sequence Player node, and add a new Function at the **On Update** binding.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4885b991-b237-4662-8175-9128a6a394fd/image_10.png)

Add an **Evaluate Proxy** node from the **On Update** node.![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8b84eef4-a1e8-4b3c-8596-0721da807150/image_11.png)

Then select the node and select the Proxy Asset in the Proxy property using the drop down.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e930d6e9-9b81-4d1e-8124-618ae863e9a3/image_12.png)

Then promote the result to a Variable, and connect the output to the Sequence Player node.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/61fb9845-db1b-4d35-bf8a-5a519c813220/image_13.png)

You can then set the active Proxy Table asset on the Evaluate Proxy node using a variety of methods, such as a Chooser Table, to dynamically change the animation set driving the character.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ccf4bb48-021c-4fd8-8ee0-9bdaf988aca0/image_14.gif)

### Create a Chooser Table Asset

A chooser asset is used to store animation data sets that comprise of an animations various iterations, that can be selected and played back based on the context. For example, a chooser table may contain a set of hit reaction animations, with each entry being an animation that reacts based on a different part of the body being hit (arms, legs, chest, head), that can then be selected based on a contextual variable, such as the location of the hit.

To create a Chooser Table asset, use (**+**) **Add** in the **Content Browser** and navigate to **Miscellaneous** > **Chooser Table**.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/617645d2-e73f-4fda-9adf-a529e87af672/image_15.png)

After creating a Chooser Table, you can open the asset to access its properties.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/164bbfb2-e271-4021-89f7-b0220b68385e/image_16.png)

Create a new Array element in the Context Data property using (**+**) **Add** and set the property to the **Context Object Type Class** option. Then expand the Index array, and set the **Class** property to your character's animation blueprint and ensure the **Direction** property is set to **Read**. You can then set the Output Object Type to the animation asset you are using. This workflow example is using Animation Sequences, so the **AnimSequenceBase** class option was selected.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/936b6c2d-d7b8-45f2-86e5-7281be15f5f5/image_17.png)

In the Chooser Table panel, you can begin to add Columns, in order to set the Variables from the animation blueprint you wish to influence the selection process using the (**+**) **Add Column** button. After creating a Column, you can define which Variable from your Animation Blueprint can influence the selection, and the values or states of the variable that must be reached in order to select the Animation Sequence asset within each row.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6dbb61ff-be99-4233-9a88-11742c5ec4d4/image_18.png)

In this workflow example, the boolean variable `IsCrouching` will select the `MM_HangingIdle` animation when the value is false, and will select the `MM_Rifle_Walk_Left` when the value is true. The `MoveemntAngle` Variable will select the `MM_HangingIdle` when the value is between `-100` and `100`, while the `MM_Rilfe_Walk_Left` animation will only be selected when the value is `0.0`.

In order to drive the characters animations using this selection process, you must set your Proxy Table Entry to **Evaluate Chooser** and assign the Chooser Table asset.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0e052f04-6ace-4ff6-b75e-cf177fe06dfd/image_19.png)

Now the selected animation will change based both on the active Proxy Table asset and the selection made by the Chooser Table.

You can also use ChooserTables without ProxyTables using an Evaluate Chooser node in your animation blueprint graph or state machine.

![ImageAltText](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/17ce25bb-d516-4933-ba1d-3afc12acc84b/image_20.png)