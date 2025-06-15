# Details Panel Customizations

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/details-panel-customizations-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/details-panel-customizations-in-unreal-engine)  
**Processed:** 2025-06-14 16:20:04

---

The [Unreal Engine Reflection System](/documentation/en-us/unreal-engine/reflection-system-in-unreal-engine) uses information from [UProperty](/documentation/en-us/unreal-engine/unreal-engine-uproperties) macros to decide how to display properties in the Details Panel. This is sufficient for most use-cases for exposing properties. However, you may want to customize how the Details Panel displays and edits information in greater detail.

Unreal Engine provides **Details Panel Customization** Interface classes to override the Details Panel and change, remove, or add elements as needed. This includes modifications to displaying specific properties, custom edit conditions, or implementations of complex custom [Slate](/documentation/en-us/unreal-engine/slate-user-interface-programming-framework-for-unreal-engine) widgets. This page provides an overview of the basics of Details Panel Customizations as well as links to tutorials showing you how to build them step-by-step.

## Details Panel Customization Classes and Methods

The interface classes used for Details Panel Customizations are:

| **Class Name** | **Description** | **Customization Methods** |
| --- | --- | --- |
| `IDetailCustomization` | The Details Panel Customization for UObject and UActor-derived classes. | CustomizeDetails |
| `IPropertyTypeCustomization` | The Details Panel Customization for structs. | CustomizeHeader, CustomizeChildren |

When you implement one of these classes, you can override their customization functions to add Slate code. The parameters expose utility classes and data about the class or struct that you are customizing. These interfaces are summarized in further detail below.

### IDetailCustomization

`IDetailCustomization` customizes the Details Panel for UObject and UActor-derived classes. Anytime you select an instance of an object with an `IDetailCustomization` assigned to it, the Details Panel will display according to the Detail Customization's rules.

`ADocumentationActor` is a simple example of a class that uses a Detail Customization. `FDocumentationActorCustomization` is a Detail Customization that adds a button to open a supplied URL in your web browser.

