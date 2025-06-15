# Niagara Lightweight Emitters Quick Start

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/lightweight-emitters-quick-start-for-niagara-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/lightweight-emitters-quick-start-for-niagara-in-unreal-engine)  
**Processed:** 2025-06-14 16:33:38

---

This Niagara Lightweight Emitters Quick Start is designed to introduce you to **lightweight emitters**, a type of emitter that can help you optimize the performance of your Niagara systems across platforms. The examples in this guide are simple, in order to clearly demonstrate the process and illustrate the advantages of using lightweight emitters.

To learn more about lightweight emitters, read the [Lightweight Emitters Overview](/documentation/en-us/unreal-engine/niagara-lightweight-emitters-overview).

## Objectives

Through this guide, you will:

-   Create a system with a regular emitter, and one with a lightweight emitter.
    
-   Create a new testing level, and place a large number of your systems.
    
-   Use Niagara Debugger to test the performance of the systems and compare the two.
    

This guide uses the Third Person template project in the Games category.

## Create Two Niagara Systems for Testing

This section covers how to create a Niagara system and add a regular emitter to it, then create a second system with a lightweight emitter.

### Create the Regular Emitter Niagara System

Follow these steps to create a new Niagara system for the regular emitter.

1.  Open a project in Unreal Engine, or create a new one.
    
    ![Create a new project](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fd800786-e009-4e5d-a150-e8d420cddd82/create-new-project.png)
2.  Open the **Content Browser**. Right-click in the Content Browser and select **Niagara System**.
    
    ![Create new system](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8c5db4d8-7e58-44dd-870a-7bfcbbee2e8e/create-new-system.png)
3.  In the Asset Browser, select the **Default System**, and click **Create**.
    
    ![Select default system](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2f6d745d-3c4d-458f-b70f-0d3e7ed238a2/select-default-system.png)
4.  Name the new system **NS\_Fountain**. Double-click the system to open it in the Niagara Editor.
    

### Add a Regular Fountain Emitter to the First System

Follow these steps to add a regular emitter to the NS\_Fountain system.

1.  Make sure the NS\_Fountain system is open in the Niagara Editor. Right-click in the workspace, and select **Add Emitter**.
    
    ![Add a regular emitter](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/84336954-b3ef-42d9-8bae-2a29c9f17201/add-emitter.png)
2.  In the Asset Browser, select the **Fountain** emitter. Then click **Add** to add a regular emitter to the NS\_Fountain system. For this example, leave the default values as they are.
    
    ![Select fountain emitter](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4e098cac-b7f6-43fa-953a-176fa59bad08/select-fountain-emitter.png)
3.  In the Niagara Editor, click to select the fountain emitter. In the **Details** panel, click the **Gear** icon to open a menu.
    
    ![Rename the fountain emitter](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8a0aebb4-1675-486d-bcf0-49cec4064684/rename-fountain-emitter.png)
4.  Select **Rename**. Name the emitter **Fountain-R** (to indicate a regular emitter).
    

You can also rename the emitter by double-clicking the name of the emitter and typing in the new name.

### Create the Lightweight Emitter Niagara System

Follow these steps to create a second system.

1.  Right-click in the Content Browser, and select **Niagara System**.
    
2.  In the Asset Browser, select the **FountainLightweight** system, and click **Create**.
    
    ![Select fountain lightweight system](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c03d6983-cf34-42d7-9613-a80ed6f1cea0/select-fountain-lightweight-system.png)
3.  Next open the NS\_Fountain\_LW system in the Niagara Editor. This system template includes a lightweight emitter for a fountain effect.
    

### Modifying the Lightweight Emitter System

The system you created in the last section already has a lightweight fountain emitter. This section explains how to make some modifications to the emitter, so it matches the fountain emitter in the first system. This will make it easier to compare the performance of each type of emitter.

Follow these steps to modify the lightweight emitter.

1.  Double-click the name of the lightweight emitter to edit the field. Rename the emitter **Fountain-LW**.
    
    ![Rename the lightweight emitter](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/534c53f3-a106-47cf-9f19-d25fb3afafbc/lightweight-emitter-name.png)
2.  Select the emitter, then click **Spawn Rate**. Change the **Rate** setting to **300**.
    
    ![Change Rate to 300](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d5712b79-b4b4-4a05-8435-2e917581a2f0/modify-spawn-rate.png)
3.  In the emitter, leave the **default** settings for the following modules:
    
    -   Initialize Particle
    -   Shape Location
    -   Add Velocity
    -   Drag
    -   Gravity Force
4.  Click the **Scale Color** module. Change the color to red, so you can distinguish more easily between the regular and lightweight systems when testing. Then click **OK**.
    
    ![Change the scale color module](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b70440ac-c8a0-44b5-a134-e0b93785be8a/change-scale-color.png)

## Create a Testing Level

This section covers how to create a testing level in your project, so you can place multiple instances of your system.

### Create a Testing Level

Follow these steps to create a new level.

1.  From the menu bar, click **File > New Level**. In the **New Level** window, select the **Basic** template, and then click **Create**.
    
    ![Create new level](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6576e9c1-ba06-455f-85e7-939a126f5937/create-new-level-basic.png)
