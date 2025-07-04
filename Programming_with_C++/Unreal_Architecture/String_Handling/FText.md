# FText

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/ftext-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/ftext-in-unreal-engine)  
**Processed:** 2025-06-14 16:24:27

---

In **Unreal Engine (UE)** the primary component for [text localization](/documentation/en-us/unreal-engine/text-localization-in-unreal-engine) is the `FText` class. All user-facing text should use this class, as it supports text localization by providing the following features:

-   [Creating localized text literals.](/documentation/en-us/unreal-engine/text-localization-in-unreal-engine#textliterals)
    
-   [Formatting Text](/documentation/en-us/unreal-engine/text-localization-in-unreal-engine#textformatting) (to generate text from a placeholder pattern).
    
-   [Generating text from numbers.](/documentation/en-us/unreal-engine/text-localization-in-unreal-engine#numericaltextgeneration)
    
-   [Generating text from dates and times.](/documentation/en-us/unreal-engine/text-localization-in-unreal-engine#chronological)
    
-   [Generating derived text](/documentation/en-us/unreal-engine/text-localization-in-unreal-engine#transformative), such as making text upper or lower case.
    

`FText` also features the `AsCultureInvariant` function (or the `INVTEXT` macro), which creates non-localized, or "culture invariant" text. This is useful for things like converting a player name from an external API into something you can display in your user interface.

You can create a blank `FText` using either `FText::GetEmpty()`, or by using just `FText()`.

## Conversion

`FText` can be converted to and from `FString`. However, because `FText` contains character strings linked to localization data, while `FString` only contains a character string, these methods are inherently lossy and will discard (or fail to create) localization data. An alternative method, [Text Value Marshalling](/documentation/en-us/unreal-engine/text-localization-in-unreal-engine#textvaluemarshalling) provides lossless conversion, although this method produces data more suitable for internal marshalling than human consumption.

The following conversion functions produce `FText` strings, but without localization data:

| `FText` Function | Description |
| --- | --- |
| `AsCultureInvariant` | Creates a non-localized and culture invariant `FText` instance from an existing `FString`. |
| `FromString` | 
Creates a non-localized `FText` instance from an existing `FString`.

This is identical to `AsCultureInvariant` in non-editor builds. In editor builds, this function does not flag the text as culture invariant, which means it could still become localizable if assigned to an `FText` property in a saved Asset.



 |
| `FromName` | Creates a non-localized `FText` instance from an existing `FName`. This is the same as calling `FromString` on the output of the `FName` parameter's `ToString` function. |

To convert from `FText` to `FString`, use the `ToString` function. The resulting `FString` will hold the string data from the `FText`, but not the localization data.

## Comparison

Because `FText` data is more complex than simple strings, it does not support overloaded-operator comparisons. Instead, it provides several functions to perform comparisons that recognize the nuanced data that it contains. The following comparison functions are available:

| `FText` Function | Description |
| --- | --- |
| `EqualTo` | This function takes an [`ETextComparisonLevel`](https://api.unrealengine.com/INT/API/Runtime/Core/Internationalization/ETextComparisonLevel__Type/index.html) value to determine what comparison rules to use. It returns a `bool` indicating whether or not the calling `FText` matches the other under those comparison rules. |
| `EqualToCaseIgnored` | This function is a wrapper for calling `EqualTo` with an `ETextComparisonLevel` value of `Second`. The return value comes directly from `EqualTo`. |
| `CompareTo` | This function takes an [`ETextComparisonLevel`](https://api.unrealengine.com/INT/API/Runtime/Core/Internationalization/ETextComparisonLevel__Type/index.html) value to determine what comparison rules to use. It returns an `int32` like most string- or memory-comparison functions, where zero indicates equality, and negative or positive values indicate that the calling `FText` sorts lower or higher, respectively, relative to the `FText` parameter. |
| `CompareToCaseIgnored` | This function is a wrapper for calling `CompareTo` with an `ETextComparisonLevel` value of `Second`. The return value comes directly from `CompareTo`. |

## Using FText in User Interfaces

### Slate/UMG

Slate and UMG use `FText` attributes or arguments for any built-in Widgets that show or manage user-facing text. We recommend using `FText` for any custom Widgets that you build.

### HUD/Canvas

To display `FText` through the HUD system with Canvas, create a new `FCanvasTextItem` and set its `Text` variable to the text you want to display, as in the following example code:

```
	`// Create a new FCanvasTextItem instance to contain the text. 	FCanvasTextItem TextItem(FVector2D::ZeroVector, TestHUDText, BigFont, FLinearColor::Black); 	// Add the text into the FCanvasTextItem. 	TextItem.Text = FText::Format(LOCTEXT("ExampleFText", "You currently have {0} health left."), CurrentHealth); 	// Draw the text to the screen with FCanvas::DrawItem. 	Canvas->DrawItem(TextItem, 10.0f, 10.0f);`

Copy full snippet
```
// Create a new FCanvasTextItem instance to contain the text. FCanvasTextItem TextItem(FVector2D::ZeroVector, TestHUDText, BigFont, FLinearColor::Black); // Add the text into the FCanvasTextItem. TextItem.Text = FText::Format(LOCTEXT("ExampleFText", "You currently have {0} health left."), CurrentHealth); // Draw the text to the screen with FCanvas::DrawItem. Canvas->DrawItem(TextItem, 10.0f, 10.0f);

When using Canvas in a HUD, you must call `DrawItem` within the `DrawHUD` function, or call it in a function chain that begins with `DrawHUD`.