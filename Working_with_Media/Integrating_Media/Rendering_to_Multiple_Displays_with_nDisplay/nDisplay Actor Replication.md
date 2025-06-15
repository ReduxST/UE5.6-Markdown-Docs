# nDisplay Actor Replication

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/ndisplay-actor-replication-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/ndisplay-actor-replication-in-unreal-engine)  
**Processed:** 2025-06-14 16:38:12

---

All inputs to the nDisplay system are handled only by the primary node. Without any replication, only the primary node would see changes in the scene. Therefore, the primary node needs to be able to replicate changes to all other parts of the nDisplay network.

To accomplish this, nDisplay offers two different kinds of Components that you can attach to your Actors:

-   The **DisplayClusterSceneComponentSyncParent** Component tracks changes in the 3D transforms of its parent Component, and pushes those changes to the other cluster nodes in the network.  
    The default DisplayClusterPawn used by the nDisplay system uses this Component.
    
-   The **DisplayClusterSceneComponentSyncParent** Component tracks changes to the 3D transforms of its child components, and pushes those changes to the other cluster nodes in the network.
    

For example, in the Actor shown below, the **DisplayClusterSceneComponentSyncParent\_Scene** Component tracks and replicates changes to the 3D transforms of its parent Actor as the Actor moves around the Level. The **DisplayClusterSceneComponentSyncThis** Component tracks and synchronizes movements of its child Static Mesh component as it moves relative to the scene graph root.

![DisplayClusterSceneComponentSyncParent](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/aadbf4a5-30d0-46b9-a138-fbeff8699a8a/01-bp-actor-sync_ue5.png "DisplayClusterSceneComponentSyncParent")

If you have other Actors in your scene that can be affected during gameplay, you must use one of these two Components to replicate those changes to all nodes. To do this:

1.  Select the Actor you need to replicate in the Level viewport or the **World Outliner** panel.
2.  In the **Details** panel, click **\+ Add Component**. Search for either **DisplayClusterSceneComponentSyncParent** or **DisplayClusterSceneComponentSyncThis**, and select it from the list.
    
    ![Add an nDisplay sync Component](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8e5cf88a-5105-497e-9a65-200574a5f706/02-add-display-sync-parent_ue5.png "Add an nDisplay sync Component")

These components do not carry out a full replication. Only the transforms of the parent Actor or of child Components are sent to the cluster.

## Replicating Custom Data

If you need to replicate other custom data between your primary node and the rest of your cluster, you can write your own C++ class that implements the `IDisplayClusterClusterSyncObject` interface. nDisplay will automatically invoke the methods in this interface to check whether each instance of this class needs to be synchronized from the primary node to the other cluster nodes.