2.  From the menu bar, click **File > Save Current Level As**. The **Save Level As** window opens.
    
3.  Select a folder for the new level. Name the new level **NiagaraLWTest**, and click **Save**.
    
    ![Save Level As window](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f0491859-e68c-4f88-ba13-3b5fd36556f1/save-level-as.png)

### Place Systems in the Testing Level

In order to really see the difference in performance between regular and lightweight emitters, you must place a large number of instances of your systems into the test level. You can use whatever method you choose to place your systems for testing. In the illustrations for the next section, the systems are placed in a 20 x 20 array.

1.  Place the **NS\_Fountain** system into the test level, and duplicate it until you have a large number of instances in the level. In the illustration below, there is a 20 x 20 array of instances of the NS\_Fountain system.
    
    ![Place regular emitter system](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9df2bcc2-1481-4718-b0e7-aab16a178e19/place-regular-emitter-system.png)
2.  Place the **NS\_Fountain\_LW** system into the test level, duplicating it the same way you did with the NS\_Fountain system. In the illustration below, the system is placed in the same 20 x 20 array as the NS\_Fountain system was.
    
    ![Place lightweight emitter system](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a07c7024-ff24-4c05-8e70-765a80caf410/place-lightweight-emitter-system.png)

## Use the Niagara Debugger to Test Performance

This section shows how to use the Niagara Debugger to compare the performance of the regular emitter and the lightweight emitter.

### Set up the Niagara Debugger

Follow these steps to open the Niagara Debugger and set it up to measure performance.

1.  Make sure you have the NS\_Fountain system in the viewport.
    
2.  From the menu bar, click **Tools > Debug > Niagara Debugger**. This opens the **Niagara Debugger**, docked in a tab next to the **Details** panel.
    
    ![Open the Niagara Debugger](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/97e09d7a-fb2d-4012-8a9a-2ab40e520142/open-niagara-debugger.png)
3.  In the Niagara Debugger, click the three dots on the **HUD** button, and check the box for **Show Overview**. An overlay of statistics displays in the viewport.
    
    ![Check Show Overview](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/734257c7-d694-40ad-952b-ade19e19f8ca/check-show-overview.png)
4.  In the **Debug Overview** section, click the first dropdown and select **Performance**. The statistics overlay in the viewport changes to track performance.
    
    ![Change Overview to Performance](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f29f299d-3499-4293-97d1-4df21cec849e/change-overview-to-performance.png)

### Compare Regular and Lightweight Emitter Performance Overlay

Follow these steps to compare the metrics in the Performance overlay for the NS\_Fountain and NS\_Fountain\_LW systems.

1.  The Performance overlay displays several statistics for the two systems. One important metric for performance is the Game Thread Average, highlighted in the illustration below.
    
    ![Close up of performance overlay](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7544de2e-4c7d-4577-aa3a-7bedcfec8167/reg-emitter-performance-closeup.png)
2.  Select the NS\_Fountain system in the Outliner to see the overlay's metrics for the regular emitter.
    
3.  Select the NS\_Fountain\_LW system in the Outliner to see the overlay's metrics for the lightweight emitter.
    

### Compare Regular and Lightweight Emitter Stat Unit Display

Follow these steps to compare the Stat Unit list of metrics for both regular and lightweight emitters.

1.  The **Stat Unit** list displays in the upper right corner of the viewport. The Performance overlay will overlap that area, making it difficult to read. To turn off the overlay, click the **HUD** button, and uncheck the box for **Show Overview** to turn off the overlay.
    
    ![Turn off performance overlay](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c9f1f982-9185-48b4-a373-0e475b56aca6/uncheck-show-overview.png)
2.  Press the **tilde** (~) key to open the console. Type `stat UNIT`, and press Enter. This displays a list of statistics in the upper right corner of the viewport.
    
    ![Use stat UNIT command](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1297852e-6fcc-4eed-9fbf-185e7da882b7/stat-unit-command-console.png)
3.  This list displays many metrics, but two important ones are the **Frame** (frame rate) and **Draw** (draw count) for the regular emitter.
    
    ![Stat Unit display for regular emitter](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7fe870f1-b864-4c2d-8758-1174006f7b48/stat-unit-display-regular.png)
4.  Select the NS\_Fountain system in the Outliner to see the metrics for the regular emitter.
    
5.  Select the NS\_Fountain\_LW system in the Outliner to see the metrics for the lightweight emitter.
    

## End Result

You should see improvement in the Game Thread Average of Niagara effects when you use lightweight emitters.

| **NS\_Fountain** | **NS\_Fountain\_LW** |
| --- | --- |
|  |  |
| 
Click image for full size.

 | 

Click image for full size.

 |

You should also see improvements in the Frame and Draw metrics when using lightweight emitters.

| **NS\_Fountain** | **NS\_Fountain\_LW** |
| --- | --- |
| ![Stat Unit display for regular emitter](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/87c5ff03-9545-44a4-97ad-128495b136ec/stat-unit-display-regular.png "Stat Unit display for regular emitter") | ![Stat Unit display for lightweight emitter](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/887453b4-aa36-4a06-8ea5-35a7451e557e/stat-unit-display-lightweight.png "Stat Unit display for lightweight emitter") |