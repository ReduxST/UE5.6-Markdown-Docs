# Using a Multi Line Trace (Raycast) by Channel

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/using-a-multi-line-trace-raycast-by-channel-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/using-a-multi-line-trace-raycast-by-channel-in-unreal-engine)  
**Processed:** 2025-06-14 16:58:04

---

**Multi LineTrace By Channel** will perform a collision trace along a given line and return all hits encountered (up to and including) the first blocking hit, returning only objects that respond to the specified Trace Channel. What this means (practically), is that if there are many **Actors** or **Components** with a collision that **Overlap** the specified Trace Channel between the start and the end of the trace, you will receive them all. But, if the first hit **Blocks** the specified Trace Channel, you will only receive that one item. If you want to receive all items regardless of overlap, or blocking a trace channel, you should use a [Multi Line Trace By Object](/documentation/en-us/unreal-engine/using-a-multi-line-trace-raycast-by-object-in-unreal-engine) node. Below, you will find steps for setting up a **Multi Line Trace By Channel** Blueprint.

### Steps

1.  Follow the steps used for the [Line Trace By Channel](/documentation/en-us/unreal-engine/using-a-single-line-trace-raycast-by-channel-in-unreal-engine) example to set up a trace.
    
2.  Replace the **LineTrace By Channel** node with the **Multi Line Trace By Channel** node.
    
3.  Drag off the **Out Hits** pin and add a **For Each Loop** node.
    
    ![Drag off the Out Hits pin and add a For Each Loop node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2c138a34-8000-4ff6-9d8f-ac5e0d20729f/guide-how-to-2b-18.png)
    
    Since multiple Actors are hit, for each of them, we want to do something (in this example, print the Actors to the screen).
    
4.  Drag off the **Array Element** and add a **Break Hit Result** node. Then, drag off the **Hit Actor**, add a **Get Display Name (Object)** node, and connect to a **Print String** node.
    
    Click image for a full view.
    
    This will now print to the string each of the Actors hit by the array.
    

## Result

Here, we have a Glass Window in front of a Physics Actor.

![A Glass Window in front of a Physics Actor](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d79df8fa-f191-461c-a7c6-885bc2e14530/guide-how-to-2b-17.png)

The Glass Window is a **Destructible Mesh**, and we have set its **Trace Response** to Visibility in its collision settings, which is set to Overlap; while the Physics Actor (Cube) has its Visibility setting to Block. You could use this for situations where you may want to shoot through an object (destroying it) while also hitting an enemy.