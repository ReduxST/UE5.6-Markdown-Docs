# Setting your Display Rate

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/setting-your-display-rate](https://dev.epicgames.com/documentation/en-us/unreal-engine/setting-your-display-rate)  
**Processed:** 2025-06-14 16:50:10

---

## Engine Tick vs Sequencer FPS

Unreal Engine tries to render frames as fast as possible. In most real-time applications, this is exactly what you want to make the player experience as smooth as possible.

For linear content we typically work within a specific frame rate based on the media we are authoring; 30 FPS and 24 FPS being the most common.

Sequencer allows you to specify a frame rate. However, this specifies the time when certain events should happen relative to the shot length. It does not necessarily throttle the Engine Tick rate to the desired Frames Per Second.

When dealing with an animation or keys on a curve this is generally fine and, when triggering sequences within a real-time application, desirable. However, when dealing with a simulation that expects predictable and consistent time steps, this can cause unexpected behavior.

In the video below a **single sprite** is added in the lower right corner which displays the **engine delta time** as seen by Niagara. You'll notice that the system is ticking as fast as it can. This tick rate will change based on the other elements within the level. If other elements are taking resources, the tick rate will drop and the time step inside the simulation will increase. As a result, your simulation can look different as you add more and more elements to your shot.

## Lock to Display Rate at Runtime

Sequencer has the option to force the engine to tick at the frame rate you specify. Even if the engine has the potential to run much faster, Sequencer will throttle it. By keeping the tick rate in sync with the frame rate your simulations will evolve in a much more consistent way and more closely match the output from the Movie Render Queue (MRQ).

Lock to Display Rate at Runtime will be applied when MRQ runs as well as playing in the editor. This will interfere with Temporal Sub Steps if you have them defined. More on this topic later.

## Fixed Tick Delta Time

Each Niagara System has the option to fix its time step length. Niagara will force the system to tick at the specified rate regardless of what the Engine Tick can handle. By using this option you can force your simulation to tick at a predictable rate.

The disadvantage with this approach is Niagara will force this tick rate even if the scene complexity and engine tick cannot really support it. Complex simulations which are forced to tick at a very small delta time can cause editor interactivity to suffer.

Being able to preview accurately in editor is a really valuable tool, but there is a limit. As complexity increases the engine tick rate will drop. Once it drops below your desired frame rate you will no longer be able to preview accurately. At this point, the most reliable way to iterate is via MRQ.