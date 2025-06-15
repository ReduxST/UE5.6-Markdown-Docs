# Unreal Cooking Insights

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/unreal-cooking-insights-in-unreal-engine-5](https://dev.epicgames.com/documentation/en-us/unreal-engine/unreal-cooking-insights-in-unreal-engine-5)  
**Processed:** 2025-06-14 16:56:02

---

**Unreal Cooking Insights** provides you with the ability to gather and display information about the way packages are cooked in your project. Large cooking times can significantly affect the productivity of teams that are working on larger projects. By showing the times it takes to cook each package, this tool can help reduce cooking times.

### Setup

You can run a trace for cooking insights from the command line by using the command:

```
	`trace=default,cook`

Copy full snippet
```
trace=default,cook

Alternatively, you can run the following command to target a specific host and platform:

```
	`MyProject -run=cook -log -trace=default,cook -tracehost=localhost -targetplatform=Windows`

Copy full snippet
```
MyProject -run=cook -log -trace=default,cook -tracehost=localhost -targetplatform=Windows

When loading a trace that contains cook data, the **Packages** table will be populated with the **load time**, **save time**, and **cooking time** for each package when the analysis is complete.

### Hierarchy Sorting

When selecting the **Hierarchy** filter, you can choose from the following Grouping options.

![hierarchy-sorting](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/df1edd7a-4141-4924-9de7-17768f0cc88e/hierarchysorting.png)

| **Hierarchy Grouping Option** | **Description** |
| --- | --- |
| Flat (All) | Creates a single group that includes all items. |
| Unique Values - Asset Class | Creates a group for each unique value. |
| Path Breakdown - Package Name | Creates a tree hierarchy out of the path structure of string values. |

### Preset Options

When observing your package data, you can navigate to **Preset** to configure your tree view.

![preset-options](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/97c55397-fec8-424b-987d-ab6fb315d902/presetoptions.png)

You can choose from the following Presets:

| **Preset Option** | **Description** |
| --- | --- |
| Default | Shows the default packages info. |
| Package Path | Groups packages by the package path. |
| Asset Class | Groups packages by their most important Assets. |

### Column Sorting

Cooking Insights groups specific package data in the following columns.

| **Column Name** | **Description** |
| --- | --- |
| Hierarchy | Hierarchy of the package's tree. |
| Id | The Id of the package. |
| LoadTime | The amount of time it took to load the package. |
| SaveTime | The amount of time it took to save the package. |
| BeginCache | The total time spent in the `BeginCacheForCookedPlatformData` function for the package. |
| IsCachedCooked | The total time spent in the `IsCachedCookedPlatformDataLoaded` function for the package. |
| Asset Class | The class of the most significant Asset in the package. |

You can sort columns into the following sorting categories.

| **Sorting Option** | **Description** |
| --- | --- |
| Sort Ascending | Sort your chosen column in ascending order. |
| Sort Descending | Sort your chosen column in descending order. |
| Sort By | 
Sort your column by the following values:

-   Package Hierarchy
-   Id
-   LoadTime
-   SaveTime
-   BeginCache
-   IsCachedCooked
-   AssetClass



 |

You can also customize the table by showing and hiding columns individually by using the following options.

| **Column Visibility** | **Description** |
| --- | --- |
| View Column | Hides or shows columns. |
| Show All Columns | Resets the tree view to show all columns. |
| Reset Columns to Default | Resets columns to default. |