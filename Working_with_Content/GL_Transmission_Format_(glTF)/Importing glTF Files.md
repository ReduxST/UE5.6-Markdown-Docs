# Importing glTF Files

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/importing-gltf-files-into-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/importing-gltf-files-into-unreal-engine)  
**Processed:** 2025-06-14 16:30:20

---

You import **glTF** content into Unreal Engine the same way you import other types of content. You can import an entire scene, or specific Assets.

You can import the following glTF formats:

| Format | Description |
| --- | --- |
| JSON `.gltf` | 
Includes the following elements, saved separately in a directory you specify:

-   **Full scene description:** saved as a JSON-formatted, human-readable UTF-8 text file with the `.gltf` extension.
-   **Texture files:** saved to the format you specify, `.png`, `.jpeg`, and so on.
-   **Binary data files:** saved separate files with a `.bin` file extension.



 |
| Binary `.glb` | Combines the full scene description, all binary data, and all textures into a single self-contained binary file. |

## Import Individual Assets from glTF Files

You can import glTF Assets into Unreal Engine the same way you import other Assets.

1.  In the **Content Browser**, do one of the following:
    -   In the **+Add** menu, use the **Import to** command. For detailed instructions see [Importing from the Content Browser](/documentation/en-us/unreal-engine/importing-assets-directly-into-unreal-engine#importingfromthecontentbrowser).
    -   Drag and drop a glTF Asset into the Content Browser. For detailed instructions see [Importing Using Drag and Drop](/documentation/en-us/unreal-engine/importing-assets-directly-into-unreal-engine#importingusingdraganddrop). Whichever workflow you use opens the **The Interchange Pipeline Configuration (Import Content)** dialog box.
2.  Set the import options as needed, and click **Import**.

## Import a glTF Scene Into an Unreal Engine Level

You can import full glTF scenes into Unreal Engine using the same scene import workflow you use for other scene formats such as FBX.

1.  From the main menu, choose **File > Import Into Level**.
2.  Select the `.gtlf` or `.glb` file that contains the scene you want to import, and click Open.
    
    The **Choose location for importing scene content** dialog opens.
    
3.  Choose the destination folder in your Unreal Engine project, and click OK.
    
    The **Interchange Pipeline Configuration (Import Content)** dialog box opens.
    
4.  Set the import options as needed, and click **Import**.