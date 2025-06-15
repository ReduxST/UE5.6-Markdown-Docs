# How to Get Animation Variables

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/how-to-get-animation-variables-in-animation-blueprints-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/how-to-get-animation-variables-in-animation-blueprints-in-unreal-engine)  
**Processed:** 2025-06-14 16:29:07

---

When developing [Animation Blueprint](/documentation/en-us/unreal-engine/animation-blueprints-in-unreal-engine)s for characters in **Unreal Engine**, it can be helpful to implement dynamic movement and locomotion **variables** to control animation behaviors.

This document will explain how to set up the **EventGraph** Animation Blueprint logic to calculate these variables in your own project. In addition, this document will also provide an explanation of how to calculate these variables in a **thread safe** [blueprint function](/documentation/en-us/unreal-engine/graphing-in-animation-blueprints-in-unreal-engine#cputhreadusageandperformance), using [property access](/documentation/en-us/unreal-engine/graphing-in-animation-blueprints-in-unreal-engine#propertyaccess) nodes to increase your projects performance and stability.

#### Prerequisites

-   A controllable Third Person Character with a [movement component](/documentation/en-us/unreal-engine/movement-components-in-unreal-engine).

You can supplement this requirement with the [Third-Person template project](/documentation/en-us/unreal-engine/third-person-template-in-unreal-engine) if needed.

## Character Object Reference

Most animation variables can be calculated using the character's [movement component](/documentation/en-us/unreal-engine/movement-components-in-unreal-engine) in the **EventGraph**. In order to use the character's movement component to calculate other animation variables, a reference variable must be created.

First, in the **EventGraph** of the character's Animation Blueprint, create an **Event Blueprint Initialization Animation** node.

![event blueprint initialize animation amination blueprint event graph node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/83284fd6-68b0-485c-bdce-68156b7b0bc8/ebia.png)

From the **Event Initialization** node, create a **Cast** node that casts the animation blueprint to the character's blueprint.

In the workflow example, the character's blueprint is the `BP_ThirdPersonCharacter` found in the Third Person template project.

Then create a **Get Owning Actor** node and connect the **Return Value** output pin of a to the **Cast** node's **Object** input pin.

![cast event graph animation blueprint node cast to third person character blueprint](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0410fd92-a57d-471e-8f46-173643a8e689/cast.png)

Next, **right-click** the cast node's **As Character** output pin and select the **Promote to Variable** option from the context menu, to create a character object reference variable.

After connecting the logic, a **character object** reference variable is accessible in your blueprint's **EventGraph** and **AnimGraph**.

![set character reference variable with cast to third person blueprint animation blueprint node event graph](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2e4b994e-e59d-48a0-a059-ee18a66362e2/thirdpbp.png)

## Movement Component Reference

In order to isolate the character's **Movement Component** from the **Character Object**, a **Get Character Movement** node is needed. From the **Set Character** variable node's **Character** output pin, create a **Get Character Movement** node.

![get character movement by create a get character movement node from the character reference node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1eab78c0-d02b-442f-9822-71cb3e70d883/getcharmovement.png)

Next, **right-click** the **Character Movement** output pin to a variable, and select promote to variable from the context menu, to create a movement component reference variable.

![set character movement component reference variable in event graph](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/deceb1fb-4f14-44a7-b79f-efdf9409696d/charmovement.png)

After connecting the logic, a **character movement component** reference variable is accessible in your blueprint's **EventGraph** and **AnimGraph**.

![full character reference and movement component reference animation blueprint event graph](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b03cbbfe-c70d-4355-ab46-849d104f8126/fullcharbp.png)

## Velocity

A character's velocity can be a helpful value to use when calculating animations that require direction or speed.

To create a velocity variable in the **EventGraph**, first create an **Event Blueprint Update Animation** node.

Next, add the **Movement Component** reference variable to the **EventGraph**. Then, you can use a **Get Velocity** node, to calculate the vector value that represents the movement component's direction and magnitude of movement.

![create a get velocity node from the movemnt component reference variable](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/461ac725-4409-4bd3-aba9-23053c53b9b6/getvelocity.png)

Next, **right-click** the **Velocity** output of the **Get Velocity** node and select the **Promote to Variable** option from the context menu to create the velocity variable.

After connecting the logic, a **Velocity** variable is accessible in your blueprint's **EventGraph** and **AnimGraph**.

![full velocity reference variable in event graph](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/49f936a8-7dca-4c76-bbb5-4dc45cdd7273/velocity.png)

Here, a **Print String** node is sending a debug message every frame with the updated **X**, **Y** and **Z** values of the character's velocity.

![velocity print string demo](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6044b9f7-d63e-488a-8526-c7d0a1605b7c/velocityegdemo.gif)

### Thread Safe

First create a new thread safe function in your character's animation blueprint.

Then, **right-click** in the graph to create a **property access** node.

From the **property access** node's drop down menu select the function, **Try Get Pawn Owner > Get Movement Component > Velocity**. Then right-click the vector output pin and select promote to variable, to create a velocity variable.

![velocity get property access context menu](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/990705b3-6f09-4322-a2a9-60703ad121db/pa.png)

After connecting the logic, a **Velocity** variable is accessible in your blueprint's **EventGraph** and **AnimGraph**.

![velocity thread safe graph full function](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/90b49def-481d-41b3-8143-3759cab83c01/velocityts.png)

In order to update this function during your project's runtime, add the thread safe Velocity function to the **Blueprint Thread Safe Update Animation** graph.

![add the velocity thread safe function to the blueprint thread safe update function](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/96e869df-b886-4f69-8caa-67b8942ed223/bptsfvelocity.png)

Your character's Animation Blueprint now calculates the character's velocity in a thread safe manner.

## Character Speed

Character movement speed can be a helpful variable to use when selecting animations based on a character's speed, such as running or walking states.

You can create a **Vector Length XY** node from the velocity variable to isolate the character's speed from the movement component velocity.

Next, **right-click** the **Vector Length XY** node's **Return Value** output pin to select **Promote to Variable** from the context menu.

![create a vectory xy node to isolate speed from the variable function](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/030886dc-1438-4576-82c7-968cbe74d00f/speed.png)

After connecting the logic, a **Speed** variable is accessible in your blueprint's **EventGraph** and **AnimGraph**.

Here, a **Print String** node is sending a debug message every frame with the updated value of the character's speed.

![print string debug displaying character speed demo](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ceeefef0-8e55-4285-a10e-c9467732e2d8/speedegdemo.gif)

### Thread Safe

First create a new thread safe function in your character's Animation Blueprint.

Next, create a **property access** node and select the **Try Get Pawn Owner > Movement Component > Velocity** function from the drop-down menu.

From the **property access** node's output, create a **Vector Length XY** node to extract the forward and lateral motion (**X** and **Y** axis).

![thread safe function to get speed of character](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/257b95ee-1191-42e7-8e54-c7f2daa82bf8/groundspeedts.png)

In order to update this function during your project's runtime, add the thread safe Speed function to the **Blueprint Thread Safe Update Animation** graph.

![add thread safe speed function to the blueprint thread safe update function](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/086bd064-a36f-4531-9cbd-a9167429f986/bptsfspeed.png)

Your character's Animation Blueprint now calculates the character's velocity in a thread safe manner.

## Movement Threshold

To control when your character's movement should trigger animation playback, you can create a Movement Threshold variable that will allow movement when the character's speed reaches a set magnitude.

From the character's speed variable in the **EventGraph**, create a **Greater Than or Equal To (>=)** node and set the value to a low number.

This number can be a very small value like `0.1`.

**Right-click** the boolean output pin of the **Greater Than or Equal To (>=)** node, and select **Promote to Variable** from the context menu.

![add a greater than or equal to node to set the min movement that will allow animations to update](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b1b1c1ea-f7c6-40a6-8987-76121d8c0189/greaterthan.png)

After connecting the logic, a **Movement Threshold** variable is accessible in the Animation Blueprint's **EventGraph** and **AnimGraph**.

Here, a **Print String** node is sending a debug message every frame with the updated state of the character's movement threshold variable.

![should move debug text demo](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1ac5156a-d6a5-4869-af62-4fb59975bc5c/shouldmoveegdemo.gif)

### Thread Safe

First, create a new thread safe function in your character's Animation Blueprint.

Create a **property access** node in the thread safe graph, and set the node to **Try Get Pawn Owner > Movement Component > Velocity**. Extract the forward and lateral movement with the **Vector Length XY** function node.

Then with a **Greater Than or Equal To (>=)** node, set the speed threshold at which movement animation should not occur.

This number can be a very small value like `0.1`.

**Right-click** the boolean output pin of the **Greater Than or Equal To (>=)** node, and select **Promote to Variable** from the context menu.

![should move thread safe funtion](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5777047d-b69b-4680-a1dc-0df33f26435a/shouldmovets.png)

In order to update this function during your project's runtime, add the thread safe Should Move function to the **Blueprint Thread Safe Update Animation** graph.

![add the should move thread safe function to the blueprint thread safe update function](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/07cceca3-5cf5-4158-bfcd-05e52273f095/bptsfshouldmove.png)

Your character's Animation Blueprint now calculates the character's movement threshold variable in a thread safe function.

## Jumping and Falling

You can use a Jumping and Falling variable to determine when to play jumping and landing animations in the character's **AnimGraph**.

First create a **Movement Component** variable into your Animation Blueprint's **EventGraph**.

You can now create a **IsFalling** function node from the **movement component** reference variable node.

**Right-click** the **Is Falling** node's **Return Value** output pin, and select the **Promote to Variable Option** from the context menu.

![add a greater than or equal to node to determine](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1716bf87-cc24-4512-8b9f-4242b5dc6128/image_19.png)

After connecting the logic, a **Jumping and Falling** variable is accessible in the Animation Blueprint's **EventGraph** and **AnimGraph**.

Here, a **Print String** node is sending a debug message every frame with the updated state of the character's Jumping and Falling variable.

![should move debug text demo](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/71ea2117-ae2a-4859-899e-46da0221e708/isfalling.gif)

### Thread Safe

First create a new thread safe function in your character's Animation Blueprint.

Create a **property access** node and set the node to **Try Get Pawn Owner > Get Movement Component > IsFalling**.

**Right-click** the property access node's output pin and select the **Promote to Variable** option from the context menu.

![blueprint thread safe function is falling](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bb691881-7c1f-40c0-b681-ba96616dbc3c/isfallingts.png)

In order to update this function during your project's runtime, add the thread safe Is Falling function to the **Blueprint Thread Safe Update Animation** graph.

![add the thread safe is falling function to the blueprint thread safe update function](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3083db52-d0c4-4b96-ac9f-0fd4345640eb/bptsfshouldmove.png)

Your character's Animation Blueprint now calculates the character's jumping and falling state variable in a thread safe function.

## EventGraph Reference

Here you can reference the full **Event Blueprint Update Animation** logic in the **EventGraph** used in the example workflow.

![full update function on event graph](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b0b1376f-9705-492e-b28d-6c8a372dd1e3/fulleventgraph.png)