# Text Localization

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/text-localization-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/text-localization-in-unreal-engine)  
**Processed:** 2025-06-14 16:53:57

---

Text in **Unreal Engine (UE)** is the primary component for localization. It is a specialized string, represented by the `FText` type in C++. This should be used when you have user-facing text that needs to be localized.

Internally, `FText` is implemented as a [`TSharedRef`](https://api.unrealengine.com/INT/API/Runtime/Core/Templates/TSharedRef/index.html) to an [`ITextData`](https://api.unrealengine.com/INT/API/Runtime/Core/Internationalization/ITextData/index.html). This makes it very cheap to copy, and the [`FTextSnapshot`](https://api.unrealengine.com/INT/API/Runtime/Core/Internationalization/FTextSnapshot/index.html) utility provides an efficient way to detect if a cached `FText` value has actually changed.

The data held within `FText` instances varies, depending on how the `FText` was created. This variance is handled by the internal "text history" (`FTextHistory`). Text histories support the culture-correct rebuilding of text, and also form the key component for the following:

-   Live culture switching.
    
-   Sending `FText` over the network.
    
-   Creating culture invariant sources.
    

Converting `FText` to [`FString`](https://api.unrealengine.com/INT/API/Runtime/Core/Containers/FString/index.html) is typically a lossy operation, as it loses the text history. It should only be done if you no longer need the localization data. For example, if there is a lower-level API that works on strings, which is managed by a higher-level API that watches for text changes (such as [`STextBlock`](https://api.unrealengine.com/INT/API/Runtime/Slate/Widgets/Text/STextBlock/index.html)). This conversion can also be used when passing the data into an external API that only accepts strings.

If you need text that not localizable (such as converting a player name from an external API into something you can display in your UI), you can use [`FText::AsCultureInvariant`](https://api.unrealengine.com/INT/API/Runtime/Core/Internationalization/FText/AsCultureInvariant/2/index.html), which produces an `FText` instance that has no localization data (and cannot be localized). The `INVTEXT` macro can do the same thing for literal strings.

## Text Literals

Localizable text is made up of three components: a **Namespace**; a **Key** (which form its identity); and a **Source String** (which is the basis of what gets translated, and acts as validation against "stale" translations). The most common way to create localizable text in UE is by using a text literal.

### Creating Text Literals in C++

Text literals can be created in C++ by using the `LOCTEXT` family of macros.

**Text Literal Macros**

| Macro | Description |
| --- | --- |
| **NSLOCTEXT** | Creates a localized piece of text by defining the Namespace, Key, and Source String. |
| **LOCTEXT** | Creates a localized piece of text by defining the Key and Source String, with the Namespace being defined with `LOCTEXT_NAMESPACE`. |

**Example:**

```
	`// Define the namespace to use with LOCTEXT 	// This is only valid within a single file, and must be undefined before the end of the file 	#define LOCTEXT_NAMESPACE "MyNamespace" 	// Create text literals 	constFTextHelloWorld= NSLOCTEXT("MyOtherNamespace","HelloWorld","Hello World!") 	constFTextGoodbyeWorld= LOCTEXT("GoodbyeWorld","Goodbye World!") 	// Undefine the namespace before the end of the file 	#undef LOCTEXT_NAMESPACE`
Copy full snippet
```
// Define the namespace to use with LOCTEXT // This is only valid within a single file, and must be undefined before the end of the file #define LOCTEXT\_NAMESPACE "MyNamespace" // Create text literals constFTextHelloWorld= NSLOCTEXT("MyOtherNamespace","HelloWorld","Hello World!") constFTextGoodbyeWorld= LOCTEXT("GoodbyeWorld","Goodbye World!") // Undefine the namespace before the end of the file #undef LOCTEXT\_NAMESPACE

### Creating Text Literals in INI Files

Text literals can be created in INI files using the [`NSLOCTEXT`](https://api.unrealengine.com/INT/API/Runtime/Engine/NSLOCTEXT/129/index.html) macro syntax.

### Creating Text Literals in Assets

Text literals can be created using `FText` properties. A Key is generated for you automatically, but you can define a custom Namespace or Key for your text by using the advanced combo next to the text field. It is also fine to use the default Namespace or Key.

## Text Formatting

Text formatting provides a way to combine text in a way that is easier to localize, by using a localizable format pattern that injects real text to replace format placeholders.

Format placeholders are contained within a pair of curly braces, and can be numbers (for index-based formatting) or strings (for name-based formatting). For example:

`"You have {0} health left."` `"You have {CurrentHealth} health left."`

Format placeholders can also specify a function (called an "argument modifier") to run on their argument data. These are specified as a pipe followed by the function name and arguments. For example:

`"{NumCats} {NumCats}|plural(one=cat,other=cats)"`

You can use the **backtick (\`)** character to escape curly braces and pipes and avoid treating them as formatting markup. You can also use the backtick to escape itself to produce a literal \` character.

**Example**: The following table assumes that the value of `Res` is an integer whose value is 10.

| Input | Formatted Text Result |
| --- | --- |
| 
```
	``Result `{ {Res} }``
Copy full snippet
```
Result \`{ {Res} }

 | 

```
	`Result { 10 }`
Copy full snippet
```
Result { 10 }

 |
| 

```
	`` Result \`\`{Res}\`\` ``  
Copy full snippet
```
Result \\\`\\\`{Res}\\\`\\\`

 | 

```
	`` Result \`10\` ``
Copy full snippet
```
Result \\\`10\\\`

 |

### Text Formatting in C++

Text formatting in C++ is handled by the [`FText::Format`](https://api.unrealengine.com/INT/API/Runtime/Core/Internationalization/FText/Format/1/index.html) family of functions. Each function takes an [`FTextFormat`](https://api.unrealengine.com/INT/API/Runtime/Core/Internationalization/FTextFormat/index.html) pattern, which will implicitly construct from an `FText` instance, followed by additional arguments as defined in the table below.

| Argument | Formatting Type | Description |
| --- | --- | --- |
| **FText::Format** | General text formatting. | Either accepts index-based arguments (using [`FFormatOrderedArguments`](https://api.unrealengine.com/INT/API/Runtime/Core/Internationalization/FFormatOrderedArguments/index.html) or variadic arguments), or name-based arguments (using [`FFormatNamedArguments`](https://api.unrealengine.com/INT/API/Runtime/Core/Internationalization/FFormatNamedArguments/index.html)). |
| [**FText::FormatOrdered**](https://api.unrealengine.com/INT/API/Runtime/Core/Internationalization/FText/FormatOrdered/index.html) | Variadic index-based formatting. | Accepts any arguments that [`FFormatArgumentValue`](https://api.unrealengine.com/INT/API/Runtime/Core/Internationalization/FFormatArgumentValue/index.html) can construct from. |
| **[FText::FormatNamed](https://api.unrealengine.com/INT/API/Runtime/Core/Internationalization/FText/FormatNamed/index.html)** | Variadic name-based formatting. | Accepts consecutive name (anything that `FString` can construct from) then value (anything that `FFormatArgumentValue` can construct from) arguments. |

You should consider pre-compiling format patterns you use frequently into an `FTextFormat` to improve formatting performance. The compiled pattern will automatically recompile if the active culture changes.

### Text Formatting in Blueprints

Text formatting in Blueprints is handled by the **Format Text** node. This node can either take a literal format pattern, or the node can have the pattern linked to another Text pin.

-   When a literal format pattern is specified, the format argument pins will be generated automatically. ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0a2b8a5a-f9de-43e9-8a7c-831ac5b46701/textformat-blueprints-01.png)
    
-   When the format pattern is linked to another Text pin, you must manually specify the arguments for the format using the **Details** panel of the node. ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/16c254af-9d47-4ad2-9ac8-1d897be03e80/textformat-blueprints-02.png)
    

### Argument Modifiers

Argument modifiers provide a way to pre-process an argument before it gets added to the formatted string. Argument modifiers are extensible. You create an argument modifier by implementing the [`ITextFormatArgumentModifier`](http://api.unrealengine.com/INT/API/Runtime/Core/Internationalization/ITextFormatArgumentModifier/index.html) interface, and registering a factory function for a given keyword (see [`FTextFormatter::RegisterTextArgumentModifier`](https://api.unrealengine.com/INT/API/Runtime/Core/Internationalization/FTextFormatter/RegisterTextArgumentModifier/index.html)).

UE provides some argument modifiers by default: there are modifiers for plurality, gender, and Hangul post-positions.

#### Plural Forms

Plural forms allow you to use different text based upon a numeric variable given to your text format. Plural forms may be cardinal (such as "There is 1 cat" or "There are 4 cats"), or ordinal (such as "You finished 1st!" or "You finished 2nd!"). Plural forms are specified as key-value pairs, and support any of the following keywords (as defined for your culture by the CLDR data): zero, one, two, few, many, other. Values are an optionally quoted string, that can also contain format markers.

**Cardinal Format Example:**

```
	`"There {NumCats}|plural(one=is,other=are) {NumCats} {NumCats}|plural(one=cat,other=cats)"`

Copy full snippet
```
"There {NumCats}|plural(one=is,other=are) {NumCats} {NumCats}|plural(one=cat,other=cats)"

**Ordinal Format Example:**

```
	`"You came {Place}{Place}|ordinal(one=st,two=nd,few=rd,other=th)!"`

Copy full snippet
```
"You came {Place}{Place}|ordinal(one=st,two=nd,few=rd,other=th)!"

#### Gender Forms

Gender forms allow you to use different text based on an [`ETextGender`](https://api.unrealengine.com/INT/API/Runtime/Core/Internationalization/ETextGender/index.html) value given to your text format, such as "Le guerrier est fort" or "La guerrière est forte". Gender forms are specified as a list of values in the order of \[masculine, feminine, neuter\], where neuter is optional. Values are an optionally quoted string that may also contain format markers.

**Format Example:**

```
	`"{Gender}|gender(Le,La) {Gender}|gender(guerrier,guerrière) est {Gender}|gender(fort,forte)"`

Copy full snippet
```
"{Gender}|gender(Le,La) {Gender}|gender(guerrier,guerrière) est {Gender}|gender(fort,forte)"

#### Hangul Post-Positions

Hangul post-positions help you follow the grammar rules present in Korean, and will insert the correct glyph(s) based on whether the value being inserted ends in a consonant or a vowel, such as "사람은" or "사자는". Hangul post-positions are specified as a list of values in the order of \[consonant, vowel\]. Values are an optionally quoted string.

**Format Example:**

```
	`"{Arg}|hpp(은,는)"`

Copy full snippet
```
"{Arg}|hpp(은,는)"

### Text Formatting Best Practices

-   When injecting a number that affects the sentence, handle these variances using the plural forms argument modifiers, rather than branching in code. When you use plural forms, the sentence is correctly translated for languages that do not share the plural rules of your source language.
    
-   When injecting a personal noun, make sure you include an argument for the gender of the person. This is important for languages with grammar rules for gender, as it allows your translators to switch their translation based on the gender (see [Gender Forms](/documentation/en-us/unreal-engine/text-localization-in-unreal-engine#genderforms)).
    
-   Avoid injecting nouns for objects (such as "table," "door," or "chair"), or be prepared to make them localizable. These nouns might have one gender in one language, and a different gender in another language. This makes the format pattern string impossible to accurately localize without per-culture metadata. Ideally, you should include full sentences rather than just the noun. This will ensure accurate translations.
    
    Future versions of UE might include a function for translators to use metadata to tag text that represents nouns, that they can later branch on in format patterns to produce accurate translations.
    
-   Avoid concatenating partial sentences. This can cause problems, as it is possible for each clause or part to be translated correctly and yet the translation of the whole could be incorrect. It is better to rewrite the text into full sentences, so you can ensure correct translation.
    

## Text Generation

Text generation uses internationalization data to produce culture-correct text that doesn't rely on direct localization. There are three types of text generation: numerical, chronological, and transformative.

### Numerical Text Generation

Numerical generation is used to convert numeric types into a text representation that is friendly for humans to read. The exact rules for this are culture-specific, and can also be tweaked on a per-generation basis if more specific control is required.

As an example, under the default generation rules, the floating-point number "1234.5" would generate as "1,234.5" under English, "1 234,5" under French, and "١٬٢٣٤٫٥" under Arabic.

#### Numerical Generation in C++

Numerical generation in C++ is handled by the following functions.

| Function | Description |
| --- | --- |
| **[FText::AsNumber](https://api.unrealengine.com/INT/API/Runtime/Core/Internationalization/FText/AsNumber/1/index.html)** | Converts any numeric type supported by UE into a user-friendly text representation ("1234.5" becomes "1,234.5"). |
| **[FText::AsPercent](http://api.unrealengine.com/INT/API/Runtime/Core/Internationalization/FText/AsPercent/1/index.html)** | Converts a float or double into a percentage text representation ("0.2" becomes 20%). |
| **[FText::AsMemory](http://api.unrealengine.com/INT/API/Runtime/Core/Internationalization/FText/AsMemory/index.html)** | Converts a value (in bytes) to a user-friendly memory representation ("1234" becomes "1.2 KiB"). |
| **[FText::AsCurrencyBase](https://api.unrealengine.com/INT/API/Runtime/Core/Internationalization/FText/AsCurrencyBase/index.html)** | Converts a value in the base representation of a currency into a user-friendly currency representation ("1234.50" for "USD" becomes "$1,234.50"). |

Most of the functions in the table take an optional `[FNumberFormattingOptions](https://api.unrealengine.com/INT/API/Runtime/Core/Internationalization/FNumberFormattingOptions/index.html)` to control the output (the default is taken from the active locale), and also an optional culture (default is the active locale).

#### Numerical Generation in Blueprints

Numerical generation in Blueprints is handled by the following nodes.

| Nodes | Description |
| --- | --- |
| **ToText (byte), ToText (integer), ToText (float)** | Converts the supported numeric types into a user-friendly text representation ("1234.5" becomes "1,234.5"). |
| **AsPercent** | Converts a float or double into a percentage text representation ("0.2" becomes 20%). |
| **AsCurrency** | Converts a value in the base representation of a currency into a user-friendly currency representation ("1234.50" for "USD" becomes "$1,234.50"). |

Most of the nodes in the table take advanced arguments to control the output.

### Chronological

Chronological generation is used to convert date and time types into a text representation that is friendly for humans to read. The exact rules for this are culture-specific, and the date/time style can be adjusted on a per-generation basis if more specific control is required.

Under the default generation rules, a date representing the 22nd day of the 5th month of the year 1998 would generate "May 22, 1998" under English (United States), "22 May 1998" under English (United Kingdom), "22 mai 1998" under French, and "٢٢‏/٠٥‏/١٩٩٨" under Arabic.

#### Chronological Generation in C++

Chronological generation in C++ is handled by the following functions.

| Function | Description |
| --- | --- |
| **[FText::AsDate](https://api.unrealengine.com/INT/API/Runtime/Core/Internationalization/FText/AsDate/index.html)** | Converts a `FDateTime` value to a user-friendly date representation. |
| **[FText::AsTime](https://api.unrealengine.com/INT/API/Runtime/Core/Internationalization/FText/AsTime/index.html)** | Converts a `FDateTime` value to a user-friendly time representation. |
| **[FText::AsDateTime](https://api.unrealengine.com/INT/API/Runtime/Core/Internationalization/FText/AsDateTime/index.html)** | Converts a `FDateTime` value to a user-friendly date and time representation. |
| **[FText::AsTimespan](https://api.unrealengine.com/INT/API/Runtime/Core/Internationalization/FText/AsTimespan/index.html)** | Converts a `FTimespan` value to a user-friendly delta-time representation (in hours, minutes, and seconds). |

Most of the above take `EDateTimeStyle` to control the output (default is taken from the active locale, but may be set as "short", "medium", "long", or "full").

Time generation expects to be given a UTC-based time by default (which it will convert to the local timezone). If the given time is not UTC-based (such as if it is already in local time), then you should pass `[FText::GetInvariantTimeZone()](https://api.unrealengine.com/INT/API/Runtime/Core/Internationalization/FText/GetInvariantTimeZone/index.html)` as the timezone argument.

#### Chronological Generation in Blueprints

Chronological generation in Blueprints is handled by the following nodes.

| Nodes | Description |
| --- | --- |
| **AsDate** | Converts a non-UTC-based "DateTime" value to a user-friendly date representation as-is (without adjusting to the local timezone). |
| **AsDate (from UTC)** | Converts a UTC-based "DateTime" value to a user-friendly date representation (adjusting to the local timezone). |
| **AsTime** | Converts a non-UTC-based "DateTime" value to a user-friendly time representation as-is (without adjusting to the local timezone). |
| **AsTime (from UTC)** | Converts a UTC-based "DateTime" value to a user-friendly time representation (adjusting to the local timezone). |
| **AsDateTime** | Converts a non-UTC-based "DateTime" value to a user-friendly date and time representation as-is (without adjusting to the local timezone). |
| **AsDateTime (from UTC)** | Converts a UTC-based "DateTime" value to a user-friendly date and time representation (adjusting to the local timezone). |
| **AsTimespan** | Converts a "Timespan" value to a user-friendly delta-time representation (in hours, minutes, and seconds). |

### Transformative

Transformative generation is used to convert text into a different representation of itself. For example, you can convert lower case text to upper case text, or convert upper case text to lower case text.

#### Transformative Generation in C++

Transformative generation in C++ is handled by the following functions.

| Function | Description |
| --- | --- |
| **[FText::ToLower](http://api.unrealengine.com/INT/API/Runtime/Core/Containers/FString/ToLower/)** | Converts a 'FText' instance to its lowercase form in a unicode compliant way. |
| **[FText::ToUpper](https://api.unrealengine.com/INT/API/Runtime/Core/Internationalization/FText/ToUpper/index.html)** | Converts a 'FText' instance to its uppercase form in a unicode compliant way. |

#### Transformative Generation in Blueprints

Transformative generation in Blueprints is handled by the following nodes.

| Node | Description |
| --- | --- |
| **Text to Lower** | Converts a "Text" instance to its lowercase form in a unicode compliant way. |
| **Text to Upper** | Converts a "Text" instance to its uppercase form in a unicode compliant way. |

## String Tables

**String Tables** provide a way to centralize your localized text into one (or several) known locations, and then reference the entries within a string table from other assets or code in a robust way that allows for easy re-use of localized text.

String Tables can be defined in C++, loaded using a CSV file, or created as an Asset. See the [String Tables](/documentation/en-us/unreal-engine/using-string-tables-for-text-in-unreal-engine) page for more information.

## Text Value Marshalling

Text values can be losslessly marshalled as strings (using [`FTextStringHelper`](https://api.unrealengine.com/INT/API/Runtime/Core/Internationalization/FTextStringHelper/index.html), or the [`ImportText`](https://api.unrealengine.com/INT/API/Runtime/CoreUObject/UObject/UScriptStruct/ImportText/index.html) and `ExportText` functions of [`UTextProperty`](https://api.unrealengine.com/INT/API/Runtime/CoreUObject/UObject/UTextProperty/index.html)).

The following formats are supported:

| Text Literal | Description |
| --- | --- |
| [`NSLOCTEXT`](https://api.unrealengine.com/INT/API/Runtime/Engine/NSLOCTEXT/129/index.html) | A text literal that specifies the Namespace, Key, and Source String. |
| `LOCTEXT` | A text literal that specifies the Key, and Source String. |
| `LOCTABLE` | A String Table reference. |
| `INVTEXT` | A piece of culture-invariant text (see [`FText::AsCultureInvariant`](https://api.unrealengine.com/INT/API/Runtime/Core/Internationalization/FText/AsCultureInvariant/2/index.html)). |
| `LOCGEN_NUMBER` | A piece of text generated from a number (see [`FText::AsNumber`](https://api.unrealengine.com/INT/API/Runtime/Core/Internationalization/FText/AsNumber/1/index.html)). |
| `LOCGEN_NUMBER_GROUPED` | A piece of text generated from a number with grouping enabled (see `FText::AsNumber` and [`FNumberFormattingOptions::DefaultWithGrouping`](https://api.unrealengine.com/INT/API/Runtime/Core/Internationalization/FNumberFormattingOptions/DefaultWithGroup-/index.html)). |
| `LOCGEN_NUMBER_UNGROUPED` | A piece of text generated from a number with grouping disabled (see `FText::AsNumber` and [`FNumberFormattingOptions::DefaultNoGrouping`](https://api.unrealengine.com/INT/API/Runtime/Core/Internationalization/FNumberFormattingOptions/DefaultNoGrouping/index.html)). |
| `LOCGEN_NUMBER_CUSTOM` | A piece of text generated from a number with custom formatting options (see `FText::AsNumber` and [`FNumberFormattingOptions`](https://api.unrealengine.com/INT/API/Runtime/Core/Internationalization/FNumberFormattingOptions/index.html)). |
| `LOCGEN_PERCENT` | A piece of text generated from a number as percentage (see [`FText::AsPercent`](http://api.unrealengine.com/INT/API/Runtime/Core/Internationalization/FText/AsPercent/1/index.html)). |
| `LOCGEN_PERCENT_GROUPED` | A piece of text generated from a number as a percentage with grouping enabled (see `FText::AsPercent`, and `FNumberFormattingOptions::DefaultWithGrouping`). |
| `LOCGEN_PERCENT_UNGROUPED` | A piece of text generated from a number as a percentage with grouping disabled (see `FText::AsPercent`, and `FNumberFormattingOptions::DefaultNoGrouping`). |
| `LOCGEN_PERCENT_CUSTOM` | A piece of text generated from a number as a percentage with custom formatting options (see `FText::AsPercent`, and `FNumberFormattingOptions`). |
| `LOCGEN_CURRENCY` | A piece of text generated from a number as a currency (see [`FText::AsCurrencyBase`](https://api.unrealengine.com/INT/API/Runtime/Core/Internationalization/FText/AsCurrencyBase/index.html)). |
| `LOCGEN_DATE_UTC` | A piece of text generated from a UTC date adjusted to the specified or local timezone (see [`FText::AsDate`](https://api.unrealengine.com/INT/API/Runtime/Core/Internationalization/FText/AsDate/index.html)). |
| `LOCGEN_DATE_LOCAL` | A piece of text generated from a non-UTC date without timezone adjustment (see `FText::AsDate`). |
| `LOCGEN_TIME_UTC` | A piece of text generated from a UTC time adjusted to the specified or local timezone (see [`FText::AsTime`](https://api.unrealengine.com/INT/API/Runtime/Core/Internationalization/FText/AsTime/index.html)). |
| `LOCGEN_TIME_LOCAL` | A piece of text generated from a non-UTC time without timezone adjustment (see `FText::AsTime`). |
| `LOCGEN_DATETIME_UTC` | A piece of text generated from a UTC date and time adjusted to the specified or local timezone (see `FText::AsDateTime`). |
| `LOCGEN_DATETIME_LOCAL` | A piece of text generated from a non-UTC date and time without timezone adjustment (see `FText::AsDateTime`). |
| `LOCGEN_TOLOWER` | A piece of text converted to lowercase in a unicode compliant way (see `FText::ToLower`). |
| `LOCGEN_TOUPPER` | A piece of text converted to uppercase in a unicode compliant way (see `FText::ToUpper`). |
| `LOCGEN_FORMAT_ORDERED` | A piece of text generated from a formatting pattern using index-based arguments (see [`FText::FormatOrdered`](https://api.unrealengine.com/INT/API/Runtime/Core/Internationalization/FText/FormatOrdered/index.html)). |
| `LOCGEN_FORMAT_NAMED` | A piece of text generated from a formatting pattern using name-based arguments (see [`FText::FormatNamed`](https://api.unrealengine.com/INT/API/Runtime/Core/Internationalization/FText/FormatNamed/index.html)). |

"Raw" strings can also be imported, but a new key will be generated for each import. This produces unstable keys for localization.

## Data Tables

One common cause of unstable localization keys is iteratively importing raw strings from a CSV file into a **Data Table**, as this causes a new key to be generated after each import. A solution for this is to assign the imported text a deterministic key post-import by overriding the `OnPostDataImport` function on your row struct, and calling `FText::ChangeKey` to assign the new key.

Typically we use the data table name as the Namespace, and a combination of the row name and property name as the Key. For example:

```
	`voidFMyTableRow::OnPostDataImport(constUDataTable*InDataTable,constFNameInRowName,TArray&OutCollectedImportProblems) 	{ 	#if WITH_EDITOR 		MyTextProperty = FText::ChangeKey( 		InDataTable->GetName(), 		FString::Printf(TEXT("%s_%s"),*InRowName.ToString(), GET_MEMBER_NAME_STRING_CHECKED(FMyTableRow,MyTextProperty)), 		MyTextProperty 		); 	#endif// WITH_EDITOR 	}`

Copy full snippet
```
voidFMyTableRow::OnPostDataImport(constUDataTable\*InDataTable,constFNameInRowName,TArray&OutCollectedImportProblems) { #if WITH\_EDITOR MyTextProperty = FText::ChangeKey( InDataTable->GetName(), FString::Printf(TEXT("%s\_%s"),\*InRowName.ToString(), GET\_MEMBER\_NAME\_STRING\_CHECKED(FMyTableRow,MyTextProperty)), MyTextProperty ); #endif// WITH\_EDITOR }

As of the 4.22 release, deterministic keys are already applied to any raw strings imported into a Data Table, but you can still override `OnPostDataImport` if you need custom keying behavior.

## Polyglot Data

Polyglot data allows new localization data to be added at runtime, either to interface with an external system, or to allow hot-fixing localization without building new `LocRes` files.

Polyglot data is comprised of: a Namespace and Key (its identity); a Native String; the category of the text (such as game, engine, editor), to control when the polyglot data is used; an optional native culture (which will fallback to the native culture of the category if unset); and a series of per-culture translations.

If you want to use polyglot data to override an existing translation, then you must ensure the Namespace, Key, and Native String of the polyglot data matches that of the source text you intend to replace.

### Polyglot Data in C++

Polyglot data in C++ is represented by the [`FPolyglotTextData`](https://api.unrealengine.com/INT/API/Runtime/Core/Internationalization/FPolyglotTextData/index.html) type, and it can either be used directly (using [`FPolyglotTextData::GetText`](http://api.unrealengine.com/INT/API/Runtime/Core/Internationalization/FPolyglotTextData/GetText/index.html) to resolve the polyglot data into a text instance), or it can be passed to [`FTextLocalizationManager::RegisterPolyglotTextData`](https://api.unrealengine.com/INT/API/Runtime/Core/Internationalization/FTextLocalizationManager/RegisterPolyglot-/index.html) (to patch existing text entries).

### Polyglot Data in Blueprints

Polyglot data in Blueprints is represented by the **Polyglot Text Data** type, and can be used with the **Polyglot Data to Text** function to resolve the polyglot data into a text instance.

## Localized Text Sources

Localized text sources are the primary way that the UE text localization manager discovers and processes localized text data. UE provides two of these by default: `FLocalizationResourceTextSource` (which hosts `LocRes` support), and `FPolyglotTextSource` (which hosts polyglot data support).

Localized text sources can provide a way to interface with an external system, and can be added on a per-project basis by creating and registering a type derived from [`ILocalizedTextSource`](https://api.unrealengine.com/INT/API/Runtime/Core/Internationalization/ILocalizedTextSource/index.html).