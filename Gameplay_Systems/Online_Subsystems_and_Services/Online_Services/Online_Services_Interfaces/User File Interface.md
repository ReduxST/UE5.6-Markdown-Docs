# User File Interface

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/user-file-interface-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/user-file-interface-in-unreal-engine)  
**Processed:** 2025-06-14 16:57:54

---

The **Online Services User File Interface** provides support for your game to read user-specific files from your platform's backend online services at runtime.

Your game might require you to read user files that are not packaged with your title. Examples may include configuration files or user-specific game save files. This interface helps you to access and download these files for use at runtime.

For title-specific file storage, see the [Title File Interface](/documentation/en-us/unreal-engine/title-file-interface-in-unreal-engine).

## API Overview

### Functions

The following table provides a high-level overview of the functions provided by the User File Interface:

| **Function** | **Description** |
| --- | --- |
| [`EnumerateFiles`](/documentation/en-us/unreal-engine/API/Plugins/OnlineServicesInterface/Online/IUserFile/EnumerateFiles) | Enumerate all available files. |
| [`GetEnumeratedFiles`](/documentation/en-us/unreal-engine/API/Plugins/OnlineServicesInterface/Online/IUserFile/GetEnumeratedFiles) | Retrieve a cached list of files enumerated by a call to `EnumerateFiles`. |
| [`ReadFile`](/documentation/en-us/unreal-engine/API/Plugins/OnlineServicesInterface/Online/IUserFile/ReadFile) | Read a file and return its contents. |
| [`WriteFile`](/documentation/en-us/unreal-engine/API/Plugins/OnlineServicesInterface/Online/IUserFile/WriteFile) | Write the file contents to a file with the provided name. |
| [`CopyFile`](/documentation/en-us/unreal-engine/API/Plugins/OnlineServicesInterface/Online/IUserFile/CopyFile) | Copy the file contents to another file. |
| [`DeleteFile`](/documentation/en-us/unreal-engine/API/Plugins/OnlineServicesInterface/Online/IUserFile/DeleteFile) | Delete a file. |

## Process Flow for Reading Files

To read, copy, or delete a file from the backend online services with the User File Interface, follow these steps:

1.  `EnumerateFiles` caches a list of all files available to retrieve from the online services with the interface.
2.  `GetEnumeratedFiles` retrieves the list of files cached with the interface by `EnumerateFiles`.
3.  For each file in the retrieved list, `ReadFile` reads the file and returns its contents.

## Modifying Files

The User File Interface also supports operations for modifying files:

-   `WriteFile` creates new files or overwrites existing ones.
-   `CopyFile` copies the contents of a user file to a different user file.
-   `DeleteFile` deletes the user file with the provided name from the backend online services.

## More Information

### Header File

Consult the `UserFile.h` header file directly for more information as needed. The User File Interface header file `UserFile.h` is located in the directory:

```
`Engine\Plugins\Online\OnlineServices\Source\OnlineServicesInterface\Public\Online`
Copy full snippet
```
Engine\\Plugins\\Online\\OnlineServices\\Source\\OnlineServicesInterface\\Public\\Online

For instructions on how to obtain the UE source code, see our documentation on [Downloading Unreal Engine Source Code](/documentation/en-us/unreal-engine/downloading-source-code-in-unreal-engine).

### Function Parameters and Return Types

See the [Functions](/documentation/en-us/unreal-engine/overview-of-online-services-in-unreal-engine#functions) section of the [Online Services Overview](/documentation/en-us/unreal-engine/overview-of-online-services-in-unreal-engine) page for an explanation of function parameters and return types, including how to pass parameters and processing the results when functions return.