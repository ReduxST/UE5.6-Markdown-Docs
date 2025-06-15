# Mirroring Animation

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/mirroring-animation-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/mirroring-animation-in-unreal-engine)  
**Processed:** 2025-06-14 16:36:14

---

Animation mirroring copies animation from one side of a character to another so you can reuse the same animation in different situations. Using the **Mirror Data Table**, and other mirroring workflows, you can mirror not only your Animation Sequences, but also curves, sync markers, and Notifies. Additionally, mirroring within Unreal Engine provides a way to create mirrored animations without needing to manage a second copy.

This document provides an overview of how to mirror animation using the Mirror Data Table and Animation Blueprints.

#### Prerequisites

-   Your project already contains a [Skeletal Mesh](/documentation/en-us/unreal-engine/skeletal-mesh-actors-in-unreal-engine) and [animations](/documentation/en-us/unreal-engine/animation-sequences-in-unreal-engine) to mirror.
-   You have an understanding of how to create and use [Animation Blueprints](/documentation/en-us/unreal-engine/animation-blueprints-in-unreal-engine).

## Mirror Data Table

To start mirroring animations, you must first create a **Mirror Data Table** Asset. Mirror Data Tables provide mirroring assignments and instructions for all the elements of a Skeleton you want to mirror.

To create it, click **Add (+)** in the Content Browser and select **Animation > Mirror Data Table**. A dialog window will appear where you must select the Skeleton you want to mirror. Select one and click **Accept**.

![create mirror data table](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c7c9c5b5-700f-4ce5-8d17-ea516019a690/table1.png)

Open the Mirror Data Table to view the editor with the following primary areas:

![mirror data table editor](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9746fe73-0b5a-4a38-bc7c-d14c9dd81a5a/table2.png)

