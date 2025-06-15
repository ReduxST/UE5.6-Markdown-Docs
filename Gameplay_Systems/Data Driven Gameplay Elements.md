# Data Driven Gameplay Elements

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/data-driven-gameplay-elements-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/data-driven-gameplay-elements-in-unreal-engine)  
**Processed:** 2025-06-14 16:18:32

---

**Data Driven Gameplay** helps mitigate the amount of work and complexity involved for games that have an extended lifetime. For example, some games may offer updates to users through an online service model. This model may adjust certain data parameters within that game to balance or add content based on user feedback.

Data Driven gameplay provides you with an interface to visualize and parameterize data creation and progression. You can move data to **Microsoft Excel** or other spreadsheet document that can be maintained and then imported to automatically take effect in the game.

**DataTables** and **CurveTables** can be imported into **Unreal Engine** through Excel documents. These Excel documents are .`xlsm` (macro enabled Excel documents) that have macro based export buttons to enable easily exporting to the intermediate data format, comma separated variables (`.csv`).

These documents reside in a single location to help make data easier to find and modify. You can download a sample `.xlsm` file by **Right-clicking** > **Save as** to download:

[Sample .xlsm file](https://d1iv7db44yhgxn.cloudfront.net/documentation/attachments/81f1970c-12dc-478a-afe5-b8196a710e72/example.xlsm)

## Data Tables

Data Tables are a table of miscellaneous but related data grouped in a meaningful and useful way, where the data fields can be any valid `UObject` property, including asset references. Before a designer can import a CSV file into a DataTable, a programmer has to create the row container telling the engine how to interpret the data.

These tables consist of column names that have a 1:1 mapping to a given code based `UStruct` and its variables, which must inherit from `FTableRowBase` to be recognized by the importer.

The first column is expected to be named Name and contains the names by which each row is accessed for use in game. Subsequent columns have a variable name for a heading and below, in the same column, the data for that row/column intersection. Given this format, a single row maps 1:1 directly to the structure inherited from `FTableRowBase`.

We created the following CSV document to showcase a Gameplay Data example where a character may gain experience points in order to attain a "level up":

```
	`/** Structure that defines a level up table entry */ 	USTRUCT(BlueprintType) 	struct FLevelUpData : public FTableRowBase 	{ 		GENERATED_USTRUCT_BODY()  	public:  		FLevelUpData() 		: XPtoLvl(0) 		, AdditionalHP(0) 		{}  		/** The 'Name' column is the same as the XP Level */  		/** XP to get to the given level from the previous level */ 		UPROPERTY(EditAnywhere, BlueprintReadWrite, Category=LevelUp) 		int32 XPtoLvl;  		/** Extra HitPoints gained at this level */ 		UPROPERTY(EditAnywhere, BlueprintReadWrite, Category=LevelUp) 		int32 AdditionalHP;  		/** Icon to use for Achivement */ 		UPROPERTY(EditAnywhere, BlueprintReadWrite, Category=LevelUp) 		TSoftObjectPtr<UTexture> AchievementIcon; 	};`
Copy full snippet
```
/\*\* Structure that defines a level up table entry \*/ USTRUCT(BlueprintType) struct FLevelUpData : public FTableRowBase { GENERATED\_USTRUCT\_BODY() public: FLevelUpData() : XPtoLvl(0) , AdditionalHP(0) {} /\*\* The 'Name' column is the same as the XP Level \*/ /\*\* XP to get to the given level from the previous level \*/ UPROPERTY(EditAnywhere, BlueprintReadWrite, Category=LevelUp) int32 XPtoLvl; /\*\* Extra HitPoints gained at this level \*/ UPROPERTY(EditAnywhere, BlueprintReadWrite, Category=LevelUp) int32 AdditionalHP; /\*\* Icon to use for Achivement \*/ UPROPERTY(EditAnywhere, BlueprintReadWrite, Category=LevelUp) TSoftObjectPtr<UTexture> AchievementIcon; };

**CSV Document:**

```
	`Name,XPtoLvl,AdditionalHP,AchievementIcon 	1,0,0,"Texture2d'/Game/Textures/AchievementIcon1'" 	2,1000,9,"Texture2d'/Game/Textures/AchievementIcon2'" 	3,1000,10,"Texture2D'/Game/Textures/AchievementIcon3'" 	4,1500,12,"Texture2D'/Game/Textures/AchievementIcon4'" 	5,2000,14,"Texture2D'/Game/Textures/AchievementIcon5'"`
Copy full snippet
```
Name,XPtoLvl,AdditionalHP,AchievementIcon 1,0,0,"Texture2d'/Game/Textures/AchievementIcon1'" 2,1000,9,"Texture2d'/Game/Textures/AchievementIcon2'" 3,1000,10,"Texture2D'/Game/Textures/AchievementIcon3'" 4,1500,12,"Texture2D'/Game/Textures/AchievementIcon4'" 5,2000,14,"Texture2D'/Game/Textures/AchievementIcon5'"

The double quotes around the asset type are important for the property importing pipeline. Without them, the text is imported as `Texture2d`.

### Data Table Importing Process

Follow the steps below to Import a CSV file:

1.  Save your file out of Excel or another spreadsheet software with the `.csv` extension.
    
2.  Open Unreal Editor, and click on **Import** in the **Content Browser**.
    
3.  Navigate and select the CSV file you want to import as a DataTable. You can choose from the following **Import As** options:
    
    -   **DataTable**
    -   **CurveTable**
    -   **Float Curve**
    -   **Vector Curve**
    -   **Linear Color Curve**
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ef3aa90f-09ab-426b-bf26-2dc419447b89/importas.png)
4.  You can choose the **DataTable Row Type** from the drop down list.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8197a9d4-1212-445f-aedb-19379fb043d9/datarowtype.png)
5.  Additional **Import Options** are available to use:
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/139d29fa-6922-46a9-846a-7ba962c1c4ab/importoptions.png)
    
    | Import Option | Description |
    | --- | --- |
    | **Ignore Extra fields** | Set to true to ignore extra fiels in the import data, if false it will warn about them |
    | **Ignore Missing Fields** | Set to true to ignore any fields that are expected but missing, if false it will warn about them |
    | **Import Key Field** | Explicit field in import data to use as key. If this is empty it uses Name for `.JSON` and the field field found for `.CSV` |
    
