# Landscape Hydro-Erosion Tool

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/landscape-hydroerosion-tool-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/landscape-hydroerosion-tool-in-unreal-engine)  
**Processed:** 2025-06-14 16:32:12

---

The **Hydro Erosion** tool uses a hydraulic erosion simulation (erosion by water) to adjust the height of the Landscape heightmap. A noise filter is used to determine where the initial rain is distributed for the simulation. Then the simulation is calculated to determine water flow from the initial rain as well as dissolving, water transfer, and evaporation. The result of the calculation provides the actual value used to lower the heightmap.

## Using the Hydro Erosion Tool

In this example, the Hydro Erosion tool has been used to paint rain erosion onto the surface of the hillside. This makes it appear that parts of the Landscape have eroded away over time as rain has fallen. The tool settings can enable the amount of rain and areas that it affects to help define the look.

Use the following controls to Sculpt with Hydro Erosion for your Landscape heightmap:

| Controls | Operation |
| --- | --- |
| 
**Left Mouse Button**

 | 

A noise filter is used to erode parts of the heightmap.

 |

![Before](https://dev.epicgames.com/community/api/documentation/image/d64111d7-cf59-446c-9e08-ab2c9af3ad8c?resizing_type=fit&width=1920&height=1080)

![After](https://dev.epicgames.com/community/api/documentation/image/0cb84610-bb61-443e-841b-649fdc447dfb?resizing_type=fit&width=1920&height=1080)

Before

After

In this example, as Hydro Erosion is used to paint onto the Landscape the heightmap runs a simulation that treats the heightmap as if rain has eroded away its surface over time. This can create interesting looks and crevices to the Landscape.

## Tool Settings

|  |  |
| --- | --- |
| 
[![Hydro Erosion Tool](https://dev.epicgames.com/community/api/documentation/image/2b497f25-a66e-4b8a-9313-4dc86c5d6782?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/2b497f25-a66e-4b8a-9313-4dc86c5d6782?resizing_type=fit)



 | 

[![Hydro Erosion Tool Properties](https://dev.epicgames.com/community/api/documentation/image/daea01cd-7bef-40bb-b513-25ff2c81f96a?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/daea01cd-7bef-40bb-b513-25ff2c81f96a?resizing_type=fit)



 |

| Property | Description |
| --- | --- |
| 
**Tool Strength**

 | 

Controls how much effect each brush stroke has.

 |
| 

**Rain Amount**

 | 

The amount of rain to apply to the surface. Larger values will result in more erosion.

 |
| 

**Sediment Cap.**

 | 

The amount of sediment that the water can carry. Larger values will result in more erosion.

 |
| 

**Iterations**

 | 

The number of iterations performed. Larger values result in more levels of erosion.

 |
| 

**Initial Rain Distribution**

 | 

Whether rain is applied randomly or to the entire area.

-   **Both**: This will use a random pattern that acts like it has rained in some places and not others to erode parts of the heightmap.
    
-   **Positive**: This will act as if it has rained in all parts of the applied area to erode parts of the heightmap.
    

 |
| 

**Rain Dist Scale**

 | 

The size of the noise filter for applying initial rain to the surface. The noise filter is related to position and scale, which means if you do not change **Rain Dist. Scale**, the same filter is applied to the same position many times.

 |
| 

**Detail Smooth**

 | 

If checked, performs a detail-preserving smoothing to the erosion effect using the specified detail-smoothing value. Larger detail-smoothing values remove more details, while smaller values preserve more details.

 |