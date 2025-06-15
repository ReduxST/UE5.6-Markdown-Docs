# Refreshing Custom Details Panels

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/refreshing-custom-details-panels-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/refreshing-custom-details-panels-in-unreal-engine)  
**Processed:** 2025-06-14 16:46:21

---

Normally, the **Details Panel** rebuilds itself only when you select an object. This means that if you use edit conditions to add, hide, or skip adding a field in a Details Panel customization, the Details Panel updates even when you change the variables used in your edit condition. Instead, the Details Panel updates when you de-select and re-select the object.

To update the **Details Panel** manually, add a delegate that calls `IDetailLayoutBuilder::ForceRefreshDetails` to any properties that you want to trigger an update. This tutorial provides a on how to create this kind of delegate.

This tutorial builds on the code from the [Details Panel Quickstart](/documentation/en-us/unreal-engine/details-panel-quickstart-guide-for-unreal-engine).

## Steps

Follow these steps to create a reusable delegate for refreshing Details:

1.  Set up your delegate to call `IDetailLayoutBuilder::ForceRefreshDetails`. The following is a simple lambda function delegate you can put inline in your `CustomizeDetails` function and reuse for all properties you want to cause a refresh:
    
    CustomClassDetailsCustomization.cpp
    
    ```
         `const FSimpleDelegate OnValueChanged = FSimpleDelegate::CreateLambda([&DetailBuilder]()      {          DetailBuilder.ForceRefreshDetails();      });`
    Copy full snippet
    ```
    const FSimpleDelegate OnValueChanged = FSimpleDelegate::CreateLambda(\[&DetailBuilder\]() { DetailBuilder.ForceRefreshDetails(); });
2.  Use `IDetailLayoutBuilder::GetProperty` to get a TSharedRef pointing at your property.
    
    CustomClassDetailsCustomization.cpp
    
    ```
         `TSharedRef<IPropertyHandle> boolPropertyHandle = DetailBuilder.GetProperty(GET_MEMBER_NAME_CHECKED(ACustomActor, CustomBool));`
    Copy full snippet
    ```
    TSharedRef<IPropertyHandle> boolPropertyHandle = DetailBuilder.GetProperty(GET\_MEMBER\_NAME\_CHECKED(ACustomActor, CustomBool));
3.  Use `IPropertyHandle::SetOnPropertyValueChanged` to assign your delegate and force the details panel to refresh anytime that property is changed.
    
    CustomClassDetailsCustomization.cpp
    
    ```
         `boolProperty->SetOnPropertyValueChanged(OnValueChanged);`
    Copy full snippet
    ```
    boolProperty->SetOnPropertyValueChanged(OnValueChanged);

With this change, any changes to the CustomBool field causes the Details Panel to refresh.