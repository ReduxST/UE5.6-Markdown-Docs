# Creating Blueprint Classes

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/creating-blueprint-classes-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/creating-blueprint-classes-in-unreal-engine)  
**Processed:** 2025-06-14 16:17:15

---

You can create **Blueprint Assets** through the **Content Browser** or the **Level Editor** using any of the methods described in this document.

## Creating Blueprint Assets in the Content Browser

The Content Browser features a dedicated **Add New** button for creating new Blueprint Assets in the current directory. You can also right-click in the **Asset View** or the **Asset Tree** to create a Blueprint Asset in the selected location.

### Using the Add New Button

1.  In the **Content Browser**, click the **Add New** button.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7469bfc5-6533-4cb2-a646-552215db8906/contentbrowseraddnew.png)
2.  Select **Blueprint Class** from the **Create Basic Asset** section of the dropdown menu.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/846ba685-3440-4abb-b515-7fc74402a95a/contentbrowserdropdown.png)
    
    You can create several different [types of Blueprint Assets](/documentation/en-us/unreal-engine/types-of-blueprints-in-unreal-engine) from the **Blueprints** option under **Create Advanced Asset**.
    
3.  Choose a **Parent Class** for your Blueprint Asset. See [Parent Classes](/documentation/en-us/unreal-engine/blueprint-class-assets-in-unreal-engine#parentclasses) for more information.
    
    ![Choose a Parent Class](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b4cc035a-4fad-4b19-90d2-39d538604814/new_asset_parent_class.png)

### Using the Asset View

1.  Right-click in the **Asset View** (right-hand panel) of the **Content Browser** to bring up the context menu.
    
2.  Select **Blueprint Class** under the **Create Basic Asset** section.
    
    ![New Asset menu](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5696c225-7325-4b3c-bc2e-8dcf92003fae/new_asset_blueprint_menu.png)
3.  Choose a **Parent Class** for your Blueprint.
    
    ![Choose a Parent Class](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/dbecd6e0-a405-4a5e-9765-4d4dec294a90/new_asset_parent_class.png)
    
    See [Parent Classes](/documentation/en-us/unreal-engine/blueprint-class-assets-in-unreal-engine#parentclasses) for more information on selecting a Parent Class.
    

### Using the Asset Tree

1.  **Right-click** on a folder in the **Asset Tree** (left-hand panel) of the **Content Browser**.
    
2.  In the context menu that appears, select **New Asset**, then select **Blueprint Class**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0e39e25a-a291-4cd8-9d73-598cfec825ff/rtclick_content_browser_asset_tree.png)
3.  Choose a **Parent Class** for your Blueprint.
    
    ![Choose a Parent Class](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/97646f0f-04a5-4745-a18d-6d1c7aef9d87/new_asset_parent_class.png)
    
    See [Parent Classes](/documentation/en-us/unreal-engine/blueprint-class-assets-in-unreal-engine#parentclasses) for more information on selecting a Parent Class.
    

## Creating in the Level Editor

You can create a **Blueprint Asset** from one or more selected **Actors** in the Level Editor. The Blueprint you create will contain your Actor (or Actors), and will maintain any property changes you have made to them in the Level Editor, as well as their spatial relationships to each other. With this feature, you can save multi-Actor systems into a single, reusable Asset.

1.  Select the Actor or Actors in the Level Editor viewport.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bac5518b-3d04-46c8-b6ee-8dff05d62a0a/multiactorselection.png)
    
2.  In the Level Editor toolbar, click the **Blueprints** dropdown menu and choose **Convert Selection to Blueprint Class**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2e8c559d-0628-4823-87cb-1150f19c6ef4/bpdropdownbutton.png) ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/27071b84-9b69-4be1-8c18-4d7080874a0d/convertselectiontobp.png)
    
    If you have only one Actor selected, the **Blueprint/Add Script** button will appear in the **Details** panel. Since creating a Blueprint Asset from a single Actor requires less information from the user, you can use this button to save time by skipping directly to the [New Subclass](/documentation/en-us/unreal-engine/creating-blueprint-classes-in-unreal-engine#newsubclass) menu.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ed3a96d2-d9c7-4b8e-87b7-41baa444a54f/bpaddscriptbutton.png)
    
3.  At this point, the editor will present three methods for creating a new Blueprint Asset from the selected Actor or Actors: **New Subclass**, **Child Actors**, and **Harvest Components**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3384f5c1-6cc1-4b4f-bb11-b76167840f88/createbpfromselection.png)
    
