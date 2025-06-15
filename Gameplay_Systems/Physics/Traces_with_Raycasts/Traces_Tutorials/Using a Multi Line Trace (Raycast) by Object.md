# Using a Multi Line Trace (Raycast) by Object

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/using-a-multi-line-trace-raycast-by-object-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/using-a-multi-line-trace-raycast-by-object-in-unreal-engine)  
**Processed:** 2025-06-14 16:58:06

---

**Multi LineTrace For Objects** will perform a collision trace along a given line and return all hits encountered, returning only objects that match one of the specified Object Types. Below, you will find steps for setting up a **Multi LineTrace For Objects** Blueprint.

## Steps

1.  Follow the steps used for the [Line Trace By Channel](/documentation/en-us/unreal-engine/using-a-single-line-trace-raycast-by-channel-in-unreal-engine) example to set up a trace.
    
2.  Replace the **Line Trace By Channel** node with the **Multi Line Trace For Objects** node.
    
3.  Drag off the **Object Types** pin and add a **Make Array** node, then use the drop-down menus to add Objects to the Array.
    
    ![Drag off the Object Types pin and add a Make Array node then use the drop-down menus to add Objects to the Array](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/23757187-7dcf-42ad-b775-e10122da8b81/guide-how-to-2b-21.png)
    
    Here we assign **WorldDynamic** and **PhysicsBody** as our Object Types. You can use the **Add pin** button to add more Object Types to the Array.
    
4.  Drag off the **Out Hits** pin of the trace node and add a **For Each Loop** node.
    
    ![Drag off the Out Hits pin of the trace node and add a For Each Loop node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/01652725-e758-48b2-b7f3-7d967e172970/guide-how-to-2b-22.png)
    
    This will allow us to do something for each of the Actors hit by the trace.
    
5.  Drag off the **Array Element** and add a **Break Hit Result** node. Then, drag off the **Hit Actor**, add a **Get Display Name (Object)** node and connect to a **Print String** node.
    
    Click image for a full view.
    
    This will now print to the screen each of the Actors hit by the array.
    

## Result

Here, we have a hanging ceiling light (World Dynamic Object Type) in front of a Physics Actor (Physics Body Object Type).

![A hanging ceiling light World Dynamic Object Type in front of a Physics Actor Physics Body Object Type](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f1089d63-7b40-4e5e-a189-a311cbf5861e/guide-how-to-2b-20.png)

Multi LineTrace For Objects, unlike Multi Line Trace by Channel, does not stop at the first object it hits, which is why the trace continues through the light to the cube.