# Crash Reporting

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/crash-reporting-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/crash-reporting-in-unreal-engine)  
**Processed:** 2025-06-14 16:16:33

---

When your game crashes, Unreal Engine creates a crash report, which it can send to the **Crash Report Client**. The Crash Report Client is an application that prompts users to provide optional comments and submit the crash report to Epic Games. You can customize the Crash Report Client packaged with your game to send crash report data to your own server to help with debugging your games.

This guide provides:

-   An overview of crash reports and their contents.
-   Information on where to find crash reports on your local machine.
-   Config variable reference and project settings for crash reporting.
-   How to modify and configure the crash reporter client for your own packaged applications.
-   Recommendations for crash report services you can use to receive crash reports on a remote server.

## Crash Reports

A crash report contains:

-   A unique random crash identifier, called **crash guid**.
-   Information about the error, such as the type (crash, assert, ensure, etc.), or the callstacks of the crashing thread and all other threads.
-   System information for the machine and application context information such as build configuration.
-   The log output at the moment of the crash. This can be device runtime logs or project editor logs.
-   Additional context provided by the game using key/value pairs.
-   Any additional comments provided by the user through the crash report client.

The following is an example of a crash report as viewed in the Crash Report Client:

![A crash report is displayed in the UE Crash Reporter client. It prompts the user for information about what they were doing when the crash occurred and shows the log dump from the moment of the crash.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/96e71422-4a6a-487a-ace1-476fed71dea8/crash.png)

### Where To Find Local Crash Reports

Crash reports from the editor are stored on your local machine in your project’s `Saved/Crashes` folder.

Alternatively, you can find crash reports on a user’s local machine in `C:\Users[Your Windows Username]\AppData\Local[Project Name]\Saved\Crashes`.

### Common Causes of Crashes in Unreal Engine

The following are the most common causes of crash reports that you will encounter. Each of these starts the Crash Reporter client with a message above the callstack giving details about the type of crash encountered.

| **Crash Source** | **Description** | **Example Image (Click to Enlarge)** |
| --- | --- | --- |
| **Crash** | 
Something has happened that the program can’t handle, so it shuts down. Reasons crashes occur include:

-   Accessing null objects.
-   Attempting to write data to objects that do not exist.
-   Accessing corrupted objects or data.
-   Stack overflows, usually due to infinite loops or infinite recursion.
-   Out-of-memory (OOM) errors.



 | 

 |
| **Assert** | 

Caused by an assert statement that a developer put in the code to purposefully crash the program based on a certain condition. This is useful for checking something that you can predict will cause problems later during runtime, giving you an opportunity to catch it early. For example:

`check(Mesh != nullptr)`

For more information about asserts in Unreal Engine, see the [documentation page on asserts](/documentation/en-us/unreal-engine/asserts-in-unreal-engine).



 | 

 |
| **Ensure** | 

Ensures check for a certain condition, but do NOT crash if they resolve false. Instead, they produce a message to the Output Log and send a report to the Crash Reporter in unattended mode. These are useful for something you want to monitor, but not necessarily crash execution for. For example:

`ensure(Number >= 0)`

For more information about Ensures in Unreal Engine, see the [documentation page on asserts](/documentation/en-us/unreal-engine/asserts-in-unreal-engine).



 | 

 |

## Add Custom Context to Crash Reports

In addition to the standard information added to a crash report, it is also possible for game projects to add their own custom context, called **game data**. This could be information about the game mode, the player’s location in the world, or other game state information vital for investigating bugs. The data is added using key/value pairs and using the `FPlatformCrashContext::SetGameData` function.

GenericPlatformCrashContext.h

```
	`/** Updates (or adds if not already present) arbitrary game data to the crash context (will remove the key if passed an empty string) */ 	CORE_API static void SetGameData(const FString& Key, const FString& Value);`
Copy full snippet
```
/\*\* Updates (or adds if not already present) arbitrary game data to the crash context (will remove the key if passed an empty string) \*/ CORE\_API static void SetGameData(const FString& Key, const FString& Value);

Note that custom context is set **before** the error occurs. When a crash report is collected, the current state of the game data values is captured and written to the report.

As an example, whenever your game enters a new game mode call:

MyGameMode.cpp

