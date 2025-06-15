# Add a Custom Trace Type to your Project

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/add-a-custom-trace-type-to-your-project-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/add-a-custom-trace-type-to-your-project-in-unreal-engine)  
**Processed:** 2025-06-14 16:04:47

---

Often you will find a need for more than just the two default **Trace Response** channels (Visibility and Camera), perhaps you have a special laser that needs to pass through a special opaque object that you can't see through or have the camera clip through. When you encounter a situation like this you can add your own custom **Trace Response** channels by following the steps below.

## Steps

1.  Open your project settings: **Edit Menu** -> **Project Settings**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e90e5a9d-d939-4664-9569-bb24dc225171/col-project-settings-1.png)
2.  Under **Engine** select **Collision**:
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/00d4f1ca-cd62-47bf-b81a-219ed867a01a/col-project-settings-2.png)
3.  Click the **New Trace Channel...** button. Name your new **Trace Channel** and set its **Default Response**. Click the **Accept** button.
    
    The **Default Response** can be **Block**, **Overlap**, or **Ignore**. Depending on your use case you'll want to choose carefully to prevent as much additional work adjusting collision profiles on your Actors.
    
4.  Any **Blueprints** open in the **Blueprint Editor** will have to be closed down and re-opened for the new Trace Channel to appear on any components or nodes.
    

## Result

You'll now have a new Trace Channel to use anywhere in the editor. Any Actors or Components you want to be able to Trace with your new Channel will have to be set to block the new Channel.