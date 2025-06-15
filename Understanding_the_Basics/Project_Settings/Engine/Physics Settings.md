# Physics Settings

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/physics-settings-in-the-unreal-engine-project-settings](https://dev.epicgames.com/documentation/en-us/unreal-engine/physics-settings-in-the-unreal-engine-project-settings)  
**Processed:** 2025-06-14 16:42:58

---

## Physics

### Replication

This is the error collection data for replicating simulated physics (rigid bodies).

| **Section** | **Description** |
| --- | --- |
| **Ping Extrapolation** | Value between 0 and 1, indicates how much velocity and ping based correction to use. |
| **Ping Limit** | For the purpose of extrapolation, ping will be clamped to this value. |
| **Error Per Linear Difference** | Error per centimeter. |
| **Error Per Angular Difference** | Error per degree. |
| **Max Restored State Error** | Maximum allowable error for a state to be considered "resolved". |
| **Max Linear Hard Snap Distance** | 
Max linear hard snap distance.

This value represents the maximum Euclidean linear distance that will be used to extrapolate the rigid body position. Any distance beyond this value will result in the rigid body "hard snapping" to the correct position.



 |
| **Position Lerp** | 

How much to directly lerp (linearly interpolate) to the correct position.

Generally this should be very low, if not 0.

A higher value will increase precision along with stuttering.



 |
| **Angle Lerp** | How much to directly lerp to the correct angle. |
| **Linear Velocity Coefficient** | This is the coefficient `k` in the differential equation: `dx/dt = k (x_target(t) - x(t))`, which is used to update the velocity in a replication step. |
| **Angular Velocity Coefficient** | This is the angular analog to `LinearVelocityCoefficient`. |
| **Error Accumulation Seconds** | Number of seconds to remain in a heuristically unresolvable state before hard snapping. |
| **Error Accumulation Distance Sq** | If the body has moved less than the square root of this amount towards a resolved state in the previous frame, then error may accumulate towards a hard snap. |
| **Error Accumulation Similarity** | If the previous error projected onto the current error is greater than this value (indicating "similarity" between states), then error may accumulate towards a hard snap. |

### Simulation

| **Section** | **Description** |
| --- | --- |
| **Default Degrees of Freedom** | 
Useful for constraining all objects in the world, for example if you are making a 2D game using 3D environments.

You can choose from the following options:

-   **Full 3D**
-   **YZ Plane**
-   **XZ Plane**
-   **XY Plane**



 |
| **Disable CCD** | 

If enabled, CCD (Continuous Collision Detection) will be ignored.

This is an optimization when CCD is never used, which improves performance.



 |
| **Simulate Anim Physics After Reset** | Defines whether to simulate anim physics nodes in the tick where they're reset. |
| **Enable 2DPhysics** | Defines whether 2D physics can be used (Box2d). |
| **Bounce Threshold Velocity** | 

Minimum relative velocity required for an object to bounce.

A typical value for simulation stability is about `0.2 * gravity`.



 |
| **Friction Combine Mode** | 

Controls how friction is computed for multiple materials.

You can choose from the following options:

-   **Average**
-   **Min**
-   **Multiply**
-   **Max**



 |
| **Restitution Combine Mode** | 

Restitution combine mode. Controls how restitution is computed for multiple materials.

You can choose from the following options:

-   **Average**
-   **Min**
-   **Multiply**
-   **Max**



 |
| **Max Angular Velocity** | Maximum angular velocity that a simulated object can achieve. |
| **Max Depenetration Velocity** | 

Maximum velocity which may be used to depenetrate simulated physics objects.

This is the maximum velocity at which the Chaos physics system will correct object penetration (overlap) when a collision is detected: if a collision is detected and there is overlap, Chaos will correct the colliding object's position to be outside the object it collided with.

A value of 0 means there is no set maximum.

Large penetrations can result in instability due to the size of the force that needs to be applied to correct object penetration. Setting the **Maximum Depenetration Velocity** to a value different than 0 means the velocity will never exceed this number, which results in more stability at the cost of objects still penetrating.



 |
| **Contact Offset Multiplier** | 

When creating a physics shape, the engine looks at its bounding volume and multiplies its minimum value by this multiplier.

A bigger number will generate contact points earlier, which results in higher stability at the cost of performance.



 |
| **Min Contact Offset** | Minimum contact offset. |
| **Max Contact Offset** | Maximum contact offset. |
| **Simulate Skeletal Mesh on Dedicated Server** | 

If enabled, simulate physics for this component on a dedicated server.

This should be set if simulating physics and replicating with a dedicated server.



 |
| **Default Shape Complexity** | 

Determines the default physics shape complexity.

You can choose from the following options:

-   **Project Default**
-   **Simple And Complex**
-   **Use Simple Collision As Complex**
-   **Use Complex Collision As Simple**



 |
| **Enable Shape Sharing** | Enables shape sharing between sync and async scenes for static rigid Actors. |
| **Enable PCM** | 

Enables persistent contact manifolds.

This will generate fewer contact points, but with more accuracy.

Reduces stability of stacking, but can help energy conservation.



 |
| **Enable Stabilization** | 

Enables stabilization of contacts for slow moving bodies.

This will help improve the stability of stacking.



 |
| **Warn Missing Locks** | 

Defines whether to warn when physics locks are used incorrectly.

Disabling this is not recommended and should only be done by very advanced users.



 |

### Optimization

| **Section** | **Description** |
| --- | --- |
| **Suppress Face Remap Table** | 
If enabled, the internal PhysX face to Unreal Engine face mapping will not be generated.

This is a memory optimization, available if you do not rely on face indices returned by scene queries.



 |
| **Support UV from Hit Results** | If enabled, store extra information to allow `FindCollisionUV` to derive UV from a line trace hit result, using the `FindCollisionUV` utility. |
| **Disable Active Actors** | 

If enabled, PhysX will not update Unreal Engine with any bodies that have moved during the simulation.

This should only be used if you have no PhysX simulation or you are manually updating the Unreal Engine data via polling PhysX.



 |
| **Disable Kinematic Static Pairs** | 

Defines whether to disable generating KS pairs.

Enabling this makes switching between dynamic and static slower for Actors, but speeds up contact generation by early rejecting these pairs.



 |
| **Disable Kinematic Kinematic Pairs** | 

Defines whether to disable generating KK pairs.

Enabling this speeds up contact generation. This is required when using APEX destruction.



 |

### Framerate

| **Section** | **Description** |
| --- | --- |
| **Anim Physics Min Delta Time** | Minimum delta time below which anim dynamics and rigidbody nodes will not simulate. |
| **Min Physics Delta Time** | The physics simulation will not run if the delta time is below this value. |
| **Max Physics Delta Time** | 
This is the maximum time step that a simulation can take.

If this is smaller than the tick of the engine, physics will move artificially slow in order to increase stability.



 |
| **Substepping** | 

Defines whether to substep the physics simulation.

This feature is still experimental. Certain functionality might not work correctly.



 |
| **Substepping Async** | 

Defines whether to substep the async physics simulation.

This feature is still experimental. Certain functionality might not work correctly.



 |
| **Tick Physics Async** | 

Defines whether to tick physics simulation on an async thread.

This feature is still experimental. Certain functionality might not work correctly.



 |
| **Async Fixed Time Step Size** | 

If using async, the time step size to tick at.

This feature is still experimental. Certain functionality might not work correctly.



 |
| **Max Substep Delta Time** | Maximum delta time (in seconds) for an individual simulation substep. |
| **Max Substeps** | Maximum number of substeps for physics simulation. |
| **Sync Scene Smoothing Factor** | Physics delta time smoothing factor for sync scene. |
| **Initial Average Frame Rate** | Physics delta time initial average. |

### Chaos Physics

| **Section** | **Description** |
| --- | --- |
| **Min Delta Velocity for Hit Events** | Minimum velocity delta required on a colliding object for Chaos to send a hit event. |
| **Default Threading Model** | 
Default threading model to use on module initialization.

Can be switched at runtime using `p.Chaos.ThreadingModel`.

You can choose from the following options:

-   **Task Graph**
-   **Single Thread**



 |
| **Dedicated Thread Tick Mode** | 

The framerate / timestep ticking mode when running with a dedicated thread.

You can choose from the following options:

-   **Fixed**
-   **Variable**
-   **Variable Capped**
-   **Variable Capped with Target**



 |
| **Dedicated Thread Buffer Mode** | 

The buffering mode to use when running with a dedicated thread.

You can choose from the following options:

-   **Double**
-   **Triple**



 |
| **Iterations** | The number of iterations to run during the constraint solver step. |
| **Collisions Pair Iterations** | 

During solver iterations, Unreal Engine solves each constraint in turn.

For each constraint, the engine runs the solve step `CollisionPairIterations` times in a row.



 |
| **Push Out Iterations** | 

The number of iterations to run during the constraint fixup step.

This applies a post-solve correction that can address errors left behind during the main solver iterations.



 |
| **Collision Push Out Pair Iterations** | 

During pushout iterations, Unreal Engine pushes out each constraint in turn.

For each constraint, the engine runs the pushout step `CollisionPairIterations` times in a row.



 |
| **Collision Margin Fraction** | 

A collision margin as a fraction of size used by some boxes and convex shapes to improve collision detection results.

The core geometry of shapes that support a margin are reduced in size by the margin, and the margin is added back on during collision detection.

The net result is a shape of the same size, but with rounded corners.



 |
| **Collision Margin Max** | 

An upper limit on the collision margin that will be subtracted from boxes and convex shapes.

See `CollisionMarginFraction`.



 |
| **Collision Cull Distance** | During collision detection, if two shapes are at least this far apart, Unreal Engine does not calculate their nearest features during the collision detection step. |
| **Collision Max Push Out Velocity** | 

The maximum speed at which two bodies can be extracted from each other when they start a frame inter-penetrating.

This can happen because they spawned on top of each other, or the solver failed to fully resolve collisions last frame.

A value of zero means "no limit".

A non-zero value can be used to prevent explosive behavior when bodies start penetrating deeply.

An alternative to using this approach is to increase the number of Velocity Iterations, which is more expensive, but will ensure the bodies are depenetrated (have their penetration reduced / removed) in a single frame without explosive behavior.



 |
| **Joint Pair Iterations** | The number of iterations to run on each constraint during the constraint solver step. |
| **Joint Push Out Pair Iterations** | 

The number of iterations to run during the constraint fixup step for each joint.

This applies a post-solve correction that can address errors left behind during the main solver iterations.



 |
| **Cluster Connection Factor** | Cluster connection factor. |
| **Cluster Union Connection Type** | 

Cluster union connection type.

You can choose from the following options:

-   **Point Implicit**
-   **Delaunay Triangulation**
-   **Minimal Spanning Subset Delaunay Triangulation**
-   **Point Implicit Augmented with Minimal Delaunay**
-   **None**



 |
| **Generate Collision Data** | Defines whether to generate collision data. |
| **Collision Filter Enabled** | Defines whether to enable the collision filter. |
| **Min Mass Threshold** | The minimum mass threshold for the results (compared with min of particle 1 mass and particle 2 mass). |
| **Min Speed Threshold** | The minimum velocity threshold for the results (compared with min of particle 1 speed and particle 2 speed). |
| **Min Impulse Threshold** | The minimum impulse threshold for the results. |
| **Generate Break Data** | Defines whether to generate break data. |
| **Breaking Filter Enabled** | Defines whether the breaking filter should be enabled. |
| **Min Mass Threshold** | The minimum mass threshold for the results (compared with min of particle 1 mass and particle 2 mass). |
| **Min Speed Threshold** | The minimum velocity threshold for the results (compared with min of particle 1 speed and particle 2 speed). |
| **Min Volume Threshold** | Minimum volume. |
| **Generate Trailing Data** | Defines whether to generate trailing data. |
| **Trailing Filter Enabled** | Defines whether the trailing filter should be enabled. |
| **Generate Contact Graph** | Defines whether to generate the contact graph. |

### Constants

| **Section** | **Description** |
| --- | --- |
| **Default Gravity Z** | Default gravity. |
| **Default Terminal Velocity** | Default terminal velocity for Physics Volumes. |
| **Default Fluid Friction** | Default fluid friction for Physics Volumes. |
| **Simulate Scratch Memory Size** | Amount of memory to reserve for PhysX simulate(), this is per pxscene and will be rounded up to the next 16K boundary. |
| **Ragdoll Aggregate Threshold** | Threshold for ragdoll bodies, above which they will be added to an aggregate before being added to the scene. |
| **Triangle Mesh Triangle Min Area Threshold** | 
Triangles from triangle meshes (BSP) with an area less than or equal to this value will be removed from physics collision data.

Set this option to less than 0 to disable it.



 |

### Physical Surface

| **Section** | **Description** |
| --- | --- |
| **Physical Surface** | 
You can have up to 62 custom physical surface types for your project.

Once you name each type, they will show up as a surface type in the physical material.



 |