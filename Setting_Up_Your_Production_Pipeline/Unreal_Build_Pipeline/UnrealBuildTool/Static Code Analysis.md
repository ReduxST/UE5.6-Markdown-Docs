# Static Code Analysis

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/static-code-analysis-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/static-code-analysis-in-unreal-engine)  
**Processed:** 2025-06-14 16:52:13

---

**Unreal Build Tool (UBT)** supports running several different static code analyzers. **Static Code Analyzers** use a variety of algorithms and techniques to inspect source code and find bugs without executing the code. This means faster analysis, earlier detection of memory leaks and logic errors, and reduced technical debt.

## Use a Static Code Analyzer with UBT

The general command-line syntax for running a static code analyzer with UBT from your Unreal Engine root directory is:

```
`Engine\Build\BatchFiles\RunUBT.bat TARGET PLATFORM Development -StaticAnalyzer=ANALYZER`
Copy full snippet
```
Engine\\Build\\BatchFiles\\RunUBT.bat TARGET PLATFORM Development -StaticAnalyzer=ANALYZER

`TARGET`, `PLATFORM`, and `ANALYZER` are required arguments in the above command you must replace with your desired values.

-   `TARGET`: A build target supported by UBT, see the documentation on [Targets](/documentation/en-us/unreal-engine/unreal-engine-build-tool-target-reference) for more information.
-   `PLATFORM`: A platform supported by Unreal Engine. Visit the [General Platform Support](/documentation/en-us/unreal-engine/tools-for-general-platform-support-in-unreal-engine) pages to learn about Unreal Engine platform support.
-   `ANALYZER`: A static code analyzer that UBT uses to analyze the provided target on the designated platform. Refer to the [Supported Analyzers](/documentation/en-us/unreal-engine/static-code-analysis-in-unreal-engine#supportedanalyzers) section below to view the available options.

### Supported Analyzers

| Analyzer | Description |
| --- | --- |
| Default | Default static analyzer for the selected compiler (if it has one). |
| VisualCpp | Built-in Visual C++ static analyzer. Only supported for Microsoft Visual C++ (MSVC) based platforms. |
| PVSStudio | 
VS-Studio static analyzer. Only supported for MSVC-based platforms.

PVS-Studio requires a license file placed next to the installed `PVS-Studio.exe` executable. For more information about PVS-Studio and obtaining a license, visit the [PVS-Studio](https://pvs-studio.com/) documentation.



 |
| Clang | 

Clang static analyzer. This forces the compiler to Clang for MSVC-based platforms.

As of UE 5.3, Clang static analysis requires you to build with the `-DisableUnity` flag. No warnings are reported if this flag is omitted. As a result of this, if you analyze the engine with `-DisableUnity`, there are additional warnings that we are actively working on resolving that might be unrelated to your project code.

One way to reduce the number of warnings is to focus Clang static analysis on a specific module by using the command-line argument `-Module=<PROJECT_MODULE>`.



 |

### Examples

Run the following command from your Unreal Engine root directory to use the default static code analyzer with Unreal Editor as the target on a Windows 64-bit platform:

```
`Engine\Build\BatchFiles\RunUBT.bat UnrealEditor Win64 Development -StaticAnalyzer=Default`
Copy full snippet
```
Engine\\Build\\BatchFiles\\RunUBT.bat UnrealEditor Win64 Development -StaticAnalyzer=Default

Run the following command from your Unreal Engine root directory to use the Visual C++ static code analyzer with the Lyra Starter Game as the target on a Windows 64-bit platform:

```
`Engine\Build\BatchFiles\RunUBT.bat LyraGame Win64 Development -StaticAnalyzer=VisualCpp`
Copy full snippet
```
Engine\\Build\\BatchFiles\\RunUBT.bat LyraGame Win64 Development -StaticAnalyzer=VisualCpp

### Command-line Options for Clang Analyzer

| Option | Description |
| --- | --- |
| `-StaticAnalyzerOutputType=html` | Writes out web pages with navigation that describe the analysis warnings. These HTML files are written into the appropriate folders within the `Engine/Intermediate/Build` directory for the selected platform and target. |
| `-StaticAnalyzerMode=shallow` | Enables shallow analysis. This means analysis completes more quickly, but is less informative than standard analysis. We do not recommend using this mode for general purposes. |
| `-StaticAnalyzerChecker=CHECKER` | Provides a list of static analyzer checkers that you want to enable rather than the default list. |
| `-StaticAnalyzerDisableChecker=CHECKER` | Disables static analyzer default checkers. This option overrides the default disabled checkers which are `deadcode.DeadStores` and `security.FloatLoopCounter`. This option is unused if `-StaticAnalyzerChecker` is set. |
| `-StaticAnalyzerAdditionalChecker=CHECKER` | Enables additional non-default static analyzer checkers. This option is unused if `-StaticAnalyzerChecker` is set. |

For a full list of Clang analyzer checkers, see [Available Checkers](https://clang.llvm.org/docs/analyzer/checkers.html) in the Clang documentation.