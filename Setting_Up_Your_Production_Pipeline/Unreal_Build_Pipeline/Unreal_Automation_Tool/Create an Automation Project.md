# Create an Automation Project

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/create-an-automation-project-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/create-an-automation-project-in-unreal-engine)  
**Processed:** 2025-06-14 16:16:44

---

To create a project-specific automation script, you need to create a new C# project in a location that Unreal Automation Tool can detect it.

## Create an Automation Project

The following steps guide you to create a new C# automation project:

1.  Open command prompt and run `GenerateProjectFiles.bat` from your Unreal Engine root directory.
    1.  This will generate a `UE5.sln` file for Visual Studio.
2.  Open the `UE5.sln` file in Visual Studio.
3.  In Visual Studio, right-click the main **Solution UE5** directory and select **Add > New Project...**
4.  With the **Add a new project** window open, find and select **C# Class Library**.
    
    Do not select the **Class Library (.NET Framework) Visual C#** option. Unreal Automation Tool targets .NET 6.0 and an error will occur if you try to target the .NET Framework.
    
5.  A menu pops up prompting you to choose settings for your new C# Class Library.
6.  Set **Project name** to be the name of your automation script. For example purposes, call this `SampleScript.Automation`.
    
    `<SCRIPT_NAME>.Automation` is the preferred naming convention for automation scripts.
    
7.  The **Location** of your project depends on whether your project is a native or foreign Unreal Engine project.
    -   Set **Location** to be `<UNREAL_ENGINE_ROOT>\Engine\Source\Programs` if your project is native.
    -   Set **Location** to be `<PROJECT_ROOT>\Build` if your project is foreign.
        
        For more information about the different between native and foreign projects, see the [Managing Game Code](/documentation/en-us/unreal-engine/managing-game-code-in-unreal-engine) documentation.
        
8.  Click **Next** to bring up an **Additional Information** window. Here you choose the **Framework** for this Class Library.
9.  In the dropdown menu, choose **.NET 6.0 (Long-term support)** and click **Create**.
10.  Visual Studio creates a new folder named `SampleScript.Automation`. Within the newly created `SampleScript.Automation` folder is a file named `Class1.cs`. Change the name of this file to `SampleScript.cs`. Visual Studio prompts you as to whether you wish to change all project references as well. Choose **Yes**.

### Project Settings

| **Setting** | **Value** | **Note** |
| --- | --- | --- |
| Name | `SampleScript.Automation` | The automation project generation script looks for a `*.csproj` file with the `*.Automation.csproj` extension. |
| Location | 
-   Native Project: `<UNREAL_ENGINE_ROOT>\Engine\Source\Programs`
-   Foreign Project: `<PROJECT_ROOT>\Build\Scripts`



 | You can save the project in a Project Build or Engine Source directory. |
| .NET Framework | 6.0 |   |

## Configure your Automation Project

### Adjust Build Settings

Before you write an automation script, there are some build settings that require adjustment:

1.  In the Visual Studio **Solution Explorer**, navigate to `SampleScript.Automation` and select it.
2.  With this folder selected, go to **Build > Configuration Manager...** in the Visual Studio menu bar.
3.  In the **Configuration Manager** window, find the `SampleScript.Automation` project.
4.  Under the Project's **Configuration** dropdown menu, select **Edit...**
    1.  A new window titled **Edit Project Configurations** should appear.
    2.  In this window, select **Release**, click **Rename**, and change **Release** to **Development**.
    3.  A new window should appear asking you to confirm your choice to rename **Release** to **Development**. Click **Yes** and close both opened windows.

### Configure Project Properties

Now you must configure the output path for your automation project:

1.  In the Visual Studio **Solution Explorer**, navigate to `SampleScript.Automation` and select it.
2.  Right-click this folder and select **Properties**.
3.  Under the **Build** tab, choose your desired **Base output path**. For our purposes, if it is not already, set the output path to **bin\\**.

If you are using a foregin UE project, you need to open your `.csproj` file and update the ProjectReference to use the `$(EngineDir)`:

```
	`<ProjectReference Include="$(EngineDir)\Source\Programs\AutomationTool\AutomationUtils\AutomationUtils.Automation.csproj" />`
Copy full snippet
```
<ProjectReference Include="$(EngineDir)\\Source\\Programs\\AutomationTool\\AutomationUtils\\AutomationUtils.Automation.csproj" />

### Verify Automation Project

