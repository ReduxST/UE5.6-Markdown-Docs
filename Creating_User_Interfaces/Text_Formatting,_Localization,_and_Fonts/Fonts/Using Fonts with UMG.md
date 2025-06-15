# Using Fonts with UMG

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/using-fonts-with-umg-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/using-fonts-with-umg-in-unreal-engine)  
**Processed:** 2025-06-14 16:59:09

---

This guide provides information on setting up **Fonts** Assets of the Text Widget via Widget Blueprints Editor.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0fdeb46f-1258-43ae-bc96-b2eab3cf30c3/01_fontwithumg_hero.png)

## Steps

Follow the steps below to see how to adjust custom Fonts and use them via UMG UI Designer of the Widget Blueprints Editor.

For this how-to guide, use **Blank Template** is used with no **Starter Content**. Settings of **Target Hardware** and **Project Settings** are used by default.

1.  Create a new [Widget Blueprint](/documentation/en-us/unreal-engine/widget-blueprints-in-umg-for-unreal-engine). Click the **Add** in the **Content Browser**, then select **User Interface > Widget Blueprint**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e30f3004-f004-4ec1-bfcb-2da8a333a417/02_newwidgetblueprint.png)
2.  **Double-click** the created **Widget Blueprint** to open it in the **Widget Blueprint Editor**.
    
3.  Find **Canvas Panel** Widget in the **Pallete** panel and drag it into the **Visual Designer** window.
    
4.  Find **Text** Widget in the **Pallete** panel and drag it into **Canvas Panel** of the **Visual Designer** window.
    
5.  Click created **Text** Widget for access the **Details** panel of this item. In the **Details** panel, under **Appearance**, find a **Font** option. With the help of this, you can adjust family type, facetype (regular, bold, itallic, and so on), size, letter spacing and so on.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/861bdaaf-99b2-438b-8785-9485f68e4ab8/03_fontoptions.png)
6.  By default, the **Unreal Engine** uses the **Roboto** font. Click the dropdown menu next to **Font Family** for selecting any custom Fonts Assets, you have created.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/65c8967a-fb6b-4eb7-a6f4-9c6fe4a17ff0/04_fontfamily.png)
    
    You can also choose option to create a custom Fonts via this menu and specify location of the new asset (it will be blank by default).
    
7.  Click dropdown menu next to **TypeFace** for selecting a style for selected Fonts Asset.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b8db5be8-e81b-462f-a489-48ccc6be0a83/05_fonttypeface.png)
8.  You can specify the size of the Fonts Asset in the input box next to **Size**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7fa751e5-7562-45f9-bb89-2c4568990bcb/06_fontsize.png)
9.  Also, you can specify a space between letter in the input box next to **Letter Spacing**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/537c9ae9-7a35-44bf-9dc7-d821d7003c39/07_fontletterspacing.png)

Currently, UMG only supports **Runtime** cached Fonts Assets. Also, if you have assigned Fonts using the old method, none of your existing file-based font settings will be lost, however going forward, you will need to create a Fonts Asset in order to use custom Fonts with UMG.

## End Result

You have get familiar with basics of adjusting **Fonts** Assets of the Text Widget via Widget Blueprints Editor. Moreover, you can style your **Fonts** by [colors, Materials, outline properties, and so on](/documentation/en-us/unreal-engine/font-materials-and-outlines-in-unreal-engine).