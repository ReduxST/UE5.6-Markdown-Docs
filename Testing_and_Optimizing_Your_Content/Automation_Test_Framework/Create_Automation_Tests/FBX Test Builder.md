# FBX Test Builder

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/fbx-test-builder-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/fbx-test-builder-in-unreal-engine)  
**Processed:** 2025-06-14 16:23:33

---

As a part of the [Automation System](/documentation/en-us/unreal-engine/automation-test-framework-in-unreal-engine), the **FBX Test Builder** is a plugin that enables you to create your own tests for individual FBX files. The FBX Test Builder creates a **Test Plan** for a single FBX file that can be used to import or reimport and check against an array of expected results. The Test Plans that are created are stored in a JSON file which shares the same name as the FBX file that is being tested except without its extension.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b0b17063-283e-441f-9f59-fd9831a82b70/fbxtestbuilder.png)

The FBX Test Builder enables you to create your Test Plans that allow you to perform a selected operation on the FBX file and then check against an array of expected results to whether it passes or fails the completed tests.

## Enabling the Plugin

Before you can start building your FBX automation tests, you will first need to enable the **FBXAutomationTestBuilder** plugin by going to **Edit** > **Plugins** > **Testing**.

Click for full size.

After enabling the plugin, you will need to restart **Unreal Engine** before you can access it.

Click for full size.

The FBX Test Builder can be accessed by using the file menu to select **Window** > **Automation Tools** > **FBX Test Builder**.

Click for full size.

## Building a Test Plan

When you use the FBX Test Builder, it operates by using a selected **Action** (or operation) that will be performed and a series of **Expected Results** that determine whether the test that is performed passes or fails for the given FBX file. This set of actions and results is called a **Test Plan**.

### Actions

For each Test Plan, there are five key Actions that can be performed and each Action has its criteria for it to be used to perform a test correctly. These Actions and their criteria are outlined below:

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/11a0dad0-cbd2-4ac4-a584-43b4052c889a/actions.png)

| Action | Steps |
| --- | --- |
| **Import** | 
-   Import the FBX file
-   Verify the expected result



 |
| **Reimport** | 

-   This must be run after an Import Test Plan where the imported assets were not deleted
-   Reimport the FBX file
-   Verify the expected result



 |
| **Add LOD (Level of Detail)** | 

-   This must be run after an Import Test Plan where the imported assets were not deleted
-   The FBX file name must be terminated by **\_lod00**
-   There must be an FBX file with the same name that is terminated by **\_lod0X** (where **X** is greater than **0**)
-   Add a LOD
-   Verify the expected result



 |
| **Reimport LOD (Level of Detail)** | 

-   Reimport the previously imported LODs with the **Import** or **Add LOD** Action.



 |
| **Import Reload** | 

-   Import the FBX file
-   Save the packages
-   Unload the created UObject from memory
-   Reload the saved packages
-   Verify the expected result



 |

### Expected Results

For each Test Plan, a list of **Expected Results** will be evaluated to determine if the test passes or fails.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/25d7a7e4-c4b4-48b8-a169-de1550528b47/expectedresult.png)

