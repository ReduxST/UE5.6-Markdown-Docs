# Time Dilation Track

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/cinematic-playback-rate-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/cinematic-playback-rate-in-unreal-engine)  
**Processed:** 2025-06-14 16:13:12

---

The **Time Dilation Track** allows you to speed up or slow down a Cinematic Sequence. Keyframes can also be added in order to add a time warp effect to the sequence.

This document explains how to create, use, and understand the Time Dilation Track.

#### Prerequisites

-   You have already created and opened a Level Sequence asset.
    
-   You have an animated Actor in Sequencer to preview the Time Dilation effect.
    

## Creation

To create a Time Dilation Track, click **Add Track (+)** and select **Time Dilation Track**.

![Time Dilation](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a422b1ae-b31c-42bb-a1af-6110b7db9c42/createtd1.png)

The Time Dilation Track creates with a value of **1.0**, which is the default speed of the game simulation.

![Time Dilation](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8e2ef906-4598-4e8a-b912-b7abd31dd5cf/tddefault.png)

## Usage

You can preview different play rates by changing the track's value while playing the sequence.

![time dilation warp](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8d2660b6-02cc-454d-b351-0af6a0d7d657/tdaffecttime1.gif)

You can also set keyframes on the Time Dilation Track in order to create a time warp effect for your sequence.

Select the track and press **Enter** to add a starting keyframe, then move the Time Marker along the timeline and change the Time Dilation value. This should automatically create a new keyframe with this value set.

![time dilation warp](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/32bd38d5-db87-4ed6-8519-5081f7aa4745/tdaffecttime2.gif)

## Time Dilation Effects

The Time Dilation Track affects more than just the Tracks contained within your Cinematic. It also slows down the global time scale of all simulations in your Level. This means that any materials, particles, or other dynamic objects in your Level will have their simulation speed affected by the Time Dilation regardless of whether they are referenced by Tracks in your sequence or not.

The example below shows the Time Dilation Track affecting the **speed of a particle simulation**, as well as the **panning texture** of the background clouds. These assets are not being directly referenced by any Tracks in Sequencer.

![time dilation world level](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cd09a2b2-81df-4e52-87c4-8459fce14f0a/tdaffectworld.gif)