```
	`void OnEnterMyGameMode() 	{ 		FPlatformCrashContext::SetGameData(TEXT("GameMode"), TEXT("MyGameModeName")); 	}  	void OnExitMyGameMode() 	{ 		FPlatformCrashContext::SetGameData(TEXT("GameMode"), FString()); 	}`
Copy full snippet
```
void OnEnterMyGameMode() { FPlatformCrashContext::SetGameData(TEXT("GameMode"), TEXT("MyGameModeName")); } void OnExitMyGameMode() { FPlatformCrashContext::SetGameData(TEXT("GameMode"), FString()); }

A crash during that game mode will contain the following XMLdata:

CrashContext.runtime-xml

```

	`<GameData> 		<GameMode>MyGameModeName</GameMode> 	</GameData>`

Copy full snippet
```
<GameData> <GameMode>MyGameModeName</GameMode> </GameData>

## Crash Reporter Infrastructure

The crash report infrastructure for UE consists of the following components:

1.  A **Crash Report Client** on the user’s machine, distributed with builds of the editor or your game. The Crash Report Client sends crash dump info to your endpoint.
    
2.  A **server** with applications and components that manage, filter, and store crash reports.
    

The sections below detail each of these components and how to set them up for your own organization.

## Crash Reporter Client

The Crash Reporter Client is a separate program that is used with both editor builds and optionally packaged with runtime builds on users’ machines. When either the editor or the packaged application crashes, the engine generates a crash report, then launches the Crash Reporter Client if available. If the Crash Reporter is not in unattended mode, it displays a window with the crash data and prompts users to send or opt out of sending the report.

### Package the Crash Reporter Client With Your Game

By default, the Crash Reporter Client is not included with packaged games. To add it to your packaged builds:

1.  In Unreal Editor, open **Project Settings** and navigate to **Project** \> **Packaging**.
    
2.  Unfold the **Advanced** dropdown.
    
3.  Enable the **Include Crash Reporter** setting.
    

Alternatively, you can add `IncludeCrashReporter=True` to your project’s `Config/DefaultGame.ini` file.

DefaultGame.ini

```
	`[/Script/UnrealEd.ProjectPackagingSettings] 	IncludeCrashReporter=True`
Copy full snippet
```
\[/Script/UnrealEd.ProjectPackagingSettings\] IncludeCrashReporter=True

### Configure Automatic Crash Reports

The following config variables decide whether or not the crash reporter should automatically send crash reports to the server. You can configure these in any `Engine.ini` file under the `[CrashReportClient]` category.

| **Config Variable** | **Description** |
| --- | --- |
| `bAgreeToCrashUpload` | Controls whether or not the Crash Report Client should automatically send in crash events. This variable is only used for Linux builds. This defaults to `false` on Windows and Mac builds, but `true` on Linux builds. |
| `bSendUnattendedBugReports` | Controls whether or not to send in crash events unattended. If enabled, the Crash Report Client will skip displaying to the user and automatically send crash events to the server. This variable functions on all platforms, and defaults to `true`. |

DefaultEngine.ini

```
	`[CrashReportClient] 	bAgreeToCrashUpload=false 	bSendUnattendedBugReports=false`
Copy full snippet
```
\[CrashReportClient\] bAgreeToCrashUpload=false bSendUnattendedBugReports=false

### Configure the Crash Reporter Client

You can customize the Crash Reporter Client on a per-project basis. The CrashReportClient settings change both the behavior and appearance of the crash reporter, including the company name and server URL. To customize your Crash Reporter Client, add the following section to your project’s `DefaultEngine.ini`:

DefaultEngine.ini

```

	`[CrashReportClient] 	CompanyName="[Your Company Name]" 	DataRouterUrl="[URL of your crash report server]" 	UserCommentSizeLimit=4000 	bAllowToBeContacted=true 	bSendLogFile=true`

Copy full snippet
```
\[CrashReportClient\] CompanyName="\[Your Company Name\]" DataRouterUrl="\[URL of your crash report server\]" UserCommentSizeLimit=4000 bAllowToBeContacted=true bSendLogFile=true

The above is an example of an entry for the CrashReportClient, and not all of the values shown are mandatory.

#### Config Variable Reference

Below is a table of available settings. These should be added to your project’s Config/DefaultEngine.ini file under the \[CrashReportClient\] section :

