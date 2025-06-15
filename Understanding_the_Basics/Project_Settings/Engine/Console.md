# Console

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/console-settings-in-the-unreal-engine-project-settings](https://dev.epicgames.com/documentation/en-us/unreal-engine/console-settings-in-the-unreal-engine-project-settings)  
**Processed:** 2025-06-14 16:15:05

---

This page is about project-wide settings for console input in Unreal Engine. Not to be confused with game console (platform) support.

## Console

### General

| **Section** | **Description** |
| --- | --- |
| **Max Scrollback Size** | The size of the history of previously input commands. |

### Auto-Complete

| **Section** | **Description** |
| --- | --- |
| **Manual Auto-Complete List** | Manual list of auto-complete commands and info specified in `BaseInput.ini` (in the `Engine/Config` folder within your engine install directory). |
| **Auto Complete Map Paths** | 
List of relative paths (for example, `Content/Maps`) to search for map names for auto-complete usage.

Specified in `BaseInput.ini` (in the `Engine/Config` folder within your engine install directory).



 |
| **Order Top to Bottom** | Defines whether console commands are ordered bottom-to-top (legacy behavior) or top-to-bottom. |
| **Display Help in Auto-Complete** | If enabled, displays the first line of any available help text in the auto-complete window, if a description isn't available. |

### Colors

| **Section** | **Description** |
| --- | --- |
| **Background Opacity Percentage** | Amount of transparency of the console background. |
| **Input Color** | The color used for text input. |
| **History Color** | The color used for the previously typed commands history. |
| **Auto-Complete Command Color** | The auto-complete color used for executable commands. |
| **Auto-Complete CVar Color** | The auto-complete color used for mutable Console Variables (CVars). |
| **Auto-Complete Faded Color** | The auto-complete color used for command descriptions and read-only CVars. |