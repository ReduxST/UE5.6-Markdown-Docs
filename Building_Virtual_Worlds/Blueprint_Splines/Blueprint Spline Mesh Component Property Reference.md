# Blueprint Spline Mesh Component Property Reference

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/blueprint-spline-mesh-component-property-reference-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/blueprint-spline-mesh-component-property-reference-in-unreal-engine)  
**Processed:** 2025-06-14 16:10:49

---

This page contains a reference listing of properties available on **Blueprint Spline Mesh Components**. The properties displayed will be slightly different if the **Blueprint Spline Mesh Component** is selected in the **Blueprint Editor**, is a **Root Component**, or if the component is selected in the **Level Editor**.

## Properties

### Transform

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/31033c13-aa50-4b33-a515-9f0017a1d528/transformcatref.png)

| Property | Description |
| --- | --- |
| **Location** | The location of the **Actor** or **Component** in **World Space** or **Relative** to its parent. |
| **Rotation** | The rotation of the **Actor** or **Component** in **World Space** or **Relative** to its parent. |
| **Scale** | The Scale of the **Actor** or **Component** in **World Space** or **Relative** to its parent. |

### Sockets

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6f7368ed-87f9-4f85-bc6d-5a23af8c0a44/socketscatref.png)

| Property | Description |
| --- | --- |
| **Parent Socket** | When this component is the **Child** of a **Skeletal Mesh Component** (or **Static Mesh Component** with a **Socket**), you can specify a **Socket** or **Joint** to attach this component to. |

### Static Mesh

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3b7dae64-a395-44a5-820d-113840503093/staticmeshcatref.png)

| Property | Description |
| --- | --- |
| **Static Mesh** | Specifies the **Static Mesh** to render for this component. |

### Materials

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3e8d8e16-3929-42b3-81ba-9d2996dda2ec/materialscatref.png)

| Property | Description |
| --- | --- |
| **Element #** | Once a **Static Mesh** has been specified in the **Static Mesh Property**, a number of additional **Material Properties** will appear. These will be named based on the **Material IDs** applied to the **Static Mesh**. |

### Spline Mesh

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/207bf603-6376-4473-b7af-a29d7eb9238e/splinemeshcat.png)

| Property | Description |
| --- | --- |
| **Start Pos** | Start location of spline, in component space. |
| **Start Tangent** | Start tangent of spline, in component space. |
| **End Pos** | End location of spline, in component space. |
| **End Tangent** | End tangent of spline, in component space. |
| **Spline Up Dir** | Axis (in component space) that is used to determine X axis for co-ordinates along spline |
| **Forward Axis** | Chooses the forward axis for the spline mesh orientation |

#### Advanced

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/70e872b4-fe3d-4cdd-b19b-f530e9610587/splinemeshcatadv.png)

| Property | Description |
| --- | --- |
| **Start Scale** | X and Y scale applied to mesh at start of spline. |
| **Start Roll** | Roll around spline applied at start, in radians. |
| **Start Offset** | Starting offset of the mesh from the spline, in component space. |
| **End Scale** | X and Y scale applied to mesh at end of spline. |
| **End Roll** | Roll around spline applied at end, in radians. |
| **End Offset** | Ending offset of the mesh from the spline, in component space. |
| **Smooth Interp Roll Scale** | If true, will use smooth interpolation (ease in/out) for Scale, Roll, and Offset along this section of spline. |
| **Spline Boundary Min** | Minimum coordinate along the spline forward axis which corresponds to start of spline. |
| **Spline Boundary Max** | Maximum coordinate along the spline forward axis which corresponds to end of spline. |

### Spline

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e08239f2-9897-423c-8c35-fef1fe07be9a/bpsm_splinecatref.png)

| Property | Description |
| --- | --- |
| **Allow Spline Editing Per Instance** | If true, spline mesh properties - StartPos, EndPos, StartTangent and EndTangent- may be edited per instance in the level viewport. |

### Physics

## Physics

![Physics body details panel showing the physics properties](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ac0d8798-d77f-4aae-b12d-2957f7e31685/details-physics.png)

| Property | Description |
| --- | --- |
| **Double Sided Geometry** | If enabled, the physics triangle mesh will use double-sided faces when doing scene queries. This is useful for planes and single-sided meshes that need traces to work on both sides. |
| **Simple Collision Physical Material** | Physical material to use for simple collision on this body. Encodes information about density, friction, and so on. |
| **Physics Type** | 
-   Simulated: Object will use physics simulation.
-   Kinematic: Object will not be affected by physics, but can interact with physically simulated bodies.
-   Default: Object will inherit from OwnerComponent's behavior.



 |
| **Mass in KG** | Mass of the body in KG. |
| **Linear Damping** | 'Drag' force added to reduce linear movement. |
| **Angular Damping** | 'Drag' force added to reduce angular movement. |
| **Enable Gravity** | If the object should have the force of gravity applied. |

