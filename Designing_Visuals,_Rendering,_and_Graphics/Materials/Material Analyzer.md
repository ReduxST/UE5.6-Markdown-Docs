# Material Analyzer

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/unreal-engine-material-analyzer-tool](https://dev.epicgames.com/documentation/en-us/unreal-engine/unreal-engine-material-analyzer-tool)  
**Processed:** 2025-06-14 16:56:47

---

The **Material Analyzer** is a developer tool that helps you identify and analyze all Materials, or [Material instances](/documentation/en-us/unreal-engine/instanced-materials-in-unreal-engine), in your project. This enables you to make changes that can provide savings in shader permutations and data storage. When you select a Material or Material instance to analyze, the tool will find all descendants of that Material (or all descendants of the Material instance's parent Material). The tool also identifies all of the base property overrides, static switches, and static component mask parameters.

## Opening the Material Analyzer

1.  In the menu bar, click **Tools > Audit > Material Analyzer**. The **Material Analyzer** window opens.
    
    ![Material Analyzer menu path](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/afa17c04-951b-4e18-9c9b-a0f8bdb08058/material-analyzer-menu.png)
2.  Click the dropdown menu next to **Material to Analyze**. Use the list or search bar to select the Material or Material instance you want to analyze.
    
    ![Select Material to analyze](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1c89aa2e-a046-4b84-8867-7c25b1362c3a/select-material-to-analyze.png)
3.  The Material Analyzer tool displays a list of all instances of the Material you selected.
    

## Viewing the Suggestion List

Below the Material instance hierarchy is a suggestion list. The suggestion list groups all Material instances with the same set of static overrides. You can click the arrow next to each line to see the specific instances identified.  
![Suggestion list](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3ab14050-6d61-4246-b26d-614fdd11c211/suggestion-list.png)

## Create a Local Collection

Each suggestion list has a **Create Local Collection** button. Click this button to place all the related instances into a local collection, so you can easily find them and update them to have more efficient parameter setups.

![Create local collection](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e4d2c7db-8ac2-4ecf-aff9-19210bdcd1ba/create-local-collection.png)

## Viewing the Static Switch Parameters List

To see the static switch parameters for a Material instance, click the arrow next to the Static Switch Parameters column to display the full list. The columns are resizable, so you can move them if the text is cut off.

![Static switch parameters](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7c135a9a-9e8d-42c0-abe6-a157b59543a6/static-switch-parameters.png)

## Reparenting Material Instances

You can reparent these Material instances to a new instance that has those same static overrides, so that the reparented Material instances only change their unique overrides. This can provide a savings in shader permutations and data storage. Make sure to remove all the static parameter overrides from the Material instances you have reparented, or else the additional data is still stored.