Before proceeding, first verify that our project has been successfully detected by Unreal Automation Tool as a new automation project. To verify that you have configured our project properly, close Visual Studio. Right-click on your project's `*.uproject` file and run `GenerateProjectFiles.bat`. Open the generated Visual Studio solution file and navigate to `..\Programs\Automation`. The new automation project `SampleScript.Automation` should now appear in this directory. This means that Unreal Automation Tool has successfully detected our new automation project.

### Add a Project Reference

You can now register your automation project with Unreal Automation Tool:

1.  In the Visual Studio **Solution Explorer**, navigate to `SampleScript.Automation` and select it.
2.  Right-click `SampleScript.Automation` and select **Add > Project Reference...**
3.  This opens a window titled **Reference Manager - SampleScript.Automation**.
4.  Find **AutomationUtils.Automation** and check the box next to the name and click **OK**.

## Add Code to an Automation Script

The [Create an Automation Project](/documentation/en-us/unreal-engine/create-an-automation-project-in-unreal-engine#createanautomationproject) and [Configure your Automation Project](/documentation/en-us/unreal-engine/create-an-automation-project-in-unreal-engine#configureyourautomationproject) sections instructed you to create an automation project named `SampleScript.Automation`. Within this folder, you also created a C# file named `SampleScript.cs`. This is the file where we add our automation script commands.

For our purposes, we will write a function that prints the terms of the Fibonacci sequence to the command line up to the number of terms specified by a command line argument that the user enters when our automation script is called. This example demonstrates the following features of automation scripts:

-   Help commands
-   Command line input
-   Command line output
-   Logging

### Automation Script Code

Below is the sample code for this automation script example. Copy and paste this code sample into the `SampleScript.cs`.

```
	`using AutomationTool;  	namespace SampleScript.Automation 	{ 		// Use [Help()] attributes to document your command and its arguments. 		[Help("Sample script printing the first N terms of the Fibonacci sequence.")] 		[Help("Usage: SampleScript -Terms=<N>")] 		[Help("Terms=<N>", "N (int) the number of terms to compute. Must be greater than or equal to 1.")]  		// BuildCommand is the base class for all commands. 		public class SampleCommand : BuildCommand 		{ 			public override void ExecuteBuild() 			{ 				// The ParseParamInt() method retrieves a command line argument for this example. 				// ParseParam() retrieves a bool, and ParseParamValue() retrieves a string. 				int NumTerms = ParseParamInt("Terms"); 				if (NumTerms < 1) 				{ 					throw new ArgumentException("Invalid number of terms specified. Enter -help for syntax."); 				} 				else 				{ 					LogInformation("Fibonacci sequence:");  					int TermA = 1; 					int TermB = 1;  					for (int i = 0; i < NumTerms; i++) 					{ 						LogInformation(" {0}", TermA);  						int TermC = TermA + TermB; 						TermA = TermB; 						TermB = TermC; 					} 				} 			} 		} 	}`
Copy full snippet
```
using AutomationTool; namespace SampleScript.Automation { // Use \[Help()\] attributes to document your command and its arguments. \[Help("Sample script printing the first N terms of the Fibonacci sequence.")\] \[Help("Usage: SampleScript -Terms=<N>")\] \[Help("Terms=<N>", "N (int) the number of terms to compute. Must be greater than or equal to 1.")\] // BuildCommand is the base class for all commands. public class SampleCommand : BuildCommand { public override void ExecuteBuild() { // The ParseParamInt() method retrieves a command line argument for this example. // ParseParam() retrieves a bool, and ParseParamValue() retrieves a string. int NumTerms = ParseParamInt("Terms"); if (NumTerms < 1) { throw new ArgumentException("Invalid number of terms specified. Enter -help for syntax."); } else { LogInformation("Fibonacci sequence:"); int TermA = 1; int TermB = 1; for (int i = 0; i < NumTerms; i++) { LogInformation(" {0}", TermA); int TermC = TermA + TermB; TermA = TermB; TermB = TermC; } } } } }

## Execute an Automation Script

You are now ready to run your automation script:

1.  Open a command prompt and navigate to your `UNREAL_ENGINE_ROOT` directory.
2.  Enter the command: `RunUAT.bat SampleCommand -Terms=6`
3.  This command builds and runs AutomationTool executing the `SampleCommand` located in the `SampleScript.cs` file.
4.  If everything goes correctly, you should see something similar to the following output in the command prompt:
    
    Click image to expand.
    
5.  You can also run: `RunUAT.bat SampleCommand -help` to display the information in the `[Help(...)]` message text from your `SampleCommand` class.
    
    Click image to expand.