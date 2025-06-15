# Title File Interface

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/title-file-interface-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/title-file-interface-in-unreal-engine)  
**Processed:** 2025-06-14 16:54:39

---

The **Online Services Title File Interface** provides support for your game to read files from your platform's backend online services at runtime.

Your game might require reading files not packaged with your title. The title file interface provides you with tools to read files that you have uploaded to backend online services. Examples of such information might include configuration files or a message of the day. This interface helps you to access and download these files for use at runtime.

For player-specific file storage, see the [User File Interface](/documentation/en-us/unreal-engine/user-file-interface-in-unreal-engine).

## API Overview

### Functions

The following table provides a high-level overview of the functions provided by the Title File Interface:

| **Function** | **Description** |
| --- | --- |
| [`EnumerateFiles`](/documentation/en-us/unreal-engine/API/Plugins/OnlineServicesInterface/Online/ITitleFile/EnumerateFiles) | Enumerate all available files. |
| [`GetEnumeratedFiles`](/documentation/en-us/unreal-engine/API/Plugins/OnlineServicesInterface/Online/ITitleFile/GetEnumeratedFiles) | Retrieve a cached list of files enumerated by a call to `EnumerateFiles`. |
| [`ReadFile`](/documentation/en-us/unreal-engine/API/Plugins/OnlineServicesInterface/Online/ITitleFile/ReadFile) | Read a file and return its contents. |

## Process Flow

To read a file from the backend online services with the Title File Interface, follow these steps:

1.  `EnumerateFiles` asynchronously caches a list of all files available to retrieve from the online services with the interface.
2.  `GetEnumeratedFiles` retrieves the list of files cached with the interface by `EnumerateFiles`.
3.  For each file in the retrieved list, `ReadFile` reads the file asynchronously and returns its contents for use in your game.

## More Information

### Header File

Consult the `TitleFile.h` header file directly for more information as needed. The Title File Interface header file `TitleFile.h` is located in the directory:

```
`Engine\Plugins\Online\OnlineServices\Source\OnlineServicesInterface\Public\Online`
Copy full snippet
```
Engine\\Plugins\\Online\\OnlineServices\\Source\\OnlineServicesInterface\\Public\\Online

For instructions on how to obtain the UE source code, see our documentation on [Downloading Unreal Engine Source Code](/documentation/en-us/unreal-engine/downloading-source-code-in-unreal-engine).

### Function Parameters and Return Types

See the [Functions](/documentation/en-us/unreal-engine/overview-of-online-services-in-unreal-engine#functions) section of the [Online Services Overview](/documentation/en-us/unreal-engine/overview-of-online-services-in-unreal-engine) page for an explanation of function parameters and return types, including how to pass parameters and processing the results when functions return.