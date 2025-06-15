# Unreal Diff Tool

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/ue-diff-tool-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/ue-diff-tool-in-unreal-engine)  
**Processed:** 2025-06-14 16:55:22

---

Manually tracking bugs and dissecting features can be challenging with large, complex files. Traditionally, diffed files are textual text-based. However, with **Assets** and **Blueprints**, a textual representation would not be constructive. That's why we crafted the UE diff tool. The UE Diff Tool compares assets in Unreal Engine. It supports:

-   Comparing an asset with a previous version of itself from source control.
-   Comparing two different assets.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/859de5ce-8e23-40e3-911c-c9b630b96702/overview.png)

When you diff an asset or two different assets, two files are compared. The differences between the two files are highlighted, making them easier to spot.

  

Not all asset types are supported. The currently supported types:

-   Blueprints
-   Blueprint adjacent types.

## Anatomy of the Diff Tool

To diff two assets against one another, navigate to the content browser, select two assets, then right-click and choose **Diff Selected**.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/538c23b4-b74f-42bc-a6c7-7d9f46fa7cf1/diffselected.png)

### Toggle Differences

When using the Diff tool, you can use the **Next** and **Previous**(Prev) arrow buttons to quickly cycle through differences or click items in the navigation tree to observe a specific difference.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1506e5ac-2466-4122-b85d-74774d9b0c13/toggledifferences.gif)

### Basic Graph Diff Navigation

You can toggle whether panning and zooming is locked between the two graphs with the **Lock/Unlock** button. To quickly find changes, zoom out using the middle mouse wheel. All unchanged nodes appear gray, while changed nodes are visible and outlined with a color code indicating the type of change.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/311faf64-bc8e-46d2-a492-a0048a103b62/lockunlock.gif)

### Color Coding

Graph changes are color coded using the following color schemes.

| Color |   | Description |
| --- | --- | --- |
| Red | Something on the left panel is missing on the right (subrtraction.) |   |
| Green | Something on the right panel is missing on the left (addition.) |   |
| Cyan | Something has changed. |   |
| Grey | Something on the left panel is missing on the right(moved nodes, comments.) |   |

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5e3d1aa8-2776-4ff1-bb94-298b9e0cbec9/overview.png)

## UE Review Tool

You can use the **UE Review Tool** to list all the assets in a shelved or submitted changelist. The tool also allows users to diff and review those assets. Currently, the Review tool is only supported for Perforce.

You can launch the Review tool from the **Revision Control** menu located on the bottom right of the Editor. If it's missing from the list, check that you're logged into perforce.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ef01e32d-2fba-44db-ad08-53ee4dd1684a/uereviewtool.gif)

## Diffing Local Asset Changes Against Current Source Control Revision

One of the benefits of source control is the ability to view previous versions of files and compare or 'diff' them to see how the files have changed. Below are a few different options to Diff your local asset changes against your current source control revision.

### Option 1

Right-click on the asset in the content browser and navigate to **Source Control** > **Diff Against Depot**.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7acc03f1-d3e8-4d21-ac31-47f0874dc67c/difflocaloption1.gif)

### Option 2

Right-click on the asset in the **View Changelists** tool and select **Diff Against Depot**.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e3e6f0dd-ea57-4074-90b3-6d2daa23a750/diffagainstdepot.gif)

### Option 3 (Blueprint Only)

From the Blueprint Editor, navigate to **Diff** > **Depot**.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/564a62fe-5cc0-4175-b0cf-b973ff671ea5/diffdepot.gif)

## Diffing Local Asset Changes Against a Specific Source Control Revision

Follow any of the options below to diff a local asset against a specific source control revision.

### Option 1

Right-click on the asset in the content browser and navigate to **Source Control** > **History**. Right-click the revision you wish to diff against and select **Diff Against Workspace File**.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/30eb90c2-9f68-4718-894c-ba869c8ad7e3/diffagainstworkspacefile.gif)

### Option 2

From the Blueprint Editor, click **Diff** and select the revision you wish to diff against.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3605585d-9649-4ed8-9e06-01259158bece/blueprinteditordiff.gif)

## Diffing an Asset's old revision against its previous revision

### Option 1

Right-click on the asset in the **Content Browser**. Navigate to **Source Control** > **History**, then right-click the revision you wish to diff against and select **Diff Against Previous Revision**.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8dad7da0-7c91-46b2-b39d-d53299b2da80/diffagainstpreviousrevision.gif)

### Option 2

In the UE Review Tool, input the CL you want to diff and click the **diff button** beside the asset.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8b4bf097-3bc1-485f-abf0-8cc89945082b/specificoption2.gif)

## Diffing a shelved CL against its previous revision

In the UE Review Tool, input the Changelist (CL) you want to diff, then click the **diff button** beside your asset.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4672e6a1-4ba2-4a7f-aa7a-0ae9ffd62a85/diffshelved.gif)