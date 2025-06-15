# Using Calibration Test Patterns with nDisplay

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/using-calibration-test-patterns-with-ndisplay-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/using-calibration-test-patterns-with-ndisplay-in-unreal-engine)  
**Processed:** 2025-06-14 16:58:21

---

When you set up a new installation that uses nDisplay, partucularly with multiple viewports spread across multiple LED screens, you may sometimes have subtle display problems that are challenging to detect and diagnose when rendering a 3D virtual world. For example, you may experience tearing between adjacent viewports, display synchronization issues, seams between adjacent viewports, or slight color variations between adjacent display devices.

To make detecting these problems easier, nDisplay offers several different 2D test patterns that tile across your display devices. The regularity of these test patterns helps draw your eye to any problems. If you ensure that your nDisplay installation renders test patterns cleanly without any visible tearing or sync issues, you can be more confident that your devices will also be locked in sync when you use them to display your 3D virtual worlds.

## Activating Test Patterns

1.  The nDisplay Plugin includes a **Display Cluster Test Patterns Actor**. Find this Actor in the **Place Actors** panel and drag it into your Level Viewport.
    
    ![Add the Test Patterns Actor](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/84a61cd9-e7fe-4014-96f9-3d6a6c6c2fd7/01-test-patterns-actor_ue5.png "Add the Test Patterns Actor")
