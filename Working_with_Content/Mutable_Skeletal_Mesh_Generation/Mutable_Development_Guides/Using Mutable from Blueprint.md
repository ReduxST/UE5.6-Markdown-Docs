# Using Mutable from Blueprint

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/using-mutable-from-blueprint-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/using-mutable-from-blueprint-in-unreal-engine)  
**Processed:** 2025-06-14 17:00:15

---

You can use the following document to learn about how to set up and use Mutable Characters in Blueprints.

## Creating a Customizable Character

You can use the following steps to create a new Mutable Character in a Blueprint.

1.  Create a new \*\*Actor Blueprint. After creating the blueprint, name and open the asset.
    
    ![custom blueprint actor](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/427d77d4-4fc1-4796-a1e9-3f89d3ed4845/image_0.png)
    
    Alternatively, you can use a class/BP that has a skeletal mesh component.
    
2.  In the blueprint editor, in the **Components** panel, select the **Skeletal Mesh** component and add a new **Customizable Skeletal** component as a child.
    
    ![add customizable skeletal mesh components](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7954d3ed-5203-4324-9e8f-259dd8198f59/image_1.png)
3.  Name the **Skeletal Mesh** and the **Customizable Skeletal** components `Body` and `Body_CO` respectively.
    
    ![name body components](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a29b9e64-3ef6-417a-8edd-80b4c3bab1ad/image_2.png)
4.  Select the **Skeletal Mesh** component, then navigate in the **Details** panel to the **Customizable Skeletal Mesh** section and set the instance to be used in the **Customizable Object Instance** property using the asset selection drop-down menu.
    
    ![select instance in details panel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3112c0e3-e660-4f8a-ac8d-f05604cd5f9a/image_3.png)
5.  Then set the **Component Name** property of the Skeletal Mesh component to `Body`. By doing this you will already see the body of the character in the BP's viewport.
    
    ![character body in viewport](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5ad88598-6974-4ce9-b460-054459a6ee5d/image_4.png)
6.  Next, add a new **Skeletal Mesh** component for the character’s head. It should be a child of the `Body` Skeletal Mesh component. Then name the new Skeletal Mesh component `Head`.
    
    ![add head body component in components panel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c838ea6b-8425-4f24-93a9-e5d9f8e71a37/image_5.png)
7.  Create a new **Customizable Skeletal** component as child of the `Head` Skeletal Mesh component and name it `Head_CO`.
    
    ![add customizable skeletal component to head component](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/521665cc-0b6e-4c65-829e-f0c8d78d63a5/image_6.png)
8.  Select the `Head` **Skeletal Mesh** component and add the same instance that we added to the body component, then set the **Component Name** property to `Head`.
    
    ![set head instance](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f4c91493-6b84-4577-96ae-bf73e24d3624/image_7.png)

Your mutable character is now set up in the Actor Blueprint and is visible in the blueprint viewport.

![completed setup of character](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/aeee771a-2ef8-43e2-a7bc-8b3d6ce95546/image_8.png)

## Changing Parameters

Parameters are stored by instances and can be accessed or modified using the API nodes. You can reference the following examples to learn how to set parameter values based on their type.

### Boolean Parameter

![boolean parameter setup](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/dbb8ebdd-c799-41ff-a2d1-cf085d00326d/image_9.png)

### Int Parameter

It's important to make sure that the desired option actually exists within the instance. Search existing parameters using the **FindParameter** node and then get the available option with **GetIntParameterAvailableOption** node. Both nodes must use the `CustomizableObject` reference variable as a target, which can be accessed through the `CustomizableObjectInstance` reference variable.

![integer int parameter setup](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ad07a753-20e1-4b5d-9fe8-6985ac70e8ae/image_10.png)

### Float Parameter

![float parameter setup](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ad91baee-2fb9-4a59-8dbf-f25ff9fa0949/image_11.png)

### Color Parameter

![color parameter setup](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e78b924f-835f-435f-a3da-3b3b45b24f2f/image_12.png)

### Projector Parameter

![projector parameter setup](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/059b4c4c-a67a-481d-870b-48f9b059350c/image_13.png)

## Update Instances

To apply recent changes in parameters, the instance needs to be updated. This can be achieved by adding an **UpdateSkeletalMeshAsync** node after one or more changes.

![update instances example blueprint](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e4613c35-b44a-49bc-a0d7-dafc1a078644/image_14.png)

## Updated Delegate

Events can be registered to this delegate. The broadcasting will take place after the completion of the skeletal mesh update.

| Bind Event to Updated Delegate | Unbind Event from Updated Delegate |
| --- | --- |
| ![bind event to updated delegate node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/822252e3-42cb-4029-820e-3a224338c505/image_15.png) | ![unbind event to updated delegate node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7c58fa33-8e9b-4d11-8659-e7493cb7a695/image_16.png) |

## Parameter Information

Sometimes, additional information like the amount of parameters within an instance, their type or the name of an int parameter's option might be useful. This information is kept in the source `CustomizableObject` reference variable, which is accessible through the instance, and can be retrieved using the following nodes:

| Node | Image |
| --- | --- |
| **Get Parameter Count** | ![get parameter count node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/333975a1-5daf-4b92-9343-015f9955d53d/image_17.png) |
| **Get Parameter Name** | ![get parameter name node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0c3996ca-1d72-41cc-86b4-d1dface32cc5/image_18.png) |
| **Get Parameter Type by Name** | ![get parameter type by name node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/76537a39-51d1-46ee-9b52-b80a2a6eb873/image_19.png) |
| **Find Parameter** | ![find parameter node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fb9924fe-bd47-49e4-aa2a-081bebc9cdee/image_20.png) |
| **Get Int Parameter Num Options** | ![get int parameter num options node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/75f33b2b-11f4-420a-aea6-a0c79e6044a3/image_21.png) |
| **Get Int Parameter Available Option** | ![get int parameter available option node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9424b4e7-a308-432c-afed-69729c5d5b84/image_22.png) |

## Changing States

States can also be queried and changed using the node API:

![get current state node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ba4355ec-30f4-4db6-a6ab-a20691605bb0/image_23.png)

As when changing parameters, the instance needs to be updated with a UpdateSkeletalMeshAsync node after a State change.

![using current state variable setup](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1dd04e89-b8f2-4632-8bcb-2615df23d106/image_24.png)

## State Information

Information about the number and name of States a **CustomizableObject** has, as well as the number and names of parameters in a State can be useful. This information is stored per **CustomizableObject**, and is accessible through a **CustomizableObjectInstance** and can be retrieved using the following nodes:

| Node | Image |
| --- | --- |
| **Get State Count** | ![get state count node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1140475a-fbe6-4f2d-8d5d-92beabde1650/image_25.png) |
| **Get State Name** | ![get state name node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bc53b702-7d99-4e85-9fe3-1f4c63e391c5/image_26.png) |
| **Get State Parameter Count** | ![get state parameter count node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/27c54443-88b4-49e4-aa24-27b3bfab8783/image_27.png) |
| **Get State Parameter Name** | ![get state parameter name node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/85fb228d-22a6-475f-b8e8-9585700812d3/image_28.png) |