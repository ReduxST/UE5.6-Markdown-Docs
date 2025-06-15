# Migrating Assets

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/migrating-assets-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/migrating-assets-in-unreal-engine)  
**Processed:** 2025-06-14 16:36:12

---

If you want to use the same Assets across multiple projects, use the **Migrate tool** to copy the Assets, along with their references and dependencies. For example, if you migrate a Material, any Texture Assets that define that Material will automatically be copied along with it. This is useful when you need to merge or fork projects, or when transitioning from a test environment into a production project.

To use the Migrate tool, follow these steps:

1.  From the **Content Browser**, select the Asset or Assets you want to migrate.
    
    *To select multiple Assets, hold down **Ctrl** and **left-click** each Asset you want to select.* If you want to select a range of Assets, **left-click** the first one, then hold down **Shift** and **left-click** the last one. This selects all Assets between the fist and last one.
    
    ![Selecting Assets to migrate from the Content Browser](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3778427d-5d14-4a61-8d98-6d03c230311d/select-assets-to-migrate.png)
    
    In this example, we have selected four Material Assets.
    
2.  **Right-click** any of the selected Assets. From the context menu that appears, select **Asset Actions > Migrate**.
    
    This opens the **Asset Report** window, which shows all of the Assets that will be copied as part of the migration process.
    
    ![Asset Report window](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/05066de0-4657-4f02-8b11-a96dfb31e4b9/asset-report.png)
    
    If you don't want to migrate an Asset in this list, uncheck the checkbox next to that Asset. Keep in mind, however, that this might break other Assets you are trying to migrate (for example, a Material will no longer show correctly if one of its Textures is missing).
    
3.  Click **OK** to confirm that you want to migrate the Assets. This will open a file browser window where you can select the project to migrate the Assets to (also known as the target project).
    
    ![Selecting a destination folder](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7b4cc2cc-7d31-45fd-99e4-a46d913ceee0/select-destination.png)
    
    Select the `Content` folder in your target project, then click the **Select Folder** button.
    
4.  After you confirm the migration, a progress bar will appear to track the migration progress.
    
    If the target project's `Content` folder contains an Asset with the same name as an Asset you want to migrate, you will see the following warning:
    
    ![An asset already exists at (location), would you like to overwrite it?](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cad06e72-9fc1-4894-b29e-2ab30158a30c/asset-migration-warning.png)
    
    Click **Yes** to overwrite the Asset, or **No** to skip the Asset and continue migrating the others. You can also make this choice for all Assets by clicking **Yes All** or **No All**.
    
5.  Once the migration completes, you will see a dialog confirming that all Assets have been migrated. Click **Show Message Log** in this dialog to view a full list of migrated Assets.
    
    ![A list of migrated Assets](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/553e3566-295c-4445-ac87-e2446ebb4167/migration-log.png)

## Troubleshooting Asset Migration

If you attempt to migrate Assets into anything other than an Unreal project's `Content` folder, you will receive the following message:

"\[file path\] does not appear to be a game Content folder. Migrated content will only work properly if placed in a Content folder. Would you like to place your content here anyway?"

If you want to be able to use your migrated content in the target project right away, click **No**, then select that project's `Content` folder.

If an Asset doesn't display correctly after migration, make sure that you also migrated all of its dependencies. Check if the Asset displays correctly in the original project, then reattempt the migration and make sure all of the Asset's dependencies are selected in the **Asset Report** window.