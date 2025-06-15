# Level Sequence

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/level-sequence-settings-in-the-unreal-engine-project-settings](https://dev.epicgames.com/documentation/en-us/unreal-engine/level-sequence-settings-in-the-unreal-engine-project-settings)  
**Processed:** 2025-06-14 16:33:07

---

## Level Sequence

### Timeline

| **Section** | **Description** |
| --- | --- |
| **Default Lock Engine to Display Rate** | 
0: Playback locked to playback frames.

1: Unlocked playback with sub-frame interpolation.



 |
| **Default Display Rate** | 

Specifies default display frame rate for newly created level sequences; also defines frame-locked frame rate where sequences are set to be frame-locked.

Examples:

-   **30 fps**
-   **120/1 (120 fps)**
-   **30000/1001 (29.97)**
-   **0.01s (10ms)**



 |
| **Default Tick Resolution** | 

Specifies default tick resolution for newly created level sequences.

Examples:

-   **30 fps**
-   **120/1 (120 fps)**
-   **30000/1001 (29.97)**
-   **0.01s (10ms)**



 |
| **Default Clock Source** | 

Specifies default clock source for newly created level sequences.

You can choose from the following options:

-   **Tick**
-   **Platform**
-   **Audio**
-   **Relative Timecode**
-   **Timecode**
-   **Play Every Frame**
-   **Custom**



 |