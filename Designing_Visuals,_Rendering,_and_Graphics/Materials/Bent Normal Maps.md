# Bent Normal Maps

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/bent-normal-maps-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/bent-normal-maps-in-unreal-engine)  
**Processed:** 2025-06-14 16:09:56

---

![Non Bent Normal](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b5c616b0-b831-4753-b136-75085441bac3/no_bentnormal_00.png)

![Bent Normal](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fcebad25-bc2c-4327-ab80-7f5efa4b82c1/bentnormal_00.png)

Using Bent normals within Materials can help improve how they react to lighting and shading. In the following document, you will find all the information you need to start using Bent normals in your Unreal Engine projects.

## Benefits to Using Bent Normals

Below, you will find some of the benefits to using Bent normals.

-   One of the biggest impacts Bent normals tend to have is to reduce the amount of light leaking that happens after a light build.
-   Bent normals can also be used with Ambient Occlusion (AO) to improve Diffuse indirect lighting. It does this by making the Diffuse indirect light closer match Global illumination (GI) by using the Bent normals for indirect lighting instead of the Normals.

![Diffuse indirect lighting using AO](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/98732f23-0cf4-4253-8a3e-8123ddf8d5ab/bentnormalaolighting.png)

![Diffuse indirect lighting using Bent normal ](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d98abd5f-4ac7-49b8-b8cc-37e6b1636e3c/bentnormallighting.png)

## Bent Normal Creation

To get the highest quality Bent Normal map, and to match Unreal Engine's assumptions on how Bent Normal maps should be calculated, make sure to adhere to the following information when creating your Bent Normal maps:

-   Use **Cosine Distribution** when creating the Bent Normal map.
    
-   You can use [Substance Designer 6](https://www.allegorithmic.com/blog/substance-designer-6-unleashed-now-scan-processing-and-new-nodes) to generate the Bent Normal map just like a standard normal map or an AO map.
    
-   When generating your Bent normal, make sure your character is in a T-Pose.
    
-   The Bent normal and the AO should use the same **distance** setup.
    
-   The Bent normal should be in the same space as your Normal map. Consult the following chart for more information:
    
    | World Space Type | Normal Map Type | Bent Normal Type |
    | --- | --- | --- |
    | World | World | World |
    | Tangent | Tangent | Tangent |
    

## Using Bent Normals in Unreal Engine

Using Bent Normal maps inside of a Material is very similar to setting up and using Normal maps. All you need to do is add the **Bent Normal** custom output node to the Material graph and then connect your Bent Normal map to the input like in the following image. Also, make sure that there is an AO map input into the **Ambient Occlusion** input.

Click for full image.

## Reflection Occlusion

Bent Normal maps are also used in a powerful but less traditional way, and that is for Reflection Occlusion / Specular Occlusion. An Ambient Occlusion (AO) map occludes Diffuse indirect light, while Reflection Occlusion is a similar concept, but applied to Specular indirect lighting. Reflection Occlusion works by intersecting the Specular lobe with the visible cone or a cone representing the unoccluded part of the hemisphere described by the Bent normal as the cone axis and the AO amount as the cone angle. This results in significantly reduced Specular light leaking especially when Screen Space Reflection (SSR) data is not available.

Multi-bounce approximation for occlusion is also supported. This means that instead of AO or Reflection Occlusion shadowing the first bounce, we can use an approximation of what many bounces will produce. With multi-bounce approximation, brighter Materials will lose less light, and colored Materials will be made more saturated.

![AO](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c6e44915-1d2d-4e9a-a4fb-afe2a9e2a4c4/reflectionbnao.png)

![Bent Normal](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/47077c81-c748-4645-825f-c8ffe289e4a6/reflectionbn.png)