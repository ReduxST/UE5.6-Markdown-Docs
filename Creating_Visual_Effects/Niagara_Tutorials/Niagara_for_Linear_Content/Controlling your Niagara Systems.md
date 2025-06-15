# Controlling your Niagara Systems

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/controlling-your-niagara-systems](https://dev.epicgames.com/documentation/en-us/unreal-engine/controlling-your-niagara-systems)  
**Processed:** 2025-06-14 16:15:59

---

## Controlling Niagara Systems with Life Cycle Tracks

At the moment the Movie Render Queue (MRQ) is simply capturing whatever the camera is pointing at. The Niagara Systems are activated when MRQ starts up. To be able to trigger the systems at a specific time and control the behavior through the shot, we need to add tracks for the systems.

Follow these steps to add a Niagara Life Cycle Track:

1.  Select a **Niagara System** from the **Outliner** window and drag it into the **Sequencer Panel**.
2.  Add a **Niagara Component track** to the Niagara System Track.
3.  Add a **Niagara System Life Cycle Track** to the Niagara Component Track.
4.  Modify the Section Range Start/End values so the red bar sits somewhere within the shot.
5.  Press **Play**.

## Life Cycle Track Modes

The default System Life Cycle Track mode controls when the system becomes active and inactive. Sequencer does not dictate the age of the system. If you pause the sequence you'll notice that the system keeps emitting so long as it remains active.

Follow these steps to switch the Age Update Mode:

1.  Over the red **System Life Cycle track**, right-click to open up the **track properties**.
2.  Under the **Properties** section, switch the **Age Update Mode** to **Desired Age**.
3.  Scrub the timeline back and forth over the Life Cycle Track.

There are 3 modes you can choose from:

**Tick Delta Time**: Allows the system to run at the engine frame rate, independent of Sequencer.

**Desired Age**: Sequencer specifies the age of the Niagara System. The Niagara System resets at the beginning of the Life Cycle Track and ticks up to the current frame. If the time line is scrubbed forward the system continues to tick to the new time. If the time line is scrubbed backward the system has to reset and tick up to the current time from the beginning of the Life Cycle track.

**Desired Age No Seek**: When playing forward this mode matches the Desired Age mode. When scrubbing backward the system stops playing and resets at the time when the play head starts to progress forward again.

In almost all scenarios, the Desired Age mode is preferred.