### Advanced

![Physics body details panel showing the advanced physics properties](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bec3129f-9e57-49af-b363-4c6fce31e1bf/details-physics-advanced.png)

| Property | Description |
| --- | --- |
| **Start Awake** | If the object should start awake, or if it should initially be sleeping. |
| **Center Of Mass Offset** | User specified offset for the center of mass of this object, from the calculated location. |
| **Mass Scale** | Per-instance scaling of mass. |
| **Max Angular Velocity** | The maximum angular velocity for this instance. |
| **Sleep Family** | The set of values used in considering when to put this body to sleep. Normal, Sensitive, Custom. |
| **Inertia Tensor Scale** | Per-instance scaling of inertia (larger values mean more difficulty rotating) |
| **Walkable Slope Override** | Custom walkable slope setting for this body. See the **[Walkable Slope](/documentation/en-us/unreal-engine/walkable-slope-in-unreal-engine)** documentation for usage information. |
| **Walkable Slope Behavior** | Behavior of this surface (whether we affect the walkable slope). |
| **Walkable Slope Angle** | Override a walkable slope, applying the rules of the Walkable Slope Behavior. |
| **Custom Sleep Threshold Multiplier** | If the Sleep Family is set to **Custom**, multiply the natural sleep threshold by this amount. A higher number will cause the body to sleep sooner. |
| **Stabilization Threshold Multiplier** | The stabilization factor for this body if Physics stabilization is enabled. A higher number will cause more aggressive stabilization at the risk of loss of momentum at low speeds. A value of 0 will disable stabilization for this body. |
| **Update Mass when Scale Changes** | If true, it will update the mass when the scale changes. |
| **Generate Wake Events** | Determines whether 'wake/sleep' events should fire when this object is woken up or put to sleep by the physics simulation. |

### Collision

## Collision

![Physics body details panel showing the collision properties](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d275f64c-b050-46ee-92c0-ae938a5224af/details-collision.png)

| Property | Description |
| --- | --- |
| **Never Needs Cooked Collision Data** | To do chaos this is to opt out of CreatePhysicsMeshes for certain meshes. Better a long term mesh is not to call CreatePhysicsMesh until is known there is a mesh instance that needs it. |
| **Collision Complexity** | Collision Trace behavior - by default, it will keep simple (convex) and complex (per-poly) separate. |
| **Collision Responses** | See the [Collision Response Reference](/documentation/en-us/unreal-engine/collision-response-reference-in-unreal-engine) documentation for more information. |
| **Simulation Generates Hit Events** | Should 'Hit' events fire when this object collides during physics simulation. |
| **Phys Material Override** | Allows you to override the PhysicalMaterial to use for simple collision on this body. |

### Advanced

![Physics body details panel showing the advanced collision properties](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/adcbb369-133f-4734-9777-1cd44b9b62d8/details-collision-advanced.png)

| Property | Description |
| --- | --- |
| **Use CCD** | If true Continuous Collision Detection (CCD) will be used for this component |
| **Ignore Analytic Collisions** | If true, ignore analytic collisions and treat objects as a general implicit surface. |
| **Smooth Edge Collisions** | Remove unnecessary edge collisions to allow smooth sliding over surfaces composed of multiple actors/components. |

### Lighting

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a09a88bc-8768-4718-a62f-9e697009b749/lightingcatref.png)

| Property | Description |
| --- | --- |
| **Cast Shadow** | is true. |

#### Advanced

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4554f300-da59-4bfc-a5e1-c4a7bcbae136/lightingcatrefadv.png)

| Property | Description |
| --- | --- |
| **Affect Dynamic Indirect Lighting** | Controls whether the primitive should influence indirect lighting. |
| **Affect Distance Field Lighting** | Controls whether the primitive should affect dynamic distance field lighting methods. |
| **Cast Dynamic Shadow** | Controls whether the primitive should cast shadows in the case of non precomputed shadowing. |
| **Cast Static Shadow** | Whether the object should cast a static shadow from shadow casting lights. |
| **Cast Volumetric Translucent Shadow** | Whether the object should cast a volumetric translucent shadow. |
| **Self Shadow Only** | When enabled, the component will only cast a shadow on itself and not other components in the world. |
| **Cast Far Shadow** | When enabled, the component will be rendering into the far shadow cascades (only for directional lights). |
| **Cast Inset Shadow** | Whether this component should create a per-object shadow that gives higher effective shadow resolution. |
| **Cast Cinematic Shadow** | Whether this component should cast shadows from lights that have bCastShadowsFromCinematicObjectsOnly enabled. |
| **Cast Hidden Shadow** | If true, the primitive will cast shadows even if bHidden is true. |
| **Cast Shadow as Two Sided** | Whether this primitive should cast dynamic shadows as if it were a two sided material. |
| **Light as if Static** |   |
| **Light Attachments as Group** | set in a parent. |
| **Indirect Lighting Cache Quality** | Quality of indirect lighting for Movable primitives. |
| **Single Sample Shadow From Stationary Lights** | Whether the whole component should be shadowed as one from stationary lights, which makes shadow receiving much cheaper. |
| **Lighting Channels** | Channels that this component should be in. |

