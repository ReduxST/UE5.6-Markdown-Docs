# Setting up Autocomplete for Editor Python Scripting

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/setting-up-autocomplete-for-unreal-editor-python-scripting](https://dev.epicgames.com/documentation/en-us/unreal-engine/setting-up-autocomplete-for-unreal-editor-python-scripting)  
**Processed:** 2025-06-14 16:49:19

---

## Prerequisite: Enable Developer Mode

Before setting up autocomplete, you will need to tell the **Unreal Engine (UE) Python Plugin** to generate the necessary stubs. You can do this by checking **Developer Mode** in **Editor Preferences > Plugins > Python**, then restarting the editor. The generated stub file will be located at `PROJECT_DIRECTORY/Intermediate/PythonStub`.

## PyCharm

Open the **Settings** window and navigate to **Project > Python Interpreter**, then click the gear and select **Show all**. In the **Python Interpreter** window, you can click the **Paths** button and click **+** to add the location of your stub file.

![Add the Python stub file path](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/aeeb58bd-aa97-479e-8990-c8af92c6f152/python-stub-path.png)

You will also need to raise the maximum Intellisense file size by navigating to **Help > Edit Custom Properties** and adding the following:

```
		`idea.max.intellisense.filesize = 25000`

Copy full snippet
```
idea.max.intellisense.filesize = 25000

After restarting PyCharm, you will be able to see functions from the UE API in the autocomplete menu.

## VSCode

Navigate to **Settings > Extension > Python** and find **Auto Complete: Extra Paths**. Click the link to open the `settings.json` file, and add the path to your stub file under `python.autoComplete.extraPaths`.

![The Python autocomplete path settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b6655547-1a5c-4de3-a67f-1cce045a707c/vscode-settings-path.png) ![Setting the path in the settings.json file](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8ab3eabf-6b03-4cef-98a5-2b47bcc61a87/vscode-code-path.png)

After restarting **Visual Studio Code (VSCode)**, you should now be able to see functions from the UE API in the autocomplete menu.

## Type Hinting

The Python plugin can now generate the stub with type hinting (for more information on type hinting, see [PEP 484](https://peps.python.org/pep-0484/)). Type hints appear in your Python IDE auto-completion menu. Type hints can be configured by first clicking on **Edit > Editor Preferences** in the Unreal Editor Menu Bar. This will open the **Editor Preferences** tab. Now navigate to **Plugins > Python** to see the available Python Script Plugin user settings. To use Type Hinting, **Developer Mode** must be enabled. Below is a table with the available Type Hinting Modes and descriptions.

| Type Hinting Mode | Description |
| --- | --- |
| **Auto-Completion** | Hints the exact parameters and return type or types of a method. |
| **Type Checker** | Adds up all possible type coercions. For example, it will hint that you can pass a Python string in place of an `unreal.Name`. This makes the auto-completion menu busy and harder to read, though this option will work better if you turn on type checking in your IDE. |
| **Off** | Turns off type hinting altogether. |

By default, the **Type Hinting Mode** is set to **Auto-Completion**.

Note that hinting is not perfect. In some cases, types are not known when generating the stub. In other cases, the C++ reflection API does not provide enough information to accurately hint when a parameter or the return value of a method can be `None`.

The stub file is regenerated each time the editor is started. As a result, you can restart the editor after exposing new functions to Python or enabling new plugins to ensure the stub file is up to date.