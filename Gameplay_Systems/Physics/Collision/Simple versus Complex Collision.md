# Simple versus Complex Collision

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/simple-versus-complex-collision-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/simple-versus-complex-collision-in-unreal-engine)  
**Processed:** 2025-06-14 16:50:31

---

In Unreal Engine, you have access to simple and complex collision shapes. **Simple Collision** are primitives like cubes, spheres, capsules, and convex hulls. **Complex Collision** is the trimesh of a given object. By default, Unreal Engine creates both simple and complex shapes, then, based on what the user wants (complex query versus simple query), the physics solver will use the corresponding shape for scene queries and collision tests.

## Usage

In the Static Mesh Editor's **Details** panel, you can find the settings for **Collision Complexity** in the **Collision** category.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cdf8c69e-0f99-4633-a52f-24c83304fe9f/staticmeshsettingscollisioncomplexity.png)

| **Setting** | **Description** |
| --- | --- |
| **Project Default** | Using the project's physics seetings, this will cause simple collision requests to use simple collision, and complex requests to use complex collision; the "default" behavior. |
| **Simple And Complex** | This flag enables the creation of simple and complex shapes, using simple shapes for regular scene queries and collision tests, and using complex (per poly) shapes for complex scene queries. |
| **Use Simple Collision As Complex** | This means that if a complex query is requested, the engine will still query against simple shapes; basically ignoring the trimesh. This helps save memory since we don't need to bake the trimesh and can improve performance if the collision geometry is simpler. |
| **Use Complex Collision As Simple** | This means that if a simple query is requested, the engine will query against complex shapes; basically ignoring the simple collision. This allows us to use the trimesh for the physics simulation collision. Note that if you are using **UseComplexAsSimple** you cannot simulate the object, but you can use it to collide with other simulated (simple) objects. |

For example, in the image below the chair on the left has simple collision, and when the Pawn above it falls onto it, it will slide off the large angled surface that covers the seat. However; the chair on the right is using **Use Complex Collision As Simple**, and when the Pawn above it falls, it will land on the seat of the chair and stay there.