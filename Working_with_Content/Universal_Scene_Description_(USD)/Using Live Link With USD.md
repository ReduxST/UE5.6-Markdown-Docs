# Using Live Link With USD

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/using-livelink-with-the-usd-importer-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/using-livelink-with-the-usd-importer-in-unreal-engine)  
**Processed:** 2025-06-14 16:59:39

---

The [Live Link](/documentation/en-us/unreal-engine/live-link-in-unreal-engine) plugin synchronizes animation assets between **Unreal Editor** and an outside *digital content creation* (DCC) tool such as Maya or Houdini, providing a fast way to preview assets as they appear in-engine. **Unreal Engine** can use **Universal Scene Description (USD)** files as part of Live Link connections and maintain them over the course of a project, improving the expedience and convenience of this workflow. This tutorial provides a walkthrough of setting up Live Link connections in Unreal Engine using USD files, and an overview of the benefits of the USD format when using Live Link.

## Overview

When you set up a Live Link connection using the **USD Stage**, it adds a custom Live Link schema to the USD prim alongside attributes that describe the connection. As long as this information remains in the USD file and both your DCC and Unreal Engine have a Live Link connection, the connection for the assets can be re-established. If either application restarts or the file was closed and reopened in the DCC, the Live Link connection will need to be re-established.

## Following This Guide

