# Using the Proxy Geometry Tool

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/using-the-proxy-geometry-tool-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/using-the-proxy-geometry-tool-in-unreal-engine)  
**Processed:** 2025-06-14 17:01:46

---

In the following How - To we will take a look at using the Proxy Geometry Tool to create new Static Meshes and Textures for your UE5 projects levels.

## Steps

1.  The  **Proxy Geometry Tools**  are part of the Merge Actor tools so to open them up you need to go to  **Tools** and then click on the **Merge Actors** option.
    
    [![Merge Actors tool](https://dev.epicgames.com/community/api/documentation/image/a97e1df1-d2fd-47b6-adf5-132148cf69c0?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/a97e1df1-d2fd-47b6-adf5-132148cf69c0?resizing_type=fit)
    
    Click image for full size.
    
2.  When the Merge Actors tool is open, you should see two icons at the top. Click on the second icon to show the options for the Proxy Geometry Tools. 
    
    [![Merge Actors tool](https://dev.epicgames.com/community/api/documentation/image/b7c66933-1a11-411a-86b3-ea1dcab1c312?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/b7c66933-1a11-411a-86b3-ea1dcab1c312?resizing_type=fit)
    
    Click image for full size.
    
    The options in the Proxy Geometry tool will only become active when you have Static Meshes selected in a level.
    
3.  Navigate to a location in a level and then start selecting Static Meshes. For this example 21 Static Meshes have been selected but please feel free to select as many Static Meshes as you want.
    
    [![Selecting Static Meshes](https://dev.epicgames.com/community/api/documentation/image/8448098a-8bb2-4623-97fb-c3c21fcfb6fc?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/8448098a-8bb2-4623-97fb-c3c21fcfb6fc?resizing_type=fit)
    
    Click image for full size.
    
4.  With the Static Meshes still selected locate the Merge Actors window and then press the **Merge Actors** button to begin the Proxy Geometry tool creation process.
    
    [![Merge Actors button](https://dev.epicgames.com/community/api/documentation/image/65ecc6ff-ea9b-4989-80bf-6cfa586778cd?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/65ecc6ff-ea9b-4989-80bf-6cfa586778cd?resizing_type=fit)
    
    Click image for full size.
    
5.  When prompted, specify a **Name** and **Location** for the new assets that the Proxy Geometry Tool will create. Once that is completed, press the **Save** button to continue the Proxy Geometry tool creation process.
    
    [![Creating Static Mesh](https://dev.epicgames.com/community/api/documentation/image/490b5476-0260-4fc2-8342-4b79c5254bbe?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/490b5476-0260-4fc2-8342-4b79c5254bbe?resizing_type=fit)
    
    Click image for full size.
    
    The time that it takes for the Proxy Geometry tool to finish can range from a few minutes to a few hours. The current progress will be shown in the following window.
    
    [![Creating Mesh Proxy](https://dev.epicgames.com/community/api/documentation/image/4b9a98a2-c808-42bf-a23a-03bee84b7221?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/4b9a98a2-c808-42bf-a23a-03bee84b7221?resizing_type=fit)
    
    Click image for full size.
    
6.  When the Proxy Geometry tool has completed, go to the Content Browser and search for the newly created assets by input the name given to them in step five.
    
    [![Newly Created Static Mesh](https://dev.epicgames.com/community/api/documentation/image/66ceed08-b0b5-4767-baf4-36e8a1e53d29?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/66ceed08-b0b5-4767-baf4-36e8a1e53d29?resizing_type=fit)
    
    Click image for full size.
    

## End Result

To view the Static Mesh that was created, go to the Content Browser and double-click on the Static Mesh that was generated. When looking at the Static Mesh in the Static Mesh Editor, note the reduced triangle and material count.   

[![The Static Mesh view.png](https://dev.epicgames.com/community/api/documentation/image/4ad3f5e8-3a43-43fe-983c-ebbc4d809f75?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/4ad3f5e8-3a43-43fe-983c-ebbc4d809f75?resizing_type=fit)

Click image for full size.