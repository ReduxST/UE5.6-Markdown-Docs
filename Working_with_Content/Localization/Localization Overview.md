# Localization Overview

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/localization-overview-for-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/localization-overview-for-unreal-engine)  
**Processed:** 2025-06-14 16:34:12

---

## Localization and Internationalization

Localization and Internationalization (L10N and I18N) are two concepts that are often combined under the umbrella of "localization". However, they are two distinct things, and **Unreal Engine (UE)** handles them in different ways. The localization system in **UE** is centered around our "text" type, whereas our internationalization support makes use of the [International Components for Unicode](http://site.icu-project.org/) (ICU) library.

While they are separate, in UE you cannot have localization at runtime without the appropriate internationalization support.

## ICU and Internationalization Support

**ICU** is a mature and robust internationalization library that UE uses to deal with anything involving culture-specific data or processing, including the following:

-   Obtaining the current culture for the platform/OS.
    
-   Handling the prioritized fallback of cultures.
    
-   Handling the culture correct formatting of numbers (including percentages and currency), and dates and times (including timezone data).
    
-   Handling the culture correct plurarity of numbers (during text formatting).
    
-   Handling Unicode compliant transformation of text (eg, ToUpper, ToLower).
    
-   Handling Unicode compliant comparison and collation of text.
    
-   Handling Unicode compliant [boundary analysis](https://unicode-org.github.io/icu/userguide/boundaryanalysis/) (characters, words, and line-breaks).
    
-   Handling Unicode compliant bi-directional (BiDi) text detection.
    

The culture-specific data that ICU needs to function is stored outside of ICU itself, and UE provides some coarse data sets that you can use to minimize your project size:

-   English (~1.77MB)
    
-   EFIGS - English, French, Italian, German, and Spanish (~2.38MB)
    
-   EFIGSCJK - English, French, Italian, German, Spanish, Chinese, Japanese, and Korean (~5.99MB)
    
-   CJK - Chinese, Japanese, and Korean (~5.16MB)
    
-   All (~15.3MB)
    

Which one of these you choose depends on what regions you localize your project for, and these choices can be set in your **Project Settings**. See [Packaging Localization Data](/documentation/en-us/unreal-engine/localization-overview-for-unreal-engine#packaginglocalizationdata) for more information.

## Cultures

Cultures in UE contain internationalization information for a particular locale. Culture names are composed of three hyphen-separated parts (an [IETF language tag](https://en.wikipedia.org/wiki/IETF_language_tag)):

-   A two-letter [ISO 639-1](https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes) language code (such as "zh").
    
-   An optional four-letter [ISO 15924](https://en.wikipedia.org/wiki/ISO_15924) script code (such as "Hans").
    
-   An optional two-letter [ISO 3166-1](https://en.wikipedia.org/wiki/ISO_3166-1) country code (such as "CN").
    

When UE looks for localization data for a particular culture, it processes them from most to least specific. For example:

-   zh-Hans-CN is processed as "zh-Hans-CN", then "zh-CN", then "zh-Hans", then "zh".
    
-   en-GB is processed as "en-GB", then "en".
    

In order to achieve the widest coverage for a particular culture, use the least specific culture code that is valid. Usually that is just the language code, but you should be aware of regional language variations that need to be considered.

In most cases these regional variations are limited to a specific country code, which makes them easy to resolve. However, there are some more complex cases as shown below.

### Chinese

Chinese has two variants, Simplified and Traditional, represented by the "Hans" and "Hant" ISO-15924 script codes. Use "zh-Hans" for your Simplified localization, and "zh-Hant" for your Traditional localization.

### Spanish

Spanish has two main variants: European and Latin American. However, there is no convenient script code that can be used to distinguish one from the other. There is an IETF language tag for Latin American Spanish ("es-419"), but most platforms will not provide this, and instead will give you an actual country code ("es-MX").

To solve this, use "es" for European Spanish, and "es-419" for Latin American Spanish. Then use the [culture remapping](/documentation/en-us/unreal-engine/managing-the-active-culture-at-runtime#cultureremapping) feature of UE to map the Latin American Spanish speaking countries to "es-419".

This can be done by adding the following to your `DefaultGame.ini` file:

```
	`[Internationalization] 	+CultureMappings="es-AR;es-419" 	+CultureMappings="es-BO;es-419" 	+CultureMappings="es-CL;es-419" 	+CultureMappings="es-CO;es-419" 	+CultureMappings="es-CR;es-419" 	+CultureMappings="es-CU;es-419" 	+CultureMappings="es-DO;es-419" 	+CultureMappings="es-EC;es-419" 	+CultureMappings="es-GT;es-419" 	+CultureMappings="es-HN;es-419" 	+CultureMappings="es-MX;es-419" 	+CultureMappings="es-NI;es-419" 	+CultureMappings="es-PA;es-419" 	+CultureMappings="es-PE;es-419" 	+CultureMappings="es-PR;es-419" 	+CultureMappings="es-PY;es-419" 	+CultureMappings="es-SV;es-419" 	+CultureMappings="es-US;es-419" 	+CultureMappings="es-UY;es-419" 	+CultureMappings="es-VE;es-419"`

Copy full snippet
```
\[Internationalization\] +CultureMappings="es-AR;es-419" +CultureMappings="es-BO;es-419" +CultureMappings="es-CL;es-419" +CultureMappings="es-CO;es-419" +CultureMappings="es-CR;es-419" +CultureMappings="es-CU;es-419" +CultureMappings="es-DO;es-419" +CultureMappings="es-EC;es-419" +CultureMappings="es-GT;es-419" +CultureMappings="es-HN;es-419" +CultureMappings="es-MX;es-419" +CultureMappings="es-NI;es-419" +CultureMappings="es-PA;es-419" +CultureMappings="es-PE;es-419" +CultureMappings="es-PR;es-419" +CultureMappings="es-PY;es-419" +CultureMappings="es-SV;es-419" +CultureMappings="es-US;es-419" +CultureMappings="es-UY;es-419" +CultureMappings="es-VE;es-419"

## Localization Targets

**Localization Targets** are named, self-contained modules of localization data. Localization Targets have the following properties:

-   They have text gathered from a specified set of sources;
    
-   They are stored in a manifest file;
    
-   They are translated in culture-specific archive files;
    
-   They are compiled into culture-specific localization resource files, and the compiled culture-specific resource files are what the system displays.
    

A project can have a single Localization Target for simplicity, or it can have multiple Localization Targets in order to break up the project's localization data into sections. The Unreal Editor has a separate Localization Target from the rest of UE, so that the Editor can be localized without distributing that localization data with games. Typically, a game will have one Localization Target for all of the base project's localization data, and additional Localization Targets for any expansions.

## Localization Pipeline

The UE localization pipeline is modeled around an "author-at-source" approach to localization. This means that if you need some text saying "Hello World!" in your UI, you just type "Hello World!" into the text property (or use the `NSLOCTEXT` or `LOCTEXT` macros in C++) and the localization gatherer takes care of capturing the text so that it can be localized.

The "author-at-source" approach is very dynamic, and this approach allows developers to avoid thinking much about localization during development. However, it can also be frustrating for teams that want strict control over the text used in their project. To address this, UE has support for [String Tables](/documentation/en-us/unreal-engine/using-string-tables-for-text-in-unreal-engine) to allow an "author-once-and-reference" approach to localization (although internally, the pipeline just treats String Tables as another "author-at-source" source).

An older (and no longer supported) method to work around the lack of native String Tables was to use a "fake" native culture (most likely "es-US-POSIX") with IDs as the source text, and then use the string collapsing functions UE had prior to version 4.14 to translate these IDs into each language. You may find references to this method in older support questions, but it should no longer be used. Projects using that method should migrate to String Tables.

The localization pipeline itself works on Localization Targets, and a Localization Target is made up of two parts: its configuration (stored in `Config/Localization/`), and its data (stored in `Content/Localization/{TargetName}/`).

If we assume a Localization Target working with English ("en") and French ("fr"), then its layout in the `Content/Localization/` folder would look like this:

```
	`{TargetName}/ 	{TargetName}.manifest 	{TargetName}.locmeta 	en/ 		{TargetName}.archive 		{TargetName}.po 		{TargetName}.locres 	fr/ 		{TargetName}.archive 		{TargetName}.po 		{TargetName}.locres`

Copy full snippet
```
{TargetName}/ {TargetName}.manifest {TargetName}.locmeta en/ {TargetName}.archive {TargetName}.po {TargetName}.locres fr/ {TargetName}.archive {TargetName}.po {TargetName}.locres

All of the above files and folders are generated by the various parts of the localization pipeline.

| Folder | Description |
| --- | --- |
| **{TargetName}.manifest** | 
-   Manifests are custom JSON files that store all of the text gathered from your source code and assets by the localization pipeline.
    
-   Manifests are re-generated each time the localization gather step is run, and shouldn't be hand-edited.
    



 |
| **{TargetName}.archive** | 

-   Archives are custom JSON files that store per-culture translations for the text gathered into the manifest.
    
-   Archives are trimmed each time the localization gather or import steps are run to remove entries for old sources.
    
-   Archives can be hand-edited, but we strongly suggest that you do not hand-edit. Our recommended workflow is to edit the exported PO files and re-import them.
    



 |
| **{TargetName}.po** | 

-   PO ([Portable Object](https://www.gnu.org/software/gettext/manual/html_node/PO-Files.html)) files contain the per-culture text to be translated, along with their current translations.
    
-   PO files are generated by the localization export text step, and are re-imported into the archives by the localization import text step.
    
-   PO is a common format, and may be edited locally either by-hand or via a translation tool like [Poedit](https://poedit.net/), or collaboratively via something like [OneSky](https://www.oneskyapp.com/) or [XLOC](http://www.xloc.com/).
    



 |
| **{TargetName}.locres** | 

-   LocRes are custom binary files that store the compiled per-culture translations for use at runtime.
    
-   LocRes files are re-generated each time the localization compile step is run, and get staged into a packaged build.
    
-   LocRes are the only files that your project will load localization data from at runtime (including in the editor), so any edits or changes to your source data (such as from importing a PO file) must be compiled before they take effect.
    



 |
| **{TargetName}.locmeta** | 

-   LocMeta are custom binary files that store the compiled target meta-data (currently only the native culture for the target) for use at runtime.
    
-   LocMeta files are regenerated each time the localization data is compiled, and is staged into a packaged build.
    



 |

Localization Targets also specify a "native" culture, which should be set to the culture that you author your content in (commonly referred to as your "source text" or "source data").

Native cultures can contain "translations" just like any other culture, although native culture translations only exist to facilitate copy-editing your source text without editing the source code or assets directly.

Foreign cultures use the native culture text as their source text for translation, and will become "stale" if the native culture text is changed (there's a setting in the localization compile step to allow stale translations if required).

For more information on optimizing your localization pipeline, see [Pipeline Optimization](/documentation/en-us/unreal-engine/pipeline-optimization-for-localization-in-unreal-engine).

## PO File Format

Unreal uses the following default format for its PO files, depending on the collapse mode being used in the PO export.

-   When using the **Identical Text Identity and Source Text** collapse mode:
    -   `msgctxt` contains the Unreal identity of the entry.
    -   `msgid` contains the source string.
    -   `msgstr` contains the translation.
-   When using the **Identical Namespace and Source Text** collapse mode:
    -   `msgctxt` contains the Unreal namespace of the entry.
    -   `msgid` contains the source string.
    -   `msgstr` contains the translation.

We also have an alternative format that produces better results if you're using Crowdin to manage your translations, though please note that this format isn't able to detect stale translations imported from PO files (as we no longer have the source the translation was made against).

This mode produces the same output when using the Identical Namespace and Source Text collapse mode, but for the Identical Text Identity and Source Text collapse mode it produces the following:

-   `msgctxt` is unused.
-   `msgid` contains the Unreal identity of the entry.
-   `msgstr` contains the source string (for the native culture), or the translation (for foreign cultures).
-   `X-Crowdin-SourceKey` header attribute specifies that `msgstr` is used as the source text from the native culture.

## Packaging Localization Data

Packaging the correct localization and internationalization data for your project requires adjusting some settings under the advanced **Packaging** section of your **Project Settings**.

The two settings you'll want to verify are:

-   **Localizations to Package** - With this you can choose which cultures you want to stage localization data for. You can use the **Show Localized** option to filter the list to only show cultures that you have `LocRes` files for.
    
-   **Internationalization Support** - With this you can choose which set of ICU internationalization data you want to stage. This option must overlap with the localization data you intend to stage.