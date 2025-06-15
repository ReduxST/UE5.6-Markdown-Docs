# Android Multi-View

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/android-multiview-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/android-multiview-in-unreal-engine)  
**Processed:** 2025-06-14 16:05:47

---

## Setup Android for Unreal Engine

To successfully package ASIS (Android Single Instance Service), you will need to setup Android SDK and NDK. Unreal Engine (UE) uses Android Studio and the Android SDK Command-Line Tools to download and install the Android SDK components required to develop Android projects. Follow the following documentation:

[

![Setting Up Android SDK and NDK](https://dev.epicgames.com/community/api/documentation/image/d922fae2-87c4-4cf2-99c8-081c7d6e0603?resizing_type=fit&width=640&height=640)

Setting Up Android SDK and NDK

Install Android Studio and automatically add SDK components.





](https://dev.epicgames.com/documentation/en-us/unreal-engine/set-up-android-sdk-ndk-and-android-studio-using-turnkey-for-unreal-engine)

If you are using Unreal Engine 5.5.x, enable the following SDK Platforms and Tools:

[![enable sdk platform and tools options](https://dev.epicgames.com/community/api/documentation/image/9805855f-ba87-49ff-ba55-bd381cd19dfd?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/9805855f-ba87-49ff-ba55-bd381cd19dfd?resizing_type=fit)

[![enable settings](https://dev.epicgames.com/community/api/documentation/image/9f64292b-a8e4-4cba-aadb-72c5757eb735?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/9f64292b-a8e4-4cba-aadb-72c5757eb735?resizing_type=fit)

[![enable settings](https://dev.epicgames.com/community/api/documentation/image/89255e19-fb59-4f04-ad24-7a5d2db0962a?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/89255e19-fb59-4f04-ad24-7a5d2db0962a?resizing_type=fit)

## Create project from template

With Android SDK/NDK installed, we can now setup the ASIS template plugin. The plugin is delivered as a separate archive, so manual steps need to be done to prepare UE source code.

## Get UE5.\* source code

Pull the latest source code from UE5 Main (Perforce or Github)

Perforce:

-   [Using Perforce as Source Control](https://dev.epicgames.com/documentation/en-us/unreal-engine/using-perforce-as-source-control-for-unreal-engine) Documentation
    
-     [How to Use Unreal Engine 5 + UE5 Source Control](https://www.perforce.com/blog/vcs/how-use-unreal-engine-5-perforce) Blog Post  
    

Github:

-   [Accessing Unreal Engine source code on GitHub](https://www.unrealengine.com/en-US/ue-on-github)
    

## Setup ASIS Plugin

### If using Perforce:

1.  Navigate to ASIS plugin folder: `UE5_Main\Engine\Restricted\NotForLicensees\Plugins\AndroidSingleInstanceService`
    
2.  Inside the `AndroidSingleInstanceService` folder, open the `Templates` folder: `UE5_Main/Engine\Restricted\NotForLicensees\Plugins\AndroidSingleInstanceService\Templates\`
    

### If using Github:

Unzip Archive provided by Epic and copy ASIS plugin contents to: `Engine\Restricted\NotForLicensees\Plugins\AndroidSingleInstanceService`

### Copy the Template

[![](https://dev.epicgames.com/community/api/documentation/image/85c2cb75-3dba-4c79-a847-58799c7c4a03?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/85c2cb75-3dba-4c79-a847-58799c7c4a03?resizing_type=fit)

Copy the **TP\_HMI\_ASIS** folder to the **UE5/Templates/**

[![](https://dev.epicgames.com/community/api/documentation/image/33141529-1936-446a-9bae-5f257853a220?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/33141529-1936-446a-9bae-5f257853a220?resizing_type=fit)

Next copy the following code to the **UE5\_Main/Templates/TemplateCategories.ini**

C++

`Categories=(Key="HMI", LocalizedDisplayNames=((Language="en",Text="Automotive\nHMI &\nVehicle Cockpit using Android Single Instance Service")), LocalizedDescriptions=((Language="en",Text="Find templates for automotive vehicle cockpit using Android Single Instance Service"), Icon="TP_HMI_ASIS/Media/AutomotiveHMI_2x.png", IsMajorCategory=true)`

Categories=(Key="HMI", LocalizedDisplayNames=((Language="en",Text="Automotive\\nHMI &\\nVehicle Cockpit using Android Single Instance Service")), LocalizedDescriptions=((Language="en",Text="Find templates for automotive vehicle cockpit using Android Single Instance Service"), Icon="TP\_HMI\_ASIS/Media/AutomotiveHMI\_2x.png", IsMajorCategory=true)

Copy full snippet(1 line long)

Run UnrealEditor. Now we should see the new HMI template when we open the Unreal Engine Project browser:

## Create Project from HMI template

[![](https://dev.epicgames.com/community/api/documentation/image/45d035b1-0bb8-4ad8-8970-80eacd081b06?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/45d035b1-0bb8-4ad8-8970-80eacd081b06?resizing_type=fit)

The project should look like this:

[![](https://dev.epicgames.com/community/api/documentation/image/77aa0022-0fc4-4861-8b0c-e8f186cf95da?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/77aa0022-0fc4-4861-8b0c-e8f186cf95da?resizing_type=fit)

[![](https://dev.epicgames.com/community/api/documentation/image/8b6f475b-f16a-49eb-8e23-4eb32d9ad702?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/8b6f475b-f16a-49eb-8e23-4eb32d9ad702?resizing_type=fit)

## Add ASIS plugin to existing Project

If you have an existing project you need to add ASIS to, do the following:

1.  Enable ASIS in the Plugin Settings
    
    [![](https://dev.epicgames.com/community/api/documentation/image/99693f46-b81a-4ab0-813d-36b3777f9ca7?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/99693f46-b81a-4ab0-813d-36b3777f9ca7?resizing_type=fit)
    
2.  Add remap plugin directory. Add next code to the {ProjectName}/Config/DefaultGame.ini
    
    C++
    
    `[Staging] +RemapDirectories=(From="Engine/Restricted/NotForLicensees/Plugins/AndroidSingleInstanceService", To="Engine/Plugins/Runtime/AndroidSingleInstanceService") +RemapDirectories=(From="Engine/Restricted/NotForLicensees/Plugins/Experimental/MultiWindow", To="Engine/Plugins/Experimental/MultiWindow")`
    
    \[Staging\] +RemapDirectories=(From=&quot;Engine/Restricted/NotForLicensees/Plugins/AndroidSingleInstanceService&quot;, To=&quot;Engine/Plugins/Runtime/AndroidSingleInstanceService&quot;) +RemapDirectories=(From=&quot;Engine/Restricted/NotForLicensees/Plugins/Experimental/MultiWindow&quot;, To=&quot;Engine/Plugins/Experimental/MultiWindow&quot;)
    
    Copy full snippet(3 lines long)
    
3.  Open your project and enable the following ASIS plugin settings
    
    [![](https://dev.epicgames.com/community/api/documentation/image/d001013c-be71-4824-870d-a2a0cc2a87ce?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/d001013c-be71-4824-870d-a2a0cc2a87ce?resizing_type=fit)
    

### Package and run ASIS example

With Android SDK/NDK and the Template setup in Unreal engine, we can now package the project as Android application:

[![](https://dev.epicgames.com/community/api/documentation/image/ddd64b53-18d4-45d5-810d-65914f2bbf95?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/ddd64b53-18d4-45d5-810d-65914f2bbf95?resizing_type=fit)

[![](https://dev.epicgames.com/community/api/documentation/image/eac5dcfd-e7ed-4069-a5e9-fcb501e678e0?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/eac5dcfd-e7ed-4069-a5e9-fcb501e678e0?resizing_type=fit)

## App Communication

With the app packaged from Unreal Engine, we will use an example client app to communicate with the Unreal Engine APK

The Unreal Engine Package will have 3 artifacts.

1.  APK with Android Service. It is located in the folder that was chosen while project package dialog.
    
2.  ASIS helper libraries that are used in the client applications.
    
    C++
    
    `Binaries/Android/aars ├── asisclientlib-1.0.1-debug.aar ├── asisclientlib-1.0.1-debug.jar ├── asiscommon-1.0.1-debug.aar`
    
    Binaries/Android/aars ├── asisclientlib-1.0.1-debug.aar ├── asisclientlib-1.0.1-debug.jar ├── asiscommon-1.0.1-debug.aar
    
    Copy full snippet(4 lines long)
    
3.  Example of client application that communicates with Service. This is NOT located in the packaged unreal project instead in the Binaries folder of your Unreal Engine Project. The location is **\\Unreal Projects\\\*Project\_Name\*\\Binaries\\Android** 
    
    [![](https://dev.epicgames.com/community/api/documentation/image/7240fbaf-c22c-44f7-ad57-40208f75d637?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/7240fbaf-c22c-44f7-ad57-40208f75d637?resizing_type=fit)
    

You can use Android Studio to open the Android project. It will automatically go through the android build process once you open it. 

[![](https://dev.epicgames.com/community/api/documentation/image/31cd8da6-d2e9-4269-bcf3-4c727fcc8aad?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/31cd8da6-d2e9-4269-bcf3-4c727fcc8aad?resizing_type=fit)

Or you could use command line.

cmd could be using to generate client apk

C++

`cd {Project_Name}\Binaries\Android\ExampleUseCase_{Project_Name}\ gradlew assembleDebug`

cd {Project\_Name}\\Binaries\\Android\\ExampleUseCase\_{Project\_Name}\\ gradlew assembleDebug

Copy full snippet(2 lines long)

The apk will be generated in:  `{Project_Name}\Binaries\Android\ExampleUseCase_{Project_Name}\app\build\outputs\apk\debug\app-debug.apk`

Back in Android Studio and with an Android device selected, you can run the app with **Shift**+**F10** or select the green Play button at the top menu

[![](https://dev.epicgames.com/community/api/documentation/image/581b9bdf-37fe-42bb-8354-852dbd018e8d?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/581b9bdf-37fe-42bb-8354-852dbd018e8d?resizing_type=fit)

### After installation Service

Now run install the Unreal Engine apk run applications to your device. You can use cmd line in the Unreal Engine package folder and run adb 

[![](https://dev.epicgames.com/community/api/documentation/image/e034fd74-9ccd-4a48-96f8-c3a2d9649a92?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/e034fd74-9ccd-4a48-96f8-c3a2d9649a92?resizing_type=fit)

In the Android Add, select Activate View1, View2, and View3 to view the Android Service communicating with the Unreal Engine application

[![](https://dev.epicgames.com/community/api/documentation/image/fe432053-8cb5-4828-b635-c1f3ffe2c359?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/fe432053-8cb5-4828-b635-c1f3ffe2c359?resizing_type=fit)

### Enable Multiview

Multiview works from version UE 5.6. Enabling Multiview requires AndroidSingleInstanceService Plugin. Go through the previous steps to enable ASIS then you can start here.

**Enable** the **Multiview** plugin in the plugin settings.

[![](https://dev.epicgames.com/community/api/documentation/image/444a150e-abd1-4ce1-8426-e9501fa28694?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/444a150e-abd1-4ce1-8426-e9501fa28694?resizing_type=fit)

Create two cameras in the level to test Multiview. The TP\_HMI\_Automotive will be used for this example.

[![](https://dev.epicgames.com/community/api/documentation/image/7e887ae0-9c00-441b-b129-2428df19b052?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/7e887ae0-9c00-441b-b129-2428df19b052?resizing_type=fit)

Next, open the Level Blueprint. Add the Camera Actors to the Blueprints. Drag off the Camera Actor node and Select ‘Get Camera View’. Then Delete the Get Camera Node, we just need the Camera Component Object Reference. 

[![](https://dev.epicgames.com/community/api/documentation/image/12b3b9de-3214-4566-8cf8-2bfb3feaa776?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/12b3b9de-3214-4566-8cf8-2bfb3feaa776?resizing_type=fit)

Then create `Register Camera for Asis`. Connect the camera object node to the respective nodes. Make sure to set the Camera Id to 1 and 2 for each camera. Connect the execution pins to **Event Begin Play.**

[![](https://dev.epicgames.com/community/api/documentation/image/3cae9dd3-d488-4f69-b453-ca6336e7d04f?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/3cae9dd3-d488-4f69-b453-ca6336e7d04f?resizing_type=fit)

Package the project for Android.

[![](https://dev.epicgames.com/community/api/documentation/image/c2e4eb63-0190-4318-92cf-2d2284f5e05b?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/c2e4eb63-0190-4318-92cf-2d2284f5e05b?resizing_type=fit)

Now we will open the client app in Android Studio. Open the example client Android application project. This is NOT located in the packaged unreal project instead in the Binaries folder of your Unreal Engine Project. The location for the course code for client app is:  `{Project_Name}\Binaries\Android\ExampleUseCase_{Project_Name}\`

Next, switch from standard ASIS to MultiviewEdit.

Edit `Binaries\Android\ExampleUseCase_{Project_Name}\app\src\main\AndroidManifest.xml`  Change game activity to **ActivityForMultiView** line 22.

[![](https://dev.epicgames.com/community/api/documentation/image/14a05b02-87ad-46bf-bb69-618c3e696578?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/14a05b02-87ad-46bf-bb69-618c3e696578?resizing_type=fit)

In Android Studio and with an Android device connected, you can run the app with Shift+F10 or select the green Play button at the top menu.

After installation Service 

Now run install the Unreal Engine apk run applications to your device. You can use cmd line in the Unreal Engine package folder and run adb.

[![](https://dev.epicgames.com/community/api/documentation/image/d51c04b4-365b-4159-8680-62d7fcbfdbd9?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/d51c04b4-365b-4159-8680-62d7fcbfdbd9?resizing_type=fit)

Select the Attach/Detach View1 and Attach/Detach View1 to view the cameras. You now have ASIS with multiview working on Android.

### Architecture Overview

[![](https://dev.epicgames.com/community/api/documentation/image/5ca825f0-bd5a-4a65-b759-6c9381d1980c?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/5ca825f0-bd5a-4a65-b759-6c9381d1980c?resizing_type=fit)

 Supported approaches

[![](https://dev.epicgames.com/community/api/documentation/image/acecd88e-51e1-4d43-88df-044a4bf147a1?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/acecd88e-51e1-4d43-88df-044a4bf147a1?resizing_type=fit)

[![](https://dev.epicgames.com/community/api/documentation/image/bafc7a28-0edd-4c83-8511-ca779bb7a26c?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/bafc7a28-0edd-4c83-8511-ca779bb7a26c?resizing_type=fit)

[![](https://dev.epicgames.com/community/api/documentation/image/8c607cab-d6a1-4512-9853-7825f9f539f1?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/8c607cab-d6a1-4512-9853-7825f9f539f1?resizing_type=fit)

### Interface Description

Class `ASISConnection`

This class allows establishing a connection and communicating with an ASIS service. It encapsulates the complexities of this communication and provides an easy to use interface for sending and receiving data and commands.

`ASISConnection.ASISConnectionCallBacks` interface defines callbacks for ASISConnection events. Implement this interface when you want to handle connection success events.

Java

`public interface ASISConnectionCallBacks { void onConnectionSuccess(); void onServiceDisconnected(); }`

public interface ASISConnectionCallBacks { void onConnectionSuccess(); void onServiceDisconnected(); }

Copy full snippet(5 lines long)

`onConnectionSuccess()` - is called when connection to the service was successfully established.

`onServiceDisconnected()` \-  is  called when a connection to the Service has been lost

`ASISConnection.EngineMessagesListener` interface defines a listener for engine messages.  Implement this interface when you want to handle messages from the engine.

Java

`public interface EngineMessagesListener { void onEngineMessage(Message message); }`

public interface EngineMessagesListener { void onEngineMessage(Message message); }

Copy full snippet(4 lines long)

`onEngineMessage(Message message)` - called when a message is received from the engine.

`Message` - values of the incoming message

Class `ASISConnection.ConnectionBuilder` 

This class implements the builder design pattern to create instances of `ASISConnection`. It follows a fluent style where methods can be chained, allowing for more readability when multiple parameters are required.

Java

`ConnectionBuilder(Context ctx)`

ConnectionBuilder(Context ctx)

Copy full snippet(1 line long)

Initializes a new instance of the \`ConnectionBuilder\` class using the given Context. 

Parameters

-   `ctx` - The Context in which to create the ConnectionBuilder.
    

Java

`public ConnectionBuilder withConnectionListener(ASISConnectionCallBacks connectionListener)`

public ConnectionBuilder withConnectionListener(ASISConnectionCallBacks connectionListener)

Copy full snippet(1 line long)

Sets the ASISConnectionCallBacks listener for the ASISConnection.

Parameters

-   `connectionListener` - The ASISConnectionCallBacks listener to set.
    

Returns

-   The ConnectionBuilder instance, allowing for method chaining.
    

Java

`public ConnectionBuilder withEngineMessageListener(EngineMessagesListener engineMessageListener)`

public ConnectionBuilder withEngineMessageListener(EngineMessagesListener engineMessageListener)

Copy full snippet(1 line long)

Sets the EngineMessagesListener for the ASISConnection.

Parameters

-   `engineMessageListener` - The EngineMessagesListener listener to set.
    

Returns

-   The ConnectionBuilder instance, allowing for method chaining.
    

Java

`public ConnectionBuilder withConnectionId(String connectionID)`

public ConnectionBuilder withConnectionId(String connectionID)

Copy full snippet(1 line long)

Sets the connectionID for the ASISConnection.

Parameters

-   `connectionID` - string with connectioID
    

Returns

-   The ConnectionBuilder instance, allowing for method chaining.
    

Java

`public ConnectionBuilder withServicePackageName(String packageName)`

public ConnectionBuilder withServicePackageName(String packageName)

Copy full snippet(1 line long)

Override default service package name

Parameters

-   `packageName` - service package name (com.epicgames.PROJECTNAME)
    

Returns

-   The ConnectionBuilder instance, allowing for method chaining.
    

Java

`public ConnectionBuilder withServiceClassName(String className)`

public ConnectionBuilder withServiceClassName(String className)

Copy full snippet(1 line long)

Override default service class name

Parameters

1.  `className` - service class name (com.epicgames.makeaar.UnrealSharedInstanceService)
    

Returns

-   The ConnectionBuilder instance, allowing for method chaining.
    

Java

`public ConnectionBuilder withObbModuleName(String obbModuleName)`

public ConnectionBuilder withObbModuleName(String obbModuleName)

Copy full snippet(1 line long)

Override default obbModuleName

Parameters

-   obbModuleName - content obb name (UE project name)
    

Returns

-   The ConnectionBuilder instance, allowing for method chaining.
    

C++

`public ConnectionBuilder withInsightsTracing()`

public ConnectionBuilder withInsightsTracing()

Copy full snippet(1 line long)

Enable InsightsTracing

Returns

-   The ConnectionBuilder instance, allowing for method chaining.
    

Java

`public ConnectionBuilder withCommandLineArgs(String cmdArgs)`

public ConnectionBuilder withCommandLineArgs(String cmdArgs)

Copy full snippet(1 line long)

Override default command line args

Parameters

1.  cmdArgs - command line arguments to start UE
    

Returns

-   The ConnectionBuilder instance, allowing for method chaining.
    

Java

`public ConnectionBuilder withOverridePropagateAlpha(boolean value)`

public ConnectionBuilder withOverridePropagateAlpha(boolean value)

Copy full snippet(1 line long)

Override default mobile propagate alpha value

Parameters

-   `value` - override mobile propagate alpha value
    

Returns

-   The ConnectionBuilder instance, allowing for method chaining.
    

Java

`public ASISConnection build()`

public ASISConnection build()

Copy full snippet(1 line long)

Builds an ASISConnection instance using the parameters that have been set.

Returns

-   A new ASISConnection instance.
    

Example:

Java

```code
`public class UseServiceActivity extends Activity      implements ASISConnection.ASISConnectionCallBacks,    ASISConnection.EngineMessagesListener .... ASISConnection mServiceConnection ; ...  mServiceConnection = new ASISConnection.ConnectionBuilder(this)					.withServicePackageName("com.epicgames.UE_PROJECT") 		.withObbModuleName("UE_PROJECT") 		.withConnectionListener(this)`

```

Expand codeCopy full snippet(14 lines long)

Java

`ASISConnection(ConnectionBuilder builder)`

ASISConnection(ConnectionBuilder builder)

Copy full snippet(1 line long)

Constructor that takes a `ConnectionBuilder` as an argument.ConnectionBuilder

This constructor is typically used through the `ConnectionBuilder`'s `build()` method.

Java

`public boolean bindToUnrealInstanceService()`

public boolean bindToUnrealInstanceService()

Copy full snippet(1 line long)

Binds  to an unreal android single instance service by the given caller.

Returns

-   `true` if binding was successful, false otherwise.
    

Java

`public void unbindToUnrealInstanceService()`

public void unbindToUnrealInstanceService()

Copy full snippet(1 line long)

Unbinds from the Unreal instance service.

Java

`public boolean isBoundToService()`

public boolean isBoundToService()

Copy full snippet(1 line long)

Checks whether the application is currently bound to the service.

Returns

-   This method returns true if the application is bound to the service.
    

Java

`public int attachSurfaceToService(int displayIndex, Surface externalSurface)`

public int attachSurfaceToService(int displayIndex, Surface externalSurface)

Copy full snippet(1 line long)

Attach an external surface to the service for rendering.

Parameters:

-   displayIndex:  the index of the display, 0 for single display.
    
-   externalSurface: the Surface to attach.
    

Returns:

-   the ID of the attached Surface.
    

Java

`public boolean detachSurfaceFromService(int attachId, Handler.Callback callback)`

public boolean detachSurfaceFromService(int attachId, Handler.Callback callback)

Copy full snippet(1 line long)

Detaches a Surface from the service by attaching ID.

Parameters:

-   attachId: the ID of the attachment to detach the Surface.
    
-   callback: a callback that will be called when detachment is complete.
    

Returns

-    true if detachment was initiated successfully, false otherwise.
    

Java

`public boolean sendData(String key, Object value)`

public boolean sendData(String key, Object value)

Copy full snippet(1 line long)

This method allows you to send key-value data to the ASIS Service.

Parameters

-   key: A String that represents the key for the data being sent.
    
-   value: The piece of data to be sent.
    

Returns

-   This method returns a boolean that indicates whether the data was sent successfully.
    

Java

`public boolean consoleCommand(String consoleCommand)`

public boolean consoleCommand(String consoleCommand)

Copy full snippet(1 line long)

Sends a console command to the connected service.

Parameters

-   consoleCommand: A String with a console command.
    

Returns

-   Returns true if the message was sent successfully.
    

Java

`public boolean sendTouchEvent(MotionEvent event, int attachId)`

public boolean sendTouchEvent(MotionEvent event, int attachId)

Copy full snippet(1 line long)

Forward touch event to the service from attached surfaces.

Parameters

-   event: Android MotionEvent representing the touch event.
    
-   attachId the ID associated with the surface.
    

Returns

-   Returns true if the touch event was sent successfully, false otherwise.
    

### Android application integration

Import ASIS java libraries to your project. 

-   Copy generated libraries from {Project\_Name}\\Binaries\\Android\\aars to your app space (e.g libs)
    

C++

`{Android_app}/libs ├── asisclientlib-1.0.1-debug.aar ├── asisclientlib-1.0.1-debug.jar ├── asiscommon-1.0.1-debug.aar └── asiscommon-1.0.1-debug.jar`

{Android\_app}/libs ├── asisclientlib-1.0.1-debug.aar ├── asisclientlib-1.0.1-debug.jar ├── asiscommon-1.0.1-debug.aar └── asiscommon-1.0.1-debug.jar

Copy full snippet(5 lines long)

-   Add import to the lig via build.gradle
    

Java

```code
`android {  	... 	repositories { 		flatDir { dirs 'libs' } 	} ... }  def asiscommonVersion = "1.0.1" def asisclientlibVersion = "1.0.1"`

```

Expand codeCopy full snippet(16 lines long)

The application activity lifecycle sequence diagram:

[![](https://dev.epicgames.com/community/api/documentation/image/8e2833c9-558d-46cf-8d14-d1dc1e11bd55?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/8e2833c9-558d-46cf-8d14-d1dc1e11bd55?resizing_type=fit)