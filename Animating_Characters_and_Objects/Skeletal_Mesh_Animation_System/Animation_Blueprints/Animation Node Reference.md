# Animation Node Reference

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/animation-blueprint-nodes-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/animation-blueprint-nodes-in-unreal-engine)  
**Processed:** 2025-06-14 16:06:34

---

An [Animation Blueprint](/documentation/en-us/unreal-engine/animation-blueprints-in-unreal-engine) (**AnimBP**) is a special class of [Blueprint](/documentation/en-us/unreal-engine/blueprints-visual-scripting-in-unreal-engine) that specifically controls an object's animations behaviors. AnimBPs are divided into two graphs, the [EventGraph](/documentation/en-us/unreal-engine/graphing-in-animation-blueprints-in-unreal-engine#eventgraph), for controlling the animation logic and interaction behaviors, and the [AnimGraph](/documentation/en-us/unreal-engine/graphing-in-animation-blueprints-in-unreal-engine#animgraph), which controls the animation pose output for the object. Each graph within an AnimBP uses [nodes](/documentation/en-us/unreal-engine/nodes-in-unreal-engine) to perform operations. These nodes can be classified into a few distinct types based on their function in an AnimBP.

## Animation Node Structure

AnimBP nodes on the AnimGraph and EventGraph can have **input** and **output** pins in which information can be passed.

![input and output pins](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/33e372fa-4cdb-4e01-88d1-a57f686aedbd/inputandoutputpins.png)

AnimBP nodes can also have property pins, such as data values or variables that can be modified with linked functions in the AnimBP AnimGraph and EventGraph.

![property pins](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9c1408fd-e33d-47ef-a77a-967531045d48/propertypins.png)

AnimBP node properties can also be accessed in the node's **Details** panel after selecting the node in the AnimBP.

![animbp node details panel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/10964e98-4a16-46b7-8449-9355ffe3621f/detailspanel.png)

## EventGraph Nodes

Event graph nodes are used to process incoming data that in turn is used to drive the pose data in the Anim Graph, such as triggering playback, activating or disabling animations functions, and updating animation data.

![event graph animation blueprint example](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7f09cd1b-0074-4f43-a77f-faed6ae82a70/eventgraphex.png)

With the **Animation Events** documentation, you can reference the function and properties of **EventGraph** AnimBP nodes.

## AnimGraph Nodes

Using data from the **EventGraph**, **AnimGraph** nodes determine the actual frame-by-frame pose to use for the animating object.

![anim graph animation blueprint example](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1bf2ec33-faeb-459b-ad11-ad255ec4ecfe/animgraphex.png)

Here you can access a reference doc for each of the main types of Anim Graph Nodes.

## Animation Node Pose Watching

When working in an AnimBP, you can toggle **Pose Watching** on specific AnimBP nodes to see a color coded debug drawing of the pose that it is generating in the **Viewport**.

![pose watch animation blueprint example](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e47d5621-26ff-4ed3-8a43-be1f52fcba1d/posewatch.png)

To toggle an AnimBP node to pose watch, **right-click** on a node that contains pose data and select **Toggle Pose Watch** from the context menu.

![pose watch animation blueprint example](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bc522b48-f402-4857-96c1-cff0f76e823a/toggleposewatch.png)

You can also have multiple nodes toggled to Pose Watch at once, allowing you to compare poses at different points in the AnimBP to find the exact point in which any errors in your current pose are introduced.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2ddd77ec-ac5a-4c4a-9ec6-d2ab416da9bf/posewatch.png)

By clicking the icon in the upper left corner of the node You can hide the node's watched pose. To change a node's watched pose color, open the **Pose Watch Manager** by navigating in the **Menu Bar** to **Window > Pose Watch Manager** and select the color option next to the desired pose.

![pose watch manager animation blueprint example](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5b9c8e29-11ed-40ac-8ed2-5983da6a9de8/posewatchmanager.png)

You can disable a Pose Watch from the color picker window or by reselecting **Toggle Pose Watch** on the Animation Node.