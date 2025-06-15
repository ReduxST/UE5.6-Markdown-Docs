# Physics Constraint Reference

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/physics-constraint-reference-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/physics-constraint-reference-in-unreal-engine)  
**Processed:** 2025-06-14 16:42:49

---

This page contains a reference listing of properties for Physics Constraints separated by major categories.

## Constraint

![Constraint Properties](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c60c3615-a670-495b-bc50-0eef5ab65001/properties-constraint.png)

| Property | Description |
| --- | --- |
| **Constraint Actor 1** | When a **Physics Constraint** is placed into the level editor you must specify **Actors** to constrain. This is the first of 2 **Actors**. |
| **Component Name 1** | The first target component that will be constrained. This can be specified when using **Actors** to constrain only a specific component and not the **Actor** root. |
| **Constraint Actor 2** | When a **Physics Constraint** is placed into the level editor you must specify **Actors** to constrain. This is the second of 2 **Actors**. |
| **Component Name 2** | The second target component that will be constrained. This can be specified when using **Actors** to constrain only a specific component and not the **Actor** root. |
| **Joint Name** | When constraining in the **Physics Asset Tool**, this is the name of the Bone that is initially constrained. |
| **Constraint Bone 1** | When constraining in the **Physics Asset Tool**, this is the name of the first joint to constrain. |
| **Constraint Bone 2** | When constraining in the **Physics Asset Tool**, this is the name of the second joint to constrain. |

## Constraint Behavior

![Constraint Behavior](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7b46b59e-acb4-4511-b2cb-5bdaafa659f2/properties-projection.png)

| Property | Description |
| --- | --- |
| **Disable Collision** | This disables collision between the constrained components. |
| **Enable Lenear Projection** | Linear Projection is a post-solve fixup where the child body is translated to resolve remaining errors using a semi-physical correction. Use this to make chains stiffer at lower iteration counts. Projection only works well if the chain is not interacting with other objects. |
| **Enable Angular Projection** | Angular Projection is a post-solve fixup where the child body is rotated to resolve remaining errors using a semi-physical correction. Use this to make chains stiffer at lower iteration counts. Projection only works well if the chain is not interacting with other objects. |
| **Enable Shock Propagation** | Shock Propagation increases the mass of the parent body for the last iteration of the position and velocity solve phases. It can help stiffen up joint chains, but is prone to introduce energy down the chain. Use this for world constraints and ragdoll physics. |
| **Projection Linear Alpha** | The amount of linear projection to apply, with 0 being no projection and 1 being full projection. |
| **Projection Angular Alpha** | The amount of angular projection to apply, with 0 being no projection and 1 being full projection. |
| **Shock Propagation Alpha** | The amount of shock propagation to apply, with 0 being no propagation and 1 being full propagation. |
| **Parent Dominantes** | When set, the parent body in a constraint will not be affected by the motion of the child. |

## Linear Limits

![Linear Limits](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/98c37dd2-b794-4645-b6c1-ab88e56e5483/properties-linear-limits.png)

| Property | Description |
| --- | --- |
| **XMotion** | 
Indicates the linear constraint applied along the X-axis.

-   **Free**: No constraint along this axis.
-   **Limited**: Limited freedom along this axis. The limit is defined for all axes by the **Linear Limit Size** property.
-   **Locked**: Fully constrained along this axis.



 |
| **YMotion** | 

Indicates the linear constraint applied along the Y-axis.

-   **Free**: No constraint along this axis.
-   **Limited**: Limited freedom along this axis. The limit is defined for all axes by the **Linear Limit Size** property.
-   **Locked**: Fully constrained along this axis.



 |
| **ZMotion** | 

Indicates the linear constraint applied along the Z-axis.

-   **Free**: No constraint along this axis.
-   **Limited**: Limited freedom along this axis. The limit is defined for all axes by the **Linear Limit Size** property.
-   **Locked**: Fully constrained along this axis.



 |
| **Limit** | The distance allowed between the two joint reference frames. |
| **Scale Linear Limits** | If true, linear limits scale using the absolute min of the 3D scale of the owning component. |

### Advanced

![Advanced Linear Limits Properties](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bba51d3e-81f5-422d-9614-c0bfc78fa23a/properties-linear-limits-advanced.png)

| Property | Description |
| --- | --- |
| **Soft Constraint** | Whether we want to use a soft constraint (spring). |
| **Stiffness** | Stiffness of the soft constraint. Only used when Soft Constraint is on. |
| **Damping** | Damping of the soft constraint. |
| **Restitution** | Controls the amount of bounce when the constraint is violated. |
| **Linear Breakable** | Whether it is possible to break the joint with linear force. |
| **Linear Break Threshold** | Force needed to break the distance constraint. |
| **Linear Plasticity** | Whether it is possible to reset spring rest length from the linear deformation. |
| **Linear Plasticity Type** | Whether linear placticity has a operation mode. |
| **Linear Plasticity Threshold** | Percent threshold from center of mass distance needed to reset the linear drive position target.This value can be greater than 1. |
| **Contact Transfer Scale** | Collision transfer on parent from the joints child. The maximum range is 0.0. |

