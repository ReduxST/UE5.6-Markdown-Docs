# Set Up the SteamVR Chaperone

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/set-up-the-steamvr-chaperone-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/set-up-the-steamvr-chaperone-in-unreal-engine)  
**Processed:** 2025-06-14 16:48:53

---

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0cd298c1-ff0f-4c62-a793-002705a3947c/svrchaperone_hero_image.png)

The SteamVR Chaperone component is used to display to the user where the soft and hard bounds of the VR interaction area are. In the following How - To we will take a look at how to add the SteamVR Chaperone to any UE4 VR Pawn.

It is **NOT** possible nor advisable to disable the Chaperone system from inside UE4. You can, however, adjust how UE4 will react to the user getting close to the boundaries.

## Steps

To add the SteamVR Chaperone system to your UE4 player pawn, you will need to do the following:

1.  Open up your projects player Pawn Blueprint and make sure the **Components** tab is visible.
    
2.  Click on the **Add Component** button and from the displayed list search for the **Steam VRChaperone** component and when located, click on it to add it to the Component list.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/25c44f71-172f-44e0-83b2-02f78bb222d2/svrchaperone_00.png)
3.  When completed, your player pawn should look like the following image.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6dba7cac-d263-4253-b3f2-4cae3df94ea1/svrchaperone_01.png)

## End Result

Now, launch your project in VR and put on your Vive HMD and when you approach the bounds of your VR interaction area you should see something similar to the following video:

## UE4 Project Downloads

Below you will find a link to where you can download the UE4 project that was used to create this example.

-   [**SteamVR Chaperone Set Up Project**](https://epicgames.box.com/s/f9aw7n5wpjc0nnzjtiom78hticmdl3w1)