The examples in this guide use Autodesk Maya and the [Unreal Live Link V2](https://apps.autodesk.com/MAYA/en/Detail/Index?id=3726213941804942083&appLang=en&os=Win64) plugin, but any DCC toolset with Live Link integration should be able to establish a connection to Unreal Engine. Review the instructions for your DCC's Live Link integration for any differences from the workflow presented here.

If you are using the Unreal Live Link V2 plugin, the installer will also set up the **Maya Live Link** plugin for Unreal Engine. Use this instead of the standard Live Link plugin if you are using Maya.

## 1\. Required Setup

To follow this guide, you need to fulfill the following prerequisites:

-   Enable the Live Link plugin for both Unreal Engine and your DCC.
    
    -   Use the Maya Live Link plugin instead if you are using Autodesk Maya.
-   Enable the **USD Importer** plugin in Unreal Engine.
    

To set up the plugins in Unreal Engine, click **Edit** \> **Plugins** to open the **Plugins** menu, then locate the plugins and enable them. Refer to the instructions for your DCC's Live Link integration or its guide on using plugins for information about how to activate it.

This guide also uses a new project created with the **Third-Person Template**. This includes the Unreal mannequin models and their animations. These are available in the `Content/Mannequins` folder in the **Content Browser**. This guide uses these assets to provide an example, but they are not necessary to follow these instructions, and you can follow along with any Skeletal Mesh.

## 2\. Establish a Live Link Connection

1.  Open both your DCC and Unreal Editor.
    
2.  Set up your DCC's Live Link integration.
    
    -   For Maya, download and install the Unreal Live Link plugin. You can download the installer [here](https://apps.autodesk.com/MAYA/en/Detail/Index?id=3726213941804942083), and once you have installed it you can open it by clicking **File** \> **Unreal Live Link**.
3.  In Unreal Editor, click **Window** \> **Virtual Production** > **Live Link** to open the **Live Link** window.
    
    ![Open the Live Link window](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c75dd540-d85f-45d3-b536-7a85ce5c6fef/livelinkwindow.png)
4.  Click the **\+ Source** button in the **Live Link** window. Highlight **Message Bus Source** and select your DCC's **Live Link connection**.
    
    Click to enlarge image.
    
    Your DCC and Unreal Engine will connect and synchronize using Live Link. However, because no asset is synchronized, you will not see any change yet.
    

## 3\. Export a USD File and Use It to Synchronize Assets

Now that you have opened a Live Link connection, export a USD file and use that to synchronize the asset.

1.  Locate the `MM_Run_Fwd` animation in the Content Browser. You can find it in `Content/Characters/Mannequins/Animations/Manny`.
    
    Click to enlarge image.
    
2.  Right-click `MM_Run_Fwd`. Click **Asset Actions** > **Export**.
    
    ![Export the animation from the Asset Actions context menu](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5c83f2cc-9250-4a90-b780-3ee8bae81f90/exportasset.png)
3.  Export the asset using the `.usda` file format.
    
    Click to enlarge image.
    
    While you need to export your file as a `.usda` file to use the USD stage, you can also export it as a `.fbx` file for the purposes of importing it into Maya.
    
4.  In the **USD Export Options** dialog, make sure **Export Preview Mesh** is checked, then click **Export**.
    
    ![Enable Export Preview Mesh in the USD options dialog](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2d0ee262-6f30-4bda-b778-d45726794106/usdoptions.png)
5.  Open your DCC and import the `.usda` file.
    
    1.  In Maya, click **File > Import**, then select **USD Import** and choose the `.usda` file. Rotate it -90 degrees on the X axis to make it face upwards.
6.  Select the **root bone**, then add the selection to Live Link.
    
    1.  In Maya, click **File** \> **Unreal Live Link** to open the **Unreal Live Link** window.
        
        ![Open the Unreal Live Link menu in Maya](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b91aa0d5-cb40-4655-8e45-25bc583fe5cc/unreallivelinkwindow.png)
    2.  Select the **root bone** of your mesh in the hierarchy and click **Add Selection** in the Live Link window to add it to your list of Live Link subjects.
        
        ![Select the root bone in Maya](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/595d6cb7-c6af-4ee0-8716-4f10ae53cf26/selectrootbone.png)
    3.  Click the dropdown for your selection's **Type** and choose **Full Hierarchy**.
        
        ![Choose the Full Hierarchy type](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4b869881-9b4a-4f8e-9ef3-6da9d432fefe/fullhierarchy.png)
        
        You will need your Object Name in a later step when you choose your Subject Name in Unreal Editor.
        
7.  Click **Window** > **Virtual Production** > **USD Stage** to open the **USD Stage** window.
    
    ![Open the USD stage](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/837f95f4-4b8a-4f64-8b6b-68e4435acc69/usdstagewindow.png)
8.  In the **USD Stage**, click **File** \> **Open**, then select the `MM_Run_Fwd.usda` file.
    
    ![Open your animation in the USD stage](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/784d8f62-580e-4fd1-93b6-1ddd8e309709/openusda.png)
9.  In the **USD Stage**, right click the **SkelRoot** for your model, then click **Set Up Live Link**.
    
    ![Set up the Live Link for your animation](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/67a8fe68-1f82-435e-b3bc-6114aec13970/setuplivelink.png)
    
    The **Live Link integrations** panel appears, and shows **DefaultLiveLinkAnimBP** as your Animation Blueprint.
    
    ![The Live Link integrations panel with default settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8d508f41-43ba-4086-8cee-2f54e8052943/integrationspanel.png)
10.  Click the **Live Link Subject Name** dropdown and select the value that corresponds to the Object Name you selected in your DCC. These need to match for the Live Link connection to work.
    

## Result

If you scrub the animation for your asset in your DCC, the animation is synchronized in Unreal Engine.

## Configuration

The following options are available in the USD Stage for configuring your Live Link setup.

### Enable and Disable the Live Link Connection

You can enable and disable the Live Link connection in the USD stage with the **Enable Live Link Connection** setting in the USD Stage.

![Enable or disable the Live Link connection](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ffbc3f7e-f5a8-4b7d-a31c-d835bf7dc668/enablelivelink.png)

This allows you to quickly alternate between viewing the animation provided using Live Link and viewing the original animation present on the USD Stage.

### Custom Animation Blueprints

By default, when you set up Live Link with your USD Stage, the skeletal mesh uses the DefaultLiveLinkAnimBP asset. This Animation Blueprint uses the **Live Link Pose** node to listen to the pose provided by your DCC.

![The Live Link Pose node in the animation graph editor](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/828e125c-3013-4d7e-89a3-71dc2e2cedb9/livelinkposenode.png)

You can use a custom Animation Blueprint instead by changing the **Anim Blueprint Asset** field in the Integrations panel. Use the Live Link Pose node in your custom Animation Blueprint to provide compatibility with Live Link.

### Choose Live Link Subjects

The **Live Link Subject Name** selects the particular Live Link subject to synchronize with this specific prim. This has to match the **Object Name** value of one of the objects added to your DCC's Live Link manager.