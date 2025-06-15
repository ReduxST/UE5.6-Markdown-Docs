# Physics Field Reference Guide

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/reference-guide-for-physics-field-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/reference-guide-for-physics-field-in-unreal-engine)  
**Processed:** 2025-06-14 16:46:09

---

This page contains reference information for the **Physics Field System** in **Unreal Engine 5**.

A Chaos Particle refers to a point in space with various properties, such as position, velocity, and mass, that can be affected by the Chaos Physics Solver. These particles can also have additional properties like orientation, angular velocity, inertia, and geometry.

The Physics Field System comes with three main types of Fields.

## List of Field Types

| Field Type | Description |
| --- | --- |
| **Transient Field** | These fields are created, executed, and destroyed at runtime during a function or event call. Transient Fields are used to add a temporary effect to the physics simulation, such as applying external strain or linear velocity to rigid bodies that overlap the field volume. |
| **Construction Field** | These fields are created in the Construction Script of the Blueprint and store the field after each compilation. The most common example of a Construction Field is the Anchor Field, used to hold Geometry Collection fractured pieces in place. You can remove all the Construction Fields of a component with the **RemoveConstructionFields** node. |
| **Persistent Field** | These fields are created and remain active until they are explicitly removed. Persistent fields are evaluated at every tick of the physics simulation. A common example is the Disable Field, which can be used to disable the fractured pieces of Geometry Collections that overlap its volume. You can remove all the Persistent Fields of a component with the **RemovePersistentFields** node. |

Each Field type applies to a specific **Physics Type**, such as Linear Force, External Strain, or Disabled Threshold, to overlapping Chaos Particles. Each Physics Type is categorized by type as Integer, Scalar, or Vector.

## List of Field Physics Types

| Type | Physics Type | Description |
| --- | --- | --- |
| **Integer** | **Dynamic State** | Sets the state of a Chaos Particle to Static, Dynamic, Kinematic, or sleeping. |
|   | **Activate Disabled** | Activates all the disabled Chaos Particles for which the field value will be 0. |
|   | **Collision Group** | Sets the Chaos Particle Collision Group. |
| **Scalar** | **External Strain** | Applies an external strain over the Chaos Particles. If this external strain is bigger than the internal one, the Geometry Collection cluster will break. |
|   | **Internal Strain** | Adds an internal strain field to the Chaos Particles. |
|   | **Disabled Threshold** | Disables the Chaos Particles if the linear or angular velocity is less than the threshold specified. |
|   | **Sleeping Threshold** | Sets the Chaos Particles to sleep mode if the linear or angular velocity is less than the threshold specified. |
|   | **Kill Particles** | Disables the Chaos Particles whose field evaluation results in a value bigger than 0. These particles are disabled immediately. |
| **Vector** | **Linear Force** | Adds a vector field to the Chaos Particle's current linear force. |
|   | **Linear Velocity** | Adds a vector field to the Chaos Particle's current linear velocity. |
|   | **Angular Velocity** | Adds a vector field to the Chaos Particle's current angular velocity. |
|   | **Angular Torque** | Adds a vector field to the Chaos Particle's current angular torque. |

Fields can use different types of **Meta Data** to add additional information on how they should be evaluated.

## List of Meta Data available for Fields

| Type | Name | Description |
| --- | --- | --- |
| **State** | **Dynamic** | Filter for Chaos Particles that are moving based on the physics simulation. |
|   | **Kinematic** | Filter for Chaos Particles that are moving, but not driven by the physics simulation. A common example is moving a Chaos Particle via animation. |
|   | **Static** | Filter for Chaos Particles that are currently not moving and cannot receive forces from the physics simulation. |
|   | **Sleeping** | Filter for Chaos Particles that are currently Sleeping and waiting to be reactivated. |
|   | **Disabled** | Filter for Chaos Particles that are currently disabled. |
|   | **All** | Filter for all Chaos Particles in the Chaos Solver, regardless of state. |
| **Object** | **Rigid** | Apply the Field to all physics rigid objects. |
|   | **Cloth** | Apply the Field to all cloth objects. |
|   | **Destruction** | Apply the Field to all Geometry Collections. |
|   | **Character** | Apply the Field to all the Rigid Body Animation Nodes. |
|   | **All** | Apply the Field to all Chaos objects. |
| **Position** | **Center of Mass** | The Field will be evaluated at the center of mass of the rigid object. |
|   | **Pivot Point** | The Field will be evaluated at the pivot point of the rigid object. |
| **Resolution** | **Minimum** | Filter for Chaos Particles that are currently enabled. |
|   | **Parents** | Filter for all the top parents' clustered Chaos Particles. |
|   | **Maximum** | Filter for Chaos Particles that are enabled and disabled. |

Each Field is defined by a Blueprint graph that connects to the **Field Node** pin of the **Physics Field** node. The graph defines the scope and properties of the Field.

The Blueprint graph is composed of **Field Nodes**, which are added as child components of the Field system Component.

## List of Field Nodes

| Field Type | Name | Description |
| --- | --- | --- |
| **Integer** | **Uniform Integer** | Sets a uniform integer value independently of the sample position. The output is equal to the magnitude. |
|   | **Radial Int Mask** | If the sample distance from the field position is lesser or greater than the radius, set the interior or exterior value to an intermediate result. The final output value will be affected by the intermediate one based on the Mask Condition. |
| **Scalar** | **Uniform Scalar** | Sets a uniform scalar value independently of the sample position. The output is equal to the magnitude. |
|   | **Wave Scalar** | Sets a temporal wave scalar value according to the sample distance from the field position. |
|   | **Radial Falloff** | Sets the Field scalar value to decrease with the distance to the sphere's center position. |
|   | **Plane Falloff** | Sets the Field scalar value to decrease with the distance to the plane defined by the position/normal pair. |
|   | **Box Falloff** | Sets the Field scalar value to decrease with the distance from the box's center position. |
|   | **Noise Field** | Defines a perlin noise scalar value if the sample is within a box. |
| **Vector** | **Uniform Vector** | Sets a uniform vector value independently of the sample position. The output is equal to the magnitude \* direction. |
|   | **Radial Vector** | Sets a radial vector value with its direction being the normalized vector from the sample position to the field position. The output is equal to the magnitude \* direction. |
|   | **Random Vector** | Sets a random vector value independently of the sample position. The output is equal to the magnitude \* random direction. |
| **Operator** | **Operator Field** | Computes a mathematical operation between two specified fields. |
|   | **To Integer Field** | Converts a scalar field to an integer field. |
|   | **To Float Field** | Converts an integer field to a scalar field. |
|   | **Culling Field** | Evaluates the input field according to the result of the culling field. |