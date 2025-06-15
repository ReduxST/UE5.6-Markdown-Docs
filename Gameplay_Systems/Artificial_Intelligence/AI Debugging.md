# AI Debugging

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/ai-debugging-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/ai-debugging-in-unreal-engine)  
**Processed:** 2025-06-14 16:05:18

---

Once you've created an AI entity you can diagnose problems or simply view what an AI is doing at any given moment using the AI Debugging Tools. Once enabled, you can cycle between viewing [Behavior Trees](/documentation/en-us/unreal-engine/behavior-trees-in-unreal-engine), the [Environment Query System (EQS)](/documentation/en-us/unreal-engine/environment-query-system-in-unreal-engine), and the [AI Perception](/documentation/en-us/unreal-engine/ai-perception-in-unreal-engine) systems all within the same centralized location.

To make the most of the AI Debugging tools, you will need a **Pawn** with an **AI Controller** in your Level that is running a Behavior Tree or has an AI Perception component. When your AI is executing an EQS, it will be reflected inside the AI Debugging tool when it is running.

## Enabling AI Debugging

To enable AI Debugging, while your game is running, press the **' (apostrophe)** key.

![Press the apostrophe key](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/17b8a8f8-5cf7-4451-bea4-99fda5bfc2e1/enabled-ai-debugging.png)

The following options are available while the AI Debugging Tools are enabled:

| Command | Option |
| --- | --- |
| **' (apostrophe key)** | Closes the AI Debugging tools. |
| **Numpad Keys (0-4)** | 
Toggles the AI information that is being displayed:

-   **Numpad 0**: Toggles the display of the currently available Nav Mesh data.
-   **Numpad 1**: Toggles the display of the general AI debug information.
-   **Numpad 2**: Toggles the display of the Behavior Tree debug information.
-   **Numpad 3**: Toggles the display of the EQS debug information.
-   **Numpad 4**: Toggles the display of the AI Perception debug information.



 |
