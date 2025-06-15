# Using Take Recorder

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/record-gameplay-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/record-gameplay-in-unreal-engine)  
**Processed:** 2025-06-14 16:45:57

---

Take Recorder enables the fast iteration of recording performances and quickly reviewing previous takes for virtual production workflows. You can easily record animations from motion capture linked to characters in the level, as well as actual Live Link data for future playback. By recording takes and adding them to Sequencer, productions of all sizes and any number of takes can easily be accommodated.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/67ac834d-29de-4fd5-871c-15663109eb82/takerecorder.png)

The most common usage of Take Recorder will be with projects using [Live Link](/documentation/en-us/unreal-engine/live-link-in-unreal-engine). Because Take Recorder enables you to quickly record performances, using Live Link is an easy way to update and iterate on previous takes.

For this how-to, we use Live Link with the Face AR Sample. If you would like to follow along, see the [Face AR Sample documentation](/documentation/en-us/unreal-engine/face-ar-sample-in-unreal-engine) for how-to set up Editor and Live Link.

## Using Take Recorder

With the connection established, we can now use Take Recorder to capture a sequence.

Make sure you enable the Take Recorder plugin. You can do this by navigating to Edit > Plugins and searching for Take Recorder.

1.  In Unreal Engine, navigate to **Window** > **Take Recorder**.
    
2.  Select your Actor from the World Outliner. In Take Recorder, select **\+ Source > From Actor > Add 'Actor Name'** .
    
    ![adding_a_source_from_actor](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bbb291dd-fbf5-4d10-85c1-831a69dc54ad/source2_callout.png)
3.  Select the Actor from the list. Under the Actor settings, make sure to change **Record Type** to the appropriate setting.
    
4.  Select **Play** and then select the red record button in Take Recorder. The recording displays data in real-time in Sequencer, and you can see the motion capture live in the viewport.
    
    ![record_button_callout](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5e387915-bc2e-4640-994b-384f6d44650e/record_button_callout.png)
5.  When you are finished recording, click the Stop button in Take Recorder.
    

You can record as many takes as you need by repeating this process.

## Organizing and Reviewing Your Takes

After you finished recording, there are two ways to view your takes in Sequencer. First, you can view the take you just recorded by selecting the **Review the Last Recording** icon (floppy disk with an eye). This allows you to review recorded tracks in Sequencer. If you decide you do not like the take and want to record again, you can switch back to record mode by selecting the **Return Back to the Pending Take** arrow icon.

![PendingTake_callout](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/97cb7c77-c30b-45c9-b47e-17b49f0821a4/pendingtake_callout.png)

To view your takes, select the **Take Browser** icon in Take Recorder. A separate window tab will appear with the folders of all your takes in the Content Browser. The Take Browser uses the location saved in the Take Recorder User Settings.

![Browse_callout](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/43823ee2-9b6b-4b03-9b38-527b1524078a/takebrowser.png) ![Content_Browser_with_takes](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5f95fbf4-51dd-4f7a-ade9-9ea92a470249/takebrowser2.png)

The default save location is under **Cinematics > Takes** To change the default save location in Content Browser, select the Take Recorder **Settings** icon. Under **User Settings**, change the **Preset Save Location** to the new location.

![TR_settings_callout](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e2f040ce-b87c-4039-bf0d-ae2d182e38cf/record_settings.png) ![TR_User_Settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/06517a3d-78ce-44f2-a1a0-b8f9a2164926/usersettings_callout.png)

To review the sequence, double-click the file from the Content Browser. You can playback the sequence the same way as any other sequence.

![Playback_example_with_two_actors](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fe4b0eaa-6a19-4a11-9aa4-8ef04953f1f1/playback_example2.png)

There is also assigned metadata for each sequence that you can see by hovering over a sequence in the Content Browser. You can also see the metadata by using the Column View Type.

![Example_of_take_metadata](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/48c7fbf5-a6bc-47f9-a8a9-8bf6eb8867e3/metadata_hover.png)

## Using Layered Take Recording

Layered Take Recording allows you to add additional recorded tracks to an existing sequence. This is particularly helpful when using motion capture for multiple actors in a sequence.

1.  Record your first take with "Actor A" as many times as you need. Then, choose the last or best take, and select **Review the Last Recording** to switch into review mode.
    
2.  In review mode, select the clapboard icon **Start a new recording using this Take as base**.
    
    ![Clapboard_icon_callout](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/17a89a73-6831-4ed6-a64b-8066cf2ee98c/layertake.png)
    
    The mode switches back to record, and you can see the take from Actor A in Sequencer.
    
3.  Add a new **Source** for the second actor, "Actor B". Click the toggle button to disable "Actor A".
    
    ![disable_actor](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e002a14e-9f28-4347-adda-2f94f807d98e/disable_actor.png)
4.  Record the take with Actor B. Once you are finished recording, select **Review the Last Recording** to playback the recordings simultaneously and preview the takes together. In this example, we hid Actor A from the viewport to record Actor B. You may or may not want to do this depending on what you are recording.
    

You can record and stack as many takes into a single sequence as you want. When you are finished, your entire sequence is saved as a single file, and each individual take is saved into a subfolder.