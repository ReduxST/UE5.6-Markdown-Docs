# DMX Sequencer Integration

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/dmx-sequencer-integration-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/dmx-sequencer-integration-in-unreal-engine)  
**Processed:** 2025-06-14 16:21:11

---

Sequencer is an Unreal Engine feature that provides easy animation and event triggering. Sequencer supports Digital Multiplex (DMX) recording, playback, and editing through custom **DMX Sequencer** tracks to help you better design and preview lighting experiences in virtual or physical shows and live events.

You can add a custom DMX track to a Level Sequence to program and control DMX without the need for Blueprints or programming.

## Add a DMX Sequencer Track to a Level Sequence

The custom DMX Sequencer track connects to a [**DMX Library**](/documentation/en-us/unreal-engine/create-a-dmx-library-and-add-fixture-patches-in-unreal-engine). You can add any [**Fixture Patch**](/documentation/en-us/unreal-engine/dmx-overview) from that DMX Library into the track, and expose the patch's attributes for sending out DMX. You can add keyframes for each attribute to the track to animate and control the DMX output. You can then replay, edit, and share the [**Level Sequence**](/documentation/en-us/unreal-engine/unreal-engine-sequencer-movie-tool-overview) that contains the DMX track.

### Steps

To add a Fixture Patch to a Level Sequence, follow these steps:

1.  Press the **\+ Track** button and select **DMX Library Track** from the list. Select the DMX Library you want to add to the sequence.
    
    Click image to expand.
    
2.  On the new DMX Library Track, click the **Add (+)** button and select a Fixture Patch to create a new track for the desired patch. You can also click **Add All Patches** in the dropdown menu to create a new track for every Fixture Patch in the library.
    
    Click image to expand.
    
3.  Expand a fixture patch track and add a new keyframe by pressing the **Add (+)** button or by modifying the value next to the attribute name. The value ranges are defined by the DMX signal format selected in the DMX Library for each Attribute.
    
    Click image to expand.
    

Sequencer sends DMX data both when you press play and when you scrub the playback head.

By default, the recorded sequence will be locked from editing. To unlock the sequence for editing, click the Lock icon next to the sequence name in the sequence editor.

Click image to expand.

## Record DMX with Take Recorder

The DMX plugin **Take Recorder** tool can listen for incoming DMX streams and record the data as new keyframes in a Level Sequence. You can then replay, edit, and share this Level Sequence. You can listen for incoming DMX for a specified Fixture Patch assigned in a DMX library, and record changes to keyframes in the Level Sequence.

### Steps

To record DMX to a level sequence, follow these steps:

1.  To open the Take Recorder, click **Window** > **Cinematics** > **Take Recorder**.
    
2.  Click **Source (+)** and select **DMX Library** from the list.
    
    Click image to expand.
    
3.  Set the DMX Library parameter to the Library containing the patch you want to record.
    
    Click image to expand.
    
4.  Click the **Fixture Patch** parameter and select a patch from the list to add it to the patch record list, or click **Add all Fixture Patches** to add all patches in the library to the patch record list.
    
    Click image to expand.
    
5.  Click **Record**. All incoming DMX that matches the patch record list will be saved into a new Level Sequence as a new keyframe.
    
6.  When you are done recording, navigate to the created sequence in the **Content Browser** to review and play back the recorded DMX. The new sequence should be saved to `Cinematics/Takes/[RecordDate]/`.
    

After recording with Take Recorder, the recorded sequence will be locked from editing. To unlock the sequence for editing, click the Lock icon next to the sequence name in the sequence editor.

Click image to expand.