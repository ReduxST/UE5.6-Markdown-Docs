# Remote Control Presets and Web Application

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/remote-control-presets-and-web-application-for-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/remote-control-presets-and-web-application-for-unreal-engine)  
**Processed:** 2025-06-14 16:46:34

---

With **Remote Control Preset**, collect and organize any UI parameters or functions in a single panel and expose them to the [Remote Control API](/documentation/en-us/unreal-engine/remote-control-for-unreal-engine). These parameters and functions can be connected to widgets in a companion web application provided by the **Remote Control Web Interface** plugin to control the engine remotely. This web application has a built-in UI editor so you can customize its interface without any additional code to create or format it.

Since this is a web application, you can run multiple clients at the same time. Any properties that are modified in one client will have their changes propagated through the web server to all the other clients. This can help create a collaborative workflow in a live environment.

![GIF of light direction rotating when controlled using a Remote Control widget](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b3d2cd59-259a-40fb-a17f-7d06c42e692d/rem-con.gif)