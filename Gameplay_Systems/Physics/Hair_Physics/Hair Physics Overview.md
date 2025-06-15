# Hair Physics Overview

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/hair-physics-in-unreal-engine---overview](https://dev.epicgames.com/documentation/en-us/unreal-engine/hair-physics-in-unreal-engine---overview)  
**Processed:** 2025-06-14 16:27:06

---

Unreal Engine's Hair rendering and simulation system uses a strand-based workflow to render each individual strand of hair with physically accurate motion. It enables artists to simulate and render hundreds of thousands (or more) photoreal hairs in real-time for grooms created in DCC packages. Real hair and fur moves in a specific way when reacting to head and body movement, wind, gravity, and other forces. Achieving realistic hair and fur animation is generally accomplished by using a physics-based simulation. Running such a complex simulation at runtime can be very computationally expensive.

![Meta Humans using realistic hair grooms](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9786ea5e-d121-4545-8af3-678aa3d3413d/hp-overview-1.png)

Hairs are challenging to simulate because of their large numbers and the complexity of the motion, both with object collisions and self-collisions.

Hair dynamics rely on complex interdependencies. In the case of animal fur, muscle and flesh simulation is responsible for a large portion of the fur motion and hair simulation itself.

When rendering and simulating realistic hair, the system uses specific "guides" to reduce the computational cost of the simulation. A guide is a subset of the total number of strands that are used for deformation. During the simulation, the guide strands are deformed and this deformation is used to interpolate movement for all the strands.

Unreal Engine uses two types of guides - **rendering guides** and **simulation guides**. Rendering guides typically provide structure to the groom, such as clumping, direction changes, and flow. These guides represent a small percentage of the total strands (typically between 5 to 10%). Manually selecting the best guides will significantly improve the quality of the deformation compared to a random sample of strands.

Simulation guides drive the shape and motion of the associated strands during physical simulation. These guides are created by resampling the rendering guides and reducing the number of vertices (points) per strand. You can set the number of points per strand to 4, 8, 16, or 32, depending on your needs.

Guides can be created in an external DCC package or inside the Unreal Engine editor. To automatically generate a guide, select the appropriate option in the **Import Options** window and select the percentage of strands that will be used for the guide.

Unreal Engine will select a random sample from the total strands when auto-generating the rendering guide. Manually creating the guides can significantly improve the quality of the deformation.

Hair simulation in Unreal Engine is implemented as part of the Niagara Visual Effects system. The simulation is performed on the GPU, and the solver is based on the XPBD (Position-Based Simulation of Compliant Dynamics) method.

### Solving the Constraints

To solve for all the different constraints, you need to provide the number of substeps and solver iterations, alongside the strands, collisions, and constitutive model parameters. The solver will target the original mesh under gravity (rest pose) to keep the final style as close to the original style as possible.

### Handling Collisions

When a physics asset is added to the Skeletal Mesh, the simulation solver handles body collisions against the primitives of that physics asset.

Self-collisions are computed based on an average velocity field built from the rasterization of the particles' velocity onto a regular voxel grid.

The system uses a mathematical model that best approximates the realistic behavior of hair strands when external forces are applied. The biggest challenge is finding a good model that enables strands to behave realistically, at low solver iteration counts.

These models control how the strands will stretch, bend, and twist during simulation. The Cosserat Rod and Angular Spring methods are available within the groom asset physics properties.

Learn more about hair simulation by going to the [Hair Rendering and Simulation](/documentation/en-us/unreal-engine/hair-rendering-and-simulation-in-unreal-engine) documentation page.