6.  This creates a DataTable object in the current directory of the **Content Browser**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7d4513c2-a311-451d-9d6d-5d85edcef6b3/datatableobject.png)
7.  You can view the contents of the DataTable in the editor by **Double-clicking** on the object. You can update the object by **Right-clicking** on the object and selecting **Reimport** from the menu.
    
    The original file path is used when reimporting the object.
    

## Data Curves

**Data Curves** work in a similar manner to DataTables, however they only support floating point types. As with DataTables, the first column is named "Name" and contains the names by which each row is accessed for use in game.

Each column heading after the first stores the X-axis variable for a curve to be plotted. The data under this heading is the Y-axis value for the given row. Given this format, a single row corresponds to a curve that code can access and interpolate data along.

Below is an example table for damage progression:

|   | 0 | 1 | 2 | 3 |
| --- | --- | --- | --- | --- |
| Melee\_Damage | 15 | 20 | 25 | 30 |
| Melee\_KnockBack | 1 | 2 | 4 | 8 |
| Melee\_KnockBackAngle | 10 | 45 | 60 | 65 |
| Melee\_StunTime | 0 | 1 | 5 | 7 |

## Curve Tables

**Curve Tables** are useful for defining two dimensional numeric data. You can edit Simple Curves and Rich Curves in the Curve Data Table Editor.

When creating a Curve Table, you can open the editor to edit curves in the table or curve view without needing to go back to the external program you created them with.

You can create Curve Tables in the Content Browser by navigating to the **Miscellaneous** section.

### Curve Table Importing Process

Follow the steps below to Import a CSV file:

1.  Save your file out of Excel or another spreadsheet software with the `.csv` extension.
    
2.  Open Unreal Editor, and click on **Import** in the **Content Browser**.
    
3.  Navigate and select the CSV file you want to import as a Curve Table. You can choose from the following **Import As** options:
    
    -   **DataTable**
    -   **CurveTable**
    -   **Float Curve**
    -   **Vector Curve**
    -   **Linear Color Curve**
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5642f166-7d72-48bf-b7af-bdd8ed99386d/importas.png)
4.  Choose the **Curve Table Type** from the drop down list. Once selected, you will be prompted to choose your interpolation type between **Constant**, **Linear**, or **Cubic**.
    
    | Interpolation Type | Description |
    | --- | --- |
    | **Constant** | Values in Y Will not be interpolated between datapoints in X. They will clamp to the previous-known value of X. |
    | **Linear** | Values in Y will be linrearly interpolated between datapoints in X. |
    | **Cubic** | Values in Y will be cubic interpolated between datapoints in X. |
    
5.  This creates a Curve Table object in the current directory of the **Content Browser**.
    
    ![curve-table-content-browser](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/78ea157e-703b-449d-9679-a391880f2110/curvetablecontentbrowser.png)
6.  You can double-click your Curve Table to open the Curve Table editor.
    
    ![curve-table-editor-view](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/30dfe636-ae82-42d7-b5c3-588f0c48bf44/viewcurvetable.png)
7.  To see your Curve Table data in graph form, click the graph button.
    
    ![curve-table-graph-view](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2fdc3d53-c7b9-4356-9081-6b4b08c50a25/curvegraphview.png)
8.  The **Curve Table View** allows multiple curves to be displayed.
    
    ![multi-curve-display](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7484d53f-2209-4add-bff6-dd8f94829aff/multicurvedisplay.png)
9.  You can **Rename** and **Delete** curves by right-clicking on a curve.
    
    ![Renaming Curves](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fe316ff2-c671-4098-aec6-07773e6a487c/renaming-curves.gif)

## Data Hookup

To use data from these tables is you must do place a Blueprint-exposed variable of either **FDataTableRowHandle** or **FCurveTableRowHandle**, depending on if you want a DataTable or CurveTable.

From a content provider's point of view, this will expose a data field with two subfields:

  

| Subfield | Description |
| --- | --- |
| DataTable/CurveTable | this is the content reference to the table that holds the data. |
| RowName | this is the name in the first column of the row you wish to get data from. |

### Data Usage (C++)

Once you have the data hooked up, the handle structures provide the helper functions `FindRow()` and `GetCurve()` that provide you a way to retrieve either a struct or curve filled with data.

In the case of a `FCurveTableRowHandle`, an `FRichCurve` pointer is returned. The `FDataTableRowHandle`, however, allows you to specify a structure in the template function call. This structure can be the final structure or any of its parents in the inheritance hierarchy.

All structures and curves returned should not be cached further than the local scope of a function. This is to ensure that if the table is refreshed from re-import, the data changes take effect immediately and that no invalid pointers are accessed.

In the above DataTable example, the asset that is referenced is a lazy loaded asset (`TSoftObjectPtr` handles this). If the Asset field type was set to `UTexture`, all of the assets would be loaded whenever the DataTable was loaded.