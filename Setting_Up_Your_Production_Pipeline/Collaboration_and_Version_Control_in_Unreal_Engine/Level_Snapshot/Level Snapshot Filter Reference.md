# Level Snapshot Filter Reference

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/level-snapshot-filter-reference-for-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/level-snapshot-filter-reference-for-unreal-engine)  
**Processed:** 2025-06-14 16:33:12

---

Only the properties of the default C++ filters are described here. Custom filters created with Blueprints will have whatever properties you assign.

## Shared Filter Properties

| Property Name | Description |
| --- | --- |
| Filter |   |
| Name | The display name in the editor. Defaults to the class name if left blank. |
| Filter Behavior | Determines whether to pass on or negate the results of the filter. |
| Ignore Filter | Determines whether or not to ignore the filter. |
| Config |   |
| Default Result\* | 
Options are:

-   Include: The Actor / property is included.
-   Exclude: The Actor / property is excluded.
-   Do Not Care:
    -   Another filter will decide. If all filters are set to Do Not Care, include the Actor / property.
    -   Use this for filters that only implement one function: IsActorValid or IsPropertyValid.



 |

\* This property is not shared by every filter.

## Actor Changed Transform Filter Properties

![Actor Changed Transform filter properties](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/602d1ba8-af0a-4dc6-96f6-e9cc81bb8de8/01-actor-changed-transform.png)

| Property Name | Description |
| --- | --- |
| Config |   |
| Transform Check Rule | 
Determines whether to allow Actors that changed location or that stayed in the same place. Options:

-   Is Valid when Transform Changed: Return True if the Snapshot and World Actors have different transforms.
-   Is Valid when Transforms Stayed Same: Return True if the Snapshot and World Actors have the same transforms.



 |
| Ignore Location | If enabled, do not compare the Actor's locations. |
| Ignore Rotation | If enabled, do not compare the Actor's rotations. |
| Ignore Scale | If enabled, do not compare the Actor's scales. |

## Actor Dependent Property Filter Properties

This filter is complex, and is based on other filters. It is intended for experienced users and should be used carefully.

![Actor Dependent Property filter properties](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bc9f5096-7251-4523-af25-7ab5624ee94b/02-actor-dependent-property.png)

| Property Name | Description |
| --- | --- |
| Config |   |
| Actor Filter | IsActorValid is run on this filter. IsPropertyValid is run on one of the below filters depending on this filter. Select a filter from the dropdown list, and configure its properties accordingly. |
| Include Property Filter | Used by IsPropertyValid when Actor Filter > IsActorValid returns Include. Select a filter from the dropdown list, and configure its properties accordingly. |
| Exclude Property Filter | Used by IsPropertyValid when Actor Filter > IsActorValid returns Exclude. Select a filter from the dropdown list, and configure its properties accordingly. |
| Do Not Care Handling | 
Determines what filter IsPropertyValid is supposed to use when IsActorValid returns DoNotCare. Options:

-   Use Include Filter: When IsActorValid returns Include, use RunOnIncludedActorFilter.
-   Use Exclude Filter: When IsActorValid returns Exclude, use RunOnExcludedActorFilter.
-   Use Do Not Care Filter: When IsActorValid returns DoNotCare, use RunOnDoNotCareActorFilter.



 |
| Do Not Care Property Filter | Used by IsPropertyValid when ActorFilter > IsActorValid returns DoNotCare and DoNotCareHandling == UseDoNotCareFilter. Select a filter from the dropdown list, and configure its properties accordingly. |

## Actor Has Tag Filter Properties

![Actor Has Tag filter properties](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/84a6c271-58f4-486b-bf56-642298ba28b9/03-actor-has-tag.png)

| Property Name | Description |
| --- | --- |
| Config |   |
| Tag Checking Behavior | 
Determines how to match Allowed Tags in each Actor. Options:

-   Has All Tags: Actors must have all tags to pass.
-   Has Any Tag: Actors must have at least one of the tags to pass.



 |
| Allowed Tags | The tags to check the Actor for. The property is a set containing multiple elements that are text strings for the tags. |
| Actor to Check | 

Determines which of the Actors to check the tags on. Options:

-   World Actor: Checks only the tags of the World Actors.
-   Snapshot Actor: Checks only the tags of the Snapshot Actors.
-   Both: Checks the tags of both groups of Actors.



 |

## Constant Filter Properties

![Constant filter properties](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/63777085-c18e-429c-a0a0-e87679c99140/04-constant-filter.png)

| Property Name | Description |
| --- | --- |
| Config |   |
| Is Actor Valid Result | 
Options:

-   Include
-   Exclude
-   Do Not Care



 |
| Is Property Valid Result | 

Options:

-   Include
-   Exclude
-   Do Not Care



 |
| Is Deleted Actor Valid Result | 

Options:

-   Include
-   Exclude
-   Do Not Care



 |
| Is Added Actor Valid Result | 

Options:

-   Include
-   Exclude
-   Do Not Care



 |

## Property Has Name Filter Properties

![Property Has Name filter properties](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a4ea9970-8c4c-493e-ae32-9a5807b9ba54/05-property-has-name.png)

| Property Name | Description |
| --- | --- |
| Config |   |
| Name Matching Rule | 
How to compare the Property Name to Allowed Names. Options:

-   Contains Exactly: The name must contain the input substring (case sensitive).
-   Contains Ignore Case: The name must contain the input substring (case insensitive).
-   Matches Exactly: The name must match the input substring (case sensitive).
-   Matches Ignore Case: The name must match the input substring (case insensitive).



 |
| Allowed Names | The names to check the property against. The property is a set containing multiple elements that are text strings for the names. |

## Property Type Filter Properties

![Property Type filter properties](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/178725ff-1ba1-4a82-bd69-5f7c13b908ac/06-property-type.png)

| Property Name | Description |
| --- | --- |
| Config |   |
| Allowed Types | The property types you want to allow. The property is a set containing multiple elements that are text strings for the types. |

## Transform Property Filter Properties

![Transform Property filter properties](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f9648e7b-1f9c-40fb-9d3f-4c387741c197/07-transform-property.png)

| Property Name | Description |
| --- | --- |
| Transform |   |
| Location | 
Options:

-   Include
-   Exclude
-   Do Not Care



 |
| Rotation | 

Options:

-   Include
-   Exclude
-   Do Not Care



 |
| Scale | 

Options:

-   Include
-   Exclude
-   Do Not Care



 |