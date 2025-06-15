# Flow Control

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/flow-control-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/flow-control-in-unreal-engine)  
**Processed:** 2025-06-14 16:23:54

---

## Switch Nodes

A switch node reads in a data input, and based on the value of that input, sends the execution flow out of the matching (or optional default) execution output. There are several types of switches available: **Int**, **String**, **Name**, and **Enum**.

In general, switches have an execution input, and a data input for the type of data they evaluate. The outputs are all execution outputs. **Enum** switches automatically generate the output execution pins from the **Enum**'s properties, while **Int**, **String**, and **Name** switches have customizable output execution pins.

### Editing Switch Nodes

When an **Int**, **String**, or **Name** switch node is added to a Blueprint, the only output execution pin available is the **Default** pin. The **Default** output execution pin will fire if the input fails to match any of the other specified output pins. It can be removed by either right-clicking on the pin and selecting **Remove Execution Pin** or by unchecking the **Has Default Pin** option in the **Details** tab for the switch node.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a6d76a5d-5e9d-45dc-a443-15fc4cbe2e7e/newswitchonint.png)

#### Editing an Int Switch:

1.  Select the switch node in the **Graph** tab to bring up its properties in the **Details** tab.
    
2.  Change the **Start Index** to the lowest integer value that you want to check against.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/76b714a9-7fbb-4e9a-800f-b384a151dc32/switchonint_startindex.png)
3.  Click on **Add Pin** on the switch node to add the pin with your **Start Index** value.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4674e132-45eb-484f-bae1-85c4bf3ee7c9/switchonint_addpin.png)

Clicking on **Add Pin** further will add more pins, with the value incremented by 1 each time. To delete an execution pin, right-click on the pin and select **Remove Execution Pin**. Note that removing an output execution pin on a **Switch on Int** node causes any higher-valued pins to decrease their value by 1 to fill the gap.

#### Editing a Name or String Switch:

1.  Select the switch node in the **Graph** tab to bring up its properties in the **Details** tab.
    
2.  Click on the ![Add Pin](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b5ab3f48-546c-4327-8c67-8eda12b42062/addpinbutton.png) icon to the right of **Pin Names**.
    
3.  Type the value you would like your **String** or **Name** to compare to in the text box that appears.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/72304960-56b2-405d-b507-fabaf5724791/switchonstring_namepin.png) ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e3a980f0-8345-427c-afe4-839088a54c90/switchonstring_withpin.png)

Repeat the process for any other pins you would like to add. Pins can also be duplicated, inserted, or deleted by clicking on the ![Pin Options](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/08b4d59e-99a0-42c4-9c2c-f71f54431f01/pinoptionsbutton.png) icon by the desired pin in the **Details** tab. To delete an execution pin, you can also right-click on the pin and select **Remove Execution Pin**.

## Standard Flow Control Nodes

These nodes provide a variety of means to control the flow of execution.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8b39e139-d354-4676-b283-f1ca239f539b/flowcontrolexpanded.png)

### Branch

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f71f4d3e-8707-4d18-b398-fca822b66bdd/branch_example.png)

The **Branch** node serves as a simple way to create decision-based flow from a single true/false condition. Once executed, the Branch node looks at the incoming value of the attached Boolean, and outputs an execution pulse down the appropriate output.

In this simple example, the branch is checking the current state of a boolean variable. If true, it sets the color of a light to be red. If false, it sets it to blue.

Click for full image.

| Item | Description |
| --- | --- |
| Input Pins |   |
| **(Unlabeled)** | This execution input triggers the branch check. |
| **Condition** | Takes in a boolean value used to indicate which output pin will be triggered. |
| Output Pins |   |
| **True** | This outputs an execution pulse if the incoming condition was `true`. |
| **False** | This outputs an execution pulse if the incoming condition was `false`. |

### DoN

![DoN Example](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2a2feed1-3e05-4442-96a0-d2ce61fa65b9/do_n.png)

The **DoN** node will fire off an execution pulse **N** times. After the limit has been reached, it will cease all outgoing execution until a pulse is sent into its **Reset** input.

For example, you could have a vehicle start twenty times, and then fail to start until a refueling event tied to the **Reset** input was activated.

Click for full image.

| Item | Description |
| --- | --- |
| Input Pins |   |
| **Enter** | This execution input triggers the DoN check. |
| **n** | This input sets the number of times the DoN node will trigger. |
| **Reset** | This execution input will reset the DoN node so that it can be triggered again. |
| Output Pins |   |
| **Exit** | This execution pin is only triggered if the DoN has not yet been triggered more than N times, or if its Reset input has been called. |

### DoOnce

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7047d5ce-c36a-4bbf-8323-caa2f3283ffd/doonce_example.png)

The **DoOnce** node - as the name suggests - will fire off an execution pulse just once. From that point forward, it will cease all outgoing execution until a pulse is sent into its *Reset* input. This node is equivalent to a DoN node where **N = 1**.