### Rendering

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/71158519-79a8-430f-bb64-2405cd479d3b/renderingcatref.png)

| Property | Description |
| --- | --- |
| **Visible** | . |
| **Hidden in Game** | Whether to hide the primitive in game, if the primitive is Visible. |

#### Advanced

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f21616b0-2c0d-43ca-b948-bc4ed95aae67/renderingcatrefadv.png)

| Property | Description |
| --- | --- |
| **Texture Streaming** | 
-   **Force Mip Streaming**: If true, forces mips for textures used by this component to be resident when this component's level is loaded.



 |
| **LOD** | 

-   **Min Draw Distance**: The minimum distance at which the primitive should be rendered, measured in world space units from the center of the primitive's bounding sphere to the camera position.
-   **Desired Max Draw Distance**: Max draw distance exposed to LDs.
-   **Current Max Draw Distance**: The distance to cull this primitive at.
-   **Allow Cull Distance Volume**: Whether to accept cull distance volumes to modify cached cull distance.
-   **Detail Mode**: If detail mode is >= system detail mode, primitive won't be rendered.



 |
| **Render In Main Pass** | If true, this component will be rendered in the main pass (z prepass, basepass, transparency) |
| **Receives Decals** | Whether the primitive receives decals. |
| **Owner No See** | If this is True, this component won't be visible when the view actor is the component's owner, directly or indirectly. |
| **Only Owner See** | If this is True, this component will only be visible when the view actor is the component's owner, directly or indirectly. |
| **Treat As Background for Occlusion** | Treat this primitive as part of the background for occlusion purposes. |
| **Use As Occluder** | Whether to render the primitive in the depth only pass. |
| **Render CustomDepth Pass** | If true, this component will be rendered in the CustomDepth pass (usually used for outlines) |
| **CustomDepth Stencil Value** | Optionally write this 0-255 value to the stencil buffer in CustomDepth pass (Requires project setting or r.CustomDepth == 3) |
| **Translucency Sort Priority** | Translucent objects with a lower sort priority draw behind objects with a higher priority. Translucent objects with the same priority are rendered from back-to-front based on their bounds origin. |
| **Lpv Bias Multiplier** |   |
| **Bounds Scale** | Scales the bounds of the object. |
| **Use Attach Parent Bound** | If true, this component uses its parents bounds when attached. |

### Tags

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f7177b87-9f16-4186-b105-f7b6467f88a2/tagscatref.png)

| Property | Description |
| --- | --- |
| **Component Tags** | Array of tags that can be used for grouping and categorizing. Can also be accessed from scripting. |

### Activation

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a012fcb1-0f6e-4a11-aed0-78ad349ea69f/activationcatref.png)

| Property | Description |
| --- | --- |
| **Auto Activate** | Whether the component is activated at creation or must be explicitly activated. |

### Events

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3f05b0aa-e9c9-43b9-aa2a-92b12e15a45e/eventscatref.png)

| Property | Description |
| --- | --- |
| **On Component Hit** | Event called when a component hits (or is hit by) something solid. |
| **On Component Begin Overlap** | Event called when something starts to overlaps this component, for example a player walking into a trigger. |
| **On Component End Overlap** | Event called when something stops overlapping this component |
| **On Component Wake** | Event called when the underlying physics objects is woken up |
| **On Component Sleep** | Event called when the underlying physics objects is put to sleep |
| **On Begin Cursor Over** | Event called when the mouse cursor is moved over this component and mouse over events are enabled in the player controller |
| **On End Cursor Over** | Event called when the mouse cursor is moved off this component and mouse over events are enabled in the player controller |
| **On Clicked** | Event called when the left mouse button is clicked while the mouse is over this component and click events are enabled in the player controller |
| **On Released** | Event called when the left mouse button is released while the mouse is over this component click events are enabled in the player controller |
| **On Input Touch Begin** | Event called when a touch input is received over this component when touch events are enabled in the player controller |
| **On Input Touch End** | Event called when a touch input is released over this component when touch events are enabled in the player controller |
| **On Input Touch Enter** | Event called when a finger is moved over this component when touch over events are enabled in the player controller |
| **On Input Touch Leave** | Event called when a finger is moved off this component when touch over events are enabled in the player controller |
| **Physics Volume Changed** | Delegate that will be called when PhysicsVolume has been changed. |

### Mobile

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/769da0c3-3641-43a7-b43b-02240f16a75a/mobilecatref.png)

| Property | Description |
| --- | --- |
| **Receive Combined Static and CSM Shadows from Stationary Lights** |   |