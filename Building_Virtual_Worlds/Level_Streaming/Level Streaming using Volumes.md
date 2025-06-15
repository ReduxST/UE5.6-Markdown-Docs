# Level Streaming using Volumes

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/level-streaming-using-volumes-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/level-streaming-using-volumes-in-unreal-engine)  
**Processed:** 2025-06-14 16:33:18

---

We want to start streaming in the patio level here, so that by the time the player rounds the corner and begins approaching the patio, the streaming level will be loaded and visible.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b97d9717-a06a-49a0-868e-0ad5363b77a0/streaminglevelvisible.png)

As part of the setup, we have two levels, **SunTemple\_Persistent** and **SunTemple\_Streaming**. Our **Player Start** is in **SunTemple\_Persistent**, and our player in the game is represented by a *Character*.

1.  Open **SunTemple\_Persistent** in the **Content Browser**.
    
2.  Move the **Player Start** to the very beginning of the temple.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f44bb89a-1617-4e9b-b777-f111478fc1e8/playerstart.png)
3.  Click on **Windows**, then select **Levels**.
    
4.  Click on the **Levels** dropdown menu, then select **Add Existing...** to add a new sublevel.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/67f53da0-112e-4e74-9a3d-2dd847af9d36/addexisting.png)
5.  Select **SunTemple\_Streaming** to add in the **Open Level** dialog, then click on **Open**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fa87a989-3e34-433a-b8dd-1d4edfc413bb/suntemplestreaming_select.png)
6.  **Right-click** on **Persistent Level** and select **Make Current** from the dropdown menu.
    

## Streaming In Levels with Volumes

1.  In the **Place Actors** panel, select the **Volumes** tab and then drag a **Level Streaming Volume** into your level.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9e012155-289b-43bc-80a2-70766cf7ddbc/levelstreamingvolumemodes.png)
2.  Arrange the **Level Streaming Volume** to encompass the whole walkable area of **SunTemple\_Streaming**. ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/72acbd6f-08a7-45dd-9888-adc51a005a9b/lsvplacement.png)
    
    Keep in mind that the logic for Level Streaming Volumes tracks where your active camera is, so if you have a camera placed at a distance from your player's Pawn or Character, you may need to adjust the size and placement of the Level Streaming Volume accordingly.
    
3.  Click on **Windows**, then select **Levels**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/58f51eb6-ee3c-4717-9707-8730e73bceca/windowlevels.png)
4.  Select **SunTemple\_Streaming**, then click on the **Level Details** icon.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0cf9ced4-7c36-4d99-ba6a-aeb38bf6eade/leveldetails.png)
5.  Next to **Streaming Volumes**, click on the plus sign (**+**) to add a new volume. Then, use the dropdown menu or the eyedropper to select the **Level Streaming Volume** you just placed in the level. ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/03c42bc5-c021-43ce-aa85-64dea5f7b075/addlsv.png)
    
6.  Ensure that the **Initially Loaded** and **Initially Visible** checkboxes are unchecked, then close the **Level Details** panel.
    
7.  Back in the **Viewport**, select the **Level Streaming Volume**. In the **Details** panel, set the following properties of the volume: **Editor Pre Vis Only** and **Disabled** should be unchecked, and **Streaming Usage** should be set to **SVB Visibility Blocking on Load**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/50198ce9-ed9e-49e6-8ad3-0eb519fc46cb/lsvsettings.png)
8.  Use **Play in Editor** to test out your streaming level.