| Settings | Description |
| --- | --- |
| **Expected Presets Type** | The predefined data that should be checked. [See below for details.](/documentation/en-us/unreal-engine/fbx-test-builder-in-unreal-engine#expectedpresetstype) |
| **Expected Presets Data Integer** | Enter the expected integer value that should be checked for the specified FBX file. |
| **Expected Presets Data Float** | Enter the expected float value that should be checked for the specified FBX file. |
| **Expected Presets Data Double** | Enter the expected double value that should be checked for the specified FBX file. |
| **Expected Presets Data String** | Enter the expected string value that should be checked for the specified FBX file. |

#### Expected Presets Type

| Check Type | Description | Required Data Types |
| --- | --- | --- |
| **Error Number** | Data should contain the number of error \[int0\]. | Integer |
| **Warning Number** | Data should contain the number of warning \[int0\]. | Integer |
| **Created Static Mesh Number** | Data should contain the number of Static Mesh created \[int0\]. | Integer |
| **Created Skeletal Mesh Number** | Data should contain the number of Skeletal Mesh created \[int0\]. | Integer |
| **Materials Created Number** | Data should contain the number of Material created \[int0\] under the target Content folder. | Integer |
| **Material Slot Imported Name** | Data should be the slot index \[int0\] and the expected original imported Material Slot Name \[string0\]. | Integer and String |
| **Vertex Number** | Data should be the total number of vertices for all LODs \[int0\]. | Integer |
| **LOD Number** | Data should be the expected number of LODs \[int0.\] | Integer |
| **Vertex Number LOD** | Data should be the LOD index \[int0\] and total number of vertices for LOD \[int1\]. | Two Integers |
| **Mesh Materials Number** | Data should contain the number of Materials indexed by the mesh \[int0\]. | Integer |
| **Mesh LOD Section Number** | Data should be the LOD index \[int0\] and the expected number of sections for a mesh \[int1\]. | Two Integers |
| **Mesh LOD Section Vertex Number** | Data should be the LOD index \[int0\], section index \[int1\], and the expected number of vertices \[int2\]. | Three Integers |
| **Mesh LOD Section Triangle Number** | Data should be the LOD index \[int0\], section index \[int1\], and the expected number of triangles \[int2\]. | Three Integers |
| **Mesh LOD Section Material Name** | Data should be the LOD index \[int0\], section index \[int1\], and the expected name of the Material \[string0\]. | Integer and String |
| **Mesh LOD Section Material Index** | Data should be the LOD index \[int0\], section index \[int1\], and the expected Material index of the Mesh's Materials \[int2\]. | Three Integers |
| **Mesh LOD Section Material Imported Name** | Data should be the LOD index \[int0\], section index \[int1\], and the expected original imported Material Slot Name \[string0\]. | Two Integers and a String |
| **LOD UV Channel Number** | Data should be the LOD index \[int0\] and the number of UV channels \[int1\] for the specified LOD. | Two Integers |
| **Bone Number** | Data should contain the number of bones created \[int0\]. | Integer |
| **Bone Position** | Data should contain the bone index \[int0\] and the position XYZ \[float0, float1, and float2\]. Optionally, you can pass a tolerance value \[float3\]. | Integer and four Floats |
| **Animation Frame Number** | Data should contain the number of frames \[int0\]. | Integer |
| **Animation Length** | Data should contain the animation length \[float0\]. | Float |

#### Setting up the Expected Result

For setting up the Expected Result, an example FBX with a box mesh that contains six different materials and textures will be used as the test case.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/aefde513-8d20-4d46-8880-401b5b6f2cc9/boxfbx1.png)

1.  Click the **Add** (**+**) button to add an Expected Result and then choose a **Expected Preset Type** that you'd like to use to check.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6227f788-ed18-45c8-8b16-ee828bf1601a/er_addexpectedresult.png)
2.  Choose a **Expected Presets Data** type that corresponds to the Expected Presets Type you want to test. In this example, **Mesh Materials Number** type is selected to check the included FBX contains six materials when imported.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9604c728-f8eb-4441-b9d8-4fc5484120c0/er_selectexpectedpresettype.png)
3.  The **Mesh Materials Number** preset type only expects an integer (use the tooltip for the preset or the table above reference what data is required) that checks the number of Materials being imported. Click the **Expected Presets Data Integer** once to add an expected result check to the array.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2858db2b-ee24-47e4-bf66-d5b10e97ba6c/er_adddatatypeinteger.png)
4.  For array element 0, enter the number of Materials that should be imported with the FBX. In the case of this example, six Materials are expected.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b4115f4c-e9f1-4c3d-bcfb-9216239e005d/er_integervalue.png)
5.  Make sure to setup the necessary [Import Options](/documentation/en-us/unreal-engine/fbx-test-builder-in-unreal-engine#importoptions) so that everything that is required by the Expected Preset Type you selected is imported correctly. For example, the Box FBX will need to import the materials and textures from the FBX so the options for **Import Materials** and **Import Textures** should be enabled.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bd826289-f94a-46ff-a71a-d1720a295cd1/er_importmaterials.png)
6.  Click the **Save JSON** button and the Test Plan will be added to the Session Frontend Automation tab where you can find it under `Engine/Import/FBX/[NameOfTheFBX]`.
    
    |   |   |
    | --- | --- |
    | ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2812e694-b3f3-46a0-a3ef-aed68060ab8f/er_savejson.png) | 
    Click image for full view.
    
     |
    | FBX Test Editor | Session Frontend Automation Tab |
    
