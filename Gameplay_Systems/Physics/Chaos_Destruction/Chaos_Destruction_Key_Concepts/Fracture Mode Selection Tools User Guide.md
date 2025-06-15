# Fracture Mode Selection Tools User Guide

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/fracture-mode-selection-tools-user-guide](https://dev.epicgames.com/documentation/en-us/unreal-engine/fracture-mode-selection-tools-user-guide)  
**Processed:** 2025-06-14 16:24:17

---

You can find similar information in video format in the Epic Developer Community site by watching the [Using the selection tools](https://dev.epicgames.com/community/learning/tutorials/k84m/chaos-destruction-fracture-and-clustering) tutorial.

The **Fracture Mode** is a [Level Editor Mode](/documentation/en-us/unreal-engine/level-editor-modes-in-unreal-engine) that contains a variety of tools, including ones used by the Chaos Destruction System for creating, fracturing, and manipulating **Geometry Collections**, the asset type for simulating real-time fracturing in Unreal Engine.

In this guide you will learn to use the various selection tools available in the Fracture Mode. These tools provide useful ways of selecting specific fractured pieces (also called Bones) in the Geometry Collection that can be further fractured or clustered.

Before learning about the Fracture Mode, you should know how to create Geometry Collections from Actors in the Level. If you are not familiar with the process, refer to the [Geometry Collections User Guide](/documentation/en-us/unreal-engine/geometry-collections-user-guide).

## Fracture a Geometry Collection

In this section, you will create and fracture a Geometry Collection so you can learn about the selection tools included with the **Fracture Mode**.

1.  Create a Geometry Collection from a Static Mesh Actor in your Level.
    
    ![Create a Geometry Collection from a Static Mesh Actor in your Level](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e8e992da-f18f-4c43-b4ef-b19864a60e49/destruction-selection-6.png)
2.  With your Geometry Collection selected, go to the **Fracture** section and select one of the fracturing tools available. Go to the **Fracture** panel and click **Fracture**. You can fracture the Geometry Collection multiple times by using the same fracturing tool, or selecting a different one each time you click Fracture.
    
    ![Go to the Fracture panel and click Fracture](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/eeb8ce15-af67-4642-af1a-957d957e7517/destruction-selection-21.png)
3.  The example below used the **Slice** and **Uniform Voronoi** fracture tools to fracture the Geometry Collection.
    
    ![The example below used the Slice and Uniform Voronoi fracture tools to fracture the Geometry Collection](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/da0262f7-9471-4626-bf9c-e8f832f2bd41/destruction-selection-20.png) ![The Geometry Collection is fractured](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8f63a7c8-1b71-4986-8854-acd09e7f9576/destruction-selection-8.png)

Refer to the [Fracturing Geometry Collections User Guide](/documentation/en-us/unreal-engine/fracturing-geometry-collections-user-guide) to learn more about fracturing Geometry Collections.

## Use the Selection Tools

The fracture hierarchy of a Geometry Collection resembles a tree structure. It contains a root bone (Level 0) with one or more child bones (Levels 1). Each child bone can, in turn, contain its own children (Level 2 and 3).

![A 4 level fracture hierarchy](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a20cd53c-5b96-4201-8fa3-a360e07812ae/destruction-selection-8b.png)

When in **Fracture Mode**, you can use the **selection tools** to select the bones of a Geometry Collection directly.

You will find the selection tools in the **Select** section with the following options:

![Selection Tools](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1098ce15-fe9b-43b9-ae80-d9c40209e78e/destruction-selection-22.png)

| Name | Description |
| --- | --- |
| **All** | Selects all the bones in the Geometry Collection. |
| **Invert** | Inverts the current selection of bones in the Geometry Collection. |
| **None** | Deselects all bones in the Geometry Collection. |
| **Parent** | Selects the parent bone of the current bone selection. |
| **Children** | Selects all the child bones of the current bone selection. |
| **Siblings** | Selects all bones that contain the same parent as the currently selected bone. |
| **Level** | Selects all bones in the same level of the hierarchy. |
| **Contact** | Selects all bones that are adjacent to any currently selected bones. |
| **Interactive** | Enables an interactive selection mode where you can use marquee selection and filtering to select a desired number of bones in the Geometry Collection. |

You can select multiple bones (fractured pieces) in the Geometry Collection by pressing **CTRL** and clicking them directly in the viewport.

### Select All Nodes

Click the **All** button to select all the bones in the Geometry Collection. This includes all the bones of each level in the hierarchy.

![Click the All button to select all the bones in the Geometry Collection](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b38dae15-5cb2-4a69-add6-70a65126eb71/destruction-selection-9.png)

### Invert Your Selection

Use the selection tools, or CTRL+click, to select any individual bones of the fracture mesh. Then, click the **Invert** button to invert your selection.

![Click the Inverse button to invert your selection](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/aee8644a-4b7b-4f5d-b13b-af540af856ea/destruction-selection-10.png)

### Deselect All Bones

Click the **None** button to deselect all bones in the Geometry Collection.

![Click the None button to deselect all bones](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c1e75fcd-40ce-43e5-bef3-2dd4351eee95/destruction-selection-11.png)

### Select the Parent Bones

Select a bone that is the child of another bone in the Geometry Collection. Click **Parent** to select the immediate parent bone to the selected child bone in the hierarchy.

![Click the Parent button to select that bone's parent bone](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/042aa6ad-eae4-46a4-82f3-d4b4d174a239/destruction-selection-14.png)

In the example below, selecting the child bone 87 and then clicking Parent selects the parent of it, Bone 12.

![The parent bone is selected in the hierarchy](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d66e64ad-e9f8-42c0-b755-e4e302fd5a44/destruction-selection-12.png)

### Select the Child Bones

Select a parent bone and click **Children** to select all child bones of the selected parent bone.

In the example below, all children of Bone 12 are selected.

![All the child bones are selected in the hierarchy](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/aa7db493-3350-4ffc-a91b-c9c66618b6c1/destruction-selection-13.png)

### Select the Sibling Bones

Select a bone in the Geometry Collection. Click **Sibling** to select all the bones that share the same parent as the selected bone(s).

![Click the Sibling button to select all bones that share the same parent](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0a73de2f-410d-498e-a579-634e4841f5ee/destruction-selection-14.png)

In the example below, Bone 87 is selected. When Sibling is clicked, all children of Bone 12 are selected because they share that same parent bone.

![All bones that share the same parent are selected in the hierarchy](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e04d3ad2-779e-4ddc-b197-cc2b990a5ee6/destruction-selection-15.png)

### Select All Bones at the Same Hierarchy Level

Select a bone in the Geometry Collection. Click **Level** to select all bones in the same level of the hierarchy.

![Click the Level button to select all bones in the same level of the hierarchy](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/836b868b-3fff-4cc8-a259-7b8cd3828af0/destruction-selection-16.png)

In the example below, the Geometry Collection contains several bones that are the same hierarchy level in their fracture tree. With Bone 5 selected, when Level is clicked in the selection tools, all other Bones at that same hierarchy level will be selected, like Bones 6, 7 and 8.

![All bones at the same level are selected in the hierarchy](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/53c3211e-00e1-4912-8dac-184e458ffc68/destruction-selection-17.png)

### Contact Selection of Bones

Click **Contact** to select all bones that are adjacent to the currently selected bones in the Geometry Collection.

![Click the Contact button to select all bones that are adjacent to the currently selected bones](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/39f17d5e-7daa-4da0-bbef-a4b053eb50f1/destruction-selection-18.png)

### Interactive Selection of Bones

Click **Interactive** to enter a marquee selection mode. Left-click and drag the mouse in the viewport to select multiple bones. You can hold the CTRL key and drag the mouse to remove bones from the selection.

The interactive selection mode has the following options:

![Interactive selection mode options](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a947704f-5854-4a93-8b49-13b5e7046ec2/destruction-selection-23.png)

| Option | Description |
| --- | --- |
| **Mouse Selection Method** | Determines the bone selection method. **Rect Select** uses a rectangular marquee for selecting all overlapping bones. **Standard Select** allows bone selection by left-clicking the mouse on each bone to select them directly. |
| **Volume Selection Method** | Determines the method used to calculate the bones selected by the filter operation. |
| **Selection Operation** | Determines whether the filter operation will **replace**, **add**, or **remove** from the current selection. |
| **Min Volume Fracture** | Determines the minimum bone volume considered for selection. |
| **Max Volume Fracture** | Determines the maximum bone volume considered for selection. |

You can filter your selection by bone size by using the **Filter Settings**. Increasing **Max Volume Fracture** to **1** will include all bone sizes in the filter operation.

Click the image for full size.

Use **Min Volume Fracture** to filter out the smallest bones. Do this until you reach a desired selection. A common example is excluding the smallest bones from the selection so you can add an additional fracture level to the biggest bones.

![You can start filtering out the smallest bones by increasing the value of the Min Volume Fracture](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fc73f50d-863b-404c-b513-f78c56c97be2/destruction-selection-filter.gif)