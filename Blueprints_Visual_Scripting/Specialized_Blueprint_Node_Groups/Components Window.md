# Components Window

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/components-window-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/components-window-in-unreal-engine)  
**Processed:** 2025-06-14 16:14:40

---

A **Component** is a piece of functionality that can be added to an Actor.

When you add a Component to an Actor, the Actor can use the functionality that the Component provides. For example:

-   A Spot Light Component will make your Actor emit light like a spot light.
-   A Rotating Movement Component will make your Actor spin around.
-   An Audio Component will give your Actor the ability to play sounds.

Components must be attached to an Actor and can't exist by themselves.

For more information on Components, please see the [Components Overview](/documentation/en-us/unreal-engine/components-in-unreal-engine) documentation.

## Components Window

With an understanding of Components, the **Components** window inside the **Blueprint Editor** allows you to add Components to your Blueprint. This provides a means of adding collision geometry via CapsuleComponents, BoxComponents, or SphereComponents, adding rendered geometry in the form of StaticMeshComponents or SkeletalMeshComponents, controlling movement using MovementComponents, etc. The Components added in the Components list can also be assigned to instance variables providing access to them in the graphs of this or other Blueprints.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6da79f18-bdc3-4588-9d20-e9f624bd1686/components_pane.png)

## Adding Components

To add a Component to a Blueprint from the **Components** window:

1.  Select the type of Component you want to add from the dropdown list, i.e. a *CameraComponent*.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/67a54191-1b18-4e82-abb2-4f8ff258ee55/add_new_component_list.png)
2.  After selecting a Component from the list, you will be prompted to enter a name for your Component.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a2e885c8-9d86-420d-b2c2-5eb99191f013/namecomponent.png)

Components can also be added by dragging-and-dropping assets from the **Content Browser** into the **Components** window.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c2879955-6702-497a-92d2-b7266ac450bf/drag_asset_components_list.png)

Assets this method applies to include: StaticMeshes, SoundCues, SkeletalMeshes, and ParticleSystems.

## Removing Components

To remove a Component from the **Components** window, **Right-click** on the Component's name and select **Delete**.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/639de036-1d86-47f1-b271-884c5ea8ce17/delete_component.png)

You can also select the Component in the window and press the **Delete** key to remove it as well.

## Transforming Components

Components, when added to an instance in your level, are placed by default at the location of that instance. However, they can be Transformed, Rotated, and Scaled as necessary in either the **Details** panel or the **Viewport** similar to the method in which you can [Transform Actors](/documentation/en-us/unreal-engine/transforming-actors-in-unreal-engine).

You can select Components for transformation either by clicking on their name in the **Components** window or by clicking directly on the Component in the **Viewport**. When Transforming, Rotating, and Scaling your Components in the **Viewport**, hold **Shift** to enable snapping. This snapping requires that snapping be enabled in the **Level Editor** and uses the **Snap Grid** settings from the **Level Editor** (see [Actor Snapping](/documentation/en-us/unreal-engine/actor-snapping-in-unreal-engine) for more information on Grid Snapping).

Exact values can also be entered for **Location**, **Rotation**, and **Scale** in the **Details** panel for your selected component.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b6089ad5-c41f-4916-b269-c07e885d5c27/transform_details.png)

Transforming, Rotating, or Scaling a parent component will propagate the transformation down to all child components as well.

## Component Assets

Once you have added a Component, you may need to specify the asset to occupy the Component (such as assigning a Static Mesh to use for a StaticMeshComponent). There are a couple of different ways you can assign an asset to use for a Component type as described below.

### Assigning Component Assets

To assign an asset to a Component in the **Components** window:

1.  With the Component selected, in the **Details** panel find the section that corresponds to your Component type.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b6b2be6a-97ef-4955-abf4-ba4147e1161f/emptycomponent.png)
    
    Above we have added a StaticMeshComponent and under **StaticMesh** is where we would assign the asset to use.
    
2.  Click the **Static Mesh** drop-down box, then select the asset to use from the context menu.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/52e23077-628a-4d22-b42e-2ccd21b72f65/selectcomponentlist.png)

Another method of assigning an asset can be done using the **Content Browser**:

1.  Select the asset you would like to assign as the asset to use with your Component in the **Content Browser**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/baa283b6-7e52-4205-be45-f3c0b196d352/selected_asset.png)
2.  With the **Component** selected, in the **Details** panel find the section that corresponds to your Component type.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5ff6dccb-3c1d-431e-af4d-5f33e1fc6947/emptycomponent.png)
    
    Above we have added a StaticMeshComponent and under **StaticMesh** is where we would assign the asset to use.
    
3.  Instead of clicking the **Static Mesh** box, since an asset is selected in the **Content Browser**, click the ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/92cca7a3-1348-4def-8b8a-6b8946f701ba/k2_button_use_scs.png) button.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7c209405-1f45-4f2d-9a93-0a327c882e27/copy_asset.png)
    
    This will assign the asset selected in the **Content Browser** as the asset to use in the Component.
    

### Removing Component Assets

To clear an assigned asset from a Component:

1.  In the **Details** panel for the Component, click the ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e19729fd-a5c4-492c-935b-b2d868e4f37c/resetbuttonicon.png) button next to the currently assigned asset.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3fd7c560-5850-4b24-8094-2cde1ef82372/resetassetbutton.png)
2.  Or, click the **Current Asset** box for your asset, then select the **Clear** from the context menu.
    
    ![Clear](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ff9f5898-524f-47ce-a010-f2d86207e9dd/clear_asset.png)
    
    In either method, the asset will be removed as being assigned to the Component.
    

### Browsing to Component Assets

You can also browse to a currently assigned asset of a Component, jumping to and locating in the **Content Browser**:

1.  In the **Details** panel for the Component, press the ![Blueprint - Browse Asset Button](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c3236ade-4060-49a4-874f-032a226d4075/k2_button_browse_scs.png) button next to the currently assigned asset.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4f019dff-0cfa-49e0-baaa-a8c16a47b846/lookup_asset.png)
2.  The **Content Browser** opens showing the assigned asset selected.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/93ecb915-d57d-4de0-a0a0-a88c239928c3/selected_asset.png)

## Renaming Component Instance Variables

Components created in the **Components** window will have an automatically generated instance variable name based on their type.

To change the name of these variables:

1.  Select the component in the **Components** window and its details will appear in the **Details** panel.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bedfd675-3917-46a9-885d-5a0954932e1b/new_component_details.png)
2.  Enter a new name for the component in the **Variable Name** field in the **Details** panel and confirm by pressing **Enter**.
    
    You can quickly rename a Component by selecting it in the **Components** window then pressing **F2**.
    

## Component Events and Functions

You can quickly add events and/or functions based on a Component to the **Event Graph** of the Blueprint through different methods. Any events or functions created in this manner are specific to that particular function and do not have to be tested to verify which Component is involved.

1.  Add a Component for which events can be created, such as a BoxComponent.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cf75f7ba-f151-4d2e-8e18-fbbbcfd6ff69/addboxcomponent.png)
2.  Provide a name for your Component, here we called it Trigger.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/de49a8e9-67d3-45af-83f1-69949dcd42ec/namedboxcomponent.png)
3.  In the **Details** panel, click the **Add Event** button and select your desired event type.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0f239677-c666-45ed-9baf-32cf6e1bc470/addeventbutton.png)
    
    You can also **Right-click** on the Component in the **Components** window and select your event from the **Add Event** context menu.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6eb1fea2-35ec-4aec-a79a-274f7335bf09/rightclickaddevent.png)
4.  In either manner, a new event node (based on the type you selected) will be added to the **Event Graph** which will automatically open.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/603979f2-4794-4e78-98c2-15f42f61ab16/eventadded.png)

Events and Functions can also be added for a Component from the **Event Graph** through the **My Blueprint** window:

1.  In the **My Blueprint** window, under **Components**, select your Component.
    
2.  **Right-click** in the graph to bring up the context menu.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/13b42491-67fd-44a6-bbb8-97a44603b115/eventsandfunctionsarea.png)
    
    If the component has any associated events or functions, they will be listed at the top.
    
    Not all Components have associated events. For instance, a PointLightComponent only has functions.
    
    You can also **Right-click** on the Component in the **My Blueprint** window to access the **Add Event** context menu.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6e349094-8f8e-4244-bd20-b6e418123d61/rightclickmyblueprint.png)