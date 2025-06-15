# Media Framework

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/media-framework-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/media-framework-in-unreal-engine)  
**Processed:** 2025-06-14 16:35:29

---

![A GIF showing media playing inside Unreal Engine](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f3bf4143-807c-4e22-8765-7957208c9b81/mediaframework.gif)

While there is currently a **Startup Movie Player** system in UE, it can only be used for playing startup movies while the Engine loads up. It cannot be used to play movies in-game, say for instance as part of a UI element or perhaps on a Static Mesh in your level like a movie playing on a TV. This is where the **Media Framework** comes in, as not only will it allow you to do both of the examples presented above, it will also provide much more general media playback capabilities (outlined below) and is also scheduled to replace the deprecated Startup Movie Player framework in a future engine release.

The Media Framework in Unreal Engine is:

-   Both Engine & Slate Agnostic
-   Able to support Localized Audio & Video Tracks
-   Accessible in the Content Browser, Material Editor, & Sound System
-   Available for use with Blueprint & the UMG UI Designer
-   Able to support Streaming Media
-   Able to Fast Forward, Reverse, Play, Pause, & Scrub Media
-   Able to support Pluggable Players

As stated above, the Media Framework itself is both Engine and Slate agnostic, which means it can be used in pretty much any application not just the game engine or the Editor. There are layers on top of the framework that provide media playback capabilities to other sub-systems as well, such as **Engine**, **Blueprints**, **Slate**, and the **UMG UI Designer**. This will cover most expected use cases, such as in-game textures & UI, in-Editor video tutorials, and Marketplace videos.

This page contains several links to additional documentation regarding Media Framework. It is recommended that you check out the Overview page for more of a breakdown of the features of Media Framework as well as the How-To and Quick Start pages for step-by-step instructions to working with Media Framework.

## Essentials