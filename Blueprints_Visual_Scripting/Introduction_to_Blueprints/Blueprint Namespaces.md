# Blueprint Namespaces

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/blueprint-namespaces-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/blueprint-namespaces-in-unreal-engine)  
**Processed:** 2025-06-14 16:10:43

---

## Blueprint Namespaces

**Blueprint Namespaces** optimize the time it takes to open a Blueprint Asset in the editor by preventing unnecessary Assets from loading. This behavior is useful for large projects because the Engine performs initialization tasks by loading all [Blueprint Function Libraries](/documentation/en-us/unreal-engine/blueprint-function-libraries-in-unreal-engine) and [Macro Library](/documentation/en-us/unreal-engine/blueprint-macro-library-in-unreal-engine) assets regardless of whether the Blueprint you were opening was referencing those Libraries.

By grouping Assets into Blueprint Namespaces, you can defer loading the Asset until its is needed. This provides an additional benefit when working inside the Blueprint Editor, as any actions that a Blueprint Asset can take from its context menu will be filtered into its Blueprint Namespace.

### Using the Feature

To see a working example of this feature, follow the steps below:

1.  Begin by creating a new **Games** > **Blank Project** > with **Starter Content** enabled named **BlueprintNamespaces**.
    
    ![image alt text](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/46c95871-0f65-47e7-a946-37c5896c7750/image_0.png)
2.  Click the **Content Drawer** to open it, then navigate to **StaterContent** > **Blueprints** and double-click the **Blueprint\_CeilingLight** Blueprint to open its **Class Defaults**.
    
    ![image alt text](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a8597603-2dd0-4d55-a6b3-cec7a4daca4c/image_1.png)
3.  From the **Toolbar**, click the **Class Settings**, then navigate to the **Details** panel **Blueprint Options** category. In the **Blueprint Namespace** variable, type your namespace into the text field.
    
    ![image alt text](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0eab24ef-8ba4-4371-9649-0677ac8bb2e7/image_1.png)
    
    In our sample we named the Blueprint Namespace "BlueprintNamespaces.StarterContent"
    
    When entering your namespace into the Blueprint Namespace text field, the editor will validate the string to ensure it does not contain any incompatible characters such as "#" or ",".
    
4.  Click **Compile** and **Save** the **Blueprint**.
    
    ![image alt text](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d78c015b-ad7b-48a3-a9c5-fa9639289978/image_3.png)
5.  Navigate to the **Content Browser**, and hover your mouse over the **Blueprint\_CeilingLight** asset to read the tooltip displaying your namespace data.
    
    ![image alt text](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8a817b59-5874-4200-9407-6fac694c31e2/image_4.png)
    
    After launching the editor, you can see which library assets have already been assigned a namespace by searching for "BlueprintNamespace=StarterContent" in the Content Browser.
    
    When you open a Blueprint asset that contains a reference to one of your newly-created assets, it is loaded as a package import dependency of the referencing Blueprint. The same behavior occurs if you base a new Blueprint on a parent Blueprint class that already references one of these assets.
    

## Importing Namespaces

Importing is a similar process to adding an "#include" for a library header in a `.cpp` source file. When working with Blueprint Namespaces You can import a namespace through any of the following methods:

### Setting the Blueprint Namespace

You can add the Blueprint Namespace to the namespace group you want to have access to in the Editor, by following the steps below:

1.  Open the **Content Drawer**, then double-click your **Blueprint** to open it's **Class Defaults**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c1cf49c9-37e2-40de-b18e-b52d4914c4d7/image_5.png)
2.  From the **ToolBar**, click the **Class Settings** and navigate to the **Details** panel **Blueprint Options** > **Blueprint Namespace** category, then type your namespace into the text field.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3742cf71-e9f0-4770-b103-fecbe0a69f55/image_6.png)
3.  From the **Toolbar**, click **Compile** and **Save**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5f7fee6d-ad8c-4b86-ab4d-f5891b90beb8/image_3.png)
    
    When you open your Blueprint, any shared library assets set to the same namespace are automatically imported when the Blueprint editor initializes.
    

### Modifying the Editor Preferences or Project Settings

If you prefer a workflow where your shared library assets are automatically imported for all Blueprint assets, you can modify the **Editor Preferences** or **Project Settings** to ensure your specified subset of shared library assets is imported by the Editor, regardless of whether the Blueprint opened will belong to or import that namespace.

Editing the Editor Preferences will affect the local instance per user while editing the Project Settings will apply to the scope of your entire project. This will affect all users who are sharing source control on your project.\*

To set up a default import set for your local editor instance:

1.  From the **Toolbar**, navigate to **Edit** > **Editor Preferences** \> **Content Editors** \> **Blueprint Editor** \> **Experimental**, and from the **Namespaces to Always Include** field, click the **Add**(**+**) button to add your namespace as an element to the list.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1a5cae68-9dfa-48f1-936a-4848499a420b/image_8.png)
    
    Navigating to Editor Preferences provides you with the ability to locally modify the Global Namespace set for the Blueprint Editor.
    

To customize your project for all users to ensure a certain subset of shared library assets is always imported project-wide, you can enable the feature by following the steps below:

