# Caching and Reusing your System

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/caching-and-reusing-your-system](https://dev.epicgames.com/documentation/en-us/unreal-engine/caching-and-reusing-your-system)  
**Processed:** 2025-06-14 16:11:45

---

## Determinism

You will have noticed that the system is erratic when being scrubbed backward. This is because the system has to reset from the beginning of the Life Cycle track and run up to the current frame. Each time it resets the random values are different.

Each Niagara Emitter can be switched to be deterministic. This causes the random seed to be the same each time the system resets.

More important than being able to scrub backward and forward, determinism allows you to re-render your shot over and over again in a predictable way. If no parameters or inputs to a system have been changed, the system should be expected to produce the same results each time it runs. This is critical when reviewing shots in a production environment when seeking approval through multiple iterations.

## Caching Niagara Simulations

As of Unreal Engine 5.2 we are able to **cache** Niagara simulations to a **Niagara Sim Cache** asset from Sequencer. To enable this feature make sure the **Niagara Sim Caching plugin** is loaded. A tutorial on Caching Niagara simulations can be [found here](https://dev.epicgames.com/community/learning/tutorials/7B3y/unreal-engine-caching-niagara-fluids-with-sequencer).

### Niagara Simulation Cache Asset

Niagara simulations can be cached to a Niagara Simulation Cache.

By default, when you cache from Sequencer, the Sim Cache data is embedded within the Level Sequence asset. This can be convenient for small simulations, but can bloat the size of your Level Sequence assets when dealing with lots of complex simulations.

You have the option to create your own Niagara Simulation Cache for each simulation. You can then separate the simulation data from the Level Sequence. The Sim Cache Asset is referenced in the Cache Track Properties inside Sequencer.

1.  From the Content Browser, right click and navigate to FX/Advanced/Niagara Simulation Cache.
2.  Rename the new asset to something appropriate to your needs.
3.  From Sequencer, right click the cache track and go to the track properties menu.
4.  Change the Sim Cache parameter to point to your new asset.

### Cache Tracks and Temporal Samples

When using Temporal Samples in Movie Render Queue (MRQ), the time at which the scene is evaluated is subdivided through the shutter open time. If you choose 9 temporal samples the final image will be a composite of 9 separate renders. Each of the 9 renders is created from a slightly different point in time. For this to work, your scene actors need to evaluate at much smaller time steps than just on the whole frames.

Caching involves storing the state of your simulation for each frame of the cache. Only whole frames are stored. If we rendered the cache using Temporal Samples we would have to render the same data over and over again, as we only have the data on whole frames.

To combat this, the caching system stores extra data to allow point data to be interpolated or extrapolated to positions off the whole frame. This allows a Temporal Sample to render your simulation at an appropriate position for the samples time.

Interpolation is the process where positions and quaternions are interpolated between the current frame's data and the surrounding frame's data. This is the most reliable method but is only possible if a particle exists on the surrounding frames.

Extrapolation uses the current frame's velocity to figure out where the position would be at an earlier or later time.

When both options are checked, Interpolation takes precedence. If Interpolation is not possible, extrapolation will be used.

The Interpolation/Extrapolation functionality is only available on point based simulations. For other grid based simulations only the whole frame data is available to the renderer.

## Using the Same System Multiple Times

To create complexity we often use very similar FX assets to populate a shot. Rather than duplicating the asset in the Content Browser for every variation you need, there are mechanisms available to support variations within a single asset.

### Random Seed Offset

Each instance of an asset has a Random Seed Offset parameter on its component. This can be used to create variations of the same system while maintaining determinism.

## User Parameters

Niagara supports User Parameters. These are parameters which are promoted to the Niagara System instance in the level. As a result variations can be defined of the same underlying Niagara System.

Sequencer supports User Parameters as tracks. The track associated with a User Parameter can be added to the Niagara Component track in sequencer and keyed for variations over time if needed.