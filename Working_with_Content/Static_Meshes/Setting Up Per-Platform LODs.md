# Setting Up Per-Platform LODs

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/setting-up-per-platform-lods](https://dev.epicgames.com/documentation/en-us/unreal-engine/setting-up-per-platform-lods)  
**Processed:** 2025-06-14 16:49:45

---

While having multiple Level of Detail (LOD) Static Meshes can help lessen the rendering cost of distance objects, the extra memory required to store this information can be an issue on platforms that have limited resources like memory. In the following How-To we will take a look at restricting the number of LOD's a platform can use.

## Steps

In the following section we will take a look at specifying which LOD's should be used when your UE5 project is used on PC, Console, and Mobile platforms.

1.  First, inside the **Content Browser**, locate a **Static Mesh** that has a few LOD's to work with and open it up inside the **Static Mesh Editor**. For this example the Static Mesh that was selected has four LOD's however you can pick one that has more or less depending on the needs of your project.
    
    Click image for full size.
    
2.  Once the Static Mesh is open in the Static Mesh Editor, go to the **Details Panel** and expand the **LOD Settings** category.
    
    Click image for full size.
    
3.  Locate the **Minimum LOD** input and then click on the small white triangle next to it to expose the per-platform LOD options.
    
    Click image for full size.
    
4.  From the displayed list, select the platform that you want to override by clicking on the platform name. For this example we will be setting overrides for **Desktop**, **Mobile** and **Console**.
    
    Click image for full size.
    
5.  The Minimum LOD setting works by restricting which LOD level should be used first. Since our example Static Mesh has four LOD's this means that we can input numbers ranging from zero to four. Inputting zero will allow each LOD to be used while inputting four will allow only the last LOD to be used. For this example input a value of **zero** into Default, input a value of **one** into Desktop, input a value of **two** into Console, and finally input a value of **three** into Mobile.
    
    Click image for full size.
    
6.  Once that is completed, make sure to press the **Save** button to save your changes.
    
    Click image for full size.
    

## End Result

Once all platforms have had their respective LOD's set, the Static Mesh is now ready to be used in your UE5 project. To get a better understanding of how this works, check out the following image:

Click image for full size.

-   When this Static Mesh is viewed on a PC, it will only display three of the four LOD's because the **Minimum LOD** for **PC** was set to a value of **one**.
-   When this Static Mesh is viewed on a Console, it will only display two of the four LOD's because the **Minimum LOD** for **Console's** was set to a value of **two**. 
-   When this Static Mesh is viewed on Mobile, it will only display one of the four LOD's because the **Minimum LOD** for **Mobile** was set to a value of **three**.