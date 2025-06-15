# Exporting Datasmith Content from Rhino

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/exporting-datasmith-content-from-rhino-to-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/exporting-datasmith-content-from-rhino-to-unreal-engine)  
**Processed:** 2025-06-14 16:22:51

---

Once you install the Datasmith Exporter Plugin for Rhino, you have an **Unreal Datasmith** (`.udatasmith`) filetype available to you when you save or export a scene.

![New Rhino export option](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/41ea7905-6675-4746-86f7-ca916216b4c7/rhinoexportoption.png "New Rhino export option")

Follow the steps below in Rhino to export your scene using this new filetype.

From the Rhino **File** menu, select either one of the following options:

![Rhino export menu](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/59c8b539-3498-4796-9a79-9a6796b7fbe4/rhinoexportmenu.png "Rhino export menu")

-   **Save As**: A `.udatasmith` file is created containing all visible elements.
    
-   **Export Selected** : A `.udatasmith` file is created containing all the selected elements. Layers containing no selected elements are not exported.
    
-   **Export with Origin** : A `.udatasmith` file is created containing all visible elements. The scene exports with the specified position offset.
    

In the **Export** window, select the **Unreal Datasmith** (`.udatasmith`) option from the **Save As type** dropdown.

![Rhino export filetypes](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/76a8ffa2-eda6-4eab-815e-cf82ed9a6918/rhinoexportfiletype.png "Rhino export filetypes")

Browse to the location where you want to save your exported file, set the **File name**, and click **Save**.

Alternatively, click the **Export 3D View** button on the Datasmith Toolbar. This creates a `.udatasmith` file containing all visible elements.

![Datasmith toolbar Export 3D View button](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ee932da3-4284-419a-8b7c-5c7ff02acb52/datasmith-export-3d-view.png)

For more information about the Datasmith toolbar, see [Using the Datasmith Toolbar](/documentation/en-us/unreal-engine/using-datasmith-with-rhino-in-unreal-engine#toolbar).

## End Result

Your `.udatasmith` file should now be ready to try importing into Unreal Engine 4. See [Importing Datasmith Content into Unreal Engine](/documentation/en-us/unreal-engine/importing-datasmith-content-into-unreal-engine). If your data needs additional cleaning, merging, or other modifications during the import process, see [Dataprep Import Customization](/documentation/en-us/unreal-engine/dataprep-import-customization-in-unreal-engine).