4.  After choosing a method, select the parent Actor class for your new Blueprint Asset from the list in the bottom portion of the window. If you are using the **New Subclass** method, the parent class will be further restricted to the class of the selected Actor or its subclasses.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/63dc92e1-9aae-4525-bdca-3ec0dc11e807/parentclassselection.png)
    
5.  Once you have selected a method and chosen a parent class, your new Blueprint Asset will appear in the Content Browser.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4e6dd2c2-dccc-4f72-b356-e1b106195c45/contentbrowserconvertedbp.png)
    

### New Subclass

**New Subclass** is only available if you have a single Actor selected. This method creates a Blueprint Asset as a subclass of your Actor or any of its subclasses, incorporating any changes you made to the Actor's properties. This is the most straightforward method. The Blueprint Asset will preserve any changes you have made to the selected Actor's properties.

### Child Actors

The **Child Actors** method creates a Blueprint Asset based on any Actor class. The new Actor will have its default Components, and one additional **Child Actor Component** for each selected Actor in the Level Editor viewport. These Child Actor Components will preserve the changes you have made to the properties of the selected Actors.

Typically, users of this method choose the base Actor class, as this will not introduce any new behaviors or unneeded Components.

### Harvest Components

The **Harvest Components** method creates a single Blueprint Asset based on any Actor class, then harvests the Components of all the selected Actors and attaches them to the new Actor. Use this method in cases where your Actors are primarily containers for their Components. For example, multiple **Static Mesh Actors** can combine efficiently into a single Actor with multiple Static Mesh Components, since they typically exhibit no behaviors other than rendering and possibly collision. However, AI-controlled characters generally need to remain as individual Actors, because they have Actor-level autonomy in their behaviors and may require individual control of Components and access to Component data.

### Creating in the Class Viewer

The [Class Viewer](/documentation/en-us/unreal-engine/class-viewer-in-unreal-engine) can also create Blueprint Assets. When using the Class Viewer, it can be helpful to filter the displayed classes as follows:

1.  In the **Class Viewer** toolbar, select **Filters**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/eafbb70e-c1f3-4ea4-b354-b04bd2bf4bb8/class_viewer_filters.png)
2.  In the **Filters** menu, select **Blueprint Bases Only**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/56737be2-d431-4690-b7a0-129fac3b9fe9/filter_blueprint_class_viewer.png)

To create a new Blueprint Asset, select the class you would like to use as a base. In this example, **CameraActor** is our base class.

1.  Click the dropdown to the right of your chosen base class, or right-click on the class directly.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/29207080-805b-4d8f-9166-8a5409aee475/class_viewer_arrow.png)
2.  The **Create Blueprint** option will appear in a context menu. Click this to open the dialog for creating a Blueprint.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/eac9157a-1705-412e-9ee5-8209659da5e9/class_viewer_down_arrow.png)
3.  Enter a name for your Blueprint Asset, and select the folder where you want to save it.
    
4.  Click "Create \[Path\]/\[Name\]" at the top of the Blueprint creation dialog. This will create your Blueprint Asset and open it in the **Blueprint Editor**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ab694f54-9fa2-4c82-9d2f-d9e51cb77aee/class_viewer_create_complete.png)
5.  Complete the process by saving your new Blueprint Asset. To do this, click **Save** in the Blueprint Editor toolbar.