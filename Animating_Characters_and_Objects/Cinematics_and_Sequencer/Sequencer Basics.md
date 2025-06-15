# Sequencer Basics

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/how-to-make-movies-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/how-to-make-movies-in-unreal-engine)  
**Processed:** 2025-06-14 16:29:11

---

This guide explains the basics of setting up **Sequencer** to create cinematics and event triggers in Unreal Engine.

## What is Sequencer?

Sequencer is Unreal Engine's cinematic editor for animating characters, cameras, properties, and other actors over time. It has a non-linear editing environment where you can create and modify tracks and keyframes along a timeline.

For an overview of Sequencer and its primary features, see [Sequencer Overview](/documentation/en-us/unreal-engine/unreal-engine-sequencer-movie-tool-overview).

![What is Sequencer](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8b6ca070-fddf-4bb9-8612-f8cfdc2233ac/whatis.gif)

## How to Create and Open Sequencer

Sequencer requires the creation of a **level sequence asset**. The asset is saved in the [Content Browser](/documentation/en-us/unreal-engine/content-browser-in-unreal-engine) and referenced by a **level sequence actor** to bind Sequencer's data to the level.

![Level Sequence Asset](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d6f13bae-0c80-4a49-be8a-8de27538deb0/sequenceasset.png)

To create a level sequence, use one of the following methods:

-   Click the cinematics icon in the [main toolbar](/documentation/en-us/unreal-engine/unreal-editor-interface) and select **Add Level Sequence**.
-   In the Content Browser, right-click an open area and select **Cinematics > Level Sequence**.

![Create Sequence](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ebbb1c16-6495-448b-8fa3-f19af40e5d67/createseq.png)

To open Sequencer, double-click any level sequence in your project. The **Sequencer Editor** will open at the bottom of the Unreal Editor.

![Sequence Open](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6b60fd77-8c0c-4f6e-abce-e9dceaddf151/seqopen.png)

## How to Create Content with Sequencer

The following guides show common actions you can perform with Sequencer.