For example, you could have the network for an opening door run through a DoOnce, and that door would open only one time. However, you could tie a trigger event into the Reset, which will cause the door to be accessible once the trigger has been activated.

Click for full image.

| Item | Description |
| --- | --- |
| Input Pins |   |
| **(Unlabeled)** | This execution input triggers the DoOnce check. |
| **Reset** | This execution input will reset the DoOnce node so that it can be triggered again. |
| Output Pins |   |
| **Completed** | This execution pin is only triggered if the DoOnce has not yet been triggered, or if its Reset input has been called. |

### FlipFlop

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/28be1dab-7592-4213-bff6-fdd63f67b5c9/flipflop_example.png)

The **FlipFlop** node takes in an execution output and toggles between two execution outputs. The first time it is called, output A executes. The second time, B. Then A, then B, and so on. The node also has a boolean output allowing you to track when Output A has been called.

Click for full image.

| Item | Description |
| --- | --- |
| Input Pins |   |
| **(Unlabeled)** | This execution input triggers the FlipFlop. |
| Output Pins |   |
| **A** | This output pin is called the first and every odd-numbered time thereafter that the FlipFlop is triggered. |
| **B** | This output pin is called the second and every even-numbered time thereafter that the FlipFlop is triggered. |
| **Is A** | Outputs a boolean value indicating whether Output A is being triggered or not. This, in effect, will toggle between `true` and `false` each time the FlipFlop node is triggered. |

### ForLoop

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9c23427b-7d18-4b55-a4f7-4345be5e41c4/forloop_example.png)

The **ForLoop** node works like a standard code loop, firing off an execution pulse for each index between a start and end.

In this simple example, the loop is triggered when the player touches a simple level trigger. The loop iterates 10 times, each time calling a Print String, which logs a prefix message along with the current iteration.

Loop iterations will take place between frames, so large loops may incur a performance hit.

Click for full image.

| Item | Description |
| --- | --- |
| Input Pins |   |
| **(Unlabeled)** | This execution input launches the loop. |
| **First Index** | Takes in an Int representing the first index of the loop. |
| **Last Index** | Takes in an Int representing the last index of the loop. |
| Output Pins |   |
| **Loop Body** | This outputs an execution pulse on each iteration of the loop as it moves between the indices. |
| **Index** | This outputs the current index of the loop. |
| **Completed** | This is a standard execution output pin that fires when the for loop has completed. |

### ForLoopWithBreak

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7098aa10-983e-400f-b7a3-7002b8658993/forloopwithbreak_example.png)

The **ForLoopWithBreak** node works in a very similar manner to the ForLoop node, except that it includes an input pin that allows the loop to be broken.

In this simple example, the loop is triggered when the player touches a simple level trigger. The loop iterates 1,000 times, each time hitting a Branch which checks to see if the loop has hit 500 iterations. If it has not, then a message with the current iteration count is broadcast to the screen. Once it exceeds 500, the Branch calls a Custom Event, which in turn breaks the loop. A Custom Event is used for visual clarity, to eliminate the need to have the wire wrap back around to the Break input pin.

Loop iterations will take place between frames, so large loops may incur a performance hit.

Click for full image.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/156d4def-c0bf-4b5c-9a4a-b0551c4dff1c/brokenat500.png)

| Item | Description |
| --- | --- |
| Input Pins |   |
| **(Unlabeled)** | This execution input launches the loop. |
| **First Index** | Takes in an Int representing the first index of the loop. |
| **Last Index** | Takes in an Int representing the last index of the loop. |
| **Break** | This execution input breaks the loop. |
| Output Pins |   |
| **Loop Body** | This outputs an execution pulse on each iteration of the loop as it moves between the indices. |
| **Index** | This outputs the current index of the loop. |
| **Completed** | This is a standard execution output pin that fires when the for loop has completed. |

### Gate

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d2eb88c7-9306-48c3-8a14-c49b576abce8/gate_example.png)

A **Gate** node is used as a way to open and close a stream of execution. Simply put, the Enter input takes in execution pulses, and the current state of the gate (open or closed) determines whether those pulses pass out of the Exit output or not.

In this simple example, a timeline with no tracks, with both auto-play and looping activated, updates the Enter input pin of a gate. In the level are two triggers. One trigger opens the gate, the other closes it. If the gate is open, then execution pulses leave the Exit pin and a Print String is called that logs a message to the screen. Once the player touches the Close trigger, the gate closes and the message stops displaying. If they then touch the Open trigger, the message starts to appear again.

Click for full image.

