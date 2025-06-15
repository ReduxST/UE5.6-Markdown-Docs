# Remote Control

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/remote-control-for-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/remote-control-for-unreal-engine)  
**Processed:** 2025-06-14 16:46:30

---

Unreal Editor offers a powerful set of tools for working with nearly every aspect of your Project's content. However, in some situations, using the Engine successfully as part of a larger content editing process requires making changes in the Project from outside the Editor UI. For example, broadcast TV and film productions need to offer operators easy and rapid control over a limited set of common capabilities, which they need to access through a custom UI that integrates with other software they use in the pipeline.

The Remote Control system makes this possible by running a web server inside the Unreal Engine that services WebSocket messages and HTTP requests made by remote web applications through a REST-like API.

In the right scenario, this offers several benefits:

-   You can create entirely new UIs that interact with Project content, focusing on the objects and properties that have meaning for your specific use case.
-   You can integrate these custom UIs with third-party applications you already use, or as a part of other web apps that you create for your organization.
-   You can operate the Engine remotely, from a different computer or mobile device that is connected to the same network as the computer running Unreal.

## What Can It Do

The Remote Control API offers a similar level of control over the Unreal Editor and the Project Content to what you have when working in Blueprint and Python.

-   Your web application can call any function that is exposed to Blueprint and Python.
-   Your web application can read and write the values of any properties exposed to Blueprint and Python or a **Remote Control Preset**.

Without any coding, you can expose Project Content to the Remote Control API through a **Remote Control Preset** and connect them to widgets in a companion web application. See [Remote Control Presets and Web Application](/documentation/en-us/unreal-engine/remote-control-presets-and-web-application-for-unreal-engine) for more details.

With some ingenuity and web development skill, you can use these relatively simple building blocks as a basis for constructing your own rich editing tools.

Remote Control is disabled by default in [packaged](/documentation/404) projects or in `-game` to accomodate virtual production workflows. You can enable Remote Control by adding the following flags to the command line when launching the instance of the project.

```
	`-RCWebControlEnable -RCWebInterfaceEnable`
Copy full snippet
```
\-RCWebControlEnable -RCWebInterfaceEnable

## Getting Started

## Reference