# Landscape Region Selection Tool

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/landscape-region-selection-tool-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/landscape-region-selection-tool-in-unreal-engine)  
**Processed:** 2025-06-14 16:32:29

---

The **Region Selection** tool selects regions of the Landscape using the current brush settings and the tool strength to be used to fit a Landscape [gizmo](/documentation/en-us/unreal-engine/landscape-copy-tool-in-unreal-engine) to a specific area or to act as a mask for copying data to, or pasting data from, a gizmo.

## Using the Region Selection Tool

In this example, the Region Selection tool has been used to paint an area of the Landscape using the default positive method, then switching to the negative mask method that enables you to paint areas that don't want to include, and finally showing the Use Region As Mask section that captures the entirety of a Landscape component that is painted rather than just areas within it.

Use the following controls to paint areas that can be used for selection by doing the following:

| **Controls** | **Operation** |
| --- | --- |
| **Left Mouse Button** | Adds to the selected region. |
| **Shift + Left Mouse Button** | Removes from the selected region. |

![Without Selection](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2d6a6dc8-e0fc-42cf-8937-9daabd70fee5/01-without-selection.png "Without Selection")

![With Selection](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b9251b8f-fab9-4fb7-a7c3-ebb32512d12d/02-with-selection.png "With Selection")

In this example, an area has been painted for selection that can then be used for masking layers or with the Copy/Paste tool.

## Tool Settings

|   |   |
| --- | --- |
| ![Landscape Select button](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f9281932-1f7a-4da7-bb86-d8db6fef7443/03-landscape-select-button.png "Landscape Select button") | ![Selection tool properties](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1be0fb0e-63e7-4bc2-b36c-b3eb9b4e9e01/04-selection-tool-properties.png "Selection tool properties") |

| **Property** | **Description** |
| --- | --- |
| **Clear Region Selection** | Clears the current selected region(s). |
| **Tool Strength** | Controls how much effect each brush stroke has. |
| **Use Region as Mask** | When checked, the region selection acts as a mask with the active area being comprised of the selected region. |
| ![Region Selection](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a897c372-f3f4-4bbb-aa09-e10e5c179a2a/05-region-selection.png "Region Selection") |   |
| **Negative Mask** | When checked, and when **Use Region as Mask** is also checked, the region selection acts as a mask, but the active area is comprised of the unselected region. |
| ![Region Mask Negative Selection](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/43c4093f-2841-4cce-a3df-ec2e8def7bb5/06-region-mask-negative-selection.png "Region Mask Negative Selection") |   |