7.  After running the test, the operation system will test if the **Mesh Materials Number** (6) of the specified LOD(0) match with the imported Asset.
    
    Click image for full view.
    
    If the test should fail, select the failed test in the Automation tab to see the reason why under the **Automation Test Results** panel.
    
    Click image for full view.
    
    The Message Log will also pop up to indicate whether the test was successful or failed and why it failed regardless of having the Session Frontend window open.
    

### Import Options

After having set up the Expected Results Test Plan, you must also make sure that the actions you want to test are set to import/reimport correctly. For example, if you are testing an FBX that imports a set number of Materials, you would want to make sure that **Import Materials** is enabled. These options are the same ones that are available when importing your own assets into the Editor via the Content Browser.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a0cc8e39-5bb4-4b63-a7c2-a5b1786b91b7/importoptions.png)

For more information, see the [FBX Import Options](/documentation/en-us/unreal-engine/fbx-import-options-reference-in-unreal-engine) page.

## Test Plan Creation Workflow

Follow the steps below to create your Test Plans for FBX testing:

1.  Copy the FBX you want to test to the following location:
    
    ```
             `[Unreal Engine Root Directory]/Engine/Content/FBXEditorAutomation`
    		
    Copy full snippet
    ```
    \[Unreal Engine Root Directory\]/Engine/Content/FBXEditorAutomation
2.  Any FBX placed in this folder location will automatically populate the **Select an FBX file** drop-down list.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9b22098d-318d-4d85-828e-412812ecfff8/testplan_selectfbx.png)
3.  Use the **Select a Test Plane** drop-down and choose **Create new plan** or select one that already exists to edit it.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c8a58209-39cf-43b6-816f-baee261974c1/testplan_createnewplan.png)
4.  Fill in the following sections:
    
    **General:**
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/dce41531-2dfe-4fbb-ae21-1a410410d745/testplan_general.png)
    
    -   **Test Plan Name** - Give a name to this test plan that you can use to select from the test plan list.
    -   **Action** - Select the type of operation that will be executed on the FBX file, such as import, reimport, add LOD, reimport LOD, or import reload.
    -   **LOD Index** - If using reimport LOD, enter the LOD index you want to reimport here.
    -   **Delete Folder Assets** - Whether to delete the imported asset at the end of the Test Plan.
    
    **Expected Results:**
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6d8bdef6-2e22-40bb-bbed-bb47f1acc422/testplan_expectedresult.png)
    
    -   Set an [Expected Presets Type](/documentation/en-us/unreal-engine/fbx-test-builder-in-unreal-engine#expectedresults) and fill in the necessary data types that are required to complete the test.
    
    **Import Options:**
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d4cfc2b2-723c-4d4a-ad3a-04110db63fb1/testplan_importoptions.png)
    -   Set the necessary [Import Options](/documentation/en-us/unreal-engine/fbx-test-builder-in-unreal-engine#importoptions) required to successfully import this particular FBX for testing.
5.  Click **Save JSON** button for your test plan to be saved and added to the available tests that will be run for this FBX file during automation testing.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6b62e75c-de33-4303-b574-97d04d65443e/testplan_savejson.png)