| **Ctrl + \` (tilde key)** | Toggles the display of the HUD class being used (if applicable). |
| **Ctrl + Tab** | Toggles the display of any Debug Messages. |

The Numpad values above and their associated debug information are for the default debugger. These values can be dynamically incremented from 0-9 on a project basis based on your project needs.

## Nav Mesh

When the AI Debugging tools are enabled, pressing Numpad 0 will toggle the display of the possible locations the AI can currently navigate to from its current position using the **Nav Mesh Bounds** Volume (if one is placed in the Level).

![Pressing Numpad 0 will toggle the display of the possible locations the AI can currently navigate to from its current position using the Nav Mesh Bounds Volume](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/91fbe389-5839-4d4e-a0a7-4dd8bb59195e/0-nav-mesh-1.png)

You can also toggle the display of the Nav Mesh during gameplay with the console command **show Navigation true** (to display the Nav Mesh) or **show Navigation false** (to hide the Nav Mesh).

## AI

With the AI Debugging tools enabled, pressing Numpad 1 will display the general AI debug information:

![Pressing Numpad 1 will display the general AI debug information](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d96da456-bcba-4d38-a4c3-a4067dd82a05/1-ai-1.png)

The AI category within the AI Debugging tools displays general information about the AI such as:

| Option | Description |
| --- | --- |
| **Controller Name** | Displays the assigned AI Controller Class. |
| **Pawn Name** | Displays the assigned Pawn Class. |
| **Movement Mode (Base)** | Displays the current movement mode (and the Mesh it is currently moving on). |
| **Nav Data (Path following)** | Displays the Navigation Class (and if the AI is moving). |
| **Behavior (Tree)** | Displays if a Behavior Tree is running (and the Behavior Tree Class it is running). |
| **Active task** | Displays the currently ticking Task of the assigned Behavior Tree. |
| **Gameplay tasks** | Displays the number of queued Tasks. An example of Gameplay Tasks includes the **GameplayAbilitySystem** tasks. |
| **Montage** | Displays the currently active Anim Montage. |

In addition to the options above, above the Pawn in the Level, you will see the assigned AI Controller Class and Pawn Class (also displayed in the upper-right corner of the Viewport).

## Behavior Tree

When the AI Debugging tools are enabled, pressing Numpad 2 will toggle the display of the [Behavior Tree](/documentation/en-us/unreal-engine/behavior-trees-in-unreal-engine) information. -t

![Pressing Numpad 2 will toggle the display of the Behavior Tree information](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9ca45e9f-e76e-4a4e-9342-c30141d0f23c/2-behavior-tree.png)

Behavior Tree debug information is split into two categories: the Behavior Tree information (left) and the Blackboard information (right). The Behavior Tree information displays the class of Behavior Tree being used and which branch of the tree is currently being executed (along with the nodes within that branch). The Blackboard debug information will display the Blackboard asset being used along with any Blackboard keys and their current values (which can be useful in determining why the AI is or is not performing an action based on the value of a key).

Inside the Behavior Tree asset, you can also add **Breakpoints** similar to normal Blueprints to pause the execution of the script when reaching a given node. This can help you diagnose what is occurring at any given time within your behaviors.

## EQS

You can display information about active [Environmental Queries](/documentation/en-us/unreal-engine/environment-query-system-in-unreal-engine) by pressing Numpad 3 when the AI Debugging tools are enabled.

![You can display information about active Environmental Queries by pressing Numpad 3 when the AI Debugging tools are enabled](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6ca3572e-bc48-4172-84c0-770d17bed710/environmet-query-system-debugging-image-1.png)

The **Visual Logger** records EQS data which can also be referred to. Please see the linked page for more details.

The EQS debug information will display the current Environmental Query that is being run along with the Generator used. In the example above, we are using a Simple Grid to determine the best possible location that provides a line of sight to the Player that is nearest the enemy AI character. For this example, we are also presented with the points on our grid (represented by spheres).

The green spheres are locations that pass our Test (has line of sight to the Player) while the blue spheres represent locations that fail our Test (does not have line of sight to the Player). Each sphere is weighted with a numerical value, and our highest weighted value is designated as the "winner" and location that the AI chooses to move to.

You can also press the / (divide) key to display a detailed table breakdown that shows the results of your Tests.

![You can also press the divide key to display a detailed table breakdown which shows the results of your Tests](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e42bf096-911c-4b7c-9327-dbcb396788ad/detailed-table-breakdown-debug.png)

In the example image above, the gray float numbers in the right-most column are the distance in cm and the green ones are the normalized values (from what has been specified in the Test).

In addition to using the AI Debugging tools, EQS provides a way to debug queries while your game is not running by using a special type of Pawn. Please see [EQS Testing Pawn](/documentation/en-us/unreal-engine/environment-query-testing-pawn-in-unreal-engine) for more information.

## Perception

At runtime with the AI Debugging tools enabled, pressing 4 on the Numpad key will display [Perception System](/documentation/en-us/unreal-engine/ai-perception-in-unreal-engine) information.

![Pressing 4 on the Numpad key will display Perception System information](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/828effb8-6398-4187-bcbe-c480813b3717/perception-debug-01.png)

Above, we have an AI character that is set up for Sight (indicated by the green debug lines drawn from the character's head). In the image below, when the AI character sees our Player (which is a source of stimuli for Sight), that location is represented by a green sphere as the **Last Known Location**.

![Location is represented by a green sphere as the Last Known Location](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6b72d204-be0e-4110-8c52-8e8b25757d39/perception-debug-02.png)

Any Senses that have been defined on the **AI Perception** Component under **Senses Config** will be displayed in the debug window.

![Any Senses that have been defined on the AI Perception Component under Senses Config will be displayed in the debug window](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a87d8221-4d23-4535-8bdb-83531a0979fb/perception-debug-03.png)

Above, we are debugging both Sight (green) and Hearing (yellow) Senses.

You can change the debug color used for Senses on the **AI Perception** Component using the **Debug Color** property.