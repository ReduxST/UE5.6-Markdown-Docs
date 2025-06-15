# Reordering and Hiding Properties

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/reordering-and-hiding-properties-in-details-panel-customizations-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/reordering-and-hiding-properties-in-details-panel-customizations-in-unreal-engine)  
**Processed:** 2025-06-14 16:47:02

---

Details Panel Customizations can change the order in which properties appear in the Details Panel, as well as show or hide properties that wouldn't ordinarily be visible. This page provides instructions on how to show, hide, and reorder both properties and categories.

## Prerequisites

This page uses the [Details Panel Customization Quickstart](/documentation/en-us/unreal-engine/details-panel-quickstart-guide-for-unreal-engine) tutorial as the basis for its examples and refers to the following:

-   FCustomDataProperty – A custom struct consisting of the following:
    -   TSoftObjectPtr CustomTexture
    -   FName CustomName
    -   FString CustomString
    -   Int32 CustomInt
-   ACustomActor – A simple Actor with the following added properties:
    -   TSoftObjectPtr CustomMesh
    -   float CustomFloat
    -   bool CustomBool
    -   FCustomDataProperty CustomData
-   FCustomDataPropertyCustomization – A Property Type Customization for FCustomDataProperty.
    
-   FCustomClassDetailsCustomization – A Detail Customization for ACustomActor.

You should also review [Refreshing the Details Panel](/documentation/en-us/unreal-engine/refreshing-custom-details-panels-in-unreal-engine) if you want to show or hide details based on changes made by the user.

## Properties

### Reorder Properties

You can re-order properties by changing the order in which you make **AddProperty** calls. The Class Details customization in the (Details Panel Customization Quickstart)\[setting-up-your-production-pipeline\\scripting-and-automating-the-editor\\slate-tools-programming\\DetailsCustomization\\Quickstart\] includes an example of re-ordering properties. The original property declarations for `ACustomActor` are as follows:

CustomActorClass.h

```
	`UPROPERTY(EditAnywhere) 	TSoftObjectPtr<UStaticMesh> CustomMesh;  	UPROPERTY(EditAnywhere) 	float CustomFloat;  	UPROPERTY(EditAnywhere) 	bool CustomBool;  	UPROPERTY(EditAnywhere) 	FCustomDataProperty CustomData;`
Copy full snippet
```
UPROPERTY(EditAnywhere) TSoftObjectPtr<UStaticMesh> CustomMesh; UPROPERTY(EditAnywhere) float CustomFloat; UPROPERTY(EditAnywhere) bool CustomBool; UPROPERTY(EditAnywhere) FCustomDataProperty CustomData;

Normally, CustomMesh and CustomFloat would appear first in the Details Panel. However, the `FCustomClassDetailsCustomization::CustomizeDetails` function adds them to the details panel as follows:

CustomActorClassCustomization.h

```
	`CustomCategory.AddProperty(GET_MEMBER_NAME_CHECKED(ACustomActor, CustomData)); 	CustomCategory.AddProperty(GET_MEMBER_NAME_CHECKED(ACustomActor, CustomBool)); 	CustomCategory.AddProperty(GET_MEMBER_NAME_CHECKED(ACustomActor, CustomMesh)); 	CustomCategory.AddProperty(GET_MEMBER_NAME_CHECKED(ACustomActor, CustomFloat));`
Copy full snippet
```
CustomCategory.AddProperty(GET\_MEMBER\_NAME\_CHECKED(ACustomActor, CustomData)); CustomCategory.AddProperty(GET\_MEMBER\_NAME\_CHECKED(ACustomActor, CustomBool)); CustomCategory.AddProperty(GET\_MEMBER\_NAME\_CHECKED(ACustomActor, CustomMesh)); CustomCategory.AddProperty(GET\_MEMBER\_NAME\_CHECKED(ACustomActor, CustomFloat));

This results in CustomData and CustomBool appearing first. Similarly, any other custom **Slate** elements will appear in the order that you add them.

If you do not add a property in your **Details Customization**, it uses the default order and the default category for your actor. See **Hide Properties** below for information on how to avoid displaying properties.

### Hide Properties

Use `IDetailCategoryBuilder::HideProperty` to selectively hide properties that would normally appear due to their UPROPERTY specifiers.

CustomClassDetailsCustomization.cpp

```
	`DetailBuilder.HideProperty(FCustomDataProperty::StaticStruct()->GetFName());`
Copy full snippet
```
DetailBuilder.HideProperty(FCustomDataProperty::StaticStruct()->GetFName());

## Categories

### Reorder Categories

Use `IDetailCategoryBuilder::SortCategories` to set the order your custom categories render in.

`IDetailCategoryBuilder::SortCategories` takes a delegate with the signature `void FunctionName (const TMap<FName, IDetailCategoryBuilder*>&)`. Any functions you use for this delegate must be static functions. The [TMap](/documentation/en-us/unreal-engine/API/Runtime/Core/Containers/TMap) is a map of all the categories added by your custom class. Once you fetch a category from it, use `IDetailCategoryBuilder::SetSortOrder` to change what order the categories appear in. `IDetailCategoryBuilder::SetSortOrder` always sorts from lowest to highest.

