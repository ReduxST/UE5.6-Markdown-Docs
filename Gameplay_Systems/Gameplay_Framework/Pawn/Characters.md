# Characters

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/characters-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/characters-in-unreal-engine)  
**Processed:** 2025-06-14 16:12:51

---

With the addition of a `CharacterMovementComponent`, a `CapsuleComponent`, and a `SkeletalMeshComponent`, the [Pawn](/documentation/en-us/unreal-engine/controllers-in-unreal-engine) class is extended into the highly-featured **Character** class. A Character is designed for a vertically-oriented player representation that can walk, run, jump, fly, and swim through the world. This class also contains implementations of basic networking and input models.

### SkeletalMeshComponent

Unlike Pawns, Characters come with a `SkeletalMeshComponent` to enable advanced animations that use a skeleton. It is possible for other Skeletal Meshes to be added to Character-derived classes, but this is the main Skeletal Mesh associated with the Character. For more on Skeletal Meshes, refer to [Skeletal Mesh Actors](/documentation/en-us/unreal-engine/skeletal-mesh-actors-in-unreal-engine) and [Skeletal Mesh Animation System](/documentation/en-us/unreal-engine/skeletal-mesh-animation-system-in-unreal-engine)

### CapsuleComponent

The `CapsuleComponent` is used for movement collision. In order to calculate complicated geometries for the `CharacterMovementComponent`, there is an assumption that the collision component in the Character class is a vertically-oriented capsule. Refer to [Collision](/documentation/en-us/unreal-engine/collision-in-unreal-engine) and [Setting Up Collisions With Static Meshes](/documentation/en-us/unreal-engine/setting-up-collisions-with-static-meshes-in-unreal-engine)

### CharacterMovementComponent

The `CharacterMovementComponent` allows avatars not using rigid body physics to move by walking, running, jumping, flying, falling, and swimming. It is specific to Characters, and cannot be implemented by any other class. Properties that can be set in the `CharacterMovementComponent` include values for falling and walking friction, speeds for travel through air and water and across land, buoyancy, gravity scale, and the physics forces the Character can exert on Physics objects. The `CharacterMovementComponent` also includes root motion parameters that come from the animation and are already transformed in world space, ready for use by physics.