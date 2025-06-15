# Setting Up Your Android Device For Development

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/setting-up-your-android-device-for-developing-applications-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/setting-up-your-android-device-for-developing-applications-in-unreal-engine)  
**Processed:** 2025-06-14 16:50:04

---

In the following section you will go over all you need to know to set up your Android device so that it can be used to run your **Unreal Engine (UE)** project.

## 1\. Installing Android USB Drivers to Your Computer

1.  Connect your Android device to your development PC via USB.
    
2.  Your device driver software should automatically install. If not, visit [Android's OEM USB Drivers](http://developer.android.com/tools/extras/oem-usb.html) page to find more driver installation links and additional information.
    
3.  Disconnect your Android device from USB and then immediately plug it back in. After the device is recognized by the PC, the following message will appear on your Android device asking you if you want to allow this PC to talk to your device. A message box will ask what you want the USB connection to do. Tap the **checkmark box** that says **Always allow this computer** and then tap the **OK** button.
    

## 2\. Enabling Developer Mode on Your Android Device

1.  Open the **Settings** menu on your Android device.
    
2.  Scroll down and select **About Phone**. Depending on your Android device, you may have an **About Device**, **About Tablet**, or **About Shield** option instead.
    
    This may be in a **More** section on newer Android versions.
    
3.  Tap the **Build Number** 7 times to activate developer mode.
    
4.  Once developer mode has been activated, a success message will display on the screen similar to the one below.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9ee68472-1c96-4c25-90af-983fcf561444/dev_mode_active.png)

## 3\. Enabling USB Debugging

1.  Open the **Settings** menu on your Android device.
    
2.  Navigate back to the **Settings** menu and select **Developer Options** which should now available.
    
3.  In the **Developer Options** menu, enable **USB debugging** by tapping it.
    
4.  When prompted, tap the **OK** button.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7982b4d9-c4ec-43d9-bb36-356b92cc3833/enable_usb_debugging_warning.png)

## 4\. Verifying That Your Device is Connected

To verify that everything has been setup correctly and that your Android device is ready for Unreal Engine development, you can do the following:

1.  Open a **Windows Command Prompt** by pressing the **Windows + R** keys to open up the **Run** command dialogue box.
    
2.  Inside of the **Open** input, type **cmd** and the press the **OK** button to open the Windows Command Prompt.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/988bd047-820b-4384-8c01-920f484bb6f6/windows_run_command.png)
3.  Inside of the Windows Command Prompt, input **adb devices** and then press the **Enter** key to display all connected Android devices.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6bec89ce-335f-4eb3-83d1-502c362454df/adb_devices.png)

1.  Open the Terminal app from /Applications/Utilities.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/dee64809-7b2b-4e40-bdcb-850d68333944/mac_terminal_activate.png)
2.  Type **adb devices** in the command prompt and you should see all devices that are connected to your Mac.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8bcf00ba-8116-44c3-b72c-be372454fe96/mac_checking_adb_devices.png)

If you still do not see your device after you input the adb devices command you can try the following items:

-   If the device is listed but shows **Unauthorized** next to the name, that indicates that you did not accept your development PC's computer's RSA key fingerprint.
    
-   If your device does not show up despite it being plugged in and setup, input the following commands in the following order into the Windows Command Prompt to restart the **Android Debug Bridge** or (ADB) service:
    
    | Property Name | Description |
    | --- | --- |
    | **ADB kill - server** | This will stop the ADB service. |
    | **ADB start - server** | This will start the ADB service. |
    
-   In some cases, a correctly configured Android device might not show up if it is connected as a **Media Device (MTP)**. If this happens, try connecting as **Camera (PTP)** by selecting the Camera (PTP) option in your Use USB to options.
    

## End Result

Once you have completed the above sections, your Android device will be ready for deployment and debugging. For further reading, we recommend that you refer to the [Android Quick Start Guide](/documentation/en-us/unreal-engine/setting-up-unreal-engine-projects-for-android-development) to learn about configuring your project for Android in the UE.