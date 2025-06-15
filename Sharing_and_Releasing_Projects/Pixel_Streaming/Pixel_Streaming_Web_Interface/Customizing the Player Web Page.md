# Customizing the Player Web Page

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/customizing-the-player-web-page-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/customizing-the-player-web-page-in-unreal-engine)  
**Processed:** 2025-06-14 16:18:23

---

Information about customizing the frontend has been moved to the [Pixel Streaming Infrastructure](https://github.com/EpicGamesExt/PixelStreamingInfrastructure/tree/master/Frontend)

## The Frontend

The frontend refers to the HTML, CSS, images, and JavaScript / TypeScript code that runs in web browsers and allows them to connect to Unreal Engine Pixel Streaming applications and interact with them. The frontend library is the foundation that developers can modify and extend to suit the needs of their Pixel Streaming experience.

Default frontend.

Frontend settings panel.

Frontend lightmode with settings panel.

Frontend with an active stream connection.

## Where

Our new Pixel Streaming Infrastructure repository contains all of the up to date information regarding the frontend elements of Pixel Streaming. If you want to customise the Pixel Streaming frontend, head to [Customizing the Player Web Page](https://github.com/EpicGamesExt/PixelStreamingInfrastructure/tree/master/Frontend)

## Why

Moving the "Customizing the Player Web Page" documentation to the Pixel Streaming infrastructure means we can provide more frequent and on the fly updates, separate from release of Unreal Engine. As the Pixel Streaming frontend evolves, we'll update the relevant information accordingly. Make sure to check back on the infrastructure frequently for new information on the frontend.

## Changes from Previous Versions

In the past, the Pixel Streaming frontend relied on two monolithic Javascript files, `app.js` and `webrtcplayer.js`. This was hard for users to extend upon and was poor reference material for those trying to modify the frontend. Additionally, this was difficult for us to maintain.

As of Unreal Engine 5.2, these have now moved to a TypeScript library in which the frontend is modularised and easily extensible.

For users on any version prior to Unreal Engine 5.2, the transition will be substantial, but for all subsequent versions our intent is to have a stable API surface and utilise semantic versioning for our releases.