# Enabling Physics Simulation on Grooms

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/enabling-physics-simulation-on-grooms-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/enabling-physics-simulation-on-grooms-in-unreal-engine)  
**Processed:** 2025-06-14 16:22:03

---

You can set up physics simulations for your grooms by enabling settings within the [Groom Asset Editor](/documentation/en-us/unreal-engine/groom-asset-editor-user-guide-in-unreal-engine) and the Groom component.

## Enabling Physics Simulation on a Groom

To enable Physics simulation for a groom go to the **Groom Asset Editor > Physics** panel. Enable the checkbox for **Enable Simulation**.

![Enable Physics Simulation setting in the Groom Asset Editor.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f67a8367-cbbc-4bbe-bfaf-a49226c0fc4c/groom-enable-physics-setting.png)

Once enabled, the groom should now simulate physics. Below is an example of the groom simulation while a character is walking.

## Physics Simulation Properties

You can find the simulation properties for grooms in the Groom Asset Editor and on a Groom component.

### Groom Asset Editor Simulation Properties

The following simulation settings are found in the Groom Asset Editor under the **Physics** and **LOD** panels.

#### Physics Panel Settings

The following settings are found in the **Physics** panel:

![Groom Asset Editor Physics Properties](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b5d611e4-2004-4de8-8601-e78709aca01b/groom-asset-editor-physics-properties.png)

| Property | Description |
| --- | --- |
| Solver Settings |   |
| **Enable Simulation** | Enables physics simulation for this groom grouping. |
| **Niagara Solver** | 
Select the solver to be used for simulation:

-   **Groom Rods:**
-   **Groom Springs:**
-   **Custom Solver:**



 |
| **Custom System** | Add a custom Niagara system to use when the property Niagara Solver is set to Custom Solver. |
| **Sub Steps** | The number of sub steps to be done per frame. Solver calls are done at 24 frames per second. |
| **Iteration Count** | The number of iterations to solve constraints with the XPBD solver. |
| External Forces |   |
| **Gravity Vector** | The acceleration vector measured in cm/s2 to be used for gravity. |
| **Air Drag** | The coefficient between 0 and 1 to be used for air drag. |
| **Air Velocity** | The velocity of the surrounding air measured in cm/s. |
| Bend Constraint |   |
| **Solve Bend** | Enables solving of the bend constraint during the XPBD loop. |
| **Project Bend** | Enables the projection of the bend constraint after the XPBD loop. |
| **Bend Damping** | Damping applied for the bend constraint using a value between 0 and 1. |
| **Bend Stiffness** | The stiffness for the bend constraint in GPa. |
| **Bend Stiffness Scale** | This curve determines how much the bend stiffness is scaled along each strand. The x-axis range is 0,1, where 0 maps to the root and 1 to the tip of the strand. |
| Stretch Constraint |   |
| **Solve Stretch** | Enables solving of the stretch constraint during the XPBD loop. |
| **Project Stretch** | Enables the projection of the stretch constraint after the XPBD loop. |
| **Stretch Damping** | The damping for the stretch constraint using a value between 0 and 1. |
| **Stretch Stiffness** | The stiffness for the stretch constraint in GPa. |
| **Stretch Stiffness Scale** | This curve determines how much the stretch stiffness is scaled along each strand. The X-axis range is 0,1, where 0 maps to the root and 1 to the tip of the strand. |
| Collision Constraint |   |
| **Solve Collision** | Enables solving of the collision constraint during the XPBD loop. |
| **Project Collision** | Enables the projection of the collision constraint after the XPBD loop. |
| **Static Friction** | The static function used for collision against physics assets. |
| **Kinetic Friction** | The kinetic friction used for collision against physics assets. |
| **Strand Viscosity** | The viscosity between 0 and 1 that is used for self-collision. |
| **Grid Dimension** | The dimension of the grid used to compute the viscosity force. |
| **Collision Radius** | The radius to be used for collision detection against physics assets. |
| **Radius Scale** | This curve determines how much the collision radius is scaled along each strand. The X-axis range is 0,1, where 0 maps to the root and 1 to the tip of the strand. |
| Strand Parameters |   |
| **Strands Size** | The number of particles per guide that are used for simulation. |
| **Strands Density** | The density of strands measured in g/cm3. |
| **Strands Smoothing** | The smoothing between 0 and 1 for the incoming guide curves that leads to better stability. |
| **Strands Thickness** | The strands thickness in centimeters that are used for mass and inertia computation. |
| **Thickness Scale** | This curve determines how much the strands thickness is scaled along each strand. The X-axis range is 0,1, where 0 maps to the root and 1 to the tip of the strand. |

#### LOD Panel Properties

The following settings are found in the **LOD** panel:

| Property | Description |
| --- | --- |
| **Simulation** | 
Overrides the simulation used to represent this level of detail. Choose between the following:

-   **Auto:** Uses the global value.
-   **Enable:** Forcibly enables the simulation for this LOD.
-   **Disable:** Forcibly disables the simulation for this LOD.



 |

### Groom Component Properties

The following properties are available on a Groom component to override simulation settings set in the Groom Asset Editor.

Before a groom simulation can be overridden with a Groom component, the groom asset must first have **Enable Simulation** enabled in the Groom Asset Editor.

![Groom Component Properties](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c7f6ecee-2554-4b02-995d-6c5f990aaf5b/groom-component-properties.png)

| Property | Description |
| --- | --- |
| **Physics Asset** | The physics asset to be used for hair simulation. |
| Simulation Settings |   |
| **Override Settings** | Makes this component's settings override the groom asset physics settings. |
| Simulation Setup |   |
| **Reset Simulation** | Make this simulation reset at some point in time. |
| **Debug Simulation** | Makes the simulation strands visible. |
| **Local Simulation** | Makes strands simulation be done in local space. |
| **Linear Velocity Scale** | The amount of linear velocities sent to the local groom space from the reference bone. |
| **Angular Velocity Scale** | The amount of angular velocities sent to the local groom space from the reference bone. |
| **Local Bone** | The name of the bone used for the simulation of local space. |
| **Teleport Distance** | Teleport distance threshold to reset the simulation. |
| Solver Settings |   |
| **Enable Simulation** | Enables the simulation of the groom groups / levels of detail. Requires both this setting and the one in the groom asset to be enabled. |
| External Forces |   |
| **Gravity Vector** | The acceleration vector measured in cm/s2 to be used for gravity. |
| **Air Drag** | The coefficient between 0 and 1 to be used for air drag. |
| **Air Velocity** | The velocity of the surrounding air measured in cm/s. |
| Material Constraints |   |
| **Bend Damping** | Damping applied for the bend constraint using a value between 0 and 1. |
| **Bend Stiffness** | The stiffness for the bend constraint in GPa. |
| **Stretch Damping** | The damping for the stretch constraint using a value between 0 and 1. |
| **Stretch Stiffness** | The stiffness for the stretch constraint in GPa. |
| **Static Friction** | The static function used for collision against physics assets. |
| **Kinetic Friction** | The kinetic friction used for collision against physics assets. |
| **Strand Viscosity** | The viscosity between 0 and 1 that is used for self-collision. |
| **Collision Radius** | The radius to be used for collision detection against physics assets. |