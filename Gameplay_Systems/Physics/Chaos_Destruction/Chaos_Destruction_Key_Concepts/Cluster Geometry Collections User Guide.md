# Cluster Geometry Collections User Guide

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/cluster-geometry-collections-user-guide-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/cluster-geometry-collections-user-guide-in-unreal-engine)  
**Processed:** 2025-06-14 16:13:47

---

You can find similar information in video format in the Developer Community site by watching the [Fracture and Clustering](https://dev.epicgames.com/community/learning/tutorials/k84m/chaos-destruction-fracture-and-clustering) tutorials.

**Fracture Mode** is a [Level Editor Mode](/documentation/en-us/unreal-engine/level-editor-modes-in-unreal-engine) that contains a variety of tools, including those used by the **Chaos Destruction System** for creating, fracturing, and manipulating **Geometry Collections**, the asset type for simulating real-time fracturing in Unreal Engine.

When you fracture a Geometry Collection, a new **fracture level** is created. This is reflected in the Geometry Collection's **Fracture Hierarchy** window.

![When you fracture a Geometry Collection, a new fracture level is created](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/db0c9140-dfd3-4353-9708-0d467d857f30/destruction-cluster-8.png)

You can also see a summary of the fracture levels in the **Level Statistics** panel.

![Level Statistics panel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/297e0af4-16b1-4458-8eda-3f5a5db04468/destruction-cluster-9.png)

Each fracture level in the hierarchy represents a **cluster of bones** (fractured pieces) for the Geometry Collection. In other words, all the bones grouped in the same level will be treated as a group when it comes to the fracture simulation.

Clustering helps reduce the performance impact of the simulation as the system has less collisions to calculate at the same time. During the simulation, the higher level clusters will break first, followed by the lower ones. In the example above, Level 1 (20 pieces) will break first, followed by Level 2 (87), and so on.

Clustering can create a more realistic destruction simulation as most objects in the real world fracture into larger pieces when strain is first applied. Clustering can also be used to give your destructible object different artistics looks by applying different fracture patterns to your Geometry Collection.

You can enable or disable Clustering during the simulation by selecting your Geometry Collection and referring to the **Details** panel. Scroll down to the **Clustering** section and toggle the **Enable Clustering** checkbox.

![Scroll down to the Clustering section and toggle the Enable Clustering checkbox](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/022ec511-6873-4ba4-86db-1f46ea0c370a/destruction-cluster-10.png) ![Clustering enabled](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d423ad77-fe52-4beb-b22f-b8cf42ca404d/destruction-cluster-clustering.gif) ![Clustering disabled](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b406d374-a937-47ad-9342-91b3ebb47def/destruction-cluster-noclustering.gif)

Fracture Mode has a variety of tools to adjust the bone clusters in your Geometry Collection. This gives you more control over the performance and aesthetics of the simulation.

In this guide you will learn how to use the available clustering tools.

Before learning about the clustering tools, you should know how to create Geometry Collections and fracture them. If you are not familiar with the process, refer to the [Geometry Collections User Guide](/documentation/en-us/unreal-engine/geometry-collections-user-guide) and the [Fracturing User Guide](/documentation/en-us/unreal-engine/fracturing-geometry-collections-user-guide).

## The Cluster Tools

In this section you will learn how to use the available clustering tools in the Fracture Mode.

### Auto Cluster

![The Auto cluster tool selected](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5fec9c4f-e6fa-484e-94fd-7e0822ab9061/destruction-cluster-11.png)

The **Auto** cluster tool creates bone clusters by using a specified number of **Cluster Sites**. This gives you precise control of how many clusters are created when the cluster operation is applied to the Geometry Collection. You can also specify whether bones grouped together should connect by enabling the **Enforce Cluster Connectivity** checkbox.

![The Auto cluster tool creates bone clusters by using a specified number of Cluster Sites](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/49662649-9530-4485-a6bf-a44d5533bbc2/destruction-cluster-12.png)

The tool is branch-based, meaning that it creates a cluster based on the current number of bones selected in the **Fracture Hierarchy**.

In the example below, the **Uniform Voronoi** fracture tool was used to create **500** sites.

![Geometry Collection fractured into 500 sites](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3d600944-2a30-41fd-9d5a-79bcde356696/destruction-cluster-13.png)

You can see the hierarchy in the Level Statistics panel or the Fracture Hierarchy window.

![Level Statistics panel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/053775fc-d1c2-4011-8de7-d5e918ab2dcc/destruction-cluster-14.png)

Select the **Auto** cluster tool and enter **200 Cluster Sites**.

![Select the Auto cluster tool and enter 200 Cluster Sites](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8a5dd590-4f08-46b9-8c97-2ed7f186822b/destruction-cluster-15.png)

Click **Auto Cluster** button to see the results.

![Click Auto Cluster to see the results](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a318ec52-b761-4e0a-a364-d5022f921e00/destruction-cluster-37.png)

Now you can see the result.

![Level 1 now has 200 bones](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a3f36fd4-0df0-4a12-b671-2219a3365f6b/destruction-cluster-16.png)

Repeat this process and add an additional 100, 50, and 15 Cluster Sites.

![The new hierarchy reflects the clusters you created](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/69c7c799-fdcb-4a69-a924-a2321ff85487/destruction-cluster-17.png)

As you can see, you can create as many fracture levels (clusters) as you want to achieve a desired effect.

### Magnet Cluster

![The Magnet Cluster tool selected](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/422ce406-f610-4a8a-a0d9-aad32d5aec20/destruction-cluster-18.png)

The **Magnet Cluster** tool creates bone clusters by grouping all connecting bones of the current selection. You can specify the number of **Iterations** to control how many bones are grouped using the operation.

![Number of Iterations in the Cluster Magnet tool](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4f298aa9-5623-46a7-90df-a82112f6f472/destruction-cluster-20.png)

In the example below, **1** iteration is used to cluster all bones on the outer ring of the selection.

|   |   |
| --- | --- |
| ![Before clustering](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/20b329cf-7266-4270-a545-a1914efde80e/destruction-cluster-19a.png) | ![After clustering](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e839bd2d-6882-42ab-b1b2-c6693cc1ab47/destruction-cluster-19b.png) |
| Before clustering | After clustering |
| *Click image for full size.* | *Click image for full size.* |

In this example, **2** iterations are used to cluster the outer 2 rings from the selection.

|   |   |
| --- | --- |
| ![Before clustering](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9f66e6cc-faf3-41dd-b6f8-d572252c7ff0/destruction-cluster-19b.png) | ![After clustering](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1e48a4c5-3cca-4770-9ba6-d0f5d4145263/destruction-cluster-19c.png) |
| Before clustering | After clustering |
| *Click image for full size.* | *Click image for full size.* |

The Magnet Cluster tool can also work with multiple selections at once. In the example below, the tool is used with 3 bones selected for 1 iteration at a time. You can see how each time we apply the operation, the connecting bones of each selection are clustered separately.

![Each time you apply the operation, the connecting bones of each selection are clustered separately](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c9ed595c-46f3-40e8-aded-9c1935d86993/destruction-cluster-magnet.gif)

### Flatten Cluster

![The Flatten Cluster tool](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0baa966f-73e6-44a7-a332-163e8ebf3f30/destruction-cluster-38.png)

The **Flatten** cluster tool flattens the bone hierarchy, removing the middle levels of the **Destruction Hierarchy**. This can be useful to remove the intermediate fracturing steps to get to a final fracture pattern.

In the example below, we see a Geometry Collection fractured into beams for its first level (Level 1), then further fractured into blocks (Level 2).

|   |   |
| --- | --- |
| ![Level 1](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e5bfa770-4dcb-4616-8fc2-c3ff69a20ccf/destruction-cluster-21a.png) | ![Level 2](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/94e59026-c41b-4ed1-9878-88ae098de636/destruction-cluster-21b.png) |
| Level 1 | Level 2 |
| *Click image for full size.* | *Click image for full size.* |

We can use the Flatten cluster tool to flatten the hierarchy and remove the beam configuration altogether. Select the root bone in the hierarchy and click **Flatten**.

|   |   |
| --- | --- |
| ![Before using Flatten](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c031a278-139c-4189-8e07-158e3ab83456/destruction-cluster-22a.png) | ![After using Flatten](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b58d9d8f-fab7-41d2-af09-c54457bf5534/destruction-cluster-22b.png) |
| Before using Flatten | After using Flatten |
| *Click image for full size.* | *Click image for full size.* |

### Cluster and Uncluster

![The Cluster and Uncluster tools](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/367910e8-4064-480d-896e-ba62b0f67f52/destruction-cluster-39.png)

The **Cluster** tool creates a bone cluster from the current bone selection. Conversely, the **Uncluster** tool removes a bone cluster from the current selection. This gives you complete control over the creation of Clusters in your Geometry Collection.

In the example below, we have a Geometry Collection fractured into blocks with two levels in the hierarchy.

![The Geometry Collection has two levels in the Fracture Hierarchy](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/195d9085-3d6a-4d78-b3a5-ccaa61fabd4f/destruction-cluster-23.png)

Select a group of bones and click **Cluster** to create a new cluster for the selected bones.

|   |   |
| --- | --- |
| ![Before using Cluster](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9d677c90-8881-4afb-94d4-9776030688ab/destruction-cluster-24a.png) | ![After using Cluster](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6892e29c-c8df-4a4c-869f-7a980a9173c6/destruction-cluster-24b.png) |
| Before using Cluster | After using Cluster |
| *Click image for full size.* | *Click image for full size.* |

Repeat this process and create two more clusters.

![Repeat this process and create two more clusters](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4e544ee1-e0d3-4d10-9c0e-bd119ec05388/destruction-cluster-25.png) ![The new hierarchy after clustering](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f6966587-15ce-41d9-bb22-093236c65af2/destruction-cluster-26.png)

You can use the **Uncluster** tool to remove a cluster by selecting the bone in the hierarchy and clicking **UnClstr**.

|   |   |
| --- | --- |
| ![Before using Uncluster](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/dc903394-57cb-41b2-abcb-3a37e4d197df/destruction-cluster-27a.png) | ![After using Uncluster](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/08a8d7a6-0a9a-4685-88ba-a96909fd95fc/destruction-cluster-27b.png) |
| Before using Uncluster | After using Uncluster |
| *Click image for full size.* | *Click image for full size.* |

### Merge Cluster

![The Merge tool](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e0ae0c71-e83a-4ea0-bf07-d17b8791d348/destruction-cluster-40.png)

The **Merge** cluster tool combines clusters into a single cluster and keeps the same structure in the hierarchy.

This can be useful to keep a certain number of bones in the hierarchy for your simulation.

In the example below you can see a Geometry Collection that has three clusters in Level 1. If we select two clusters and click **Cluster**, both clusters combine into one. However, the hierarchy now looks like this:

|   |   |
| --- | --- |
| ![Before using Cluster](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c3520cfe-e7a0-45bc-92cf-9a266d8cdac9/destruction-cluster-28a.png) | ![After using Cluster](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9ae9bafa-a19f-4245-8d0a-e040d6e56dc5/destruction-cluster-28b.png) |
| Before using Cluster | After using Cluster |
| *Click image for full size.* | *Click image for full size.* |

As you can see, the hierarchy has been altered after the operation. In contrast, if we use the **Merge** cluster tool, the hierarchy remains the same:

|   |   |
| --- | --- |
| ![Before using Merge](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/10ad0e86-df17-44cd-a591-45edcf10aa82/destruction-cluster-28a.png) | ![After using Merge](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1a113f52-a7b6-4d20-a341-f7f77d787086/destruction-cluster-28c.png) |
| Before using Merge | After using Merge |
| *Click image for full size.* | *Click image for full size.* |

### Level Up Cluster

![The Level Up cluster tool](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f8d6a697-fbef-4a90-ad45-04ab8f80b1a4/destruction-cluster-41.png)

The **Level Up** cluster tool moves the selected bones to a higher level in the hierarchy. Select the desired nodes in the **Fracture Hierarchy** window and click **Level Up** to see the results.

You can also perform this operation on the entire hierarchy by selecting the root bone and clicking **Level Up**.

![Before using the Level Up tool](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f3f0de91-33b1-4d0c-82de-5a6db1f1811b/destruction-cluster-29a.png)

![After using the Level Up tool](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f71fc7d3-1289-47f0-b30a-f4775a1fd31f/destruction-cluster-29b.png)

### Drag and Drop Clustering

You can create bone clusters manually by dragging and dropping bones directly in the **Fracture Hierarchy** window. You can drag clusters or leaf nodes into other clusters.

In the example below, the Geometry Collection has **2** bones in **Level 1** and **25** bones in **Level 2** of the hierarchy.

|   |   |
| --- | --- |
| ![Level 1](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1d2088e3-d92b-4d77-a735-da9806f7112e/destruction-cluster-30a.png) | ![Level 2](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/53a5be49-fb80-49d7-a8ad-edc250ce27e8/destruction-cluster-30b.png) |
| Level 1 | Level 2 |
| *Click image for full size.* | *Click image for full size.* |

You can select any bone in the hierarchy and move it to alter the clusters in the level above.

![You can select any bone in the hierarchy and move it to alter the clusters in the level above](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0cdfac15-f761-490a-8876-cd4384dd0be6/destruction-cluster-manual-cluster.gif)

## Embedded Geometry Tools

The Fracture Mode comes with tools to embed additional geometry into the fracture simulation. The primary purpose of embedded geometry is to add a layer of visual complexity to augment the simulation. For this reason, embedded geometry does not have any collision nor is it considered part of the simulation.

A common example is using embedded geometry to create the internal structure of a building. This can be rebar, cabling or grout within the walls.

In the example below, we have a Geometry Collection that has been cut diagonally. Drag a **Static Mesh** into the Geometry Collection and make sure it intersects with the Geometry Collection.

![Drag a Static Mesh into the Geometry Collection and make sure they intersect](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a878475b-aae7-44c3-945c-4c6ca0b47c30/destruction-cluster-31.png)

Duplicate the Static Mesh and move it to the other side of the Geometry Collection.

![Duplicate the Static Mesh and move it to the other side of the Geometry Collection](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f47b863b-fb62-4f35-a673-246930cba2c7/destruction-cluster-32.png)

Select both Static Meshes and the Geometry Collection and go to the **Embed** section and click **Auto**.

![Click Auto to embed the Static Meshes into the Geometry Collection](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4552432b-1134-42e8-8817-83e34375ce27/destruction-cluster-33.png)

You can now remove the Static Meshes from the level. You will notice that the Static Meshes still appear to be intersecting the Geometry Collection.

Go to the **Content Browser** and open the **Geometry Collection** asset. Scroll down to the **Embedded Geometry Exemplar** section and expand it. Notice how the Static Mesh has been added to the list along with the **Instance Count** denoting that we are using 2 instances of the Mesh in the Geometry Collection.

![Scroll down to the Embedded Geometry Exemplar section and expand it](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9eebeea3-abf8-4679-8006-b7e6659c5d4b/destruction-cluster-34.png)

You can continue to add Static Meshes to the Geometry collection by clicking **Auto** to embed them into the Geometry Collection.

![The meshes are embedded to their respective bones in the Geometry Collection](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ef88c041-99bb-4ec5-81ea-9d6e0b39b2c1/destruction-cluster-embedded-1.gif)

If you want to embed a Static Mesh that does not overlap the Geometry Collection, select a bone in the Geometry Collection and the Static Mesh, then click **Embed**.

![Select the Static Mesh and bone of the Geometry Collection and click Embed](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/373484cc-d993-4ee3-9aac-4d4bf26d0d98/destruction-cluster-35.png) ![The Mesh is embedded to the Geometry Collection bone without overlapping it](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/50f259f2-a0cf-4358-b885-b1b000cc0000/destruction-cluster-embedded-2.gif)

Click **Flush** to remove all embedded geometry from the Geometry Collection.

![You can remove all embedded geometry from the Geometry Collection by clicking Flush](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b4a19bea-1d75-468a-8123-ddbf95cd9bc9/destruction-cluster-36.png)