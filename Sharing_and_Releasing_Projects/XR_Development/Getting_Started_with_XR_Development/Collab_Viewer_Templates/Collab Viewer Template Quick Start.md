# Collab Viewer Template Quick Start

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/collab-viewer-template-quick-start-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/collab-viewer-template-quick-start-in-unreal-engine)  
**Processed:** 2025-06-14 16:13:51

---

This page contains detailed, step-by-step instructions for getting started with the Collab Viewer Template on your local network with its default content. By the end of this page, you'll know how to start up the runtime experience the Collab Viewer Template provides for you, what your options are for interacting and moving around the scene, and how to get multiple other people on your network to join the same shared experience with you.

The workflow here uses the AEC Collab Viewer template as an example, but the workflows function equally well for the OEM/Manufacturing template.

-   [1 - Packaging and Distributing](/documentation/en-us/unreal-engine/collab-viewer-template-quick-start-in-unreal-engine#1-packaginganddistributing)
-   [2 - One Person Starts a Server](/documentation/en-us/unreal-engine/collab-viewer-template-quick-start-in-unreal-engine#2-onepersonstartsaserver)
-   [3 - Other People Join](/documentation/en-us/unreal-engine/collab-viewer-template-quick-start-in-unreal-engine#3-otherpeoplejoin)
-   [4 - On Your Own](/documentation/en-us/unreal-engine/collab-viewer-template-quick-start-in-unreal-engine#4-onyourown)

## 1 - Packaging and Distributing

To take advantage of all the features of the Collab Viewer Template, you'll first need to package your Project to an *.exe* file. When you want multiple people to connect to a single session, each person needs to run the application from a copy of that packaged *.exe* file. Therefore, one person on the team needs to package the Project from the Unreal Editor, then distribute that *.exe* file to everyone else who you need to join the same session.

To package and share your Project:

1.  Create a new Project from the Collab Viewer Template, if you haven't already, and open it in the Unreal Editor.
2.  Select a template category.
    
    Click for full image.
    
3.  Select the **Collab Viewer** template.
4.  Select **Create Project**.
5.  From the main toolbar, choose **Platforms Menue > Windows > Package Project.**
    
    Click for full image.
    
6.  Browse to the folder on your computer where you want the Unreal Editor to place the packaged version of your Project, and click **Select Folder**.  
    ![Select a folder](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/80e747c9-7cd2-4019-a20b-00d5a4947f54/03-select-folder_ue5.png "Select a folder")
    
    The Unreal Editor begins the packaging process.
    
    ![Packaging progress](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/44bd3999-2e07-4ed0-b6ec-dc2a099cb178/04-packaging-project-message_ue5.png "Packaging progress")
7.  When the packaging process is finished, go to the folder that you selected in step 3 above. You'll find a folder called **WindowsNoEditor** with contents similar to the following:  
    ![Package contents](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cf87ea35-1f84-4293-b74d-20e9d94a7478/05-package-project-folder_ue5.png "Package contents")  
    Each person who wants to join the same session in the Collab Viewer will need to have all of the files in this folder on their local computer. It's up to you how best to achieve this for your organization.  
    For example, you could zip up the files in this folder and place the archives in a shared location on your local network. Other users could then copy them to their computer and extract them.

For more information about packaging, and how you can configure the process, see also [Packaging Projects](/documentation/404).

You **must** follow this packaging and distribution process each time you change the content in your Project. The 3D models in your Level are not replicated automatically between networked users; they are compiled into the packaged application. In order for everyone in a session to see the latest content, everyone needs to be using the same version of the packaged application.

## 2 - One Person Starts a Server

In this step, you'll start up a server—a special instance of the Collab Viewer application that other people can connect to.

1.  Double-click the *.exe* file for your packaged application.  
    In the example below, the Project is named **CollabProject**, so its packaged application is named *CollabProject.exe*.  
    ![Packaged executable](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/586fced1-4a98-4af7-a26b-8f9e4629faa5/06-package-template_ue5.png "Packaged executable")
2.  In the welcome screen, set a display name for yourself. This name appears above the head of your avatar, so that other people in the same session can identify you. 
    
    Click for full image.
    
    Click the arrow to go to the next step.
    
3.  Leave the next setting at its default value of **Host a session**.
    
    Click for full image.
    
    Click the arrow to complete the server setup.
    
    If you only want to use the Collab Viewer Template to make a single-person experience without the ability for other users in your network to join in, you could instead choose the **Single Session** option here. It gives you exactly the same runtime experience as starting as a host, except that your application doesn't become visible to other people in your network.
    

You'll start in the main sample Level.

Click for full image.

Use the [desktop controls](/documentation/en-us/unreal-engine/interacting-with-the-collab-viewer-in-unreal-engine#desktopcontrols) or [VR controls](/documentation/en-us/unreal-engine/interacting-with-the-collab-viewer-in-unreal-engine#vrcontrols) to move around the scene and interact.

-   You can press the **Spacebar** key (or either thumbstick button in VR) to open an Interaction Menu that lets you make selected objects transparent (**Xray**), teleport to preset **Bookmark** locations, move objects around in 3D space, scale your viewpoint, cut and remove a section of the geometry, or load new Datasmith assets during runtime.
    
    Click for full image.
    
-   You can also use the menu at the top right to switch between different movement modes—fly, walk, orbit—and, if you have a compatible VR headset set up, to switch into VR.
    
    ![Toolbar](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9e28db15-a80f-4f90-ba48-d711504b6f56/11-menu-toolbar_ue5.png "Toolbar")

To learn more, see:

-   [Interacting with the Collab Viewer](/documentation/en-us/unreal-engine/interacting-with-the-collab-viewer-in-unreal-engine)
-   [Measuring in the Collab Viewer](/documentation/en-us/unreal-engine/measuring-in-the-collab-viewer-in-unreal-engine)
-   [Annotating in the Collab Viewer](/documentation/en-us/unreal-engine/annotating-in-the-collab-viewer-in-unreal-engine)
-   [Saving and Loading a Session](/documentation/en-us/unreal-engine/saving-and-loading-a-session-in-unreal-engine)

While you're working, your computer becomes visible as a server to other computers in your network. As other people join your session, you'll see their avatars appear.

## 3 - Other People Join

In this step, each person who joins the session launches a separate instance of the packaged application on a different computer, and they all connect to the same server.

Each individual should follow these instructions to join the session:

1.  Double-click the *.exe* file for your packaged application. For example, in this case, the Project is named **CollabProject**, so its packaged application is named *CollabProject.exe*.  
    ![Packaged executable](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1eed2339-eaf2-41d7-881a-e4649c365915/12-select-collab-template_ue5.png "Packaged executable")
2.  In the welcome screen, set a display name for yourself. This name appears above the head of your avatar, so that other people in the same session can identify you.
    
    Click for full image.
    
    Click the arrow to go to the next step.
    
3.  Change the next setting to **Join a session**.
    
    Click for full image.
    
    Click the arrow to go to the next step.
    
4.  The application scans the network, and lists all available servers.
    
    Click for full image.
    
    -   If you see the server you want in the list, click its name to join the session. 
        
        ![Click the server name](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/806a5b7d-a150-4d78-a132-70f7c1dbe621/16-server-list_ue5.png "Click the server name")
    -   If you don't see the server you want, try the **Refresh** button to re-scan the network for servers.
        
        ![Refresh the list of servers](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/54bd7e9e-6c63-44c6-b901-a3ef3bbfef1b/16-1-refresh-button_ue5.png "Refresh the list of servers")
    -   If the application can't detect the server, but you know its IP address, activate the **Manually specify an IP Address** switch.
        
        ![Switch to manual IP mode](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b87f2d04-83f7-4135-ab94-09f8568d5274/17-specify-ip-address_ue5.png "Switch to manual IP mode")
        
        Enter the IP address in the field provided, and click **Join**.
        
        Click for full image.
        

You'll start in the main Level. You'll be able to see an avatar for the person running the server, and one for each other person who joins the session:

Click for full image.

The avatars are slightly different for each user:

-   Each avatar is accompanied by the display name its user entered in the welcome menu.
    
-   Each avatar is assigned a random color.
    
-   Users in the Walk and VR modes have an avatar that resembles a human shape as on the right in the image above. Users in other navigation modes are represented by a camera as on the left in the image above.
    
-   All avatars move and rotate around the scene as their corresponding user moves and looks around, so that you can see where other users are focusing their attention.
    

Use the [desktop controls](/documentation/en-us/unreal-engine/interacting-with-the-collab-viewer-in-unreal-engine#desktopcontrols) or [VR controls](/documentation/en-us/unreal-engine/interacting-with-the-collab-viewer-in-unreal-engine#vrcontrols) to move around the scene and interact.

## 4 - On Your Own

Now that you understand how to run the Collab Viewer Template and connect with others, you're ready to get started using the same runtime experience to review your own content. Continue on with the instructions in the [Adding Your Own Content to the Collab Viewer Template](/documentation/en-us/unreal-engine/adding-your-own-content-to-the-collab-viewer-in-unreal-engine) guide for instructions on getting your own content added to the Project and set up to work in the same runtime experience.