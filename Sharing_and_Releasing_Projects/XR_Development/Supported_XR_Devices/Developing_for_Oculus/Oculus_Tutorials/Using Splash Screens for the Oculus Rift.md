# Using Splash Screens for the Oculus Rift

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/using-splash-screens-for-the-oculus-rift-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/using-splash-screens-for-the-oculus-rift-in-unreal-engine)  
**Processed:** 2025-06-14 17:01:03

---

Skill\_family: Tutorial Level 1 Version: 5.0 Parent: sharing-and-releasing-projects/xr-development/supported-xr-platforms/developing-for-oculus/OculusHowTo Order: 2 tags: Oculus prereq: sharing-and-releasing-projects/xr-development/supported-xr-platforms/developing-for-steamvr/HowTo/StandingCamera prereq: sharing-and-releasing-projects/xr-development/making-interactive-xr-experiences/using-motion-controllers prereq: sharing-and-releasing-projects/xr-development/supported-xr-platforms/developing-for-oculus/OculusHowTo/GuardianSystem

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/52051557-4708-4639-8bd4-0da5a93ab8e9/htsplashscreen_hero_image.png)

Whenever you are changing levels in your UE VR project, the user could experience some framerate issues due to the massive amount of data that is being unloaded and loaded. To help avoid this issue and mask any frame rate issues that might arise when loading a new level you can display a Splash screen or movie to the user. In the following tutorial we will go over how to setup and call a splash screen in your UE projects.

## Steps

\* For this How - To you will need to download, unzip and import the two files contained in the following zip file, **[Oculus Splash Screen Source Files](https://d1iv7db44yhgxn.cloudfront.net/documentation/attachments/9d51a798-a51d-4935-b567-ed49a72cdb1f/oclussplashscreensourcecontent.zip)**

1.  Open up your VRPawn and go to the **Event Graph**. Right-click inside the Event Graph and search for and add the following Blueprint nodes:
    
    -   Event Begin Play
    -   Set Tracking Origin
    -   Enable Auto Loading Splash Screen
    -   Add Loading Splash Screen
    -   Hide Splash Screen
        
        Click for full image.
        
2.  Since we want the Splash screen to be called each time a level is loaded, we will want first to make sure that we enable the autoloading of Splash screen and then set what we want to use as the Splash screen. Finally, we will want to hide the Splash Screen so that we can call it when we need it later. Now set up the nodes in your VRPawn Event Graph to match the following image:
    
    Click for full image.
    
    Make sure that you check the **Auto Show Enabled** property on the **Enable Auto Loading Splash Screen** so that the Splash screen will be automatically called each time a level is loaded.
    
3.  In the **Add Loading Splash Screen** node, there is a **Texture** input which controls what Texture or Movie will be displayed when this is node is called. Set the Texture used to be the **T\_UE4\_Logo\_00** or any other Texture of your choosing.
    
    Click for full image.
    
    When selecting a Texture to be used as a Splash image, it is best to set the Texture compression setting to **UserInterface2D** and also to enable the **Never Stream** option to make sure you will see the highest quality version of your Splash screen.
    
4.  Now connect the following three nodes to the VRPawn Event graph so that we can show and hide the Splash screen. When completed your setup should match the following image:
    
    -   Motion Controller (L)Trigger
    -   Show Loading Splash Screen
    -   Hide Loading Splash Screen
        
        Click for full image.
        
        While you can display Splash screen in this manner, you will want to add this functionality a level Blueprint so that when the level is loaded, the Splash screen will be displayed until the level is done with loading.
        
5.  After that has been completed and you VRPawn Blueprint looks like the following image, put on your HMD grab your Touch controllers and stand in the middle of your VR interaction area.
    
    Click for full image.
    

## End Result

Now when you squeeze the left trigger on the Touch, your scene should go black, and the Texture of the UE logo or the image you selected will be displayed. Releasing the left trigger on the Touch will bring you back the level back into view like in the following video.

## UE Project Downloads

Below you will find a link to where you can download the UE project that was used to create this example.

-   [**Oculus Rift Splash Screens Example Project**](https://epicgames.box.com/s/1rirqbohl7inchgnssznuam7ylalrzk4)