2.  Activate your choice of test patterns by issuing the `nDisplay.Calibration.Pattern` console command, or by sending a cluster event to the network. See the [Console Command Syntax](/documentation/en-us/unreal-engine/using-calibration-test-patterns-with-ndisplay-in-unreal-engine#consolecommandsyntax) and [Cluster Event Syntax](/documentation/en-us/unreal-engine/using-calibration-test-patterns-with-ndisplay-in-unreal-engine#clustereventsyntax) sections below for details.
    
    In both cases, you need to specify the name of the pattern you want to activate, the viewports that you want to show the test pattern. Each pattern also offers additional optional parameters to control aspects like the scale of the pattern and rate of motion across the viewports.
    

### Console Command Syntax

The `nDisplay.Calibration.Pattern` console command has the following syntax:

```
	`nDisplay.Calibration.Pattern [pattern ID] [viewport IDs] [material parameter 1] … [material parameter N]`

Copy full snippet
```
nDisplay.Calibration.Pattern \[pattern ID\] \[viewport IDs\] \[material parameter 1\] … \[material parameter N\]

with the following parameters:

| Parameter | Description |
| --- | --- |
| **pattern ID** | Specifies the test pattern you want to activate. This name should match the name assigned to one of the test patterns registered with the **Display Cluster Test Patterns Actor**. If it does not match one of those test patterns, the current test pattern will be removed. |
| **viewport IDs** | 
Specifies the nDisplay viewports that should show the test pattern. This must be one of the following values:

-   The ID of a viewport section in your nDisplay calibration flle.
-   A comma-separated list of viewport IDs that match viewport sections in your nDisplay configuration file.
-   The special value `*`, which applies the test pattern to all viewports.



 |
| **material parameter** | 

A list of parameters and values that override default settings for the chosen pattern. Each parameter should be in the form `<name>:<type>:<value>`, where `<name>` is the name of the parameter you want to set, `<type>` is the type of data managed by that parameter, and `<value>` is the actual value you want to set. Use the table in the [Test Patterns and Parameters](/documentation/en-us/unreal-engine/using-calibration-test-patterns-with-ndisplay-in-unreal-engine#testpatternsandparameters) section below as a reference to the names and types.

-   Parameters with type `scalar` require values that are a single floating-point number.
-   Parameters with type `color` require values that are made up of four floating-point numbers separated by commas. These numbers are interpreted in **RGBA** order: red, green, blue, alpha.



 |

For example, this console command sets all viewports to show the `TPSCircles` pattern:

```
	`nDisplay.Calibration.Pattern TPSCircles *`

Copy full snippet
```
nDisplay.Calibration.Pattern TPSCircles \*

This console command shows the `TPSCircles` pattern only on three viewports, named `vp1`, `vp2`, and `vp3`:

```
	`nDisplay.Calibration.Pattern TPSCircles vp_1,vp_2,vp_3`

Copy full snippet
```
nDisplay.Calibration.Pattern TPSCircles vp\_1,vp\_2,vp\_3

This console command is the same as above, but also overrides the default values for the width and color of the lines in the pattern:

```
	`nDisplay.Calibration.Pattern TPSCircles vp_1,vp_2,vp_3 LineWidth:scalar:0.2 LineColor:color:1,0,0,0`

Copy full snippet
```
nDisplay.Calibration.Pattern TPSCircles vp\_1,vp\_2,vp\_3 LineWidth:scalar:0.2 LineColor:color:1,0,0,0

### Cluster Event Syntax

To activate a test pattern by sending a cluster event to your nDisplay network, set up your cluster event as follows:

|   | Description |
| --- | --- |
| **Event category** | `nDisplay` |
| **Event type** | `Calibration` |
| **Event name** | `Pattern` |
| **Parameter 1** | 
`PatternId = <pattern ID>`

Where `<pattern ID>` specifies the test pattern you want to activate. This name should match the name assigned to one of the test patterns registered with the **Display Cluster Test Patterns Actor**. If it does not match one of those test patterns, the current test pattern will be removed.



 |
| **Parameter 2** | 

`ViewportId = <viewport IDs>`

Specifies the nDisplay viewports that should show the test pattern. `<viewport IDs>` must be one of the following values:

-   The ID of a viewport section in your nDisplay calibration flle.
-   A comma-separated list of viewport IDs that match viewport sections in your nDisplay configuration file.
-   The special value `*`, which applies the test pattern to all viewports.



 |
| **Additional parameters** | 

You can pass additional parameters to the cluster event to override default settings exposed by the chosen pattern. Each parameter you pass should be in the form `<name> = <type>:<value>`, where `<name>` is the name of the parameter you want to set, `<type>` is the type of data managed by that parameter, and `<value>` is the actual value you want to set. Use the table in the [Test Patterns and Parameters](/documentation/en-us/unreal-engine/using-calibration-test-patterns-with-ndisplay-in-unreal-engine#testpatternsandparameters) section below as a reference to the names and types.

-   Parameters with type `scalar` require values that are a single floating-point number.
-   Parameters with type `color` require values that are made up of four floating-point numbers separated by commas. These numbers are interpreted in **RGBA** order: red, green, blue, alpha.



 |

## Test Patterns and Parameters

This section describes the test patterns that come pre-installed with nDisplay, along with the parameters you can specify for each.

If you select your **Display Cluster Test Patterns Actor** in the Level Viewport or the **World Outliner**, you'll see the list of all available calibration patterns in the **Details** panel under the **Display Cluster > Calibration Patterns** property.

### TPSCircles

![TPSCircles](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fc02c2ce-046c-4798-b42e-dd06215a8db0/tpscircles.png "TPSCircles")

| Name | Type |
| --- | --- |
| Repeats | scalar |
| LineWidth | scalar |
| LineColor | color |

### TPSColoredBars

![TPSColoredBars](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b9101d3b-72a2-46bc-917e-9cd4a60b9840/tpscoloredbars.png "TPSColoredBars")

| Name | Type | Notes |
| --- | --- | --- |
| Shades | scalar |   |
| Direction | scalar | 
Sets the direction of the bars. Accepts the following values:

-   `0`: vertical
-   `1`: horizontal



 |

### TPSGrayBars

![TPSGrayBars](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d97a7d40-cb27-4b77-bef5-9e0b35fa835b/tpsgraybars.png "TPSGrayBars")

| Name | Type | Notes |
| --- | --- | --- |
| Shades | scalar |   |
| Direction | scalar | 
Sets the direction of the bars. Accepts the following values:

-   `0`: vertical
-   `1`: horizontal



 |

### TPSGridCircles

![TPSGridCircles](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/13b3e1be-5161-4963-9791-5c4053ef1fb6/tpsgridcircles.png "TPSGridCircles")

| Name | Type |
| --- | --- |
| Repeats | scalar |
| LineWidth | scalar |
| LineColor | scalar |

### TPAChevron

![TPAChevron](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/66f2c916-849a-43a9-a332-cfa33e48350a/tpachevron.png "TPAChevron")

| Name | Type |
| --- | --- |
| Repeats | scalar |
| LineWidth | scalar |
| LineColor | scalar |
| Speed | scalar |

### TPAGrid

![TPAGrid](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e8b784a0-042d-4b24-81a1-c21b95c3d105/tpagrid.png "TPAGrid")

| Name | Type |
| --- | --- |
| Repeats | scalar |
| LineWidth | scalar |
| LineColor | scalar |
| Speed | scalar |

### TPAMirroredChevron

![TPAMirroredChevron](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4891946b-99c9-4b35-92d1-c3d621ad5b8c/tpamirroredchevron.png "TPAMirroredChevron")

| Name | Type |
| --- | --- |
| Repeats | scalar |
| Color1 | color |
| Color2 | color |
| Speed | scalar |

### TPARadar

![TPARadar](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2c1da23c-56cf-4761-836b-0d690d4948de/tparadar.png "TPARadar")

| Name | Type |
| --- | --- |
| Speed | scalar |
| Power | color |

### TPAStrips

![TPAStrips](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7a3f16ba-47cb-440b-bf42-ec22147c2ea8/tpastrips.png "TPAStrips")

| Name | Type | Notes |
| --- | --- | --- |
| Repeats | scalar |   |
| LineWidth | scalar |   |
| LineColor | scalar |   |
| Speed | scalar |   |
| Direction | scalar | 
Accepts the following values:

-   `0`: vertical
-   `1`: horizontal



 |

You can also use your own custom test pattern. Create a new Post-Process Material in your Project, and add it to the **Calibration Patterns** property of your **Display Cluster Test Patterns Actor**. Once you do this, you'll be able to trigger your own test pattern across your nDisplay cluster using either the console command or the cluster event methods shown above.