| **Property** | **Description** | **Default Value** |
| --- | --- | --- |
| CrashReportClientVersion | Version number of the crash report client. | Empty |
| CompanyName | Set company name displayed in the "Allow contact" text. If empty, the text will not mention a specific company. | Empty |
| DataRouterUrl | Server that will recieve crash reports. | Empty |
| UserCommentSizeLimit | Maximum number of characters a user is allowed to enter in the comment field. | 4000 characters |
| bSendLogFile | If enabled, the “Send log file” checkbox is enabled by default. | true |
| bHideLogFilesOption | If enabled, the “Send log file” checkbox is visible. | false |
| bAllowToBeContacted | If enabled, the “Allow contact” checkbox is enabled by default. | true |
| bIsAllowedToCloseWithoutSending | Controls whether the user is allowed to close the dialog without sending a report. | true |
| bShowEndpointInTooltip | Controls whether the tooltip appearing over the send button should display the domain where crashes are sent. | true |
| bIsAllowedToCopyFilesToClipboard | Controls whether the “Copy files” button should be visible. Allows users to copy diagnostic files to clipboard. Only available on Windows platform. | false |
| bHideRestartOption | Controls whether the “Send and restart” button is visible. | true |

### Where Do Crash Events Go?

Editor builds always include the Crash Report Client, but including it in packaged builds is optional. The Crash Report Client sends crash reports and telemetry to different destinations depending on what type of build they occur in.

Packaged builds always use the Crash Reporter configuration values specified for your project, see [Configure the Crash Reporter](/documentation/en-us/unreal-engine/crash-reporting-in-unreal-engine#configurethecrashreporter). As of UE 5.4, Epic Games does not receive reports from packaged builds, regardless of whether they’re development or shipping builds, as there is no way for us to determine whether a packaged game is intended for end users or for testing.

By default, Editor builds distributed from the Epic Games Launcher send bug reports to Epic Games to help identify issues with the public release of Unreal Engine. To opt out of unattended bug reports, follow these steps:

1.  Open **Editor Preferences** in Unreal Editor.
    
2.  Navigate to the **Privacy** > **Bug Reports** category.
    
3.  Select **Don’t Send**.
    

![Select ](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/89a86180-0828-4e67-bb1b-03ed5e41d249/privacyunattendedbugreports.png) Privacy > Bug Reports if you don't want the editor to send bug reports to Epic Games." loading="lazy" />

Users are still prompted to send crash reports when crashes occur, but you can opt out of these by closing the crash reporter client or clicking **Close Without Sending**.

Editor builds created from source do not send crash report data to Epic Games.

The following table summarizes where UE sends crash events in different types of builds:

| **Build Type** | **Launcher Build** | **Source Build** |
| --- | --- | --- |
| **Development Editor or Game** | Epic Games/Custom | None/Custom |
| **Packaged Title** | None/Custom | None/Custom |

## Crash Report Server

To make the most of the crash reporter, you need to set up a server that can receive remote users’ crash reports and symbolicate them. UE does not include such a component with its source code or binaries. However, using the source code for the Crash Report Client can give you a starting point to create your own custom solution. There are also several third-party crash report services that you can deploy.

The following crash report services are commonly used within the UE community. Each one has documentation for integrating them with UE’s crash reporter:

| **Crash Report Service** | **UE Documentation Link** |
| --- | --- |
| [\[Backtrace\](https://backtrace.io/)](https://backtrace.io/) | [\[Setting Up Backtrace for Unreal Engine\](https://docs.saucelabs.com/error-reporting/platform-integrations/unreal/setup/)](https://docs.saucelabs.com/error-reporting/platform-integrations/unreal/setup/) |
| [\[Bugsplat\](https://www.bugsplat.com/)](https://www.bugsplat.com/) | [\[Bugsplat -- Unreal Engine\](https://docs.bugsplat.com/introduction/getting-started/integrations/game-development/unreal-engine/)](https://docs.bugsplat.com/introduction/getting-started/integrations/game-development/unreal-engine/) |
| [\[Sentry\](https://sentry.io/welcome/)](https://sentry.io/welcome/) | [\[Sentry -- Crash Report Client for Unreal Engine\](https://docs.sentry.io/platforms/unreal/configuration/setup-crashreporter/)](https://docs.sentry.io/platforms/unreal/configuration/setup-crashreporter/) |