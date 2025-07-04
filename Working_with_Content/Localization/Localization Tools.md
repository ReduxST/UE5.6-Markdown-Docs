# Localization Tools

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/localization-tools-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/localization-tools-in-unreal-engine)  
**Processed:** 2025-06-14 16:34:13

---

## The Localization Dashboard

The **Localization Dashboard** in **Unreal Engine (UE)** is a tool that takes care of managing your localization targets. While it's still classed as experimental, it is stable and is used internally for all of our projects. It is the recommended way to manage **Localization Targets**, and can be accessed through the **Tools** menu in the editor.

The Dashboard will create a **Game** Localization Target for you by default, and unless your project is particularly complex, this is probably the only Localization Target you need. You can use the **Gather Text** settings to specify where your source code and Assets can be found, and you can use the **Cultures** settings to specify which languages you are going to localize your project for. This includes setting your **Native** culture to the language you author your content in.

If you add a new Localization Target, make sure you specify an appropriate loading policy for it (typically **Game**). If you don't, the Localization Target does not get loaded at runtime.

Once your Localization Target is set up, you can use the toolbar under the **Cultures** section to **Gather**, **Export**, **Import**, and **Compile** your project texts. This is a process that can be run iteratively over time as new translations become available, or as new source text is added.

Once you run these actions, you will find some INI files in your `Config/Localization` folder. These are generated each time those actions are run using the Dashboard, and do not need to be submitted to source control unless you plan to [automate your localization](/documentation/en-us/unreal-engine/localization-tools-in-unreal-engine#automatinglocalization) pipeline.

Currently the Localization Dashboard and localization commandlets (which form the localization pipeline) have two completely different configuration layouts for a Localization Target (with the Localization Dashboard generating the commandlet version).

## Translation Editor

The **Translation Editor** is accessible through the Localization Dashboard. This provides a simple way to check the translation for a piece of text. It provides three translation tabs in its UI:

-   **Untranslated**: Text that has no translation associated with it.
    
-   **Needs Review**: Text that has previously been translated against an older version of the source text.
    
-   **Completed**: Text that has been translated against the current version of the source text.
    

The Translation Editor is a simple tool that is not updated frequently, and is probably lacking features that you would want for a comprehensive translation effort (for example, it has no translation memory). Because of this, we recommend that you only use the Translation Editor for spot-fixes. Instead of using the Translation Editor, we recommend that you use the PO export/import pipeline, combined with an external translation tool (such as [Poedit](https://poedit.net/), [OneSky](https://www.oneskyapp.com/), or [XLOC](http://www.xloc.com/)) for general translation work.

## Translation Picker

The **Translation Picker** is an experimental tool that is not updated frequently. This tool lets you interrogate information from the text values used in your UI, including when using **Play in Editor (PIE)**.

Enable the Translation Picker by clicking **Editor Preferences > Experimental**. Once enabled, it can be accessed through the **Window** menu in the Editor.

When the Translation Picker is active, it will show a floating window near your cursor that lists all the text values used by the widget under the cursor. Once you have found the text value you want to inspect, you can press the ESC key to lock the picker to that selection.

Localizable text (in other words, text that has an identity and has also been gathered and compiled into a LocRes file) will show an inline editable text field that can be used to spot-fix the current translation. ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e78bdb17-2dad-4889-b974-1694465caaab/loctools-01.png)

The ability to edit a translation inline was broken in Unreal Engine versions 4.13 - 4.21, but it has been fixed for Unreal Engine version 4.22.

## Automating Localization

Localization automation is available by using the Localize script of the **Unreal Automation Tool** (UAT). This script provides a way to run various parts of the localization pipeline, and you can use it to generate nightly localization updates for your products, as well as to interface with your external localization provider. This script is currently hard-coded for a **Win64 Development Editor** build.

Prior to Unreal Engine version 4.22:

-   This script was named **Localise**. This name still exists as an alias.
    
-   `OneSky` was the default value for the `LocalizationProvider` argument. If you are not using a localization provider, you will have to set this argument to an empty string.
    

A basic invocation, without an external localization provider, for an in-source build (a project within the Unreal Engine root folder) would look like this:

```
	`Localize-UEProjectDirectory="YourProject"-UEProjectName="YourProject"-LocalizationProjectNames="TargetName"`

Copy full snippet
```
Localize-UEProjectDirectory="YourProject"-UEProjectName="YourProject"-LocalizationProjectNames="TargetName"

A basic invocation, without an external localization provider, for an out-of-source build (a project outside the UE root folder) would look like this:

```
	`Localize-UEProjectRoot="Path/To/Project"-UEProjectDirectory=""-UEProjectName="YourProject"-LocalizationProjectNames="TargetName"`

Copy full snippet
```
Localize-UEProjectRoot="Path/To/Project"-UEProjectDirectory=""-UEProjectName="YourProject"-LocalizationProjectNames="TargetName"

Interfacing with an external localization provider involves creating a class deriving from `LocalizationProvider`. We provide two localization providers by default, OneSky and XLOC.

| Localization Provider | Implementation Information |
| --- | --- |
| **OneSky** | 
-   Implemented by `OneSkyLocalizationProvider.`
    
-   Create a class derived from `OneSkyConfigData` to contain your configuration data, and pass the Name of the configuration to the `-OneSkyConfigName` argument to choose the correct configuration.
    
-   Pass the name of your OneSky group to the `-OneSkyProjectGroupName` argument.
    
-   Pass `-LocalizationProvider=OneSky` to use the OneSky localization provider.
    



 |
| **XLOC** | 

-   Implemented by `XLocLocalizationProvider.`
    
-   Create a class derived from `XLocLocalizationProvider` and fill in the `Config` variable with your configuration data.
    
-   Override `StaticGetLocalizationProviderId` and `GetLocalizationProviderId` to return the name of your configuration, and pass this name to the `-LocalizationProvider` argument to choose the correct configuration.
    



 |