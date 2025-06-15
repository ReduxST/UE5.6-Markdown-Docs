# Configure Automation Tests

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/configure-automation-tests-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/configure-automation-tests-in-unreal-engine)  
**Processed:** 2025-06-14 16:14:47

---

## Test Groups

Test groups are sets of tests collected from a list of filters based on test names.

You can refer to them through the command line argument `-ExecCmds="Automation RunTest"` or through the **Test Automation** window filter. This is useful to collect tests that belong to different sections.

You can define a test group by editing the `DefaultEngine.ini` config file and adding the following line:.

```
`+Groups=(Name="Group1", Filters=((Contains=".Some String."))) +Groups=(Name="Group2", Filters=((Contains="Group2.", MatchFromStart=true),(Contains=".Group2.")))`
Copy full snippet
```
+Groups=(Name="Group1", Filters=((Contains=".Some String."))) +Groups=(Name="Group2", Filters=((Contains="Group2.", MatchFromStart=true),(Contains=".Group2.")))

Afterward, you can reference a test group with `Group:<GroupName>` in the `ExecCmds` argument and in [Gauntlet](/documentation/en-us/unreal-engine/gauntlet-automation-framework-overview-in-unreal-engine).

## Excluding Tests

During project development, you may need to exclude tests temporarily.

To exclude a test, edit the `DefaultEngine.ini` or the corresponding platform config file with the following line:

```
`+ExcludeTest=(Test="<test or section name>",Reason="<a reason>",Warn=False)`
Copy full snippet
```
+ExcludeTest=(Test="<test or section name>",Reason="<a reason>",Warn=False)

You can exclude all tests that start with a string by inputting a partial name.

You can exclude by Rendering Hardware Interface (RHI) by adding the following line:

```
`+ExcludeTest=(Test="<test or section name>",Reason="<a reason>", RHIs=("Vulkan", "DirectX 11"),Warn=False)`
Copy full snippet
```
+ExcludeTest=(Test="<test or section name>",Reason="<a reason>", RHIs=("Vulkan", "DirectX 11"),Warn=False)

The RHI name must match the syntax from `Engine\Source\Runtime\AutomationTest\Public\AutomationTestExcludelist.h`

Excluded tests will show as "Skipped" with the reason attached as an info event.

You can also exclude tests in the Editor from the **Test Automation** window by selecting the **Exclude** button next to the test's selection checkbox.