# Using a Single Line Trace (Raycast) by Object

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/using-a-single-line-trace-raycast-by-object-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/using-a-single-line-trace-raycast-by-object-in-unreal-engine)  
**Processed:** 2025-06-14 16:58:08

---

**Line Trace For Objects** will perform a collision trace along a given line and return the first Object the trace hits that matches one of the specified Object Types. To set up a **Line Trace For Objects** Blueprint, do the following:

## Steps

1.  Follow the steps used for the [Line Trace By Channel](/documentation/en-us/unreal-engine/using-a-single-line-trace-raycast-by-channel-in-unreal-engine) example to set up a trace.
    
2.  Replace the **Line Trace By Channel** node with the **Line Trace For Objects** node.
    
3.  Drag off the **Object Types** pin and add the **Make Array** node.
    
    ![Drag off the Object Types pin and add the Make Array node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ff8e9a25-292b-4e14-b517-8f3820c98855/guide-how-to-2b-12.png)
4.  On the **Make Array** node, specify the **ObjectType** you want to trace for (via the drop-down menu).
    
    ![Specify the ObjectType you want to trace for via the drop-down menu](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d0c9ca92-04b4-4914-a962-424740f589f2/guide-how-to-2b-13.png)
    
    Here, we are tracing for **WorldDyanmic** Objects. You can add more by clicking the **Add Pin** button.
    
5.  You can set the rest of the trace up the same way a **Line Trace By Channel** is setup.
    
    Click image for a full view.
    

## Result

We have added a single WorldDynamic Object to our level.

![A single WorldDynamic Object in our level](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/812ef67c-6d6f-45a0-ad2f-00b3e75c2d1b/guide-how-to-2b-16.png)

Only the added Actor is now returning as a hit; consequently, the cubes (since they are Physics Actors) do not return a hit.