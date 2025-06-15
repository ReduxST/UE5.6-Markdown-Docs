# Movement Components

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/movement-components-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/movement-components-in-unreal-engine)  
**Processed:** 2025-06-14 16:37:05

---

**Movement Components** provide a form a movement to the Actor (or Character) that they are a sub-object of.

## Character Movement Component

The **CharacterMovementComponent** allows avatars not using rigid body physics to move by walking, running, jumping, flying, falling, and swimming. It is specific to **Characters** and cannot be implemented by any other class. It is automatically added when creating **Blueprints** based on the Character class and not manually added.

Properties that can be set include values for falling and walking friction, speeds for travel through air and water and across land, buoyancy, gravity scale, and the physics forces the Character can exert on Physics objects. The CharacterMovementComponent also includes root motion parameters that come from the animation and are already transformed in world space, ready for use by physics. See [Root Motion](/documentation/en-us/unreal-engine/root-motion-in-unreal-engine) for more information.

For information on working with Character Movement, see [Setting Up Character Movement](/documentation/en-us/unreal-engine/setting-up-character-movement).

## Projectile Movement Component

A **ProjectileMovementComponent** updates the position of another Component during its tick. Behavior such as bouncing after impacts and homing toward a target are supported by this type of Component. Normally the root Component of the owing Actor is moved, however another Component may be selected (see [SetUpdatedComponent](/documentation/en-us/unreal-engine/API/Runtime/Engine/GameFramework/UMovementComponent/SetUpdatedComponent)). If the Updated Component is simulating physics, only the initial launch parameters (when initial velocity is non-zero) will affect the projectile, and the physics simulation will take over from there.

An example of a Blueprint using a ProjectileMovementComponent is shown below (click for full sized image).

## Rotating Movement Component

The **RotatingMovementComponent** performs continuous rotation of a Component at a specific rotation rate. Rotation can optionally be offset around a pivot point. Important to note, collision testing is not performed during movement.

An example of using a RotatingMovementComponent might be in the form of an airplane's propellers, or a windmill, or even a series of planets revolving around the sun.