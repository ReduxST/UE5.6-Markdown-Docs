# Property Access

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/property-access-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/property-access-in-unreal-engine)  
**Processed:** 2025-06-14 16:45:00

---

**Property Access** allows you to access components and variables that are only accessible on the **Game Thread** anywhere within an Animation Blueprint. Calling a component or variable using Property Access takes a snapshot of its data, which you can use to drive function logic in the [Anim Graph](/documentation/en-us/unreal-engine/graphing-in-animation-blueprints-in-unreal-engine#animgraph), [Animation Node Function](/documentation/en-us/unreal-engine/graphing-in-animation-blueprints-in-unreal-engine#animation-node-function), a [Blueprint Thread Safe Function](/documentation/en-us/unreal-engine/graphing-in-animation-blueprints-in-unreal-engine#threadsafeupdateanimation), or in the Event Graph. Using Property Access reduces the amount of work your project must evaluate on the **Game Thread**, and also reduces the amount of manual blueprint scripting you must perform, leading to increased game and workflow performance.

You can use the following documentation to learn more about using Property Access nodes, pins, and functions that you can use to optimize your project's animation system.

## Overview

When creating logic in an [Animation Blueprint](/documentation/en-us/unreal-engine/animation-blueprints-in-unreal-engine), you will typically use the [Event Graph](/documentation/en-us/unreal-engine/graphing-in-animation-blueprints-in-unreal-engine) to set variables and interface with other Blueprints and Components. The Event Graph is always evaluated on your project's **Game Thread**.

To increase your animation system's performance, you can run **Event Graph** functions on the same **Worker** **Thread** the Animation Graph is updating on, using **Property Access Functions**. For example, you can use Property Access to directly access the character's Velocity without the need to cast to the character blueprint and create a function node to extract the velocity vector.

| Without Property Access | With Property Access |
| --- | --- |
| ![traditional casting and variable setting on event graph](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cadc1025-09a0-4592-8107-0b70a4ed7aca/traditional.png) | ![property access](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e27dbc12-ca7c-4075-81b7-5a6610ab751f/propertyaccess.png) |

## Property Access Functions

Property Access works by evaluating a function graph to take a snapshot of a Game Thread variable's or component's data, and converting that data to be [Thread Safe compatible](/documentation/en-us/unreal-engine/graphing-in-animation-blueprints-in-unreal-engine#threadsafeupdateanimation). When creating a Property Access node, or calling a Property Access function on an Animation Blueprint Node pin, you can select from a number of pre-generated functions that access your project's base components and variables.

These functions can provide variables and components such as a character's velocity, movement direction, or a movement component reference, that you can use to drive animation pose selection or blending in the AnimGraph.

![property access node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/16f40105-e89f-4658-8af7-103c219ae59a/propertyaccessnode.png)

For more information about binding Property Access nodes and pins, see the [Property Access Bindings](/documentation/en-us/unreal-engine/property-access-in-unreal-engine#propertyaccessbindings) section.

### Custom Property Access Functions

You can also create custom Property Access Functions in order to output more specific or unique values. To create a custom Property Access function, start by adding a new function to the graph, by selecting **Add** (**+**) in the **My Blueprint** panel.

![add function button](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d039b55c-0ddb-4531-8b7e-d141f94ed435/addfunction.png)

Create a Return Node, and connect it to the Function Node.

![add return node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9f219b29-a90b-453e-871c-27922e5fbe53/addreturnnode.png)

Select the **Return Node** and enable the **Pure** property in the **Details** Panel.

![enabled pure property](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/66ca9e1b-8c14-42cf-93a3-4dbab1ce983c/markpure.png)

Add a new Output value using **Add** (**+**) and name the output, `ReturnValue`.

The Output must be named `ReturnValue` exactly. Any other name will result in the Property Access Function being inaccessible from a Property Access node or pin binding.

![create function output](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/20dba6a8-6dcf-4d4d-9637-610ae055b60b/createoutput.png)

You can now build any logic to set the Return Node's Output pin, which will then become the output of any Property Access node or pin bound to your function.

You can now bind the Property Access Function to any Property Access node or pin by selecting the function using the Bind drop down-menu. Property Access Functions are color-coded depending on the data type of the Output.

![property node function](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cfb0b34d-a5c7-4f51-b65e-21f6a8f1b72a/pafunction2.png)

For optimized performance, we recommend you enable the Thread Safe property for Property Access Functions. After enabling the function as thread safe, you will need to make all of your variable and component references using Property Access as well. By making custom Property Access functions Thread Safe, you can significantly increase your animation system's performance.

## Property Access Bindings

You can access default and custom Property Access Functions anywhere in an Animation Blueprint using either a Property Access [node](/documentation/en-us/unreal-engine/property-access-in-unreal-engine#asanode), or [as a pin](/documentation/en-us/unreal-engine/property-access-in-unreal-engine#asapin) binding on an existing Animation Blueprint node.

### As a Node

You can create a Property Access node anywhere in an Animation Blueprint. To create a Property Access node, right-click in the **AnimGraph** and select **Property Access** from the **Variables** category.

![create property access node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3899a06f-7e45-415e-8eef-77a9c43a165f/propertyaccess1.png)

After creating a Property Access node, you will need to bind it to a **Function** to reference the component or variable you want to access. You can also bind custom Property Access function graphs, if they meet the necessary requirements. To bind a function to a Property Access node, select a Function from the **Bind** drop-down menu.

Functions are organized by hierarchy, with parent component functions containing child functions that correspond to their child properties. For example, you can navigate beyond a parent Function, to isolate a more specific property that it contains. In this example, a Get property path is created from **TryGetPawnOwner**, to **GetActorLocation**, to a specific axis float value (**X**, **Y**, or **Z**).

![bind property access node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f593389d-25f6-4691-a3c7-8310c059a1fd/propertyaccess2.png)

Once you bind a Property Access node, you can use the node to access the component or variable in your graph, to drive a node's logic.

![property access example](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/eff36225-bb6a-48d0-a746-a622ff82bcab/propertyaccess3.png)

## As a Pin

You can also bind Property Access Functions directly to some AnimNode pins. To bind a Property Access Function to an AnimNode pin, select the node in the graph and navigate in the node's Details panel to the Input pin binding settings. Select **Function** from the Pin drop-down menu to dynamically drive the pins value.

![property access function as a pin](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e3167656-2fd3-4f05-b957-1fcc18883f4e/propertyaccess3.png)

## Property Access Settings

The Property Access context-menu contains the following selections and properties:

![property access context menu settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/16818172-5db2-49a0-93cc-91f3d38b4d27/pasettings.png)

| Name | Description |
| --- | --- |
| **Call Site** | 
The **Call Site** controls which thread to execute the bound Property Access function on. You can select the following options:

-   **Automatic**: Automatically determines the **call site** for the bound Property Access Function based on context and thread safety. You should leave this as the selection in most cases.
-   **Thread Safe**: Evaluates the bound Property Access Function on the **Worker Thread**.
-   **Game Thread** (**Pre-Event Graph**): Evaluates the bound Property Access Function on the **Game Thread**, before the **Event Graph** is evaluated.
-   **Game Thread** (**Post-Event Graph**): Evaluates the bound Property Access Function on the **Game Thread**, after the **Event Graph** is evaluated.
-   **Worker Thread** (**Pre-Event Graph**): Evaluates the bound Property Access Function on the next available **Worker Thread**, before the Event Graph is evaluated.
-   **Worker Thread** (**Post-Event Graph): Evaluates the bound Property Access function on the next available** Worker Thread**, after the** Event Graph\*\* is evaluated.



 |
| **Functions** | Select a Property Access Function to bind to the node or pin. |
| **Properties** | Select a Variable or Component Reference contained within your Animation Blueprint, that you can bind to the Property Access node or pin. |

## Additional Resources

For more information about using Blueprint Thread Safe Functions and Property Access to optimize your animation system, see the [Animation Optimization](/documentation/en-us/unreal-engine/animation-optimization-in-unreal-engine) documentation.

For a workflow example of using Blueprint Thread Safe Functions and Property Access to get Animation Variables, see the [How to Get Animation Variables](/documentation/en-us/unreal-engine/how-to-get-animation-variables-in-animation-blueprints-in-unreal-engine) documentation.

For a workflow example of optimizing an Unreal Engine project to use Thread Safe functions, see the [Adapting Lyra's Animation System](https://www.unrealengine.com/en-US/tech-blog/adapting-lyra-animation-to-your-ue5-game) blog post.