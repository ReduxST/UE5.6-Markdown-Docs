# Using PGC with World Partition

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/using-pgc-with-world-partition-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/using-pgc-with-world-partition-in-unreal-engine)  
**Processed:** 2025-06-14 17:00:32

---

When PCG assets are assigned to an [World Partition - Data Layer](https://dev.epicgames.com/documentation/en-us/unreal-engine/world-partition---data-layers-in-unreal-engine) and a [HLOD Layer](https://dev.epicgames.com/documentation/en-us/unreal-engine/world-partition---hierarchical-level-of-detail-in-unreal-engine), the PCG graph generates the actors and assigns them to the same data layer and HLOD layer.

## Using Data Layers

In the example below, there are two [partitioned](https://dev.epicgames.com/documentation/en-us/unreal-engine/using-pcg-generation-modes-in-unreal-engine?application_version=5.5) PCG volumes. One generates rock meshes and is assigned to the **DL\_Rocks** data layer. The other generates tree meshes and is assigned to the **DL\_Trees** data layer.

[![A generated tree selected in the Data Layers window. It is assigned to the DL_Trees data layer.](https://dev.epicgames.com/community/api/documentation/image/f8dee1ca-d02c-4b6a-81a4-674ff579b077?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/f8dee1ca-d02c-4b6a-81a4-674ff579b077?resizing_type=fit)

Selecting the generated meshes in the **Data Layers** window shows that the rocks are automatically assigned to **DL\_Rocks** and the trees are automatically assigned to **DL\_Trees**.

### Data Layer Settings for Spawn Actor and Create Target Actor Nodes

The Spawn Actor and Create Target Actor nodes each have a setting called Data Layer Source Type that controls how the node assigns actors to a Data Layer.  

[![The Data Layer Settings.](https://dev.epicgames.com/community/api/documentation/image/326e94bd-d8f1-4034-aebe-eb065739e388?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/326e94bd-d8f1-4034-aebe-eb065739e388?resizing_type=fit)

The Data Layer Source Type can be set to the following options:  

-   **Self**: The Spawn Actor or Create Target Actor node assigns the same Data Layers to the spawned actors as the source PCG Component actor.
    
-   **Data Layer References**: The node assigns Data Layers using an input Param Data set by the **Data Layer Reference** **Attribute**.
    

The Spawn Actor and Create Target Actor nodes support filtering using the **Included Data Layers** and **Excluded Data Layers** properties, which can be inputs or direct references.

There is also an **Add Data Layers** category where you can specify additional Data Layers to assign, either as input or as direct references.

### Get Actor Data Layers

The **Get Actor Data Layers** node reads the **ActorReference** attribute from the inputs, and then outputs all the Data Layers used by those inputs into the **DataLayerReference** attribute. The output is a single Param Data that contains one entry per Data Layer asset.

[![The Get Actor Data Layers node](https://dev.epicgames.com/community/api/documentation/image/0691e266-9534-4149-a952-d135fb26169a?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/0691e266-9534-4149-a952-d135fb26169a?resizing_type=fit)

### Partition By Actor Data Layers

The **Partition By Actor Data Layers** node takes Point Data as input, and outputs one or more partitions of Point Data based on the Data Layers in the input Point Data.

[![The Partition by Actor Data Layers node.](https://dev.epicgames.com/community/api/documentation/image/6e2c16f7-3467-469f-93c8-39cc3bccc3d2?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/6e2c16f7-3467-469f-93c8-39cc3bccc3d2?resizing_type=fit)

The node resolves input points using an **ActorReference** attribute to get the Data Layers used by the Actor. Then it creates a Point Data and a Data Layer Partition for every combination of those Data Layers found on the input.

To include or exclude data layers from the process, use the **Included Data Layers** and **Excluded Data Layers** inputs on the node, or use **DataLayer** asset references in the node settings.

[![Using a DataLayer asset reference in the node settings](https://dev.epicgames.com/community/api/documentation/image/5713699a-8c1b-4f82-8176-f486e0d6f3e3?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/5713699a-8c1b-4f82-8176-f486e0d6f3e3?resizing_type=fit)

Using a DataLayer asset reference in the node settings

When using Included Data Layers, any other Data Layer will be ignored. When using Excluded Data Layers, all Data Layers will be considered except for the excluded Data Layers.

#### Example 1

The input data has three Points that point to three different actors. One actor uses **DataLayerA**, and the other two actors use **DataLayerB**.

The output will include two Point Data, and two Data Layer Partitions (stored as Param Data).

The first Point Data will contain the point that is using **DataLayerA.** The second Point Data will contain both points that are using **DataLayerB**.

The first Data Layer Partition will contain one entry with a **DataLayerReference** attribute pointing to the **DataLayerA** asset. The second partition will contain one entry with a **DataLayerReference** attribute pointing to the **DataLayerB** asset.

#### Example 2

The input has the following Points:

-   a Point that resolves to **DataLayerA**
    
-   a Point that resolves to **DataLayerB**
    
-   a Point that resolves to both **DataLayerA** and **DataLayerB**
    

The output will include three Point Data with a single point each, and three Param Data.

The first Point Data will contain the point that is using DataLayerA. The second Point Data will contain the point that is using DataLayerB. The third Point Data will contain the point that is using both **DataLayerA** and **DataLayerB**.

The first Data Layer Partition will contain one entry with a DataLayerReference attribute pointing to the DataLayerA asset. The second partition will contain one entry with a DataLayerReference attribute pointing to the DataLayerB asset.  The third partition will contain two entries, one that points to the **DataLayerA** asset and one that points to the **DataLayerB** asset.

## Using HLOD Layers

In the example below, there is a **Surface Sampler** that generates rock meshes.

[![A Blueprint graph showing a Surface Sampler.](https://dev.epicgames.com/community/api/documentation/image/62742f80-a7d0-4bb4-bbc3-aaf905519a98?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/62742f80-a7d0-4bb4-bbc3-aaf905519a98?resizing_type=fit)

The PCG Graph that contains the sampler is set to assign all of its components and actors to an HLOD layer called **MyHLODLayer**.

[![The PCG graph's HLOD settings.](https://dev.epicgames.com/community/api/documentation/image/985ac0b1-e2d4-4c67-95fa-5f886b1f7e9f?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/985ac0b1-e2d4-4c67-95fa-5f886b1f7e9f?resizing_type=fit)

Selecting the generated meshes shows that the generated rocks are automatically assigned to **MyHLODLayer**.

[![Multiple rock meshes are selected. All of them are assigned to MyHLODLayer.](https://dev.epicgames.com/community/api/documentation/image/834e1b60-a4a4-4b36-95ac-4d9ef6dc09dd?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/834e1b60-a4a4-4b36-95ac-4d9ef6dc09dd?resizing_type=fit)

### HLOD Settings for Spawn Actor and Create Target Actor Nodes

The Spawn Actor and Create Target Actor nodes each have a setting called **HLODSource Type** that controls how the node assigns actors to an HLOD Layer.

[![The HLODSource Type setting](https://dev.epicgames.com/community/api/documentation/image/9c5fc1cc-2583-4708-a52a-39317cc8d367?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/9c5fc1cc-2583-4708-a52a-39317cc8d367?resizing_type=fit)

The **HLODSource Type** can be set to the following options:

-   **Self**: The Spawn Actor or Create Target Actor node assigns the same HLOD Layer to the spawned actors as the source PCG Component actor.
    
-   **Reference**: The node assigns an HLOD Layer through a direct reference to the HLOD Layer on the node settings.
    
-   **Template**: The node uses the HLOD Layer reference from its Template Actor.