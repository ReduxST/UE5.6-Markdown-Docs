# Project Settings

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/project-settings-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/project-settings-in-unreal-engine)  
**Processed:** 2025-06-14 16:44:57

---

The **Project Settings** window provides access to configuration options that affect:

-   Your Unreal Engine project.
-   How the engine behaves when running your project.
-   How the project should run on specific platforms.

Some plugins also append their configuration options to the Project Settings window.

All of the settings in this window are stored in your project's default engine configuration file (`Engine.ini`). The Project Settings window provides a visual, intuitive, and searchable user interface for editing these. You can also manually edit the `Engine.ini` file to change individual settings.

## Accessing Project Settings

To open the Project Settings window, from Unreal Engine's main menu, go to **Edit > Project Settings**.

![Selecting Project Settings in Edit menu](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/67ded7cf-dc69-47b5-91e0-6a372126360a/001-edit-menu.png)

## Categories and Sections

The Project Settings window is divided up into categories and sections of related options. Select a category from the navigation on the left to open its associated settings in the right-hand panel. You can also search for a specific option by name.

You can export the settings into a backup file on your computer or import settings from the file by clicking **Export** or **Import** in the upper-right corner of the Project Settings window.

The editor `.ini` file is updated every time you change something in the Project Settings, and the values in it apply to all platforms. The editor `.ini` file is in `<ProjectDirectory>\Config\DefaultEngine.ini`.

Platform `.ini` files have to be edited manually in a text editor and only apply to a specific platform. An example of a platform `.ini` file is `<ProjectDirectory>\Config\Windows\WindowsEngine.ini`

The Project Settings window contains the following sections and categories: