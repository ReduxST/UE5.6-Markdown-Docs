# Generating More Efficient Results

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/generating-more-efficient-results-with-the-proxy-geometry-tool-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/generating-more-efficient-results-with-the-proxy-geometry-tool-in-unreal-engine)  
**Processed:** 2025-06-14 16:25:27

---

Surprisingly, there are times when adding a little geometry will actually result in more efficient proxy results.  This is due to the fact that the underlying spatially sampling and remeshing steps in the proxy lod pipeline are built around concepts that remove inaccessible geometry.  In the following How-To we will take a look at how to address issues like this in your Unreal Engine 4 (UE4) projects.

## Steps

1.  First, locate a group of Static Meshes that are arranged to form some type of room that has an opening like in the following image.
    
    ![Proxy_Geo_HT_GettingMore_01.png](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/58ad708a-b17f-42e8-8810-a9bc3b613ccf/proxy_geo_ht_gettingmore_01-resize793x274.png "Proxy_Geo_HT_GettingMore_01.png")
2.  Select all of the Static Meshes that make up the room along with any items the room might contain and then run the Proxy Geometry Tool create a new proxy Static Mesh.
    
    ![Proxy_Geo_HT_GettingMore_02.png](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7e3b6ca0-f94d-49ee-96fa-d0e9285fa1ac/proxy_geo_ht_gettingmore_02-resize784x271.png "Proxy_Geo_HT_GettingMore_02.png")
3.  While the Proxy Geometry Tool did a great job creating a new Static Mesh, there is a lot of detail on the inside of the room that could be removed. To help the Proxy Geometry Tool better understand that, it should remove all of the geometry inside of the building, add a small Static Mesh to the level, and position it so that it covers any openings the room might have.
    
    ![Proxy_Geo_HT_GettingMore_03.png](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a0c32ddb-9612-4167-baec-2977b0bb4386/proxy_geo_ht_gettingmore_03-resize779x277.png "Proxy_Geo_HT_GettingMore_03.png")
4.  Once all the openings have been covered by pieces of geometry, run the Proxy Geometry Tool one more time. 
    

## End Result

When the Proxy Geometry Tool finishes, take a look inside the room. Notice how almost every single triangle on the inside has been removed, like in the following image.  
![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/407d3767-51cf-43eb-9420-cbde4c19cc42/proxy_geo_ht_gettingmore_04.png "Proxy_Geo_HT_GettingMore_04.png")

The reason for this is because adding a new Static Mesh to this model to act as a blocker allowed the Proxy Geometry Tool to automatically remove all the room's internal structure early in the proxy generation. This results in a much shorter production time, a smaller number of final triangles, and a better use of the texture space.  In many cases the addition of geometry in the form of a closed door, a floor, or simply a few planes to seal the backside of a complicated facade will greatly simplify the results.