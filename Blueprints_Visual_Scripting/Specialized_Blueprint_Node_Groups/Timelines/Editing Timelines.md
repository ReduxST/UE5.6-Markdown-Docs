# Editing Timelines

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/editing-timelines-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/editing-timelines-in-unreal-engine)  
**Processed:** 2025-06-14 16:21:44

---

**Timelines** can be edited by **Double-clicking** on the Timeline node in the **Graph** tab or on the Timeline in the **My Blueprint** tab. This opens the **Timeline Editor** in a new tab.

## Timeline Editor

[![Blueprint Timeline Editor](https://dev.epicgames.com/community/api/documentation/image/6e44536d-af86-4aae-a863-afec370143db?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/6e44536d-af86-4aae-a863-afec370143db?resizing_type=fit)

| Button/Checkbox | Description |
| --- | --- |
| 
[![](https://dev.epicgames.com/community/api/documentation/image/279f7f2f-c1a0-4d90-9276-6aab28626c0a?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/279f7f2f-c1a0-4d90-9276-6aab28626c0a?resizing_type=fit)



 | 

Adds a new float track to the Timeline, for animating scalar float values.

 |
| 

[![](https://dev.epicgames.com/community/api/documentation/image/5f011ac8-1520-4384-9a4d-94544b9a6678?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/5f011ac8-1520-4384-9a4d-94544b9a6678?resizing_type=fit)



 | 

Adds a new vector track to the Timeline, for animating float vector values such as rotation or translation.

 |
| 

[![](https://dev.epicgames.com/community/api/documentation/image/49f245a5-3b38-45dc-94fa-3ee4e37a6497?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/49f245a5-3b38-45dc-94fa-3ee4e37a6497?resizing_type=fit)



 | 

This adds an event track, which provides another execution output pin that will be triggered at keyframed times on the track.

 |
| 

[![](https://dev.epicgames.com/community/api/documentation/image/3b598399-a6e9-4116-b1c3-50523accc766?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/3b598399-a6e9-4116-b1c3-50523accc766?resizing_type=fit)



 | 

Adds a new linear color track to the Timeline, for animating colors.

 |
| 

[![](https://dev.epicgames.com/community/api/documentation/image/e64885a5-17d6-411e-bfe3-435c49e8a1d1?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/e64885a5-17d6-411e-bfe3-435c49e8a1d1?resizing_type=fit)



 | 

Add an external curve to the Timeline. This button is only active if an external curve is selected in the **Content Browser**.

 |
| 

[![](https://dev.epicgames.com/community/api/documentation/image/6cf211ad-480c-4aa9-aa0e-f130d204fecb?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/6cf211ad-480c-4aa9-aa0e-f130d204fecb?resizing_type=fit)



 | 

Allows you to set the playback length for this Timeline.

 |
| 

[![](https://dev.epicgames.com/community/api/documentation/image/fd0d2f0b-83ec-4038-9e25-d83f47fe8a27?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/fd0d2f0b-83ec-4038-9e25-d83f47fe8a27?resizing_type=fit)



 | 

If this is not active, the last keyframe of a sequence is ignored. This can help prevent skipping when an animation is looping.

 |
| 

[![](https://dev.epicgames.com/community/api/documentation/image/156f95e2-5812-4236-af95-6d35c5816180?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/156f95e2-5812-4236-af95-6d35c5816180?resizing_type=fit)



 | 

If active, this Timeline node does not require an execution input to begin, and will start playing as soon as the level begins.

 |
| 

[![](https://dev.epicgames.com/community/api/documentation/image/e0c9d797-ac1c-4c1d-8ae6-a5956cf1e88d?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/e0c9d797-ac1c-4c1d-8ae6-a5956cf1e88d?resizing_type=fit)



 | 

If active, the Timeline animation will repeat indefinitely unless stopped via the Stop input pin.

 |
| 

[![](https://dev.epicgames.com/community/api/documentation/image/0233ada8-2774-4e1f-9942-f15a61e0126c?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/0233ada8-2774-4e1f-9942-f15a61e0126c?resizing_type=fit)



 | 

If active, the Timeline animation will be replicated across clients.

 |

## Adding Tracks

Timelines use **Tracks** to define the animation of a single piece of data. This can be a float value, vector value, color value, or events. Tracks can be added to the Timeline by clicking one of the **Add Track** buttons. For instance, click the button and enter a name for the new track. Press **Enter** to save the name for your new float track.

[![Blueprint Timeline - Add Float Track](https://dev.epicgames.com/community/api/documentation/image/02c05d7d-44db-4251-9485-16e852833735?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/02c05d7d-44db-4251-9485-16e852833735?resizing_type=fit)

1.  **Track Name** - You can enter a new name for the track into this field at any time.
    
2.  **External Curve group** - Allows you to choose an external curve asset from the **Content Browser** instead of creating your own curve.
    
3.  **Track timeline** - This is the keyframe graph for this track. You will place keyframes into this and see the resulting interpolation curve.
    

## Adding Keys

Once you have tracks in place, you can then start adding keys to define your animation.

For more information on working with keys and curves in Timelines, please see the [Keys and Curves page](https://dev.epicgames.com/documentation/en-us/unreal-engine/keys-and-curves-in-unreal-engine).

[![](https://dev.epicgames.com/community/api/documentation/image/5fb5d0f7-cb05-4521-b3e3-130c2d62bdb3?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/5fb5d0f7-cb05-4521-b3e3-130c2d62bdb3?resizing_type=fit)

Once you have finished editing your track, the data or event execution from the track is output through a data or execution pin with the same name as the track.

[![Blueprint Timelines - Track Data Output](https://dev.epicgames.com/community/api/documentation/image/9a0884b6-e598-411d-a20e-1044d0d76bc3?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/9a0884b6-e598-411d-a20e-1044d0d76bc3?resizing_type=fit)