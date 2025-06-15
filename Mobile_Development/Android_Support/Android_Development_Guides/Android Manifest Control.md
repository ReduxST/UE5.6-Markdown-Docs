# Android Manifest Control

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/how-to-use-android-manifest-control-in-unreal-engine-projects](https://dev.epicgames.com/documentation/en-us/unreal-engine/how-to-use-android-manifest-control-in-unreal-engine-projects)  
**Processed:** 2025-06-14 16:29:26

---

The `AndroidManifest.xml` file is used to store various Android system permissions and settings that are set in the **Advanced APK Packaging** section of your **Projects Settings**. The following document shows how you can input commands that will be added to the `AndroidManifest.xml` file to meet the needs of your **Unreal Engine** (UE) project.

## Android Manifest Location

Before you can locate the `AndroidManifest.xml` file for your project, you will first need to either package the project or deploy the project to your Android device. Once the project has been built or deployed you will then find the `AndroidManifest.xml` file in `(YourProjectName)\\Intermediate\Android\arm64`.

Click for full image.

You should **never** edit the `AndroidManifest.xml` file under any circumstances. Any edits that need to be made to the `AndroidManifest.xml` file should be done inside the UE Editor in the Advanced APK Packing section.

## Android Manifest Layout

In a typical `AndroidManifest.xml` file you will find the following three sections.

-   **Application Definition**
-   **Activity**
-   **Requirements**
    
    ```
              `<manifest xmlns:android="http://schemas.android.com/apk/res/android"               package="com.YourCompany.Project"               android:versionCode="1"               android:versionName="1.0."> 		               <-- Application Definition -->               <application android:label="@string/app_name" android:icon="@drawable/icon" android:hasCode="true">                <activity android:name="com.epicgames.unreal.GameApplication"                </activity>               </application> 		                <-- Requirements -->                <uses-sdk android:minSdkVersions="9"/>                <uses-feature android android:glEsVersion="0x00020000" android:required="true" />                <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>           </manifest>`
    		
    Copy full snippet
    ```
    <manifest xmlns:android="http://schemas.android.com/apk/res/android" package="com.YourCompany.Project" android:versionCode="1" android:versionName="1.0."> <-- Application Definition --> <application android:label="@string/app\_name" android:icon="@drawable/icon" android:hasCode="true"> <activity android:name="com.epicgames.unreal.GameApplication" </activity> </application> <-- Requirements --> <uses-sdk android:minSdkVersions="9"/> <uses-feature android android:glEsVersion="0x00020000" android:required="true" /> <uses-permission android:name="android.permission.WRITE\_EXTERNAL\_STORAGE"/> </manifest>

Please note that the above Android Manifest file is not a working manifest file and is only shown for reference purposes.

## Extra Tags for Manifest

Navigate to **Extra Tags for <manifest> node** in the **Advanced APK Packaging** section. You can add additional tags for the Manifest by clicking on the **Plus** sign icon to add a new element to the tags array and then inputting the tag or tags you want to use into the input box. For this example the following tag was used, **android:sharedUserId="Foo"**.

Click for full image.

Tags that are input into the **Extra Tags for <manifest> node** section will be added to the **manifest** section of the `AndroidManifest.xml` file.

```
	`<manifest xmlns:android="http://schemas.android.com/apk/res/android" 		package="com.YourCompany.Project" 		android:sharedUserId="Foo" 		android:versionCode="1" 		android:versionName="1.0">`
Copy full snippet
```
<manifest xmlns:android="http://schemas.android.com/apk/res/android" package="com.YourCompany.Project" android:sharedUserId="Foo" android:versionCode="1" android:versionName="1.0">

## Extra Tags for Application

Navigate to **Extra Tags for <application> node** in the **Advanced APK Packaging** section. You can add additional tags for the Application by clicking on the **Plus** sign icon to add a new element to the Application array and then inputting the tag you want to use. For this example the following tag was used, **android:hardwareAccelerated="True"**.

Click for full image.

Items that are input into the **Extra Tags for <application> node** section will be added to the **Application Definition** section of the `AndroidManifest.xml` file.

```
	
	`<application android:label="@string/app_name" 	 android:icon="@drawable/icon" 	 android:hardwareAccelerated="True" 	 android:hasCode="true">`
Copy full snippet
```
<application android:label="@string/app\_name" android:icon="@drawable/icon" android:hardwareAccelerated="True" android:hasCode="true">

## Extra Settings for Application

Navigate to **Extra Settings for <application> section (\\n to separate lines)** in the **Advanced APK Packaging** section. You can add additional settings for the Application to use by inputting the settings you want to use into the **Extra Settings for** section. If you have more than one setting you want to use, separate each setting by adding **\\n**. For this example the the following two items were added, **android:banner="Foo"** and **android:vmSafeMode="True"**.

Click for full image.

Items that are input into the **Extra Settings for <application>** section will be added to the **Activity** section of the `AndroidManifest.xml` file.

```
		`</activity> 		<activity android:name=".DownloaderActivity" android:screenOrientation="sensorLandscape" android:configChanges="mcc|mnc|uiMode|density|screenSize|orientation|keyboardHidden|keyboard" android:theme="@style/UnrealSplashTheme" /> 		<meta-data android:name="com.epicgames.unreal.GameActivity.DepthBufferPreference" android:value="0" /> 		<meta-data android:name="com.epicgames.unreal.GameActivity.bPackageDataInsideApk" android:value="false" /> 		<meta-data android:name="com.epicgames.unreal.GameActivity.bVerifyOBBOnStartUp" android:value="false" /> 		<meta-data android:name="com.epicgames.unreal.GameActivity.bShouldHideUI" android:value="true" /> 		<meta-data android:name="com.epicgames.unreal.GameActivity.ProjectName" android:value="AndroidProject" /> 		<meta-data android:name="com.epicgames.unreal.GameActivity.bHasOBBFiles" android:value="true" /> 		<meta-data android:name="com.epicgames.unreal.GameActivity.bSupportsVulkan" android:value="true" /> 		<meta-data android:name="com.google.android.gms.games.APP_ID" android:value="@string/app_id" /> 		<meta-data android:name="com.google.android.gms.version" android:value="@integer/google_play_services_version" /> 		<activity android:name="com.google.android.gms.ads.AdActivity" android:configChanges="keyboard|keyboardHidden|orientation|screenLayout|uiMode|screenSize|smallestScreenSize" /> 				android:banner="Foo" 				 android:vmSafeMode="True" 				<service android:name="OBBDownloaderService" /><receiver android:name="AlarmReceiver" /></application>`
Copy full snippet
```
</activity> <activity android:name=".DownloaderActivity" android:screenOrientation="sensorLandscape" android:configChanges="mcc|mnc|uiMode|density|screenSize|orientation|keyboardHidden|keyboard" android:theme="@style/UnrealSplashTheme" /> <meta-data android:name="com.epicgames.unreal.GameActivity.DepthBufferPreference" android:value="0" /> <meta-data android:name="com.epicgames.unreal.GameActivity.bPackageDataInsideApk" android:value="false" /> <meta-data android:name="com.epicgames.unreal.GameActivity.bVerifyOBBOnStartUp" android:value="false" /> <meta-data android:name="com.epicgames.unreal.GameActivity.bShouldHideUI" android:value="true" /> <meta-data android:name="com.epicgames.unreal.GameActivity.ProjectName" android:value="AndroidProject" /> <meta-data android:name="com.epicgames.unreal.GameActivity.bHasOBBFiles" android:value="true" /> <meta-data android:name="com.epicgames.unreal.GameActivity.bSupportsVulkan" android:value="true" /> <meta-data android:name="com.google.android.gms.games.APP\_ID" android:value="@string/app\_id" /> <meta-data android:name="com.google.android.gms.version" android:value="@integer/google\_play\_services\_version" /> <activity android:name="com.google.android.gms.ads.AdActivity" android:configChanges="keyboard|keyboardHidden|orientation|screenLayout|uiMode|screenSize|smallestScreenSize" /> android:banner="Foo" android:vmSafeMode="True" <service android:name="OBBDownloaderService" /><receiver android:name="AlarmReceiver" /></application>

## Extra Tags for com.epicgames.unreal Game Activity

You can add additional tags for the **Extra Tags for com.epicgames.unreal.GameActivity activity node** by clicking on the **Plus** sign icon to add a new element to the **Extra Tags for com.epicgames.unreal.GameActivity node** array and then inputting the tag you want to use.

Click for full image.