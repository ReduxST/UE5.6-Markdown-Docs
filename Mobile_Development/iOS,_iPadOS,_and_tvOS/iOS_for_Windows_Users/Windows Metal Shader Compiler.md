# Windows Metal Shader Compiler

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/using-the-windows-metal-shader-compiler-for-ios-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/using-the-windows-metal-shader-compiler-for-ios-in-unreal-engine)  
**Processed:** 2025-06-14 17:02:18

---

The Windows Metal shader compiler currently does not work in UE 5.1 through UE 5.4.

**Unreal Engine** can compile shaders for Apple's **Metal** API on a Windows machine, greatly simplifying the workflow for iOS applications. To enable this functionality, you need to install Apple's **Metal Developer Tools for Windows**. Unreal Engine will automatically use this toolset once it is set up.

## Steps

To install Metal Developer Tools for Windows, follow these steps:

1.  Sign in to your **Apple Developer Account** in your web browser, then navigate to the **Downloads** section.
    
2.  In the tabs on the upper-right of the Downloads page, click the **Release** tab.
    
    ![The Beta Downloads page](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7b226c83-e60d-4e3b-a2e2-b599441bad92/betadownloads.png)
3.  In the Software Downloads page, click the **Applications** button.
    
    ![The Applications button](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b6d8b09d-879c-48b5-89f5-f625d74c034d/applications.png)
4.  Scroll down the page until you find the entry for **Metal Developer Tools for Windows**, then click the **Download** button to download the installer.
    
    The download entry for the Metal Developer Tools for Windows. Click to enlarge image.
    
5.  Run the installer to install the Metal Developer Tools.
    

## Final Result

Once you have completed setup for the Metal Developer Tools for Windows, your Windows installation of Unreal Engine will be able to compile shaders for Metal 2.0. No additional setup is required.