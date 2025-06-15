# Importing Grooms

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/importing-grooms-into-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/importing-grooms-into-unreal-engine)  
**Processed:** 2025-06-14 16:30:21

---

In this page, you'll learn about the groom import process and available options when importing an Alembic (\*.abc) file with a groom.

## Prerequisites

Importing an Alembic file and rendering its groom in Unreal Engine requires the following plugins to be enabled in the **Plugins** browser:

-   Alembic Groom Importer
-   Groom

Enabling plugins requires the editor to be restarted. For more information on setting up a project to use grooms, see [Setting up a Project to use Grooms](/documentation/en-us/unreal-engine/setting-up-a-project-for-grooms-in-unreal-engine).

## Groom Import Process

The following flowchart describes the high-level process of bringing your own Alembic files that contain a groom into Unreal Engine and attaching them to an animate skeletal mesh character.

![Groom Import Process Flow Chart](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4b90c569-be92-4973-bf1b-29fb2b08d449/groom-import-process.png)

The flow works like this:

1.  Create your groom in your preferred Digital Content Creation (DCC) application, such as Autodesk Maya.
2.  Export the groom as an Alembic (\*.abc) file.
3.  Import the Alembic file with the groom into Unreal Engine.
4.  (Optional) Create a [Groom Binding](/documentation/en-us/unreal-engine/setting-up-bindings-for-grooms-in-unreal-engine) asset in the Content Browser and link it to your skeletal mesh.
5.  Place the groom asset in the Level.
    -   This can be done as an actor on its own or as part of a Blueprint using a Groom component.
6.  Attach the Groom component to a Skeletal Mesh Socket with Transfer Skinning.
7.  Set up and assign a material using the Hair domain to the groom asset. Once these steps are completed, you will have an interactive groom that you can use on any animated skeletal mesh that it's attached to.

For a more complete walk through of this process, see the [Groom Quick Start Guide](/documentation/en-us/unreal-engine/hair-simulation-and-rendering-quick-start-guide-in-unreal-engine).

Additional details about setting up your groom for export from your DCC application and import into Unreal Engine are covered in the [Alembic for Grooms Specification](/documentation/en-us/unreal-engine/using-alembic-for-grooms-in-unreal-engine). It covers the schema that enables Unreal Engine to import grooms directly.

## Groom Import Options

When you import an Alembic file with a groom, the **Groom Import Options** window opens.

![Groom Import Options](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cc25e2f2-9055-4537-b629-4737c285a477/groom-import-options.png)

The top section of the Groom Import Options dialog describes the **validity** of the imported groom file. It also includes a list of all the **hair attributes** which will be imported with this groom. Several attribute types are supported, such as Root UV, per-control point color, and more.

![Groom Import Options Stats](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c268a6dd-2947-46ae-9d30-0d70c42fb1dd/groom-import-options-1.png)

The **Conversion** section includes options to rotate and scale the groom asset prior to import. This allows application of a global transform to each curve / control point.

![Groom Import Options Conversion Settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/753e19ac-a30a-49c9-b7d3-2d41a85958c7/groom-import-options-2.png)

| Property | Description |
| --- | --- |
| **Rotation** | Sets the rotation in Euler angles (degrees) to fix up or front axes. |
| **Scale** | Scales the value to convert the file unit into centimeters. |

The **Preview** section includes all the imported groups of the groom. For each group, you can visualize the number of rendering curves and guides, and configure both decimation and interpolation settings. Both settings can be edited later from the [Groom Asset Editor](/documentation/en-us/unreal-engine/groom-asset-editor-user-guide-in-unreal-engine) after import.

![Groom Import Options Preview Settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1df428e8-d745-4867-af8f-456caa15b812/groom-import-options-3.png)

| Property | Description |
| --- | --- |
| Groups: Index\[n\] |   |
| **Group Name** | The name given to this group. |
| **Group ID** | The ID given to the hair strands in this group. |
| **Curve Count** | The number of hair strands within this groom group. |
| **Guide Count** | The number of simulation guides within this groom group. |
| Interpolation: Decimation Settings |   |
| **Curve Decimation** | Reduce the number of hair strands in a uniform manner. |
| **Vertex Decimation** | Reduce the number of vertices for each hair strand in a uniform manner. |
| Interpolation: Interpolation Settings |   |
| **Guide Type** | 
Select the type of guides to use for groom simulation:

-   **Imported Guides:** This option uses imported guide data from a groom asset if it exists.
-   **Generated Guides:** This option generates guides from the imported rendering curves. The value set for **Guide density** defines the fraction of curves used as guides.
-   **Rigged Guides:** This option converts guides into skeletal bones, which enables the use of animation systems and tools. The intent with this option is to use this only with a lower number of guides, such as pony tails, dreadlocks, and or similar hair styles.



 |
| **Generated guide density** | Density factor for converting hair into guide curve if no guides are provided. This value should be between 0 and 1, and can be thought of as a ratio / percentage of strands used as guides. |
| **Rigged guide num. curves** | Number of guides that are generated on the groom and the skeletal mesh. |
| **Rigged guide num. points** | Number of points / bones per generated guide. |
| **Interpolation Quality** | 

Defines the quality of the interpolation when interpolating guides motions onto the strands. Select one of the following options:

-   **High:** Build interpolation data using curve shape matching search. This results in high quality interpolation data, but is relatively slow to build and can take several dozen minutes to complete.
-   **Medium:** Build interpolation data using curve shape matching search but within a limited spatial range. This is a tradeoff between low and high in terms of quality and build time. This can take several dozen minutes to complete.
-   **Low:** Build interpolation data based on nearest neighbor search. Low quality interpolation data, but fast to build and only takes a few minutes to complete.



 |
| **Interpolation Distance** | 

Defines the metric used for pairing guides and strands together. Select one of the following options:

-   **Parametric:** Build interpolation data based on curve parametric distance.
-   **Root:** Build interpolation data based on distance between guide's root and strand's root.
-   **Index:** Build interpolation data based on guide and strands vertex indices.
-   **Distance:** Build interpolation data based on curve Euclidean distance.



 |
| **Randomize Guide** | When enabled, the guides used for interpolation are slightly randomized to break up clumps that can happen. |
| **Use Unique Guide** | When enabled, a single guide is used for motion interpolation. |