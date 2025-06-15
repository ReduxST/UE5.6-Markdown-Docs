# Developers Folder

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/developers-folder-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/developers-folder-in-unreal-engine)  
**Processed:** 2025-06-14 16:20:15

---

The **Developers** folder in the **Content Browser** is where you can duplicate and work on Assets without worrying about breaking things in your project. Use the Developers folder to experiment with different things, from small-scale Asset modification to project-wide refactors.

If you work in a shared project with other developers, each developer has their own folder.

The Developers folder uses the same name as your Windows username, but without characters that aren't allowed in Unreal Engine folder names, like periods or spaces.

Because the Developers folder is meant to act as a sandbox environment, you should never reference Assets from this folder anywhere outside this folder. Doing so can cause errors when cooking the project or cause cooking to fail.

## Enabling the Developers Folder

If you don't see the Developers folder in your Content Browser, follow these steps to enable it:

1.  In the **Content Browser**, click **Settings**.
    
2.  From the Settings menu, enable the **Show Developer Content** option.
    

Click the image for full size.

## Collaborating with Other Developers

If you use [source control](/documentation/en-us/unreal-engine/source-control-in-unreal-engine), you can configure Unreal Engine to see Assets in other developers' folders. To do this, follow these steps:

Click the image for full size.

1.  In the **Content Browser**, click the **Filters** button.
    
2.  From the Filters menu, select **Other Filters > Other Developers**.
    

## Excluding the Developers Folder from Cooked Builds

If you want to make sure that you don't accidentally package broken or in-progress Assets, you can exclude the Developers folder from cooked builds.To do this, follow these steps:

Click the image for full size.

1.  From the main menu, go to **Edit > Project Settings** and search for the **Directories to never cook** array.
    
    You can find this array by using the **Search** box at the top of the section.
    
2.  Click the **Add (+)** button to add a new item to the array.
    
3.  Click **…** to open a list of folders in your project.
    
4.  Click the **Developers** folder to select it.