CustomClassDetailsCustomization.h

```
	`static void SortCustomDetailsCategories(const TMap<FName, IDetailCategoryBuilder*>& AllCategoryMap);`
Copy full snippet
```
static void SortCustomDetailsCategories(const TMap<FName, IDetailCategoryBuilder\*>& AllCategoryMap);

CustomClassDetailsCustomization.cpp

```
	`//Custom details with two category names.  	void FCustomClassDetailsCustomization::CustomizeDetails(IDetailLayoutBuilder& DetailBuilder) 	{ 		IDetailCategoryBuilder& CustomCategory = DetailBuilder.EditCategory(FName("Custom Settings")); 		IDetailCategoryBuilder& DataCategory = DetailBuilder.EditCategory(FName("Data")); 		CustomCategory.AddProperty(GET_MEMBER_NAME_CHECKED(ACustomActor, CustomBool)); 		CustomCategory.AddProperty(GET_MEMBER_NAME_CHECKED(ACustomActor, CustomMesh)); 		DataCategory.AddProperty(GET_MEMBER_NAME_CHECKED(ACustomActor, CustomData)); 		DataCategory.AddProperty(GET_MEMBER_NAME_CHECKED(ACustomActor, CustomFloat)); 		DetailBuilder.SortCategories(&SortCustomDetailsCategories); 	}  	//Sort detail categories  	void FCustomClassDetailsCustomization::SortCustomDetailsCategories(const TMap<FName, IDetailCategoryBuilder*>& AllCategoryMap) 	{ 		(*AllCategoryMap.Find(FName("Custom Settings")))->SetSortOrder(1); 		(*AllCategoryMap.Find(FName("Data")))->SetSortOrder(0); 	}`
Copy full snippet
```
//Custom details with two category names. void FCustomClassDetailsCustomization::CustomizeDetails(IDetailLayoutBuilder& DetailBuilder) { IDetailCategoryBuilder& CustomCategory = DetailBuilder.EditCategory(FName("Custom Settings")); IDetailCategoryBuilder& DataCategory = DetailBuilder.EditCategory(FName("Data")); CustomCategory.AddProperty(GET\_MEMBER\_NAME\_CHECKED(ACustomActor, CustomBool)); CustomCategory.AddProperty(GET\_MEMBER\_NAME\_CHECKED(ACustomActor, CustomMesh)); DataCategory.AddProperty(GET\_MEMBER\_NAME\_CHECKED(ACustomActor, CustomData)); DataCategory.AddProperty(GET\_MEMBER\_NAME\_CHECKED(ACustomActor, CustomFloat)); DetailBuilder.SortCategories(&SortCustomDetailsCategories); } //Sort detail categories void FCustomClassDetailsCustomization::SortCustomDetailsCategories(const TMap<FName, IDetailCategoryBuilder\*>& AllCategoryMap) { (\*AllCategoryMap.Find(FName("Custom Settings")))->SetSortOrder(1); (\*AllCategoryMap.Find(FName("Data")))->SetSortOrder(0); }

### Hide Categories

Use `IDetailCategoryBuilder::HideCategory` to hide an entire category. You can use categories you defined with UPROPERTY specifiers or one you defined as part of a detail customization. Provide the `FName` of the category.

CustomClassDetailsCustomization.cpp

```
	`void FCustomClassDetailsCustomization::CustomizeDetails(IDetailLayoutBuilder& DetailBuilder) 	{ 		FName CustomCategoryName = FName("Custom Settings"); 		IDetailCategoryBuilder& CustomCategory = DetailBuilder.EditCategory(CustomCategoryName); 		DetailBuilder.HideCategory(CustomCategoryName); 	}`
Copy full snippet
```
void FCustomClassDetailsCustomization::CustomizeDetails(IDetailLayoutBuilder& DetailBuilder) { FName CustomCategoryName = FName("Custom Settings"); IDetailCategoryBuilder& CustomCategory = DetailBuilder.EditCategory(CustomCategoryName); DetailBuilder.HideCategory(CustomCategoryName); }

### Advanced Categories

Use `IDetailCategoryBuilder::SetShowAdvanced` to designate a category to show only when you expand the **Advanced** section of the **Details Panel**.

CustomClassDetailsCustomization.cpp

```

	`void FCustomClassDetailsCustomization::CustomizeDetails(IDetailLayoutBuilder& DetailBuilder) 	{ 		FName CustomCategoryName = FName("Custom Settings"); 		IDetailCategoryBuilder& CustomCategory = DetailBuilder.EditCategory(CustomCategoryName); 		CustomCategory.SetShowAdvanced(true); 	}`

Copy full snippet
```
void FCustomClassDetailsCustomization::CustomizeDetails(IDetailLayoutBuilder& DetailBuilder) { FName CustomCategoryName = FName("Custom Settings"); IDetailCategoryBuilder& CustomCategory = DetailBuilder.EditCategory(CustomCategoryName); CustomCategory.SetShowAdvanced(true); }