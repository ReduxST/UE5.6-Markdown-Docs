# Importing Assets Directly

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/importing-assets-directly-into-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/importing-assets-directly-into-unreal-engine)  
**Processed:** 2025-06-14 16:30:08

---

This page describes two of the most common methods of importing content into **Unreal Engine 5**. There are other, more advanced methods of importing specialized content, such as using [Datasmith](/documentation/en-us/unreal-engine/datasmith-plugins-overview) to import content from CAD applications. However, for most types of basic content – such as Textures or Static Meshes – the methods described on this page should be enough.

## Required Setup

Before you can follow the instructions on this page, download and extract these [Sample Assets](https://d1iv7db44yhgxn.cloudfront.net/documentation/attachments/1af9a0ee-7181-4739-be82-a08c177aaeb3/sampleassets.zip).

## Selecting Files to Import

### Importing from the Content Browser

To import one or more Assets using the **Content Browser**'s **Import** button, follow these steps:

1.  Open an instance of the **Content Drawer** or **Content Browser**. To do this, click the **Content Drawer** button in the lower left corner of the Unreal Editor.
    
    Location of the Content Drawer button. Click the image for full size.
    
2.  In the [**Sources**](/documentation/en-us/unreal-engine/sources-panel-reference-in-unreal-engine) panel on the right, from your project's folder tree, select the folder where you want to import your Asset.
    
    If the folder you selected cannot contain any Assets, clicking the **Add** and **Import** buttons will have no effect. For example, you cannot import Assets into a project's top-level folder (`All`, in the screenshot below).
    
    ![Sources panel in the Content Browser](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8a420b37-c510-4089-9dee-3a6d5e9d1fc5/content-browser-select-folder.png)
    
    In this example, we have created a new folder called ImportedContent and selected it in the Sources panel.
    
3.  Do **one** of the following:
    
    -   Click the **Add** button. Then, from the context menu, select **Import to \[folder path\]**.
        
        Click the image for full size.
        
        Note that the folder path displayed in this menu option is different from what you see in the folder tree of the Content Browser. `/Game/` is the equivalent of `All/Content/`.
        
        You can also open this context menu by right-clicking inside the folder window in the Content Browser, or by right-clicking any folder in the tree and hovering over **Add/Import Content**.
        
    -   Click the **Import** button.
        
        ![Import button in the Content Browser](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/98f44e0d-ded1-484e-99e9-3fc0f1f80770/import-button.png)
4.  In the window that opens, browse to the folder where you extracted the downloaded Sample Assets. Click and drag to select all four of the files in this folder, then click **Open**.
    
    ![Opening the downloaded Assets](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/440f531e-aae2-476a-94d7-d8112e8a3848/select-files-to-import.png)

#### Step Result

After you click **Open**, Unreal Engine will display a dialog with import options for the Assets you selected. Refer to the [Importing the Assets](/documentation/en-us/unreal-engine/importing-assets-directly-into-unreal-engine#importingtheassets) section below.

### Importing Using Drag and Drop

To import one or more Assets using drag and drop, follow these steps:

1.  Open an instance of the **Content Drawer** or **Content Browser**. To do this, click the **Content Drawer** button in the lower left corner of the Unreal Editor.
    
    Location of the Content Drawer button. Click the image for full size.
    
2.  In the [**Sources**](/documentation/en-us/unreal-engine/sources-panel-reference-in-unreal-engine) panel on the right, from your project's folder tree, select the folder where you want to import your Asset.
    
    If the folder you selected cannot contain any Assets, clicking the **Add** and **Import** buttons will have no effect. For example, you cannot import Assets into a project's top-level folder (`All`, in the screenshot below).
    
    ![Sources panel in the Content Browser](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/48aa0469-0c3f-41fe-9138-c96cd34dc85a/content-browser-select-folder.png)
    
    In this example, we have created a new folder called ImportedContent and selected it in the Sources panel.
    
3.  Open your operating system's file manager (**Windows Explorer** on Windows, or **Finder** on macOS). Then, navigate to the folder where your Assets are located.
    
4.  Select your Assets, then drag and drop them into the **Content Browser**.
    
    Click the image for full size.
    

#### Step Result

After you click **Open**, Unreal Engine will display a dialog with import options for the Assets you selected. Refer to the [Importing the Assets](/documentation/en-us/unreal-engine/importing-assets-directly-into-unreal-engine#importingtheassets) section below.

## Importing the Assets

Regardless of the method you used, after you selected the files you want to import, the **Import Options** window will appear. These options will change depending on which type of file you are importing. For example, the screenshot below shows import options for an FBX file.

![FBX import options window](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9422003d-f976-423d-9d04-caf50b90e057/fbx-import-options.png)

To learn more about these import options, refer to the [FBX Import Options Reference](/documentation/en-us/unreal-engine/fbx-import-options-reference-in-unreal-engine) page.

To complete the import process, you can either:

-   Click **Import All** to import all of the selected Assets.
    
-   Click **Import** for each individual Asset if you want to configure their settings separately.
    

During the import process, a dialog box will appear in the lower right corner of your screen informing you that `T_Rock_04_n.TGA` was imported as a normal map. This is because Unreal Engine automatically detects some Texture types, like Normal maps, and imports them as the correct Asset type. Click **OK** to close this dialog box.

![Texture import confirmation window](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0fd173f2-5f56-4b9c-a172-c4a9e70d707b/texture-import-confirmation.png)

#### Step Result

Unreal Engine creates `.uasset` files in your project that hold the contents of each file you imported.

## Saving the Imported Assets

After you finish importing your Assets, you will notice that their icons are marked with an asterisk (\*) in the Content Browser. The asterisk means that the Assets are not saved yet.

Unreal Engine doesn't move the files you selected into your project folder. Instead, it creates `.uasset` files to store the newly imported Assets.

![Unsaved Assets in the Content Browser](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fed39a10-ae9b-47bf-b13b-dffd11105899/unsaved-assets.png)

Click the **Save All** button in the Content Browser's menu bar to save the imported Assets.

![Save All button in the Content Browser](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4439fef9-2b1f-473b-b9e3-cf9518e69681/save-all-button.png)

A dialog will appear that lists all of the unsaved Assets and gives you the choice to select which ones you want to save by enabling or disabling the checkbox next to that Asset's name.

Select the Assets you want to save, then click **Save Selected**.

![Save Selected button](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6a99a27c-b00c-4953-9b4e-97087f39ae99/save-dialog-confirmation.png)

After you save the Assets, you'll notice that the asterisks on their icons have been removed, indicating that the Assets have been successfully saved.

![Saved Assets in the Content Browser](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fda8b7f5-f1ef-4e16-bc85-0593ee211001/saved-assets.png)

#### Step Result

Unreal Engine saves all the `.uasset` files that were created after import.