## Angular Limits

![Angular Limits Properties](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bc092daf-2019-4f88-b830-9de32c9237d8/properties-angular-limits.png)

| Property | Description |
| --- | --- |
| **Swing 1Motion** | 
Indicates whether the Swing1 limit is used.

-   **Free**: No constraint around the axis.
-   **Limited**: Limited freedom around this axis. The limit for each Angular Motion is controlled individually by a correspondingly named Limit property:
    -   **Swing 1Limit Angle**
    -   **Swing 2Limit Angle**
    -   **Twist Limit Angle**
-   **Locked**: Full constraint around this axis.



 |
| **Swing 2Motion** | 

Indicates whether the Swing2 limit is used.

-   **Free**: No constraint around the axis.
-   **Limited**: Limited freedom around this axis. The limit for each Angular Motion is controlled individually by a correspondingly named Limit property:
    -   **Swing 1Limit Angle**
    -   **Swing 2Limit Angle**
    -   **Twist Limit Angle**
-   **Locked**: Full constraint around this axis.



 |
| **Twist Motion** | 

Indicates whether the Twist limit is used.

-   **Free**: No constraint around the axis.
-   **Limited**: Limited freedom around this axis. The limit for each Angular Motion is controlled individually by a correspondingly named Limit property:
    -   **Swing 1Limit Angle**
    -   **Swing 2Limit Angle**
    -   **Twist Limit Angle**
-   **Locked**: Full constraint around this axis.



 |
| **Swing 1Limit Angle** | Angle of movement along the **XY** Plane. |
| **Twist Limit Angle** | Angle of movement along the **XZ** Plane. |
| **Swing 2Limit Angle** | Symmetric angle of roll along the X-axis. |

### Advanced

![Advanced Angular Limits Properties](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/abdbf68b-a3ff-4d75-bd99-dfdb319900fa/properties-angular-limits-advanced.png)

| Property | Description |
| --- | --- |
| **Swing Limits** |   |
| **Soft Constraint** | Whether we want to use a soft constraint (spring). |
| **Stiffness** | Stiffness of the soft constraint. Only used when Soft Constraint is on. |
| **Damping** | Damping of the soft constraint. |
| **Restitution** | Controls the amount of bounce when the constraint is violated. |
| **Twist Limits** |   |
| **Soft Constraint** | Whether we want to use a soft constraint (spring). |
| **Stiffness** | Stiffness of the soft constraint. Only used when Soft Constraint is on. |
| **Damping** | Damping of the soft constraint. |
| **Restitution** | Controls the amount of bounce when the constraint is violated. |
| **Angular Breakable** | Whether it is possible to break the joint with angular force. |
| **Angular Break Threshold** | Torque needed to break the joint. |
| **Angular Placticity** | Whether it is possible to reset rotations from the angular displacement. |
| **Angular Placticity Threshold** | Degree threshold from target angle needed to reset the target angle. |

## Linear Motor

![Linear Motor Properties](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/69abff8d-79a7-48fd-9047-74275ea1676e/properties-linear-motor.png)

| Property | Description |
| --- | --- |
| **Position Target** | Enables the position linear motor on one or more axes and sets the local position desired. |
| **Strength** | How much force to apply to reach the desired position. |
| **Velocity Target** | Enables the velocity linear motor on one or more axes and sets the desired velocity. |
| **Strength** | How much force to apply to reach the desired velocity. |

### Advanced

![Advanced Constraint Motor Physics](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/57414376-d2a0-42e9-acae-4c3e7eed3851/physics-constraint-motor-advanced.png)

| Property | Description |
| --- | --- |
| **Max Force** | The force limit of the drive. |

## Angular Motor

![Angular Motor Properties](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f930780b-4134-47bd-bb0b-213fde5faac9/properties-angular-motor.png)

| Property | Description |
| --- | --- |
| **Angular Drive Mode** | 
Whether this angular motor uses SLERP (Spherical Linear Interpolation) or decomposes into a Swing Motor and a Twist Motor (cone and roll constraints). SLERP will not work if any of the angular constraints are locked.

-   **SLERP**: Sets the motor to SLERP (Spherical Linear Interpolation) mode. SLERP mode will not work if any of the axis of the angular constraint is locked.
-   **Twist and Swing**: Sets the motor to **Twist and Swing** (cone and roll constraints) mode.



 |
| **Target Orientation** | Target orientation relative to the body reference frame. |
| **Drives** | Depending on the Angular Drive Mode setting, you can enable or disable the different motors for that mode. |
| **Strength** | The force applied to reach the target orientation. |
| **Target Velocity** | Target angular velocity relative to the body reference frame |
| **Drives** | Depending on the Angular Drive Mode setting, you can enable or disable the different motors for that mode. |
| **Strength** | The force applied to reach the target velocity. |

### Advanced

![Advanced Constraint Motor Physics](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/544e1bb9-dafa-4e44-9d97-c8d54b92da13/physics-constraint-motor-advanced.png)

| Property | Description |
| --- | --- |
| **Max Force** | The force limit of the drive. |