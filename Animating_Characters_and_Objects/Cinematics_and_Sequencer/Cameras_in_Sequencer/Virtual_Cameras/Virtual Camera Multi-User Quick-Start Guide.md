# Virtual Camera Multi-User Quick-Start Guide

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/virtual-camera-multi-user-quick-start-guide-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/virtual-camera-multi-user-quick-start-guide-in-unreal-engine)  
**Processed:** 2025-06-14 17:03:10

---

You can use a **Multi-User** **Virtual Camera** (**VCam**) workspace to control and render Vcams in the same scene using multiple workstations. This lets multiple users simultaneously work on the same scene. **Multi-User Vcam** Multi-User Actor Replication feature, which is in beta.

Multi-User Vcam can only be used in Virtual Production projects.

This document provides an example workflow, which you can use to set up a connected work environment that enables [multiple users](/documentation/en-us/unreal-engine/multi-user-editing-in-unreal-engine) to operate [VCams](/documentation/en-us/unreal-engine/virtual-cameras-in-unreal-engine) in the same scene simultaneously.

#### Prerequisites

-   Enable the **Multi-User Editing** [Plugin](/documentation/en-us/unreal-engine/plugins-in-unreal-engine). In the **Menu Bar**, navigate to **Edit** > **Plugins**, and locate the **Multi-User Editing** plugin under the **Editor** section. Alternatively, you can use the **Search Bar**. After enabling the plugin, restart the editor.

![The Plugins window showing the Multi-User Plugin](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a2ee369a-a69e-4f77-b126-17043cd29da8/mu-plugin.png)

-   You must have a functional **Virtual Production** project. If you do not have one, you can use the [Template](/documentation/en-us/unreal-engine/working-with-projects-and-templates-in-unreal-engine) project.
    
-   You must have a **Multi-User Editor Server**. For more information, refer to the [Multi-User Quick Start Guide](/documentation/en-us/unreal-engine/multi-user-editing-in-unreal-engine).
    
-   Your project must have a [Virtual Camera (VCam) Actor](/documentation/en-us/unreal-engine/virtual-cameras-in-unreal-engine).
    

#### Launching an MU Session

Replication of a virtual camera between instances of Unreal Engine uses Multi-User Editing. All clients must be in a shared Multi-User (MU) session. For more information on joining an MU, session see [Multi-User Editing in Unreal Engine](/documentation/en-us/unreal-engine/multi-user-editing-in-unreal-engine)

#### Replicating a VCam Actor

When a VCam actor is added to the scene in an MU session, the actor is displayed in the editor on every client. This is because no client has declared that it is the author of the VCam’s properties.

To declare authorship over a VCam, tap or click the **Multi User** button in the lower left corner of the VCam. This disables the output providers and modifier stack evaluation on the other clients, which hides the HUD and ensures that this client determines the values used by the Vcam. Tapping again relinquishes authorship and enables the output providers, HUD, and modifiers on every client so that a new client can claim authorship.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e2f1057e-502c-4556-b3cf-7501b63843a4/mu-vcamhud.png)

#### Recording Remotely

To record a Virtual Camera on a machine other than its host machine, you must add its respective Record Camera (named \[VCamActorName\]\_Record) to [Take Recorder](/documentation/en-us/unreal-engine/record-gameplay-in-unreal-engine), rather than the VCamActor itself.

## Legacy Roles for MU

The legacy Virtual Camera Multi-User workflows are deprecated, but still function in Unreal Engine 5.4.

This workflow does not support new, high-frequency replication

This section provides an example workflow for using the legacy system for limited, low-frequency virtual camera operation in Multi-User mode.

#### Prerequisites

-   Enable the **Switchboard** [Plugin](/documentation/en-us/unreal-engine/plugins-in-unreal-engine). In the **Menu Bar**, navigate to **Edit** > **Plugins** and locate the **Switchboard** plugin under the **Virtual Production** section. Alternatively, you can use the **Search Bar**. After enabling the Plugin, restart the editor.

![image alt text](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ec9993d2-a8dc-4cad-b7f3-9301d24a9357/plugin.png)

You can access the Switchboard application using the Icon in the Unreal Engine Toolbar, after the plugin has been successfully installed.

![image alt text](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a00d363e-fbe6-46d4-8c5d-853095063816/icon.png)

-   You must have a functional **Virtual Production** project. If you do not have one, you can use the [Template](/documentation/en-us/unreal-engine/working-with-projects-and-templates-in-unreal-engine) project.
    
-   You must have a **Multi-User Editor Server**. For more information, refer to the [Multi-User Quick Start Guide](/documentation/en-us/unreal-engine/multi-user-editing-in-unreal-engine).
    
-   Your project must have a [Virtual Camera (VCam) Actor](/documentation/en-us/unreal-engine/virtual-cameras-in-unreal-engine).
    

## Declare Virtual Production Roles

The **Switchboard** application requires each user to occupy a **VP Role**, such as an **Editor** or **Render**, to differentiate and identify which user is associated with which [VCam Actor](/documentation/en-us/unreal-engine/virtual-cameras-in-unreal-engine).