1.  **Data Table**, which contains the list of elements to mirror. This list auto-populates depending on the bone, notify, and other element names, which you can configure in the [Data Table Details](/documentation/en-us/unreal-engine/mirroring-animation-in-unreal-engine#datatabledetails).
2.  [**Data Table Details**](/documentation/en-us/unreal-engine/mirroring-animation-in-unreal-engine#datatabledetails), which contains configuration settings for the mirroring behavior.
3.  **Row Editor**, which provides settings for the selected entry where you can edit the element name, the mirrored name, and the element type.

### Adding and Editing Entries

To add a new table entry, click the **Add (+)** toolbar button and fill the four properties in the **Row Editor** panel.

-   **Row Name**, which is the name of the entry.
-   **Name**, which is the name of the first bone to mirror.
-   **Mirrored Name**, which is the name of the second bone to mirror. Left or right bones can go in either of these properties, but these properties must contain the symmetrical bones.
-   **Mirror Entry Type**, which is the element type to mirror. You can select the following types:
    -   Bone
    -   [Animation Notify](/documentation/en-us/unreal-engine/animation-notifies-in-unreal-engine)
    -   [Curve](/documentation/en-us/unreal-engine/animation-curves-in-unreal-engine)
    -   [Sync Marker](/documentation/en-us/unreal-engine/animation-notifies-in-unreal-engine#addsyncmarker.)
    -   Custom, which provides a code foundation for extending the Mirror Data Table in C++ by adding additional types.

![add mirror entry](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/51649a42-730d-4f04-9285-0ed8456240ab/table3.png)

In order to have a fully mirrored character, it is necessary that the table contains most skinned bones, including central bones like **pelvis**, **spine**, **neck**, and **head**. This is so that the mirroring operation can appropriately flip the rotations of those bones along the mirror axis. For these entries, both the **Name** and **Mirrored Name** should match.

![mirror central bones](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/43f85064-4f2b-4a85-8afd-dded882c9512/table4.png)

### Data Table Details

The Data Table Details panel contains configurations and other settings for the mirror behavior:

![data table details](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0c60b30e-7ab2-4919-a6d0-844f1780cd5e/table5.png)

| Name | Descriptions |
| --- | --- |
| **Mirror Find Replace Expressions** | An array of expressions that are used to automatically populate the table with common mirror entries. Refer to the [Find and Replace Expressions](/documentation/en-us/unreal-engine/mirroring-animation-in-unreal-engine#findandreplaceexpressions) section for more information. |
| **Mirror Axis** | 
The axis of mirroring, which is across the front of the character. In most cases this should be **X**.

![mirror axis](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a2f386a7-ba61-4c2d-8499-84d62e9f9f1e/axis.png)

 |
| **Skeleton** | The Skeleton Asset to use for the mirror operation. |
| **Row Struct** | The structure to use for each row of the table. You must inherit from `FTableRowBase` if you want to extend this. |
| **Strip from Client Builds** | Enabling this will not cook this Data Table into client builds. Useful if you are making confidential tables that only servers should know about. |

### Find and Replace Expressions

**Find** and **Replace Expressions** are array entries you can add to the Data Table Details that automatically search and replace certain string text of elements in the skeleton. These expressions are then used to inform which elements are automatically populated when creating or reimporting the skeleton.

![find and replace expression properties](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2c875758-dde6-4c58-affc-f24cb584fd9e/expression1.png)

Each array requires the following expressions:

| Name | Description |
| --- | --- |
| **Find Expression** | The text to search for. In most cases this will likely be the symmetry modifiers for your element names, such as `_l`, `left_`, or `_left_`. |
| **Replace Expression** | The text to replace. In most cases this will likely be the symmetry modifiers for your element names, such as `_r`, `right_,` or `_right_`. |
| **Find Replace Method** | 
The search method to use when replacing text. You can select from the following options:

-   **Prefix**, which will search for text only at the beginning of the name.
-   **Suffix**, which will search for text only at the end of the name.
-   **Regular Expression**, where you can write a custom expression for finding and replacing names.



 |

When using **Regular Expression** as your method, you can write custom [Regular Expressions](https://en.wikipedia.org/wiki/Regular_expression) for **Find Expression** and **Replace Expression**.

For example, **Index 12** of the default array contains the following expression, searching for common central bone names and assigning to the **Name** and **Mirrored Name** properties:

-   Find Expression: `((?:^[sS]pine|^[rR]oot|^[pP]elvis|^[nN]eck|^[hH]ead|^ik_hand_gun).*)`
-   Replace Expression: `$1`

In cases where your symmetry text modifiers are in the middle of an element name, such as `finger_left_index1`, you can write the following expression to correctly search and replace:

-   Find Expression: `(\S*)_left_(\S*)`
-   Replace Expression: `$1_right_$2`

The array comes pre-populated with common expressions, such as searching and replacing several permutations of symmetry modifiers as pre or postfixes. You can change this default array from the [Project Settings](/documentation/en-us/unreal-engine/project-settings-in-unreal-engine). In the main Unreal Engine menu bar, select **Edit > Project Settings**, then navigate to the **Engine > Animation** section and locate the **Mirroring** property section.

![expression project settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ad6e089e-9862-4367-b6ae-3375b22edda1/projectsettings.png)

## Mirroring Animation

Once you have created and populated your Mirror Data Table, you can now mirror your animations in [Animation Blueprints](/documentation/en-us/unreal-engine/animation-blueprints-in-unreal-engine). This is done using the **Mirror** AnimGraph node.

To create it, right-click in the AnimGraph and select your table from the **Mirroring** category.

![mirror animation blueprint](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2ca86eb2-0898-4c0d-b7f6-112feca70287/mirror1.png)

You can preview the mirroring effect by providing an input pose and bool variable, enabling or disabling the mirroring.

![enable or disable mirroring](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/10de4afb-108b-4a3c-ba8f-6ce3f92eb4e3/mirror2.gif)

The Mirror node contains the following properties:

![mirror properties](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/beca1330-55ff-4589-8244-ad0fc92755a2/mirror3.png)

| Name | Description |
| --- | --- |
| **Mirror** | Enables or disables the mirror effect. This is exposed as a pin by default. |
| **Mirror Data Table** | The [Mirror Data Table](/documentation/en-us/unreal-engine/mirroring-animation-in-unreal-engine#mirrordatatable) to use for mirroring. |
| **Blend Time on Mirror State Change** | 
The length of time to blend between mirror states when **Mirror** is enabled or disabled. Using this also requires you to use an [Intertialization](/documentation/en-us/unreal-engine/animation-blueprint-blend-nodes-in-unreal-engine#intertialization) node after the Mirror node.

![blend time on mirror state change](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/66e300d9-b2e6-4568-8098-925b59ecedab/blendtime.gif)

 |
| **Reset Child on Mirror State Change** | Enabling this will reinitialize the source pose when the mirror state changes. |
| **Bone** | Whether or not to include bone data in the mirroring. |
| **Curve** | Whether or not to include curve data in the mirroring. |
| **Attributes** | Whether or not to include notify and sync marker data in the mirroring. |

### Detecting Mirrored Animation in Blueprint Notifies

If you are using [Custom Notify States](/documentation/en-us/unreal-engine/animation-notifies-in-unreal-engine#customnotifystates), then you may want to change it to have a different behavior based on the mirrored state. You can differentiate between mirrored states in the Notify Blueprint using the **Is Triggered By Mirrored Animation** node.

In this example, it is being used in the **Received Notify Function** to branch the logic, checking if the notify was received from a mirrored animation or not.

![is triggered by mirrored animation](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/78a708f9-8e2e-4b08-b2e0-d1bc5348c96b/mirror4.png)