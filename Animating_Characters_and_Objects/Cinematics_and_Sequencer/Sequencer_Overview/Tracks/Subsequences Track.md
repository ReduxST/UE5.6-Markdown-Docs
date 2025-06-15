# Subsequences Track

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/cinematic-subscequences-track-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/cinematic-subscequences-track-in-unreal-engine)  
**Processed:** 2025-06-14 16:13:20

---

In large-scale cinematic productions, it may be necessary to have multiple artists working on the same sequence or even shot at the same time. The Subsequences Track enables this type of workflow by allowing additional sequence assets to be contained within the same sequence. Subsequences can also be used to organize your scene so that repetitive tracks and content are partitioned away into their respective disciplines' subsequence.

This document provides an overview of how to create and use the Subsequences Track.

#### Prerequisites

-   You have an understanding of [Sequencer](/documentation/en-us/unreal-engine/how-to-make-movies-in-unreal-engine) and its [Interface](/documentation/en-us/unreal-engine/sequencer-cinematic-editor-unreal-engine).

## Creation

To create a Subsequences Track, click the **Add (+) Track** button in Sequencer and select **Subsequences Track**.

![create subsequence track](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a3e85f2d-a689-4764-9f32-6a277a698cdf/addtrack.png)

From there you can add sequences by either clicking **Add (+) Sequence** and selecting a sequence from the menu, or by dragging a Level Sequence from the [Content Browser](/documentation/en-us/unreal-engine/content-browser-in-unreal-engine) onto the Subsequences Track.

![add subsequence](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8f24e4f1-aba3-41f1-a8b3-bdb2dae4e51c/addsequence.png)

Once added, a subsequence section will display the name of its corresponding Level Sequence and the number of tracks contained within it.

![subsequence information](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ef08a1e0-e967-44ff-b52f-438a5ca02269/subsceneinfo.png)

## Working in the Subsequence

Once a subsequence is added to a sequence, it can be opened by double-clicking its section. When you open a subsequence in this way, it will be displayed within the context of the parent sequence. This means it continues to evaluate tracks from the parent in order to provide the full scene context, even though the current Sequencer view only shows the subsequence.

![subsequence context](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fbf0bc5f-4f07-4dc0-a8db-1ae9a4ced132/subscenecontext.gif)

When viewing subsequences from the parent sequence context, start and end times will be displayed for both the base subsequence, and the trimmed subsequence. In this example, you can see a subsequence with both the **Start** and **End** times being trimmed in the parent sequence, and how that information is displayed in the subsequence.

![subsequence trim view](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/eddd596a-2422-4da2-a5f3-ccd3e4c5c323/subscenetrimview.png)

1.  The trimmed area. This is the region that will be played from the parent sequence.
2.  The full playable sequence area. This area has been trimmed, and will not play in its entirety.

Conversely, you can also trim the **Start** and **End** times within a subsequence and observe the trimmed region from the parent sequence.

![subsequence trim view](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/03ee3b06-c6b2-4551-9903-fb8a95f0365d/internaltrim.png)

This context view can be enabled or disabled by toggling **Evaluate Sub Sequences In Isolation** from Sequencer's [Playback Menu](/documentation/en-us/unreal-engine/sequencer-cinematic-toolbar-in-unreal-engine#playbackoptions).

When working within subsequences, you can add tracks, keyframes and other content as with any other sequence, and can preview the results alongside the contents in the parent sequence. As such, subsequences are not only useful for limiting file conflicts, but also for compartmentalizing Sequencer content within different subsequences.

![subsequence light](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a8e084d4-1309-4447-b9b9-1ae1b2c2cfa5/lightexample.png)

