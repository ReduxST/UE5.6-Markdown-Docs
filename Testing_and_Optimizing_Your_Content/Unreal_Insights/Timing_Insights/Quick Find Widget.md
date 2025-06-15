# Quick Find Widget

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/using-the-quick-find-widget-in-timing-insights-for-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/using-the-quick-find-widget-in-timing-insights-for-unreal-engine)  
**Processed:** 2025-06-14 17:01:49

---

The **Quick Find** widget is used to search and filter events displayed in the [Timing panel](/documentation/en-us/unreal-engine/using-the-timing-panel-in-unreal-insights-for-unreal-engine). The widget can be opened from the Timing panel context menu by right-clicking on a **Timing event** or by using the **CTRL** + **F** shortcut when the Timing view has focus.

![The Quick Find Widget is displayed with several filters.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4b39d606-eab3-41ba-b87d-f7281a0c9874/main-image.png)

The Quick Find widget search logic is defined using **Groups** and **Filters**. Group nodes contain child Filter nodes and define the logic applied to the children's result. Filter nodes are leaf nodes, and each contains one filter.

Each filter contains:

-   The filter type, that can be selected from a drop down menu.
    
-   The filter operator, also selectable using a drop down menu.
    
-   The filter value, that can be entered using a text box.
    

Once the filter logic is created, it can be used to search for events or filter the tracks from the Timing View.

## Filter Groups and Group Types

Filter groups determine how values should be returned from the filters grouped underneath them. The following are the available filter group types:

| **Filter Group Type** | **Description** |
| --- | --- |
| All Of (AND) | Returns only filter results if they match ALL of the filters in the group. |
| Any Of (OR) | Returns filter results that match ANY of the filters in the group. |

You can add multiple filter groups to create more complex logic.

## Filter Values

You can use the following parameters as values for individual filters:

| **Filter Name** | **Value Type** | **Description** |
| --- | --- | --- |
| Start Time | Float | The timer's starting time. |
| End Time | Float | The timer's ending time. |
| Duration | Float | The length the timer is active. |
| Track | String | The name of the track the timer belongs to. |
| Timer ID | Int | The timer's unique ID. |
| Timer Name | String | The name of the timer. |
| Metadata | See Description | Uses two different fields to search based on a key-value pair. The first field is a Key, which you can designate the value type for yourself. This is the Key that the Metadata filter will search for. The second value is a metadata value to compare against. |

### Start Time, End Time, Duration, and Timer ID Operators

Numeric filters use standard boolean operators for comparisons.

### Track and Timer Name Operators

String-based filters use the following string operators for comparisons:

| **Operator** | **Description** |
| --- | --- |
| IS | Returns values that exactly match the provided string. |
| IS NOT | Returns values that do not match the provided string. |
| CONTAINS | Returns values that contain the provided string as a substring. |
| NOT CONTAINS | Returns values that do not contain the provided string. |

### How to Use Metadata Filters

When you add a Metadata filter, it provides multiple fields you can fill with metadata you want to filter for. These fields are as follows:

![The quick find widget with sections of a filter labeled according to the key below.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ad46a4aa-2a1d-4264-94ff-74e07611368b/metadata-filters.png)

| **Index** | **Field** | **Description** |
| --- | --- | --- |
| 1 | Key | Contains a metadata field. It must be a string value, and it must be an exact match. |
| 2 | DataType | The type of the metadata field you want to search for. For example, a string or a float. |
| 3 | Operator | The operator you want to apply to the metadata value and the value in the Value text box (see below). Available operators depend on the selected DataType. |
| 4 | Value | The value you want to use as the second member of the operator. The inputted value must be compatible with the selected DataType. |

As an example, you can create a metadata filter with the key "AssetPath" with String as youir type and a value containing the string "Pawn."

![Example of filters according to the above description.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7fb25ea9-6e2f-4f07-9365-47b39550702c/filters-1.png)

The second example below shows a combination of a metadata filter with other types of filters. It searches for all timer name events with the name "FRDGBufferPool\_CreateBuffer" that have a metadata field with the key "SizeInBytes" of a type Int, and a value greater than 6500.

![Example of filters according to the above description.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0aaa49bd-a401-40de-aba9-df350a72c6a1/filters-2.png)

You can use the special string `*` to display all events that have attached metadata, regardless of key, type, or value.

## Controls

The controls at the bottom of the Quick Find panel are as follows:

| **Operation** | **Description** |
| --- | --- |
| **Find First** | Searches for the first event matching the filter in the order of the event's start time. If a match is found it is selected and the Timing view brings it into view. |
| **Find Previous** | Searches for the previous event matching the filter starting from the current selected event's start time. If no event is selected, it acts as a **Find First**. |
| **Find Next** | Searches for the next event matching the filter starting from the current selected event's start time. If no event is selected, it acts as a **Find Last**. |
| **Find Last** | Searches for the last event matching the filter in the order of the event's start time. If a match is found it is selected and the Timing view brings it into view. |
| **Metadata** | Provides a field for filtering by multiple metadata fields. See How to Use Metadata Filters below for more details. |
| **Apply Filter** | Highlights all timing events that pass the filter logic from the tracks. |
| **Clear filters** | Stops highlighting events based on the filter's logic. |

If you make changes to the filter's logic, you must click **Apply Filter** again to highlight events based on the new logic.