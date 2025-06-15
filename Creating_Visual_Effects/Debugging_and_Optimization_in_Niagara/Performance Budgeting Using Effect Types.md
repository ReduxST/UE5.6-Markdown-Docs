# Performance Budgeting Using Effect Types

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/performance-budgeting-using-effect-types-in-niagara-for-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/performance-budgeting-using-effect-types-in-niagara-for-unreal-engine)  
**Processed:** 2025-06-14 16:42:23

---

### When to Use Performance Budgeting

When building a game, you can have a lot of variability in the FX workload depending on the scene composition. Sometimes you may want to take actions to help manage the performance, such as culling instances outside a certain range, or instances that exceed a specified budget usage.

**Effect Type** assets allow you to configure a variety of settings once, then apply them across a collection of Niagara systems.

### How to Create an Effect Type Asset

To create an Effect Type asset, right-click in the **Content Browser** and select **FX > Niagara Effect Type**.

Click image for full size.

### Effect Type Budgeting Options

In the Effect Type asset, you can set several different methods to cull systems that are exceeding your budget usage. These options are all available under the heading **Budget Scaling**.

Click image for full size.

-   **Max Global Budget Usage**: This option lets you set up a budget above which any system is culled. You will normally set this to a value between 0 and 1, which represents a percentage from 0-100%. You can set it to 1.5 if you want the system to be more permissive. What this means is, as soon as any system reaches this percentage of your budget, it is culled. This is the best option if you are favoring performance over visuals.

Click image for full size.

-   **Max Distance Scale by Global Budget Use**: This option lets you set up a curve to define how the distance at which you cull systems decreases as your budget use increases. For example, if your budget use is very high, then Niagara only renders systems that are close and not those that are far away.
    
-   **Max Instance Count Scale by Global Budget Use**: This option lets you set up a curve that defines how as your budget use increases, the number of instances in your level is scaled down. This scales down all instances of all systems that match this Effect Type.
    
-   **Max System Instance Count Scale by Global Budget Use**: This option lets you set up a curve that defines how as your budget use increases, the number of instances in your level is scaled down. However, in this option, instead of culling all instances in all systems, you are culling a number of instances per system.
    

For each of those 3 options that take Start X, Start Y, End X, and End Y values, those values define a linearly interpolated curve. Anything above that curve will be culled. For an example, see the following diagram of what the curve would look like.

Click image for full size.