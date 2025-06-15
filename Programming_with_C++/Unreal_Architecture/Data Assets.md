# Data Assets

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/data-assets-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/data-assets-in-unreal-engine)  
**Processed:** 2025-06-14 16:18:28

---

A **Data Asset** is an asset that stores data related to a particular system in an instance of its class.

-   **Assets** can be made in the [Content Browser](/documentation/en-us/unreal-engine/content-browser-in-unreal-engine) using native classes that inherit from [UDataAsset](/documentation/en-us/unreal-engine/API/Runtime/Engine/Engine/UDataAsset). If you want data inheritance or a more complex hierarchy, we recommend creating Data Only Blueprint Classes.
    
-   Inheriting from a [Primary Data Asset](/documentation/en-us/unreal-engine/API/Runtime/Engine/Engine/UPrimaryDataAsset) implements a **Primary Asset Id** and has asset bundle support, which allows it to be manually loaded and unloaded from the [Asset Manager](/documentation/en-us/unreal-engine/asset-management-in-unreal-engine).
    
-   Instances of native subclasses can be created directly as Data Assets in the Unreal editor and will use the name of the native class as the **PrimaryAssetType**.
    

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/210f4aa2-1c22-4c9c-bed4-de31ba7c3e8d/dataassetclasspreview.png)

In the image above, when creating a new data asset in the editor, you will be prompted to choose from a list of native subclasses

-   [Blueprint](/documentation/en-us/unreal-engine/blueprints-visual-scripting-in-unreal-engine) subclasses can be created to add variables and then subclassed again by Data Only Blueprint that sets those variables. With Blueprint subclasses, we recommend using Data Only Blueprints instead of the Data Asset instance to handle data inheritance and update the parent class.

## Creating a Data Asset

To inherit or create your own **Data Asset**, follow the steps below:

1.  Navigate to **Tools** > **New C++ Class** then create a new class based on a **DataAsset**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/68a67714-2680-410b-8328-d1c1a7c477bc/inheritdataasset.png)
2.  Add your class data members.
    
    ```
            `USTRUCT()         struct FMyAssetInfo {             GENERATED_BODY() 				              UPROPERTY(EditAnywhere)             FString AssetName; 				              UPROPERTY(EditAnywhere)             UTexture2D* AssetThumbnail; 				              UPROPERTY(EditAnywhere)             UStaticMesh* AssetStaticMesh;          }; 				  		         UCLASS()         class PROJECTExample_API UExampleDataAsset : public UDataAsset {             GENERATED_BODY() 				              UPROPERTY(EditAnywhere)             TArray<FMyAssetInfo> AssetItems;         };`
    Copy full snippet
    ```
    USTRUCT() struct FMyAssetInfo { GENERATED\_BODY() UPROPERTY(EditAnywhere) FString AssetName; UPROPERTY(EditAnywhere) UTexture2D\* AssetThumbnail; UPROPERTY(EditAnywhere) UStaticMesh\* AssetStaticMesh; }; UCLASS() class PROJECTExample\_API UExampleDataAsset : public UDataAsset { GENERATED\_BODY() UPROPERTY(EditAnywhere) TArray<FMyAssetInfo> AssetItems; };
3.  Build your project.
    
4.  In the Unreal editor, right-click on the **Content Browser**, then select **Miscellaneous** > **Data Asset**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/81e8d170-c544-456d-b6d9-6a503fd1b85b/createdataasset.png)
5.  When prompted to choose your class for the data asset instance, your asset should be populated in the list.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c76acb1d-aae1-44a3-a81f-5abb157b8d1e/pickdataassetclass.png)
6.  Open your **Data Asset Blueprint** to observe the member variables.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fd2d5a82-bde6-4673-ad1c-d5a0a076ffd0/blueprintdataasset.png)

When using [Property Specifiers](/documentation/en-us/unreal-engine/unreal-engine-uproperties), you can observe all of your member variables in an asset so designers can modify the data directly from the editor.

## Primary Data Asset

A **Primary Data Asset** is a Data Asset that implements a `GetPrimaryAssetId` function and has asset bundle support, which allows it to be manually loaded/unloaded from the Asset Manager.

The **PrimaryAssetType** is equal to the name of the first native class going up the hierarchy or the highest-level Blueprint class. For example, if you have a `UPrimaryDataAsset` **\->** `UParentNativeClass` **\->** `UChildNativeClass` **\->** `DataOnlyBlueprintClass`, then the type will be a `ChildNativeClass`.

Alternatively, if you have a `UPrimaryDataAsset` **\->** `ParentBlueprintClass` **\->** `DataOnlyBlueprintClass`, then the type will be a `ParentBlueprintClass`.

To change this behavior, you can override the `GetPrimaryAssetId` function in your native class or copy those functions into a different native base class.

### Creating a Primary Data Asset

To inherit or create your own Primary Data Asset, follow the steps below:

1.  Navigate to **Tools** > **New C++ Class,** then create a new class based on a PrimaryDataAsset.
    
2.  Add your class members and override the **GetPrimaryAssetID** function.
    
    ```
             `UCLASS()          class PROJECTExample_API UExampleDataAsset : public UPrimaryDataAsset {              GENERATED_BODY() 			               UPROPERTY(EditAnywhere)              FString AssetName; 			               UPROPERTY(EditAnywhere)              UTexture2D* AssetThumbnail; 			               UPROPERTY(EditAnywhere)              UStaticMesh* AssetStaticMesh;  		          GetPrimaryAssetId() const override { return FPrimaryAssetId("AssetItems", GetFName()); }           };`
    Copy full snippet
    ```
    UCLASS() class PROJECTExample\_API UExampleDataAsset : public UPrimaryDataAsset { GENERATED\_BODY() UPROPERTY(EditAnywhere) FString AssetName; UPROPERTY(EditAnywhere) UTexture2D\* AssetThumbnail; UPROPERTY(EditAnywhere) UStaticMesh\* AssetStaticMesh; GetPrimaryAssetId() const override { return FPrimaryAssetId("AssetItems", GetFName()); } };

## Loading and Unloading Assets

**Unreal Engine** automatically handles [Asset](/documentation/en-us/unreal-engine/assets-and-content-packs-in-unreal-engine) loading and unloading to provide developers a method to communicate with the Engine when each asset is needed. However, you may want precise control over when assets are discovered, loaded, and audited. For these cases, we recommend using the [Asset Manager](/documentation/en-us/unreal-engine/asset-management-in-unreal-engine).

### Asynchronous Asset Loading

Unreal Engine simplifies the process of asynchronously loading asset data. These methods work identically in development and with cooked data on devices, so you do not need to maintain two code paths for loading data on demand.

See [Asynchronous Asset Loading](/documentation/en-us/unreal-engine/asynchronous-asset-loading-in-unreal-engine) for documentation.