# Media Folder Structure

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/media-folder-structure-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/media-folder-structure-in-unreal-engine)  
**Processed:** 2025-06-14 16:35:27

---

![The recommended Media folder structure in the Content Browser](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c6673d10-a73e-4138-a54d-716291c1efb2/cb_media.png)

The **Media** folder includes all the files associated with using media in your production. Some of the files in this section will be automatically populated at the Root level of the Content Browser by the [Media Framework](/documentation/en-us/unreal-engine/media-framework-in-unreal-engine) plugin. The folders here are used in the background by the Media Profiles, but you should almost never have reason to work with them directly.

-   Bundles - Auto populated at the Content Root level by the Media Framework plugin.
    
-   Proxies - Auto populated at the Content Root level by the Media Framework plugin.
    
-   MediaOutputs
    
-   MediaProfiles
    
    -   MPR\_(Description1)
        
    -   MPR\_(Description2)
        
-   MediaSources - All Actors related to media content, with separate folders for each Media Source.
    

A diagram showing the recommended Media folder structure for your project in the Content Browser.