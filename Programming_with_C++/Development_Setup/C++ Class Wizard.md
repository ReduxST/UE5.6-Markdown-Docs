# C++ Class Wizard

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/using-the-cplusplus-class-wizard-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/using-the-cplusplus-class-wizard-in-unreal-engine)  
**Processed:** 2025-06-14 17:01:22

---

Windows macOS Linux

The **C++ Class Wizard** provides a fast and easy way to add native C++ code classes into your project for you to extend with your own functionality, if you wish. This converts a content-only project into a code project. You can access the C++ Class Wizard and create a new C++ class by following these steps:

Check [Setting Up Visual Studio](/documentation/404) to ensure that you have a compatible version of Visual Studio installed before proceeding. For information about the correct version of Xcode, refer to the [Unreal Engine Release Notes](/documentation/en-us/unreal-engine/whats-new).

1.  In the main editor, select **Tools > New C++ Class...**
    
    ![Open a new CPP class from the menu bar.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1c62e718-7b3e-4413-9760-5213c323deef/new-cpp-class.png "New CPP Class")
2.  The **C++ Class Wizard** will appear and show **Common Classes** by default. If you do not see the class you are looking for, you can view the entire Class hierarchy listing by selecting **All Classes**.
    
    |   |   |
    | --- | --- |
    | 
     | 
    
     |
    | Common Classes | All Classes |
    
3.  Choose the Class you want to add. For the purposes of this demonstration, we will choose to create a new **Actor** Class. Select the **Actor** Class, then click **Next >**.
    
4.  You will then be prompted to enter a **Name** for your new Class. Do so, then click **Create Class**. This will create the header (`.h`) and source (`.cpp`) files.
    
    Class names can only contain alphanumeric characters and cannot contain spaces. The field will notify you if you enter an invalid name.
    
5.  In Unreal Engine, **Live Coding** is now enabled by default. A Live Coding window will appear and compile the new class files that were created.
    
6.  The code will immediately open in Visual Studio, ready for editing.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3d2592c6-86bd-4d12-a1a2-53ccebcb6593/code-in-vs.png)
    
    The code will immediately open in Xcode, ready for editing.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5a9191d8-09d2-4744-8552-884c7b5c0e4f/codeediting_xcode.png)