| Item | Description |
| --- | --- |
| Input Pins |   |
| **Enter** | This execution input represents any execution that is to be controlled by the gate. |
| **Open** | This execution pin sets the state of the gate to *open*, allowing execution pulses to pass through to the Exit output pin. |
| **Close** | This execution pin sets the state of the gate to *closed*, stopping execution pulses from passing through to the Exit output pin. |
| **Toggle** | This execution pin reverses the current state of the gate. *Open* becomes *closed* and vice versa. |
| **Start Closed** | This boolean input determines the starting status of the gate. If set to *true* the gate begins in a closed state. |
| Output Pins |   |
| **Exit** | If the gate status is currently *open*, then any execution pulses that hit the Enter input pin will cause a pulse to leave the Exit output pin. If the gate is *closed*, the Exit pin is nonfunctional. |

### MultiGate

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/25befdf6-d1da-46c3-9728-8bb836911cdc/multigate_example.png)

The **MultiGate** node takes in a single data pulse and routs it to any number of potential outputs. This can take place sequentially, at random, and may or may not loop.

In this example, a simple looping and auto-playing timeline is outputting a pulse every half-second. That pulse hits the MultiGate and is routed accordingly, triggering one of a series of Print String nodes, which, when played in order, reveal a special message.

Click for full image.

| Item | Description |
| --- | --- |
| Input Pins |   |
| **(Unlabeled)** | This is the primary execution input that takes in any pulses that need to be routed by this MultiGate. |
| **Reset** | This sets the current output index back to 0 by default, or to the currently set *Start Index*, if not -1. |
| **Is Random** | If set to *true*, then the outputs are chosen in random order. |
| **Loop** | If set to *true*, then the outputs will continuously repeat in a loop. If *false*, then the MultiGate ceases to function once all outputs have been used. |
| **Start Index** | Takes in an Int to represent the output index the MultiGate should use first. A value of -1 is the same as not specifying a start point. |
| Output Pins |   |
| **Out #** | Each output represents a possible output pin that the MultiGate may use to send out a routed execution pulse. |
| **Add pin** | Though not really an output pin, this button allows you to add as many outputs as you like. Outputs can be removed by right-clicking and choosing Remove Output Pin. |

### Sequence

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d03a95bd-5909-40f4-ba76-4b712ba6e9f1/sequence_example.png)

The **Sequence** node allows for a single execution pulse to trigger a series of events in order. The node may have any number of outputs, all of which get called as soon as the Sequence node receives an input. They will always get called in order, but without any delay. To a typical user, the outputs will likely appear to have been triggered simultaneously.

In this example, the sequence node is called at the beginning of the level. It then fires off 5 Print String nodes in order. However, without a meaningful delay, it will seem as if the messages appear at almost the same time as one another.

Click for full image.

| Item | Description |
| --- | --- |
| Input Pins |   |
| **(Unlabeled)** | This is the primary execution input that takes in any pulses that need to be routed by this Sequence. |
| Output Pins |   |
| **Out #** | Each output represents a possible output pin that the Sequence may use to send out a routed execution pulse. |
| **Add pin** | Though not really an output pin, this button allows you to add as many outputs as you like. Outputs can be removed by right-clicking and choosing Remove Output Pin. |

### WhileLoop

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/05404767-5aea-4c4b-a7d2-c3418d3fe73a/bp_whileloop-1.png "BP_WhileLoop-1.png")

A test condition and a body are all that make up a **WhileLoop**. Before executing the statement(s) in its body, the Blueprint evaluates WhileLoop's test condition to determine if it is true. After executing the statement(s) in its body, the Blueprint re-evaluates the test condition, and if the condition remains true, it keeps executing the statement(s) in the loop's body. Otherwise, if the test condition returns false, the Blueprint terminates the loop and exits the loop's body.

The following table describes the node's pins:

| Item | Description |
| --- | --- |
| Input Pins |   |
| **(Unlabeled)** | This is the primary execution input that takes in any pulses that will drive this WhileLoop. |
| **Condition** | This is the loop's test condition. |
| Output Pins |   |
| **Loop Body** | This outputs an execution pulse on each iteration of the loop as it moves between the indices. |
| **Completed** | This is a standard execution output pin that fires as soon as the loop ends. |

**Best Practice:** Consider these questions when using WhileLoop.

-   What is the loop's terminating condition?
    
-   Is the condition initialized before the loop's first test?
    
-   Is the condition being updated in each loop cycle before testing the condition again?
    

Answering these three questions should help you avoid infinite loops, which can cause your game to become unresponsive (or crash).

#### Example Usage

The following example shows a Blueprint printing `Start WhileLoop` to the **Viewport** (1) before entering the WhileLoop body and evaluating whether **Counter** is less than **Count Limit** (2). While the test condition (2) evaluates `true`, the Blueprint remains in the WhileLoop body and increments the counter integer before printing `Counter Value: [Counter]` to the Viewport (3). When the test condition (2) evaluates `false`, the Blueprint exits the WhileLoop body, and prints `WhileLoop Completed` to the Viewport.

Click for full image.