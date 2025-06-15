# Importing Fonts

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/importing-fonts-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/importing-fonts-in-unreal-engine)  
**Processed:** 2025-06-14 16:30:18

---

In this guide, you'll learn how to import your own Font files into **Unreal Engine**.

![Banner Image](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a414b54b-d929-4a88-9840-b9469ef88abb/ue5_1-importing-fonts-banner.png "Banner Image")

When you start to import your Fonts, you can choose between several methods and choose the method that best fits your workflow. The available methods you can use to import are:

-   Using the Content Browser's Import button
-   Drag-and-drop method into the Content Browser
-   Using the Font Editor

You also have the choice between **TrueType Font** (`TTF`) and **OpenType Font** (`OTF`) files when importing your fonts. Choose the import method and font type that best fits your needs.

For this how-to guide, we are using the **Blank Template** project, using no **Starter Content**, with default **Target Hardware** and **Project Settings**.

## Using the Content Browser

You can use the Content Browser's **Import** button to select your `TTF` or `OTF` font file.

1.  In the Content Browser, click the **Import** button.
    
    ![Click the Import button in the Content Browser](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2005ad8d-a545-4531-9457-3bfde3b58a7d/ue5_1-01-click-import.png "Click the Import button in the Content Browser")
2.  After the **Import** dialog window appears, navigate to the `TFF` or `OTF` font file you want to import and select it. Then, click **Open**.
    
    ![Select Font in the Import dialog window](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/16f4203e-da44-4306-9dff-153fa5ce33d1/ue5_1-02-select-font.png "Select Font in the Import dialog window")
3.  After a moment, the **Font Face Import Options** dialog will appear. Select **Yes** from the options listed to create your Font Face asset and your Composite Font asset in your Content Browser.
    
    ![Select Yes in the Font Face Import Options dialog window](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/dfb53a33-308d-4028-86ac-77a0f339392e/ue5_1-03-import-option-window.png "Select Yes in the Font Face Import Options dialog window")
4.  The Font Face asset can now be found in your folder hierarchy.
    
    ![The imported Font Face asset in folder](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3017580b-8cd6-4112-8459-3e0182e2b5a1/ue5_1-04-added-font-asset.png "The imported Font Face asset in folder")

## Using Drag-and-drop

You can **Drag-and-drop** a `TTF` or `OTF` file directly into the Content Browser to create your font assets.

1.  Navigate to the folder where you've stored your `TTF` or `OTF` file(s) in the **File Explorer**. Drag the file into the **Content Browser** to start the import process.
    
    ![Drag the file into the Content Browser](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8caef6a8-8f97-41b2-b083-b6c93802c6b4/ue5_1-05-drag-font.png "Drag the file into the Content Browser")
2.  After a moment, the **Font Import Options** will appear. Select **Yes** from the options listed to create your Font Face asset and your Composite Font asset in your Content Browser.
    
    ![Select Yes in the Font Face Import Options dialog window](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9a840c7c-0425-4b3f-b051-d759bc430413/ue5_1-03-import-option-window.png "Select Yes in the Font Face Import Options dialog window")
3.  The Font Face asset can now be found in your folder hierarchy.
    
    ![The imported Font Face asset in folder](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fe932be5-354a-436f-8d0e-7ecb2a5dc54f/ue5_1-04-added-font-asset.png "The imported Font Face asset in folder")

## Using the Font Editor

You can import and create Font Face assets directly from the [Default Font Family](/documentation/en-us/unreal-engine/font-asset-and-editor-in-unreal-engine#defaultfontfamily) list in the **Font Editor** removing the need to import a font asset first then assign it.

1.  Open an existing **Font** asset or create a new one using the **+Add** button in the Content Browser.
    
    ![Click the Add button in the Content Browser](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8ac5dcaa-40b9-4793-b11d-8dc79dfd6749/ue5_1-06-click-add.png "Click the Add button in the Content Browser")
2.  **Font Editor** window appears.
    
    ![Font Editor window](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cce6223c-fc8b-4915-86e1-dceda0aca20e/ue5_1-07-font-editor-window.png "Font Editor window")
3.  Click the **Add Font** button to add a new font selection to the **Default Font Family**.
    
    ![Click the Add Font button](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/eefbe82c-fa67-4b4f-aea3-e3542df0bf80/ue5_1-08-click-add-font.png "Click the Add Font button")
4.  Select the **folder** button next to the selection dropdown.
    
    ![Select the **folder** button](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c9e6ce3e-41cc-4f2e-8d41-02db5452470d/ue5_1-09-name-and-browse.png "Select the **folder** button")
5.  After the **Import** dialog box appears, navigate to the `TFF` or `OTF` font file you want to import and select it. Then, click **Open**.
    
    ![Select Font in the Import dialog window](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8b0f4e64-67a2-42f0-87f7-7c5d58a2f584/ue5_1-02-select-font.png "Select Font in the Import dialog window")
6.  Next, the **Save Font Face** window will appear. Give your font a name and choose the save location in your game folder's hierarchy. Then, click **Save**.
    
    ![The Save Font Face window](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cd4d502c-dcb2-43ef-83ef-a4f42be137bf/ue5_1-10-save-font-window.png "The Save Font Face window")
7.  The Font Face asset can now be found in your folder hierarchy.
    
    ![The imported Font Face asset in folder](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fb4486fd-3752-4042-960a-812ebee47b96/ue5_1-04-added-font-asset.png "The imported Font Face asset in folder")

## End Result

Now that you've seen how to import using the various methods, you should be able to import your own font files using any one of these options for use in your games and projects.