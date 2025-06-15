# Connecting Unreal Engine to Motionbuilder with Live Link

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/live-link-stream-motionbuilder-to-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/live-link-stream-motionbuilder-to-unreal-engine)  
**Processed:** 2025-06-14 16:34:00

---

Using Live Link, you can stream content from MotionBuilder into Unreal Engine in real time, in order to preview your content in Unreal without needing to export and import. There are also a variety of settings for controlling the session's IP address and casting.

![motionbuilder live link unreal](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/edada165-cff7-49cf-bfdc-3bc03e4d0980/overview.gif)

This document provides an overview of how to set up a Live Link session between MotionBuilder and Unreal Engine, as well as the settings available to you.

#### Prerequisites

-   You have read **[Live Link](/documentation/en-us/unreal-engine/live-link-in-unreal-engine)** and have enabled the **Live Link** plugin.
    
    ![live Link plugin](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/db4de85f-c815-4ebb-9aeb-d9e2e9f28da6/plugin.png)
-   You have a Skeletal Mesh Actor for use in Unreal Engine and MotionBuilder. If you do not have one, then you can create a project using the [Third Person Template](/documentation/en-us/unreal-engine/third-person-template-in-unreal-engine), and [**Export the SK\_Mannequin**](/documentation/en-us/unreal-engine/working-with-assets-in-unreal-engine#assetactions) Skeletal Mesh to FBX in order to **[Import to MotionBuilder](https://help.autodesk.com/view/MOBPRO/2022/ENU/?guid=GUID-EE540CA9-C320-44C1-B1A5-528A1CB52726)**
    
-   You can optionally **[Characterize](https://knowledge.autodesk.com/guidref/MOBPRO/2022/learn-explore/GUID-84A1329D-FBB5-483A-86BA-2F54248D0309)** your character in MotionBuilder in order to use the Control Rig.
    

## MotionBuilder Setup

Follow these steps to set up Unreal Live Link in MotionBuilder and begin broadcasting a Live Link signal.

### Install Plugin

You will need to download and install the MotionBuilder Live Link plugin. To do this, first using this link: [GitHub - ue4plugins/MobuLiveLink: Plugin for MotionBuilder that send data to Unreal Engine](https://github.com/ue4plugins/MobuLiveLink).

On that page, click \*Releases\*\*.

![MotionBuilder Live Link plugin GitHub page Releases link](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4c62f74f-0c59-4427-bbf9-7e59e09069f6/github-mobu-releases.png)

You can now choose the plugin version appropriate for whatever version of Motionbuilder you are currently using. Download the file, and extract it at a convenient location.

![MotionBuilder Live Link plugin release versions list](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6091fe82-280c-4bb0-8f61-773b86360601/github-mobu-release-list.png)

Now you will assign the plugin path to MotionBuilder. In MotionBuilder, click **Settings > Preferences** in the main menu bar to open the **Preferences** window, and navigate to the **SDK** category. Click **Add** then browse to the location of the extracted folder containing your MotionBuilder plugin. Restart MotionBuilder afterward.

![install motionbuilder plugin](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fc0931d7-8228-4a09-8b37-41c029f6de3d/mobusdk.png)

After restarting MotionBuilder, you should now see the **UE - LiveLink** entry in the **Devices** category of the **Asset Browser** tab.

![UE LiveLink devices](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b80c29be-395f-4e95-90b0-b01ed9c142db/devices.png)

### Broadcast Live Link

Ensure your MotionBuilder scene contains the characters you want to use, then drag the **UE - LiveLink** plugin into the viewport.

![drag drop plugin](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/76f9f701-7e5d-4945-8ecd-2661cfaad393/dragplugin.png)

This will open up the **Live Link Connection** window, which you can find under the **Devices** section of the **Navigator**.

![motionbuilder live link window](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ded85724-358f-448e-8fc6-3e7c86246eae/livelinkmobuwindow.png)

Click the **Subject Selector (...)** button, expand and select your character's **Root Bone**, then click **Add**. You must ensure the selected root bone also matches the root (top-most) bone from the imported **[Skeleton](/documentation/en-us/unreal-engine/skeletons-in-unreal-engine)** in your project.

![add live link subject](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ec05a029-f0be-411b-8983-fd56a08c6479/subjectselector.png)

This will add your character as a **Subject** to stream over to Unreal Engine. You can optionally enable **Stream Viewport Camera**. This will make MotionBuilder's camera streamed as a Live Link subject to Unreal Engine, from which you can select it as a source to drive the editor camera.

![stream viewport camera](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d398ecc6-37da-4559-9af9-e9a7bdd30f53/subject2.png)

You can optionally rename your Subject by editing the **Subject Name** field. This will help distinguish it in the Live Link broadcast.

![live link subject name](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/02e65204-29a0-4717-aaa4-40929838759e/subject3.png)

Click the button next to **Online** to enable content streaming. The Online status button will change from **red (Offline)** to **green (Online)**. At this point, MotionBuilder is now broadcasting a Live Link signal.

![live link online](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fc5c07a6-59be-45d2-8950-f050f966d409/online.png)

When MotionBuilder loses focus and becomes a background application, its performance will be throttled, which could lead to stuttering during the streaming process. To prevent this from occurring, enable the **Always refresh viewer** option, located in the Navigator's **System** menu.

![always refresh viewer](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/586d30b5-8274-4dff-b8a7-9bb5c3d9e65f/refreshviewer.png)

## Unreal Engine Setup

Follow these steps to connect Unreal Engine to your MotionBuilder Live Link broadcast, in order to preview the connection on a character.

### Setup Connection

With MotionBuilder running in the background, open Unreal Engine and select **Window > Live Link** from the main menu bar. This will open the **Live Link Connection Window**, which will enable you to connect to the running instance of MotionBuilder.

![live link connection window](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b031f9bc-3597-4c43-b0fc-39ab1e678577/livelinkwindow.png)

Click the **\+ Source** button, then select your MotionBuilder broadcast signal from **Message Bus Source**.

![live link](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ad76b5d0-6e3d-408a-bf52-8c25d2b19768/addsource.png)

The Connection Window will update to show the connected Source Type, Subjects, and Status.

![live link connected](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/50a150b0-e4db-461b-86f3-db9bfa30fe20/livelinkconnected.png)

Refer to the **[Live Link Overview](/documentation/en-us/unreal-engine/live-link-in-unreal-engine)** page for more information on Live Link **Options**, **Roles** and **Status Indicators**.

### Preview Live Link

You can now preview the Live Link connection on your character. Open your character's **Skeletal Mesh** asset from the **Content Browser**.

![skeletal mesh](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/31670f2b-797c-435d-9b70-c2fe3eb1fb2a/opensk.png)

In the **Preview Scene Settings** tab, set the following properties:

-   Preview Controller: **Live Link Preview Controller**
-   Subject Name: ***Subject name from MotionBuilder***
-   Enable Camera Sync: **Enabled**

![skeletal mesh live link preview](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8e9dd6be-188c-4003-bcde-7994d022df72/sksettings.png)

Your MotionBuilder Subject is now connected to this window and will stream data. The MotionBuilder viewport will also stream to this view if **Enable Camera Sync** and **Stream Viewport Camera** are enabled from MotionBuilder.

![skeletal mesh live link preview](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c30c283c-f9c5-401e-9735-538ad2c8006d/overview.gif)

You can alternatively use **[Blueprint functions](/documentation/en-us/unreal-engine/using-live-link-data-in-unreal-engine)** to establish a connection instead of manually connecting through the Live Link window. Instead of using a Preview Controller, you can also use a **[Live Link Component](/documentation/en-us/unreal-engine/live-link-in-unreal-engine#livelinkcomponents)** attached to an Actor, or the **Live Link Pose** node in an Animation Blueprint.

## MotionBuilder Settings

The MotionBuilder Live Link Plugin contains various advanced settings for controlling your Live Link casting behavior. To access these settings, click the **Settings** tab in the **Live Link Connection** window.

![motionbuilder settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9040e715-c73c-4eea-a133-9afd304efd60/advancedsettings.png)

### Linking to Other Machines

By default, using Live Link to connect MotionBuilder to Unreal Engine works as long as the session is running on the same device. If you are on a local area network where multiple devices are being used, and you want to broadcast to a different device, then you will need to use **Unicast** and **Static Endpoints** with explicit Local **IPv4 Addresses** set on them.

The **Unicast Endpoint** can be considered as one end of the Live Link bridge, whereas **Static Endpoints** are the other end of the bridge. Together they form an active Live Link connection.

To set up a Unicast Endpoint, copy your **IPv4 Address** into the **Unicast Endpoint** property. To get your IPv4 Address, you can type "ipconfig" into a **Windows Command Prompt** window to view and copy it. You must also specify a **port number** at the end of the address.

![unicast endpoint](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/47f0c213-f0bf-4ae7-8bed-b348a31fe85b/unicast.png)

Port **6666** is reserved and cannot be used for Motion Builder Unicast Endpoints.

In Unreal Engine, on the other receiving PC, open the **[Project Settings](/documentation/en-us/unreal-engine/project-settings-in-unreal-engine)** window by clicking **Edit > Project Settings** and navigate to the **UDP Messaging** panel. In the **Transport** category, expand the advanced details and input the same address and port from the host machine's **Unicast Endpoint** in the **Static Endpoints** property.

![static endpoint](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/dec58ae5-5a81-4055-8646-ce90e1a9653e/staticend.png)

You should now be able to receive the remote Live Link source when adding sources to the Live Link Connection Window.

![remote live link source](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e6c9c35d-7afe-471c-8fca-bb37bf5208e7/addsourceremote.png)

The inverse of this process will work as well. You can instead set a **Unicast Endpoint** in the **UDP Messaging Project Setting** and set the **Static Endpoint in MotionBuilder**.

![static unicast endpoint](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/336cd65b-4d08-427a-a7ad-165c9fd9c270/reverseconnection.png)

### Broadcast Satellites

Rather than a single MotionBuilder live link instance broadcasting to multiple Unreal Engine destinations at the same time, you can set up a single Unreal Engine receiver to re-broadcast the live link source to other machines. This can be useful if the live link source is located far away from all receivers, or has limited bandwidth.

![unreal rebroadcast live link signal](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/630caf2d-15b7-41b5-b590-ba4bae29c48b/satellite.png)

To enable this behavior, first select your live link **source** and **subject** in the **Live Link Connection Window** and enable **Rebroadcast Subject**.

![rebroadcast subject](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5b20c43e-5301-4135-8d63-8c006df2cc9e/rebroadcast.png)

The second checkbox associated with Rebroadcast Subject is used with Live Link Hub. You must select both checkboxes to enable Rebroadcast Subject.

Next, you will need to set a **Unicast Endpoint** in the **UDP Messaging Project Setting** on the machine that is performing the rebroadcast**.**

![rebroadcast unicast endpoint](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4cc94590-3a0a-45ba-9245-ddb00f815e5c/rebroadcast2.png)

Now when selecting Live Link sources from other machines, you can choose the re-broadcasted source from an Unreal Engine instance.

![rebroadcast live link](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/55718ba1-23fd-41f5-ac1f-db4b2b8ceaa2/rebroadcast3.png)

### Multicast

Multicast is an internet specification through which clients can participate in network communication. Multicast is represented using **Class D** addresses which are different from the standard class address space that you usually see in endpoint to endpoint communication. Multicast addresses range from 224.0.0.0 and to 239.255.255.255.

Clients can subscribe to the multicast group that tells the router, switch, or operating system that it is interested in multicast messages on that given IP. Unreal Engine uses multicast group **230.0.0.1** at port **6666**. On startup, Unreal Engine will transmit a signal to the network that it would like to join the 230.0.0.1:6666 multicast group. Any multicast message received with that specified IP and port will then be assigned to that Unreal Engine instance inbound socket for processing by the engine.

The purpose of the multicast address is to notify other Unreal Engine instances about the presence of other Unreal Engine instances on the network. This is done using a discovery message that is sent on the multicast socket. The discovery message will be received by the other instances and contained within that message is the specific IP or port that can be used to directly communicate with the Unreal Engine instance. Direct communication will then occur using this known endpoint (IP and port) and no further communication will occur over the multicast group. This is equivalent to manually adding the static endpoint. The multicast mechanism enables this automatically.

Typically most routers will not propagate multicast messages beyond the local area network (LAN) unless they are configured to do so. In most cases, you can only discover Unreal Engine instances on the same local area network.

Live Link is generally not aware of multicast communication when it is happening. All of this network communication occurs through the message bus and using UDP messaging. Live Link is made aware of the available endpoints through its interaction with the message bus and when sending its own discovery message over the message bus framework. All of the endpoints that have been discovered will be made available to Live Link as receivers and Live Link will send its discovery message to those receivers.

#### Change Multicast Range

If you want to change the multicast range group, it will need to be changed in both the **UDP Messaging Project Settings** and the **Live Link plugin Engine.ini** file.

You can locate **Multicast Endpoint** in the UDP Messaging Project Setting.

![multicast](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/958f367d-c8ab-4481-b70a-82f42ad54dc6/multicast1.png)