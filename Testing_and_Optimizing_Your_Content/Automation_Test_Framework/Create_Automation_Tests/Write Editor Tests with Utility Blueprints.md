# Write Editor Tests with Utility Blueprints

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/write-editor-tests-with-utility-blueprints-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/write-editor-tests-with-utility-blueprints-in-unreal-engine)  
**Processed:** 2025-06-14 17:05:16

---

The **EditorTests** plugin is required. To enable it, follow these steps:

1.  Select **Edit > Plugins** to open the **Plugin** panel.
2.  Use the search bar to find the plugin.
3.  Enable the corresponding checkbox.
4.  Restart Unreal Editor.

You can create scripts for automated tests in the Editor with [Editor Utility Blueprint](/documentation/en-us/unreal-engine/scripting-the-unreal-editor-using-blueprints).

## Creating Editor Utility Blueprint Tests

You can create an Editor Utility Blueprint by clicking the **Add** button in the **Content Browser**, selecting **Editor Utilities > Editor Utility Blueprint**, then searching for "EditorUtilityTest" in the **Pick Parent Class** window.

Name the asset appropriately as its path will be used to name the test using the following pattern: `Project.Blueprints.EditorUtilities.<content path>.<asset name>`.

## Implementing Editor Utility Blueprint Tests

Editor Utility Blueprints have two event suggestions by default:

-   **Prepare Test** - Use this to perform any setup required before starting the test and then call **Finish Prepare Test**. If this event fails or times out, the **Start Test** event will not be called.
-   **Start Test** - The main event. After calling this, you can use normal utility Blueprint nodes before calling **Finish Test** to finish the test.

You must call **Finish Test**, or the test will timeout. You can set up additional instructions on test completion by overriding the **Finished Test** function. The code execution must be blocking.

You can set timeouts and metadata in the asset's **Details** panel.

## Testing Editor Utility Blueprint with Editor Utility Test

To automate testing, you can create an Editor Utility Test Blueprint that instantiates a corresponding Editor Utility Blueprint.

In the Blueprint graph, add the **Construct** node and set the **Class** to the relevant Editor Utility class. Afterward, you can call any class function.

You can store the **Construct** node's return value in a variable to use multiple calls without re-instantiation.