1.  Navigate to the **Edit** \> **Project Settings** > **Editor** > **Blueprint Project Settings** > **Experimental**, then in the **Namespaces to Always Include** Array List, click **Add**(**+**) to add your namespace to the list:
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/65137c11-a5c5-45ce-acfb-936a78aedca7/image_9.png)
    
    In the Project settings, we have edited the Blueprint Project Settings to include a Namespace called "BlueprintNamespaces.StarterContent".
    

-   You can choose to explicitly import one or more namespaces for your Blueprint by clicking the **Add**(**+**) button.
    
-   Adding an import will immediately load any shared libraries that are currently assigned to the namespace.
    
-   Removing an import does not have any negative performance effects in the editor, however you will no longer have the type and action menu filtering behavior associated with that namespace.
    

### Implicitly Importing a Namespace

You can implicitly import a namespace by selecting a non-imported type or action item in the context menu. When you select an unloaded type picker, then that type's package is loaded on the selection of a strong reference type.

This may seem to compromise the auto-import behavior, however, selecting a non-imported type takes the additional step of implicitly adding that type's namespace into the Blueprint's explicit import set described in the method above.

To see this feature working:

1.  Create a new Blueprint asset named **TestType**, then navigate to the **Class Settings** > **Details** > **Blueprint Options** and assign it to a namespace called "YourNameSpace.AutoImportTest":
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7445856c-c18d-4162-9aed-e8073fb21fb0/autoimporttype.png)
    
    In our example we named our Blueprint Namespace as BlueprintNamespaces.AutoImportTest.
    
2.  Click **Compile** and **Save**, then re-launch the editor.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e9e2299b-6ccb-4b80-a3ce-b6418a777b58/image_10.png)
3.  Click the **Content Drawer**, then navigate to **Content** > **StarterContent** > **Blueprints** and double click **Blueprint\_CeilingLight** to open its **Class Defaults**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4a6c3337-29a1-43f1-a55c-561e7ba7cc29/image_11.png)
    
    You can open any of your existing Blueprints, or create a new one. In our example, we chose to use the existing Blueprint\_CeilingLight.
    
4.  From the **Class Defaults**, navigate to **My Blueprint** > **Variables** and click **Add**(**+**) to create a new variable named **TestTypeVar**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/076ec105-c590-43b4-ab4d-c1695de87144/image_12.png)
5.  Click the **Boolean** drop-down arrow to bring up the pin type selector, then In the text field search and select **TestType** then choose **Object Reference**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/290eafcb-0cae-418b-b3c4-ef0ce0e618f0/image_13.png)
6.  Click the **Class Settings**, then navigate to the **Details** panel > **Imports** > **Imported Namespaces**, and you will see YourNamespace.AutoImportTest is now listed among the Imported Namespaces category.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b53ca200-5399-40ba-93db-8d1fdd625ebf/image_14.png)

Using Auto-import doesn't require the type to be unloaded. Your namespace (if non-global and not yet imported) is auto-imported upon selection. Enabling namespace import features will auto-import that asset's namespace into the Blueprint.

-   If you change a default value on any function input argument, then the local variable will import any namespace associated with the value.
    
-   Changing the default value of a struct or container type will import any namespace associated with the container's inner value and struct child member property.
    
-   Adding any new component in the Components panel will automatically import any namespace associated with that selected component type. This behavior also applies to non-imported component types.
    

## Filtering Non-Imported Types and Actions

By default, non-imported types and actions are displayed in the context menu, but if you wish to enable an additional layer of filtering for non-imported types:

1.  Click the **Content Drawer**, then click **Add(+) > Create an Advanced Asset > Blueprints > Blueprint Function Library** named **Bp\_FilterFunctionLibrary**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/160603a0-d367-47e8-b5b5-bc12b16e0f62/image_15.png)
2.  Double-click the **Bp\_FilterFunctionLibrary** to open its **Class Defaults**. From the **My Blueprint** panel, navigate to the **Functions** category and rename **NewFunction\_0** to **FilteredFunction\_0**. **Class Settings** and navigate to **Details** > **Blueprint Options** > **Blueprint Namespaces**, then enter "YourNamespace.FilterTest".
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a2729103-625a-4d83-b9fe-d4d571cfc855/image_16.png)
    
    In our example, this becomes "BlueprintNamespaces.FilterTest".
    
3.  Click the **Add(+)** button to create a new function named **FilteredFunction\_1**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b544ab2c-29c9-4866-83fc-069c8dd99a77/image_17.png)
4.  Click the **Class Settings** then from the **Details** panel, navigate to **Blueprint Options** > **Blueprint Namespace**, then select Your namespace from the drop down menu "YourNamespace.FilterTest" (in the example shown below, this becomes "BlueprintNamespaces.FilterTest").
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3b97f17a-52cc-40d0-b9a7-d544bd960b8d/image_18.png)
5.  Click **Compile** and **Save**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/83dc4328-b3a6-4e7a-95b3-c159ccf4bdfb/image_19.png)
6.  Navigate to **Content** > **StarterContent** > **Blueprints** and double click the **Blueprint\_CeilingLight** to open its **Class Defaults**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f0d625d4-fbc7-42bc-8c19-5a55234ec75d/image_20.png)
7.  From the **Class Defaults**, navigate to the **Event Graph** then right click to open the **Actions** menu. When you search for your **Filtered Function** it will appear in the context menu.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0366e32a-bfd0-4991-b76c-a1c0cd47fe34/image_21.png)