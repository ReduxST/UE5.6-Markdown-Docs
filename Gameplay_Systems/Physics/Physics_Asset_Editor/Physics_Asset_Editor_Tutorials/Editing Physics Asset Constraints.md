# Editing Physics Asset Constraints

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/editing-physics-asset-constraints-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/editing-physics-asset-constraints-in-unreal-engine)  
**Processed:** 2025-06-14 16:21:41

---

Below are several common procedures, and steps, associated with editing **Physics Constraints** in the **Physics Asset Editor**.

## Editing Physics Constraints

The use of Physics Constraints is covered in the [Physics Constraints User Guide](/documentation/en-us/unreal-engine/constraints-user-guide-in-unreal-engine) and their properties are covered in the [Physics Constraint Reference](/documentation/en-us/unreal-engine/physics-constraint-reference-in-unreal-engine). This section will only cover workflows that are specific to the Physics Asset Tool or ones that have deviated substantially from the norm.

1.  Double-click your **Physics Asset** to open it in the Physics Asset Editor.
2.  Select a **Physics Constraint** in the **Viewport** or in the **Skeleton Tree** panel.
3.  **Move and rotate** the Physics Constraint using the **Translation** and **Rotation** tools to create the rotational point of the "joint" the Physics Constraint will form.
4.  Edit the Physics Constraint's properties in the **Details** panel.
    
    You can switch Swing1, Swing2, and Twist from Limited to Locked quickly by using the "**1**", "**2**", and "**3**" keys respectively. The "**4**" key can be used cycle through them setting one to limited and the other two to locked.
    
5.  **Save** often.

See the [Physics Constraint Reference](/documentation/en-us/unreal-engine/physics-constraint-reference-in-unreal-engine) for more information on the Physics Constraint properties in the Physics Asset Editor.

## Aligning Physics Constraints

If you are using the Physics Constraint's **Linear** or **Angular** limits, you will be able to see their alignment:

![You will be able to see  alignment](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8ab7bc10-892c-4904-8a4e-a239bc468046/physics-asset-user-guide-limits.png)

By then translating and rotating the Physics Constraint, you can align the limits to give the desired results. In the most basic of terms, when a Physics Constraint is limited, you can see a yellow line suspended in a green arc or cone structure. The line will be "constrained" within this arc or cone.

For more information on Physics Constraints and their properties, see the [Physics Constraints User Guide](/documentation/en-us/unreal-engine/constraints-user-guide-in-unreal-engine).

## Copying Physics Constraints

While in either mode, properties from one Constraint can be copied to other Constraints:

1.  Select the **Physics Constraint** you wish to copy data from.
2.  **Press Ctrl + C**.
3.  Select **Physics Constraints** you wish to apply data to.
4.  **Press Ctrl + V**.

## Deleting Physics Constraints

There is no easy way to recreate a Physics Constraint, be mindful of this when deleting them.

1.  Double-click your **Physics Asset** to open it in the Physics Asset Editor.
2.  Select the **Physics Constraint** you want to delete in the **Viewport** or in the **Skeleton Tree** panel.
3.  Press the **Delete** key.

## Recreating a Physics Constraint

There is no easy way to recreate a Physics Constraint, be mindful of this when deleting them.

Physics Constraints are only created on the generation of a Physics Body and are only generated upstream. So, if you remove a Physics Constraint from the shoulder, you would have to remove the upper arm Physics Body (which will remove the elbow Physics Constraint), then re-create the upper arm Physics Body. This would create the shoulder Physics Constraint, but not the elbow Physics Constraint, so you would have to continue this process down the arm.