![The Documentation Actor's details, including the Document Link and the Open Help URL button.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b8c47bed-93b0-4e49-a3b8-71d6bb79b554/helpurlexample.png)

#### IDetailCustomization::CustomizeDetails

```
`virtual void (IDetailLayoutBuilder& DetailBuilder) override;`
Copy full snippet
```
virtual void (IDetailLayoutBuilder& DetailBuilder) override;

`IDetailCustomization::CustomizeDetails` provides a place to add Slate code that overrides the Details Panel for `UObject` and Actor-derived classes. Anything you do not explicitly change displays the default details panel without the Detail Customization, giving you room to focus only on what you want to add or rearrange.

### IPropertyTypeCustomization

`IPropertyTypeCustomization` is the base class to customize the Details Panel display for a custom property type. Anytime you expose an instance of a property type to the Details Panel for editing – either through Blueprint-defined variables or `UPROPERTY` specifiers such as `EditAnywhere` or `EditDefaultsOnly`.

Examples of structs in Unreal Engine that use property type customizations include:

| Struct | Customization | Description of property customization |
| --- | --- | --- |
| `FFrameRate` | `FFrameRateCustomization` | Adds a custom dropdown that helps narrow down the valid values for framerates. |
| `FGameplayTag` | `FGameplayTagCustomization` | Shows a button that brings up the Gameplay Tag editor. |

![The Gameplay Tag Editor, displayed from a dropdown in the Details Panel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fdcdc77d-edd8-40fd-9078-377ad7e6cc32/gameplaytageditor.png)

#### IPropertyTypeCustomization::CustomizeHeader

`IPropertyTypeCustomization::CustomizeHeader` overrides the **header** portion of a custom property type's Details Panel.

```

`virtual void CustomizeHeader(TSharedRef<IPropertyHandle> PropertyHandle, FDetailWidgetRow& HeaderRow, IPropertyTypeCustomizationUtils& CustomizationUtils) override;`

Copy full snippet
```
virtual void CustomizeHeader(TSharedRef<IPropertyHandle> PropertyHandle, FDetailWidgetRow& HeaderRow, IPropertyTypeCustomizationUtils& CustomizationUtils) override;

The header represents the details of a property handle, including the collapsible drop-down that appears above the property's members. In a struct that doesn't implement the Property Type Customization interface, the property's name appears in this section.

![Details Customization displaying a struct called ](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c0818f0d-ad2e-42ec-a1a6-547361b5ad8e/mystruct.png)

The Details Customization for a struct called "MyStruct." It includes a customized header (1) and children (2).

If you declare this `IPropertyTypeCustomization::CustomizeHeader` without any parameter arguments, the `IPropertyTypeCustomization::CustomizeChildren` function displays at the same hierarchical level as a class's other child properties, with no collapsible drop-down displayed in Unreal Editor.

Alternatively, you can customize your header but override CustomizeChildren to do nothing.

#### IPropertyTypeCustomization::CustomizeChildren

`IPropertyTypeCustomization::CustomizeChildren` customizes the section that appears when you click a property's collapsible drop-down to display all its child properties.

```
`virtual void CustomizeChildren(TSharedRef<IPropertyHandle> PropertyHandle, IDetailChildrenBuilder& ChildBuilder, IPropertyTypeCustomizationUtils& CustomizationUtils) override;`
Copy full snippet
```
virtual void CustomizeChildren(TSharedRef<IPropertyHandle> PropertyHandle, IDetailChildrenBuilder& ChildBuilder, IPropertyTypeCustomizationUtils& CustomizationUtils) override;

In a struct without a Property Type Customization, all properties defined as part of the struct appear in this section.

![image alt text](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a77324d4-0007-4d76-a14e-84a0c16c181b/helloworldexample.png)

Example of a custom struct with CustomizeChildren (1) filled but no CustomizeHeader. Fields appear inline with the Actor's other properties (2) instead of in a drop-down.

If you override this function without providing any code, none of the child properties of the struct will appear in the Details Panel. To display them, you need to use `IDetailChildrenBuilder::AddProperty`. You can loop through the full list of your property's children to display all of them.

```
`void FCustomDataDetailsCustomization::CustomizeChildren(TSharedRef<IPropertyHandle> PropertyHandle, IDetailChildrenBuilder& ChildBuilder, IPropertyTypeCustomizationUtils& CustomizationUtils) { 	if (!PropertyHandle->IsValidHandle()) 	{ 		return; 	} 	 	uint32 NumChildren = 0; 	PropertyHandle->GetNumChildren(NumChildren); 	 	for (uint32 ChildIndex = 0; ChildIndex < NumChildren; ChildIndex++) 	{ 		ChildBuilder.AddProperty(PropertyHandle->GetChildHandle(ChildIndex).ToSharedRef()); 	}`
Copy full snippet
```
void FCustomDataDetailsCustomization::CustomizeChildren(TSharedRef<IPropertyHandle> PropertyHandle, IDetailChildrenBuilder& ChildBuilder, IPropertyTypeCustomizationUtils& CustomizationUtils) { if (!PropertyHandle->IsValidHandle()) { return; } uint32 NumChildren = 0; PropertyHandle->GetNumChildren(NumChildren); for (uint32 ChildIndex = 0; ChildIndex < NumChildren; ChildIndex++) { ChildBuilder.AddProperty(PropertyHandle->GetChildHandle(ChildIndex).ToSharedRef()); }

## Helper Classes

The following class interfaces provide useful functions to access slate class properties.

| **Class Name** | **Description** |
| --- | --- |
| `IDetailLayoutBuilder` | Utility functions for accessing and changing UObject or UActors' properties and categories. |
| `IDetailChildrenBuilder` | Utility functions for accessing and changing a custom property type's properties and categories. |
| `IPropertyHandle` | Wrapper containing information about a property within the Details system. Used to customize an individual property. |
| `IPropertyTypeCustomizationUtils` | Miscellaneous utilities for property type customizations. |

### IDetailLayoutBuilder

`IDetailLayoutBuilder` provides utility functions for accessing and changing a UObject or UActor's properties and categories. `IDetailLayoutBuilder` is available in `IDetailCustomization::CustomizeDetails`.

### IDetailChildrenBuilder

`IDetailChildrenBuilder` provides utility functions for accessing and changing a custom property type's properties and categories. It works similarly to `IDetailLayoutBuilder`, but is limited only to child properties of the property that the parent `IPropertyTypeCustomization` customizes.

### IPropertyHandle

`IPropertyHandle` is a wrapper that contains information about a property within the Details system, including delegates that respond to the property being changed and a reference to the property itself. IPropertyTypeCustomization has two functions that both provide references to the IPropertyHandle for the property you are customizing. the `IDetailCustomization`, and `IDetailLayoutBuilder` interfaces get a shared reference (`TSharedRef`) to the `IPropertyHandle` for any child properties of the class it is customizing.

### IPropertyTypeCustomizationUtils

`IPropertyTypeCustomizationUtils` provides references to common fonts, access to the thumbnail pool, and a shared reference to the `IPropertyUtilities` interface.

`IPropertyUtilities` provides a variety of utility functions. This includes the ability to force or request a refresh of the Details Panel, access to information about the user's current selection, and a utility function that can create a Color Picker window. `IPropertyTypeCustomizationUtils` is available through `IPropertyTypeCustomization::CustomizeHeader` or `IPropertyTypeCustomization::CustomizeChildren`.

## Tutorials

The following tutorials provide more details and examples for specific operations when customizing the Details Panel: