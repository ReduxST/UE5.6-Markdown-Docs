# Animation Attributes

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/fbx-attributes-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/fbx-attributes-in-unreal-engine)  
**Processed:** 2025-06-14 16:23:19

---

Custom node attributes can be imported in your FBX [Animation Sequences](/documentation/en-us/unreal-engine/animation-sequences-in-unreal-engine) for creating varied animation data-driven setups. Unlike other animation data, such as [Curves](/documentation/en-us/unreal-engine/animation-curves-in-unreal-engine), attributes are stored per-sequence and support various property types.

This document provides an overview of how to import and reference animation attributes in Unreal Engine.

#### Prerequisites

-   You are familiar with [creating custom attributes](https://knowledge.autodesk.com/support/maya/learn-explore/caas/CloudHelp/cloudhelp/2019/ENU/Maya-Basics/files/GUID-C7385EC4-74E1-4F6E-8C9D-60F5CCDA7994-htm.html) on nodes in Autodesk Maya.
-   Your project contains a [Skeletal Mesh](/documentation/en-us/unreal-engine/skeletal-mesh-assets-in-unreal-engine).
-   You are familiar with importing [Animation Sequences](/documentation/en-us/unreal-engine/animation-sequences-in-unreal-engine).

## Importing Attributes

To start importing animation attributes in your Animation Sequence, you must ensure that a Bone contains an attribute with animation. Typically, this is done in DCC software, such as Autodesk Maya. In this example, the **root Bone** has a custom float attribute.

![custom attribute in maya](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/aacb5c8d-8c32-4420-83df-9b5623369b67/import1.png)

The currently supported attribute data types for importing are **Floats**, **Integers**, **Strings**, and **Transforms**.

### Project Settings Setup

In order for attributes to import correctly, you will need to ensure they are defined in your Project Settings. From the main menu in Unreal Engine, go to **Edit > Project Settings**, navigate to the **Engine > Animation** section, and locate the **Custom Attributes** settings. The following settings are available:

![project settings custom attributes](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/57059a83-1190-4fce-9287-e7f863e6f86a/projectsettings.png)

| Name | Description |
| --- | --- |
| **Bone Timecode Custom Attribute Name Settings** | 
A list of timecode-related properties and their default mappings to custom attributes. You can change these settings to map to different timecode attributes if your project is using different attribute names.

-   **Hour Attribute Name** is an **Integer** attribute and is set by default to **TCHour**.
-   **Minute Attribute Name** is an **Integer** attribute and is set by default to **TCMinute**.
-   **Second Attribute Name** is an **Integer** attribute and is set by default to **TCSecond**.
-   **Frame Attribute Name** is an **Integer** attribute and is set by default to **TCFrame**
-   **Subframe Attribute Name** is a **Float** attribute and is set by default to **TCSubframe**
-   **Rate Attribute Name** is an **Integer** attribute and is set by default to **TCRate**.
-   **Takename Attribute Name** is a **String** attribute and is set by default to **Takename**.

![timecode custom attributes](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d64117a7-2a15-4c60-ada6-2f1cd198df43/projectsettings2.png)

These will be included in the list of attribute names to import and will act as if they were added to the Bone Custom Attributes Names array.



 |
| **Bone Custom Attributes Names** | 

An array where you define your custom attribute names to search for when importing animation. Defining an attribute name on this list will search all Bones in your skeleton for the attribute.

Click **Add (+)** to add an attribute to the list, then fill in the following properties:

-   **Name**, which is the name matching your custom animation attribute.
-   **Meaning**, which is an optional field where you can define additional context for this attribute.

![bone custom attribute names](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e4539497-faa0-45c0-8d05-8555b559a609/projectsettings3.png)

 |
| **Bone Names with Custom Attributes** | 

An array where you can define a list of Bones to filter for custom attributes when importing animation. Defining a Bone on this list will cause all custom attributes to import from that Bone when importing animation.

Click **Add (+)** to add an item to the list, then define a Bone name.

![bones names with custom attributes](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a6d235d9-4e47-4432-832c-1d6f8a83e120/projectsettings4.png)

 |
| **Attribute Blend Modes** | 

An array where you define how certain attributes behave during blends. This overwrites the global **Default Attribute Blend Mode** per attribute.

Click **Add (+)** to add an item to the list, define an attribute name, then set the blend mode:

-   **Override** will overwrite the custom attribute value based on the highest weight during the blend.
-   **Blend** will set the average value of the custom attribute between the animations according to their weight.

![attribute blend modes](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6c29d79b-a97c-4ef3-b6f8-7094bfe2b0a0/projectsettings5.png)

 |
| **Default Attribute Blend Mode** | The default blend mode to use for all custom attributes. Similar to **Attribute Blend Modes**, you can select from **Override** or **Blend**. |
| **Transform Attribute Names** | The transform node name to search for when importing [transform attributes](/documentation/en-us/unreal-engine/fbx-attributes-in-unreal-engine#transformattributes). |

Depending on how you want to import custom attributes, you may want to set values on either **Bone Custom Attribute Names** or **Bone Names with Custom Attributes**. For example, if you wanted to import two custom attributes created on the **root Bone**, you could either:

-   Create two array entries under **Bone Custom Attributes Names**, and match the names to your attributes.
    
    ![bone custom attribute names example](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/66749331-9b62-4f7b-8085-5b54781ffdb9/projectsettings7.png)
    
-   Create an entry under **Bone Names with Custom Attributes**, and name it **root**.
    
    ![bone names with custom attributes example](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0dc7827a-1cfa-495d-bc2d-812494c91ba7/projectsettings8.png)
    

After you set up your custom attribute project settings, you can [import your Animation Sequence](/documentation/en-us/unreal-engine/animation-sequences-in-unreal-engine) containing the custom attributes. When importing the FBX, ensure that **Import Custom Attribute** is enabled.

![import custom attribute](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6f160421-105f-4e45-b002-aeb4749e75b9/import2.png)

### Animation Sequence

After you import your Animation Sequence containing the custom attributes, you can view the attributes in the [Animation Sequence Editor](/documentation/en-us/unreal-engine/animation-sequence-editor-in-unreal-engine). Attributes are located as tracks within the [timeline](/documentation/en-us/unreal-engine/animation-sequence-editor-in-unreal-engine#asseteditor) under the convention **Attributes > Bone > Attribute Name**.

![attributes in animation sequence](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fed99b0b-7008-4f5e-a629-76af006be4b8/animseq1.png)

Hovering your cursor over an attribute will provide you with details about the attribute, including its type and number of keyframes.

![attribute information](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/41315ebf-f2b7-4982-b237-13ae0282f2b0/animseq2.png)

## Transform Attributes

You can also import custom **transform attributes**, which require a different workflow for importing. Transform attributes are useful for providing auxiliary transform information within an Animation Sequence without adding extra [Sockets](/documentation/en-us/unreal-engine/skeletal-mesh-sockets-in-unreal-engine) or Bones.

![transform attribute](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ddc576b1-ff3d-4cef-8359-94cf39ce6d02/trans1.png)

### FBX Setup

Since Bones already contain base transform attributes, you must instead create a child node of the Bone that you want to apply a custom attribute to. This can be a **locator** or an empty **node**.

In this example, a **locator** named "MyTransformAttribute" is parented to a **hand Bone**. Like any other node or attribute, this can be keyframed in any arbitrary way.

![create and parent locator to bone](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/90b10335-b76e-4b0d-8999-374e07eb8823/trans2.png)

### Settings and Import

Next, you need to define the name of the transform attribute in the [Custom Attributes Project Settings](/documentation/en-us/unreal-engine/fbx-attributes-in-unreal-engine#projectsettingssetup). Locate **Transform Attribute Names**, click **Add (+)** to create an item, and then add the name of the transform attribute node.

![transform attribute names](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3f516726-49c3-4a40-8f15-8ad5f8d42573/trans3.png)

You can now [import your Animation Sequence](/documentation/en-us/unreal-engine/animation-sequences-in-unreal-engine) containing the custom transform attributes. Once imported, the transform attribute will be visible as a track within the [timeline](/documentation/en-us/unreal-engine/animation-sequence-editor-in-unreal-engine#asseteditor) under the convention **Attributes > Bone > Attribute Name**.

![transform attributes in animation sequence](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bef74561-32d3-49c2-8f85-57308d9af1cd/trans4.png)

You can visualize custom transform attributes in the Animation Sequence Viewport by clicking **Character > Bones**, then enabling **Attributes** in the Viewport menu.

![show transform attribute](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/77a5489b-3540-4418-8992-0a54949ee77b/trans5.png)

## Referencing Attributes

Attributes can be referenced and read in [Blueprints](/documentation/en-us/unreal-engine/blueprints-visual-scripting-in-unreal-engine) by using **Get Attribute** functions targeting a **Skeletal Mesh Component**. You can use the following functions:

-   Get Float Attribute
-   Get String Attribute
-   Get Integer Attribute
-   Get Transform Attribute

![reference attributes in blueprints](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7d443004-5cf8-457b-ad1b-15b7fed35c1f/ref1.png)

These functions contain the following common pin information:

| Name | Description |
| --- | --- |
| **Target** | The **Skeletal Mesh Component** to target. |
| **Bone Name** | The name of the Bone containing the custom attribute. |
| **Attribute Name** | The name of the custom attribute to look for. |
| **Default Value** | If the attribute cannot be found, then this value will be sent to **Out Value**. |
| **Lookup Type** | 
Determines how the attribute is to be found on the Skeleton. You can select from the following:

-   **Bone Only**, which will only search for the attribute on the provided **Bone Name**.
-   **Immediate Parent**, which will search for the attribute on the provided **Bone Name** and its first parent Bone.
-   **Parent Hierarchy**, which will search for the attribute on the provided **Bone Name** and directly upward in the hierarchy until the root Bone.



 |
| **Out Value** | Passes the value of the attribute, or **Default Value** if the attribute is not found. |
| **Return Value** | Outputs **true** if the attribute is found when executing this function, otherwise will output **false**. |

### Get Attribute Ref

You can also use **Get Attribute Ref** functions. These functions require a **Variable** connected to **Out Value**, where it will write the value to the Variable you linked to the pin. Unlike the Get Attribute functions, Get Attribute Ref will maintain the last value of the attribute if it fails to find it.

![get attribute ref](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0e4480ad-2b66-4566-9eef-bc37b6db3dac/ref2.png)