1.  On your primary workstation in the Unreal Editor, navigate to the Toolbar, and select the **VP Roles**, then select (**+**) **Add Role** from the drop-down menu. Give the new role a name. In this workflow example the primary workstation is named Editor.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fbfaba06-6a7b-49bd-b46b-1b2e08d6cc6d/addnewrole.png) ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3eb1705d-860b-4e1a-8866-473012869138/editorprodrole.png)
2.  Using the same steps, add a second **Role** for your secondary device to occupy. In this workflow example, the secondary workstation is named Render.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/44d66b75-4608-400a-b75f-fda481bd802a/renderprodrole.png)
3.  In the **Menu Bar**, navigate to **Edit** > **Project Settings**, and under the **Multi-User Editing** section,set the **Validation Mode** property to **Soft**, using the drop-down menu.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e7c959b4-3377-4fb1-981b-566175874b4d/softauto.png)

If your project contains any dirty packages, an error prompt displays when you join a multi-user session. You then have the opportunity to cancel the connection or to fix any present issues. If you choose to proceed any dirty packages will be deleted.

Your project is now ready to connect other devices using Switchboard for multiple users to operate VCams simultaneously in the same scene.

For more information about connecting multiple users using the **Switchboard** plugin, refer to the [Switchboard](/documentation/en-us/unreal-engine/switchboard-in-unreal-engine) and the [Switchboard Quick-Start Guide](/documentation/en-us/unreal-engine/switchboard-quick-start-for-unreal-engine) documentation.

## Connect Your Devices

After creating your VP Roles in the Unreal Editor, use the Switchboard application to connect your devices to the Multi-User session.

1.  In the Toolbar, click the options menu next to the Switchboard button, and select **Launch Switchboard Listener.**
    
    ![image alt text](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6b2ed0ea-2a30-4540-94c5-7b1649ceb821/listener.png)
2.  In the Toolbar, launch the **Switchboard application**.
    
    ![image alt text](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2ac7f72d-3058-452f-bf86-07ea17483836/launch.png)
3.  In the **Add Device** drop-down, select **Unreal**. This creates a new Switchboard Device, which represents the primary workstation.
    
    ![image alt text](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/73305afa-28ea-42a6-ab84-69544ef45233/mu-switchboard-createdevice.png)
4.  In the provided field, set the **Name** and **IP Address** for the primary work station. The name must be the same name as the primary workstation role set in Unreal Engine. This workflow example uses **Editor** as the name.
    
    ![image alt text](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ce89a37f-9b0d-483a-a385-735cdf03f3a3/mu-switchboard-createdevice2.png)
5.  Repeat steps 1-3 to create a second Switchboard Device. For the second device, use the same name as the second workstation's role. Both devices should now be listed in the Switchboard application, in the **Unreal Devices** list. This workflow example uses the name **Render**.
    
    ![image alt text](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/36fa1d5e-a930-46a5-bad8-4f65f3f4d17a/enableindividual.png)
6.  To automatically open a network connection and to connect a device to the Multi-User Editor session, select the **Auto-Join** and **Network Connection** icons for each device in the **Unreal Devices** list. When a device successfully connects to the network, the **Connection Indicator** appears blue.
    
    ![image alt text](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7be3aa24-ef2e-4c72-aa97-45ea0307a26d/greenconec.png)
7.  Assign a **VP Role** to each connected device. In the Switchboard's **Menu Bar**, navigate to **Settings** > **Settings**, and scroll down to each connected device's section. In the **Roles** property, select one of the Unreal Engine **VP Roles**, for each device, using the drop-down menu.
    
    ![image alt text](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/54db017e-2a93-4398-a90d-539b8dc7917f/settingssettings.png)

You can open a **Network Connection** and enable **Auto-Join** for every listed device by using the **Auto-Join** and **Network Connection** icons in the Unreal Device's list header.

![image alt text](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4f9dd680-4f71-40a6-8a8b-0eeb541a55f4/enableall.png)

With your workstations connected, and their roles assigned, you can now launch each device and start operating VCams in a Multi-User environment.

## Multi-User Virtual Camera Operation

1.  To connect your primary workstation to the multi-user session, open the Switchboard application, go to the **Unreal Devices** list, locate the primary **Editor** device, and click the **Launch**.
    
    ![image alt text](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/24ef4258-1649-4c34-b30c-53d580722506/connect.png)
    
    Once your project has launched, you can verify that the editor is connected to the multi-user session in the **Multi-User Browser** window. You can open the Multi-User Browser in the Menu bar, navigating to **Window** > **Multi-User Browser**.
    
    ![image alt text](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1f8e3505-87ce-4f6f-b065-b7340d09702e/connected.png)
2.  In the **World Outliner**, select the **VCamActor**.
    
3.  Select the **VCam component** in the VCam actor's **Details** panel.
    
4.  Set the **Role** property to **Edit** in the **Virtual Camera** properties section and select the **Editor** VP Role from the drop down menu.
    
    ![image alt text](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d457ed0b-7829-41a1-9e0d-4d08aa575366/editvcamsettings.png)
5.  Enable the Virtual Camera by toggling the **Enabled** property.
    
6.  In the Switchboard application, launch the **Render** device by clicking the **Launch** icon. Following the steps above, verify that the secondary **Render** device is also connected to the multi-user session, using the **Multi-User Browser** window.
    
7.  Now that both editor instances are open, move the **Virtual Camera** on the primary **Editor** device and see the changes replicated in the secondary **Render** device in real time. In the example below the **Editor** device (**Left**) is operating a **VCam Actor** and the **Render** device (**Right**) is receiving the changes and rendering the scene.
    

![image alt text](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/adb35a17-d97a-4e97-a513-b0cc8b8359e3/mu-vcam-demo.gif)