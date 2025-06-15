# Multi-User Replication

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/multi-user-replication-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/multi-user-replication-in-unreal-engine)  
**Processed:** 2025-06-14 16:37:30

---

## Overview

Multi-User Replication offers real-time replication of actor properties between clients through [Multi-User Editing](/documentation/en-us/unreal-engine/multi-user-editing-in-unreal-engine). This user guide will show how to use Multi-User Replication.

This feature is intended for replicating objects between editors. This system is not intended for gameplay replication.

## Prerequisites

To use Multi-User Replication, you must configure your Unreal Engine project to use Multi-User Editing, be running a Multi-User Server, and have joined a session. For more information on this setup process, see [Getting Started with Multi-User Editing](/documentation/en-us/unreal-engine/getting-started-with-multi-user-editing-in-unreal-engine).

## Open The Replication Tab

Once you have joined a Multi-User session, click the **Replication** tab.

![The Replication tab](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/435e4b23-e17c-4863-8c9f-fe71ccccdd75/replication-tab.png)

## Replicate a Property

Multi-User Replication does not replicate the entire actor and it is not suggested to attempt replicating every property on an actor due to bandwidth limitations. Instead, individual properties are selected for replication.

To replicate a property in real-time using Multi-User Replication, follow these steps:

1.  Click **Add** in the **Replication** tab and select an actor to replicate.
    
    ![Adding an actor](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7a2174ae-1703-4472-a375-f9243c8fb358/add-actor.png)
2.  Click **Edit** in the bottom panel, and select the property from the component that it is on.
    
    ![Selecting a property](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b06e78c1-7925-47f6-bbb7-d5ce57c8a8fd/edit-property.png)
    
    The added property should be automatically assigned to the client that added it. That client's evaluation of the property is now being replicated to the other clients in the session.
    
3.  To pause replication of an actor, click the **Pause** button next to the actor's name. To resume replication, click the **Play** button.
    
    ![The Pause button](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7721b199-0fed-42d9-a7ce-54cb9dc766b1/pause-replication.png)

## Set the Replication rate

By default, actors added to replication are attempted to be replicated at 30 frames per second. To change this rate, right-click the actor and hover over the component whose rate you want to change.

![The rate settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3397933b-13f7-45d3-be44-e3655bff2036/set-rate.png)

The rate can be set to one of the following options:

-   **Realtime**: The component will replicate as fast as the engine is able to evaluate.
-   **Specified Rate**: The component will attempt to replicate at the rate specified in Replication Rate.

If the editor is evaluating at a rate lower than the specified replication rate, the replication rate will be capped at the lower rate.

## Change the Property Author

To change the client acting as the author of the replication of all properties on an actor, right-click the actor in the top panel and click a new author in the **Reassign All To** category.

![Clicking a new author](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/616faaf2-6991-491a-9c5a-497dddeb3310/change-all-properties.png)

To change the client acting as the author of the replication of a single property, navigate to that property in the bottom panel and click the **Author** dropdown to select a new author.

![Clicking the Author dropdown](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/46d5d841-efcb-4cb2-b490-7d3652b2637e/change-one-property.png)

Multiple clients can replicate the same actor if the clients are assigned as the authors of different properties.

## Using Multi-User Replication Presets

In complex replication environments, it can be valuable to save the assignments of actors and properties to be recalled later. This can be accomplished through the use of Replication Presets.

Presets work by mapping the actor label to the client name. If multiple clients share the same name, presets will not function. To avoid this, set the client's **Display Name** from the **Multi-User Editing** section of the project settings.

### Create a Replication Preset

To create a Replication Preset, follow these steps:

1.  In the **Replication** tab, click **Presets** > **Save Preset as...**.
    
    ![Saving a preset](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8eb14aa5-b5fc-4583-8960-c54d587718ad/preset.png)
2.  Save the preset.
    

Do not forget to persist the preset asset if you plan to use it in different sessions in the future.

### Load a Replication Preset

To load a preset, follow these steps:

1.  In the **Replication** tab, click **Presets**, then click the preset asset to load.
    
    ![Loading a preset](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a01eb114-f790-4298-8d35-a3849e5659a9/load-preset.png)

## Advanced Topic: Default Properties

You can configure the properties that are added by default when you add a component of a given class for replication.

To configure the default properties, follow these steps:

1.  From Unreal Engine's main menu, go to **Edit** > **Project Settings**.
    
2.  In the Multi-User Replication section, expand **Replication Editor Settings**.
    
3.  Under **Default Property Selection**, map classes (typically those of components) to the properties you want to automatically add.
    
    ![Default Property Selection](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f27f30ce-d3a6-4425-9b9f-f8d9bd3a4e83/map-classes.png)
4.  Under **Default Added Subobject Rules**, you can specify which types of actors the rules defined in **Default Property Selection** are applied to. This allows you to only apply the defaults for the components specified in **Default Property Selection** to the desired actor classes.
    
    -   As key, you assign the class of actor you want the rule to apply; by default, there is a rule that is applied to all actor classes.
    -   As value, you specify the types of subobjects, typically components, for which you want the rules from **Default Property Selection** to apply.
    
    ![Default Added Subobject Rules](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3909efb5-6a0b-4690-bbf4-4805a22370d3/subobject-rules.png)