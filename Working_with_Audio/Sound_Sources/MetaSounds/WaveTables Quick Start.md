# WaveTables Quick Start

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/wavetables-quick-start-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/wavetables-quick-start-in-unreal-engine)  
**Processed:** 2025-06-14 17:04:08

---

**WaveTables** store periodic wave data in lookup tables and provide a way to perform wavetable synthesis and sampling in **MetaSounds**.

This guide teaches you how to create a MetaSound powered by two WaveTables with different Sample Modes.

-   **Fixed Resolution** - Enforces uniform resolution of all WaveTables in the bank. This mode supports lockstep mixing, interpolating, and spatializing, which is useful for oscillating or enveloping.
-   **Fixed Sample Rate** - Enforces uniform sample rate for all WaveTables in the bank. This mode supports discrete audio playback at a shared speed, which is helpful for sampling and granulating.

## Create the Fixed Resolution WaveTable Bank

Click image for full size.

To create the Fixed Resolution WaveTable Bank:

1.  In the **Content Browser**, click the **Add** button.
2.  Select **Audio > WaveTable > WaveTable Bank**.
3.  Name the WaveTable Bank `WTB_FixedResolution`.
4.  Double-click the WaveTable Bank to open the **WaveTable Bank Editor**.
5.  In the **Details** panel:
    1.  Disable **Bipolar**.
    2.  Click the **Add Element (+)** button for **Entries** twice.
    3.  Expand **Index \[0\]** and set **Curve Type** to **Linear (Ramp Out)**.
    4.  Expand **Index \[1\]** and set **Curve Type** to **Linear (Ramp In)**.
6.  Save the WaveTable Bank.
7.  Close the **WaveTable Bank Editor**.

## Create the Fixed Sample Rate WaveTable Bank

Click image for full size.

To create the Fixed Sample Rate WaveTable Bank:

1.  In the **Content Browser**, click the **Add** button.
2.  Select **Audio > WaveTable > WaveTable Bank**.
3.  Name the WaveTable Bank `WTB_FixedSampleRate`.
4.  Double-click the WaveTable Bank to open the **WaveTable Bank Editor**.
5.  In the **Details** panel:
    1.  Click the **Add Element (+)** button for **Entries** twice.
    2.  Expand **Index \[0\]**:
        1.  Set **Curve Type** to **Sine (360 deg)**
        2.  Set **Duration (Sec)** to 0.5.
    3.  Expand **Index \[1\]**:
        1.  Set **Curve Type** to **Sine (360 deg)**.
        2.  Set **Duration (Sec)** to 1.0.
6.  Save the WaveTable Bank.
7.  Close the **WaveTable Bank Editor**.

## Create the MetaSound Source

Click image for full size.

Construct a MetaSound that uses the WaveTable Banks for generating and enveloping. Follow the steps below to build a MetaSound with the graph above.

1.  In the **Content Browser**, click the **Add** button.
2.  Select **Audio > MetaSound Source**.
3.  Name the new MetaSound `MSS_WaveTableDemo`.
4.  Double-click the MetaSound to open the **MetaSound Editor**.
5.  In the **Interfaces** panel, click the **Remove (Trash Bin)** button next to the **UE.Source.OneShot** Interface entry. This removes the On Finished Output node, which isn't used on looping sounds.

### Build the Generator Section

1.  Find the **On Play Input** node in the graph and drag off of the pin into an empty space. Enter "Trigger Repeat" into the node search to create a connected node. You can move the node around the graph by dragging it.
2.  On the **Trigger Repeat** node:
    1.  Set **Period** to 1.0.
    2.  Drag off the **RepeatOut** pin and create a **Trigger Counter** node.
3.  On the **Trigger Counter** node:
    1.  Set **Reset Count** to 2.0.
    2.  Drag off the **On Trigger** pin and create a **WaveTable** **Player** node.
    3.  Connect the **Count** pin to the **Index** pin of the **WaveTable Player** node.
4.  On the **WaveTable Player** node:
    1.  Click the **Bank** dropdown and set it to `WTB_FixedSampleRate`.
    2.  Set **Pitch Shift** to 440.0.
    3.  Enable **Loop**.

### Build the Envelope Section

1.  Right-click in an empty space and create a **Get WaveTable From Bank** node.
2.  On the **Get WaveTable From Bank** node:
    1.  Click the **Bank** dropdown and set it to `WTB_FixedResolution`.
    2.  Drag off the **TableIndex** pin and select **Promote to Graph Input**. This creates a **Float Input** node named TableIndex.
    3.  Drag off the **Out** pin and create a **WaveTable Envelope** node.
3.  On the **WaveTable Envelope** node:
    1.  Drag off the **On Play** pin and create a **Get On Play** node.
    2.  Click the down arrow at the bottom of the node to expand the pin list.
    3.  Set **Mode** to Loop.

### Connect the Outputs

1.  Right-click in an empty space and create a **Mono Mixer (2)** node.
2.  On the **Mono Mixer (2)** node:
    1.  Connect the **In 0** pin to the **Mono Out** pin of the **WaveTable Player** node.
    2.  Connect the **Gain 0 (Lin)** pin to the **Out** pin of the **WaveTable Envelope** node.
    3.  Connect the **Out** pin to the **Out Mono Output** node.
3.  Save the MetaSound.

## Test the MetaSound

Click the **Play** button on the **MetaSound Editor Toolbar** to play the MetaSound. You can adjust the **TableIndex** graph input value by clicking the **Input Widget (Dial)** on the node and dragging up or down.

The WaveTables in `WTB_FixedSampleRate` alternate playback every second. The gain is controlled by a WaveTable from `WTB_FixedResolution`, which is selected by the TableIndex graph input. TableIndex values between 0 and 1 produce a blend between the WaveTables in the bank.

## Own Your Own!

Now that you've finished this Quick Start, consider taking this project further. Below are some suggestions you can explore on your own.

-   Build a MetaSound with the WaveTable nodes not used in this guide, such as the **WaveTable Oscillator** node and **Evaluate WaveTable** node. For more information on WaveTable nodes, see [MetaSounds Reference Guide](/documentation/en-us/unreal-engine/metasounds-reference-guide-in-unreal-engine).
-   Customize your WaveTable curves by setting the **Curve Type** to **Custom**. See [Curve Editor](/documentation/en-us/unreal-engine/animation-curve-editor-in-unreal-engine) for more information about the toolbar and editing curves.
-   Import audio files as a WaveTable by setting the **Curve Type** to **File** and the **Wave Table Settings > File Path.**