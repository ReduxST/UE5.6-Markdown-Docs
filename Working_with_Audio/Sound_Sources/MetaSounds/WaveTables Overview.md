# WaveTables Overview

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/wavetables-overview-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/wavetables-overview-in-unreal-engine)  
**Processed:** 2025-06-14 17:04:06

---

**WaveTables** store periodic wave data in lookup tables and provide a way to perform wavetable synthesis and sampling in **MetaSounds**.

## WaveTable Banks

Unreal Engine stores WaveTables in **WaveTable Bank** assets.

You can create a WaveTable Bank in the **Content Browser** by clicking the **Add** button and selecting **Audio > WaveTable > WaveTable Bank**.

### Editor

Click image for full size.

You can edit a WaveTable Bank in the **WaveTable Bank Editor**. Double-click a WaveTable Bank in the Content Browser to open the WaveTable Bank Editor.

The WaveTable Bank Editor has three main UI components.

1.  **Curve Editor Toolbar** - Use these tools to change your viewing mode or edit Custom Curve Type WaveTables. For more information about the toolbar and editing curves, see [Curve Editor](/documentation/en-us/unreal-engine/animation-curve-editor-in-unreal-engine).
2.  **Details** **Panel** \- Edit the WaveTable Bank's properties.
3.  **Transform Curve** **Panel** \- View all of the WaveTable curves in the WaveTable Bank.

### Properties

You can find the WaveTable Bank's properties in the Details panel.

| **Property** | **Description** |
| --- | --- |
| **Sample Mode** | 
The sampling mode used for the bank. Options include:

-   **Fixed Resolution** - Enforces uniform resolution of all WaveTables in the bank. This mode supports lockstep mixing, interpolating, and spatializing, which is useful for oscillating or enveloping.
-   **Fixed Sample Rate** - Enforces uniform sample rate for all WaveTables in the bank. This mode supports discrete audio playback at a shared speed, which is useful for sampling and granulating.



 |
| **Resolution / Sample Rate** | The number of samples cached for each bank entry. |
| **Bipolar** | If enabled, the curve is clamped between -1.0 and 1.0, which is useful for waveform generation and oscillation. If disabled, the curve is clamped between 0.0 and 1.0, which is useful for enveloping. |
| **WaveTable Size (MB)** | (Read-only) The total size of all WaveTable data within the bank. |
| **Entries** | The array of WaveTables in the bank. |
| **Curve Type** | 

The curve to apply when transforming the output. Options include:

-   Presets, such as Sine (360 deg) and Linear (Ramp In).
-   **Shared** - Reference a shared **Curve** asset.
-   **Custom** - Design a custom curve.
-   **File** - Generate a WaveTable from an audio file.



 |
| **Duration (Sec)** | (Fixed Sample Rate only) The duration of the curve. |

## MetaSound Nodes

There are three categories of WaveTable MetaSound nodes.

-   Generators
-   Envelopes
-   Utility

For more information about each of the nodes below, see [MetaSounds Reference Guide](/documentation/en-us/unreal-engine/metasounds-reference-guide-in-unreal-engine).

### Generators

MetaSound supports several core generator nodes, such as **Sine** and **Saw**. They are powerful synthesis tools, but WaveTable generator nodes are even more so.

With WaveTable generator nodes, you can use custom waves and samples to drive your synthesis.

These nodes include:

-   **WaveTable Player** - Plays the WaveTable at the given index of a WaveTable Bank. This node expects a Fixed Sample Rate WaveTable Bank.
-   **WaveTable Oscillator** - Plays the WaveTable at the given frequency. This node expects a Fixed Resolution WaveTable Bank.

### Envelopes

MetaSound also supports several core envelope nodes, such as **AD Envelope** and **ADSR Envelope**. WaveTable envelope nodes improve on those traditional options as well.

With WaveTable envelope nodes, you can use custom waves and samples for more powerful modulation.

These nodes include:

-   **WaveTable Envelope** - Reads the WaveTable over the given duration. This node expects a Fixed Resolution WaveTable Bank.
-   **Evaluate WaveTable** - Evaluates the WaveTable at the given input value.

### Utility

You can use the **Get WaveTable From Bank** node to get a WaveTable to use as an input into another node. The **TableIndex** float input supports blending between WaveTables in a Fixed Resolution bank.