Unlike [Shots](/documentation/en-us/unreal-engine/sequences-shots-and-takes-in-unreal-engine#shots), multiple subsequences that are stacked in Sequencer will not overwrite the bottom ones. All subsequences will evaluate when played at the same time.

### Collaboration

As subsequences affect a different Level Sequence from the main sequence, multiple artists can work on a single cinematic at the same time without any file conflicts occurring. In this example, you can see two different subsequences being used to contain content from both the **Visual Effects** and **Lighting** disciplines.

![sequencer artist collaboration](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c4cf7c06-bc7d-42a1-95d0-c68af4f48c51/collaboration.png)

### Hierarchical Bias

Due to the nature of the Root Level Sequence, Shot, and Subsequence systems, there may be cases where the same Actor is being referenced by both the shot and the Root Level Seqeunce, which can cause conflicts. **Hierarchical Bias** can be used to arbitrate which reference of that Actor should be prioritized to evaluate over other sources. This property is found when right-clicking **Shots** or [Sub Sequence](/documentation/en-us/unreal-engine/cinematic-subscequences-track-in-unreal-engine), navigating to the **Properties** menu, and locating **Hierarchical Bias**.

![set hierarchy bias value in shots properties menu](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2f8db512-d5ef-4ce8-9594-5b0b84059d11/hierarchicalbias.png)

Increasing the bias number on a source will cause that source to "win", decreasing the number will cause it to "lose", and having equal bias between sources will cause all sources to evaluate together and blend when possible.

The default value for Hierarchical Bias on the top-level (root) sequence is **0**, while for subsequences it is **100**. This causes shot sources to take precedence over Root Level Seqeunce sources. Bias also compounds for each subseqeunce layer added, so if a shot sequence contained a child Sub Sequence, then it would have a total bias of **200** (100 + 100), causing the deepest level of influence to "win'' by default.

This effect is demonstrated in the image below, where:

1.  The root sequence, which has a default bias of 0, and cumulative bias of **0**.
    
2.  The first child sequence, which has a default bias of 100, and cumulative bias of **100**.
    
3.  The second child sequence, which has a default bias of 100, and cumulative bias of **200**.
    

#### Bias Example

The following example demonstrates how to utilize Hierarchical Bias values in your sequences.

A **Light Actor** is placed in a Level, and is referenced by three different sequences:

-   The **Root Level Sequence** references this light, and its color is keyframed to **red**.

![root level sequence bias 0 red light](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/73659617-26eb-40bc-aa80-3d37f3f5af32/red.png)

-   Within the Root Level Sequence is a **Shot**, and its color is keyframed to **green**.

![shot sequence bias 100 green light](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4e42e144-9783-491f-beb5-b82da83d32a4/green.png)

-   Within the Shot, is a [Sub Sequence](/documentation/en-us/unreal-engine/cinematic-subscequences-track-in-unreal-engine), and its color is keyframed to **blue**.

![sub sequence bias 100 cumulative bias 200 blue light](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ed82e75f-e71c-4fb2-ba2b-17eef008bda0/blue.png)

By default, the **Sub Sequnce**, and **blue** light take priority, because it has the largest cumulative bias. For reference, each sequence's bias value is listed below:

-   Root Level Sequence = **0**
    
-   First child sequence = **100**
    
-   Second child sequence = **200** (**100** + **100**)
    

![root level sequence is keyed red but displays blue due to bias](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/440fcb3d-02f8-4a65-897e-cf0ff2c5e9f5/rootsequenceblue.png)

If you right-click the Sub Sequence section and lower its hierarchical bias to **\-50**, then that will cause the **Shot**, and **green** light to take priority. This is because the Sub Sequence's cumulative bias is now smaller than its parent, causing the green light to have the largest bias.

At this point, each sequence's bias value would be:

-   Root Sequence = **0**
    
-   First child sequence = **100**
    
-   Second child sequence = **50** (**100** - **50**)
    

![negative bias reduces an assets influence](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fa04aadf-ed97-418c-9633-2e3eb0f4a3b2/negativebias.png)

Setting all the bias values to **0** will cause all sequences to evaluate together and the results will be blended. In this example, the red, green, and blue light color values are combined, becoming **white**.

At this point, each sequence's bias value would be:

-   Root Sequence = **0**
    
-   First child sequence = **0**
    
-   Second child sequence = **0** (**0** + **0**)
    

![setting all bias to zero will blend shots evenly](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a64c6d36-5386-46bd-8e6a-9193807924c1/zerobias.png)

## Section Editing

Each subsequence section functions similar to most [Sections](/documentation/en-us/unreal-engine/creating-animation-keyframes-in-unreal-engine#sections), meaning they can be moved, trimmed or edited.

![edit trim subsequence](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/19719eda-8401-403f-87e2-4cf2c8115017/subsceneedit.gif)

To differentiate your subsequences from one another, you can change the color that is displayed on all sections in a track by clicking the color bar on the track header. This will open the **Color Picker** from which you can select a new color for this track.

![subsequence color](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8b510519-c763-481c-a8b1-3d0f854f4dcd/subscenecolor.gif)

### Looping

When extending the section beyond its default time, it expands the sequence's playback range in a linear fashion. If you want to loop the sequence instead, right-click on the section and enable **Properties > Can Loop**.

![loop subsequence](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/75275e99-1bb5-4bfe-a7e7-4f5b602ed1df/looping.gif)

## Properties

Right-clicking a subsequence section and navigating to the **Properties** menu will reveal the following properties:

![subsequence properties](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1b9a36c6-4fca-4b65-8be5-cb633d1c63ca/properties.png)

| Name | Description |
| --- | --- |
| **Time Scale** | Controls the playback rate of the subsequence. A value of 1 will result in a normal playback speed, larger numbers will play faster, and smaller numbers will play slower. |
| **Hierarchical Bias** | Controls the [Hierarchical Bias](/documentation/en-us/unreal-engine/cinematic-subscequences-track-in-unreal-engine#hierarchicalbias) of the subsequence. Larger numbers will cause this subsequence to take priority over other sources when referencing the same Actors. |
| **Sub Sequence** | The sequence asset that is played by this subsequence. |
| **Network Mask** | The network realm that this subsequence is hosted on. This can be set to **Client**, **Server**, or **Both**. It is important to set this appropriately depending on your sequence's content. For example, if a subsequence contains only audio, then it should usually be set to **Client** only as audio is not played over the server. |