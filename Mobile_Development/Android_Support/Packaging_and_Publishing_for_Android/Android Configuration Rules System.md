# Android Configuration Rules System

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/using-the-android-configuration-rules-system-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/using-the-android-configuration-rules-system-in-unreal-engine)  
**Processed:** 2025-06-14 17:01:15

---

The Android Configuration Rules system gives Android developers using Unreal Engine control over determining if a particular Android-based device has the needed hardware and software to run their project. The following information and steps will enable you to develop your UE4 projects for the devices and software you intend to support.

## Config Rules File

To get started, create a new text file called **configrules.txt** and place it in your projects **Build/Android** directory.

Click for full image.

Once you have the configrules.txt file created and placed in the Build/Android directory, open it up in your text editor of choice and add the following text, making sure that it is the first item in the file.

```
	`// version:1`

Copy full snippet
```
// version:1

The above text is the version code parsed by the ConfigRulesTool during packaging, and must be present in this form (one space between "//" and "version:", and no spaces after the colon). The number starts at one and should be incremented any time you update the file. UE4 will then use this number to determine if a newer version should be used than what is currently embedded in the Android Package (APK).

Any line that starts with a **//** or **semicolon(;)** is treated as a comment and ignored.

Commands are used to manipulate case-sensitive variables which either trigger an immediate action or are passed on to the engine. Any variables still defined after the Config Rules runs may be queried from C++ with the following function:

```
	`FString* FAndroidMisc::GetConfigRulesVariable(const FString& Key);`

Copy full snippet
```
FString\* FAndroidMisc::GetConfigRulesVariable(const FString& Key);

**Example:**

```
	`#if PLATFORM_ANDROID 	If (FAndroidMisc::GetConfigRulesVariable(TEXT("myflag") == TEXT("true")) 	{ 		UE_LOG(LogAndroid, Display, TEXT("myflag was set!")); 	} 	#endif`
Copy full snippet
```
#if PLATFORM\_ANDROID If (FAndroidMisc::GetConfigRulesVariable(TEXT("myflag") == TEXT("true")) { UE\_LOG(LogAndroid, Display, TEXT("myflag was set!")); } #endif

It is also possible to get access to a TMap with the key/value entries if you would like to iterate over them:

```
	`TMap<FString, FString> FAndroidMisc::GetConfigRulesTMap();`

Copy full snippet
```
TMap<FString, FString> FAndroidMisc::GetConfigRulesTMap();

**Example:**

```
	`#if PLATFORM_ANDROID 	TMap<FString, FString> ConfigRules = FAndroidMisc::GetConfigRulesTMap(); 	for (const TPair<FString, FString>& Pair : ConfigRules) 	{ 		FString VarKey = Pair.Key; 		if (VarKey.StartsWith("myvars_")) 	{ 			FString VarValue = Pair.Value; 			UE_LOG(LogAndroid, Log, TEXT("Found variable %s = %s"), *VarKey, *VarValue); 	} 	} 	#endif`

Copy full snippet
```
#if PLATFORM\_ANDROID TMap<FString, FString> ConfigRules = FAndroidMisc::GetConfigRulesTMap(); for (const TPair<FString, FString>& Pair : ConfigRules) { FString VarKey = Pair.Key; if (VarKey.StartsWith("myvars\_")) { FString VarValue = Pair.Value; UE\_LOG(LogAndroid, Log, TEXT("Found variable %s = %s"), \*VarKey, \*VarValue); } } #endif

## Config Rules Variables

Variables may be used in values with the following syntax:

```
	`$(varname)`

Copy full snippet
```
$(varname)

This means that the following:

```
	`"$(SRC_DeviceMake) $(SRC_DeviceModel)"`

Copy full snippet
```
"$(SRC\_DeviceMake) $(SRC\_DeviceModel)"

Would be replaced with the values of **SRC\_DeviceMake** and **SRC\_DeviceModel** separated by a space.

The following variables are defined automatically before configrules.txt is parsed:

| **Variable Name** | **Description** | **Example Value** |
| --- | --- | --- |
| memory | Total memory in megabytes. | 3550 |
| hardware | The chipset (either Hardware from /proc/cpuinfo or getprop ro.hardware). | Qualcomm Technologies, Inc SDM845 |
| ro.hardware | The result from "getprop ro.hardware". | blueline |
| processor | Processor type from /proc/cpuinfo. | AArch64 Processor rev 12 (aarch64) |
| processorCount | Processor count from /proc/cpuinfo. | 8 |
| useAffinity | Whether or not to set thread affinity to little cores for some threads. | true |
| hasNEON | Indicates processor supports NEON features (SIMD). | true |
| isARM64 | Indicates processor supports ARM64 ABI. | true |
| littleCoreMask | Bitmask indicating which cores are little. | 0x0f |
| bigCoreMask | Bitmask indicating which cores are big. | 0xf0 |
| SRC\_GpuVendor | Vendor from GLES20.glGetString(GLES20.GL\_VENDOR). | Qualcomm |
| SRC\_GpuFamily | GPU family from GLES20.glGetString(GLES20.GL\_RENDERER). | Adreno (TM) 630 |
| SRC\_GlVersion | GL version from GLES20.glGetString(GLES20.GL\_VERSION). | OpenGL ES 3.2 [\[email protected\]](/cdn-cgi/l/email-protection) (GIT@3f88ca2, I42f6fe38fb) (Date:07/13/18) |
| SRC\_AndroidVersion | Android version from android.os.Build.VERSION.RELEASE. | 9 |
| SRC\_DeviceMake | Device manufacturer from android.os.Build.MANUFACTURER. | Google |
| SRC\_DeviceModel | Device model from android.os.Build.MODEL. | Pixel 3 |
| SRC\_DeviceBuildNumber | Device build number from android.os.Build.DISPLAY. | PD1A.180720.030 |
| SRC\_VulkanVersion | Version of Vulkan support. | 1.1.0 |
| SRC\_VulkanAvailable | Indicates if Vulkan is supported by the device. | true |
| SRC\_UsingHoudini | Indicates ARM emulated on Intel processor by Houdini. | false |
| SRC\_SDKLevel | SDK level from android.os.Build.VERSION.SDK\_INT. | 28 |
| supportsFloatingPointRenderTargets | Indicates GPU supports FP render targets. | true |
| TextureFormats | Comma-separated list of supported texture formats by GPU. | ASTC,ATC,ETC2,ETC1 |
| navigationBarHeight | Height of Android navigation bar in pixels. | 132 |
| statusBarHeight | Height of Android status bar in pixels. | 66 |
| screenWidth | Screen width in pixels. | 1080 |
| screenHeight | Screen height in pixels. | 2160 |

## Config Rules Commands

Commands can be used with valid arguments in the forum of **action:argument**. These are defined below along with use case examples.

**Set** allows you to assign one or more variables and their specified values:

```
	`set:(myvar=true)`
Copy full snippet
```
set:(myvar=true)

If you have more than one variable, you can use a **comma** (**,**) to separate them:

```
	`set:(myvar=false,myvar2="something",myvar3="else")`
Copy full snippet
```
set:(myvar=false,myvar2="something",myvar3="else")

**clear** allows you to clear the value assigned to variables.

```
	`clear:(myvar)`

Copy full snippet
```
clear:(myvar)

You can clear more than one variable at a time using a **comma** (**,**) to separate the values you want to clear.

```
	`clear:(myvar,myvar3)`

Copy full snippet
```
clear:(myvar,myvar3)

**condition** evaluates the list of conditions and if all are true it applies optional set and clear commands.

```
	`condition:((comparison)[,(comparison)],[(set)],[(clear)]`

Copy full snippet
```
condition:((comparison)\[,(comparison)\],\[(set)\],\[(clear)\]

The comparisons are made up of three parts in parentheses separated by commas. The three parts are **SourceType**, **CompareType**, and **MatchString**.

```
	`(SourceType=isARM64,CompareType=CMP_EQUAL,MatchString="true")`

Copy full snippet
```
(SourceType=isARM64,CompareType=CMP\_EQUAL,MatchString="true")

**SourceType** specifies the first argument for comparison and will usually be a variable name. The following are the three special SourceType values that can be used:

| **Command Name** | **Description** |
| --- | --- |
| SRC\_PreviousRegexMatch | The group returned from the last regex expression condition. |
| SRC\_CommandLine | The command line embedded in the APK. |
| \[EXIST\] | Used with MatchString to see if a variable exists or not. |

**MatchString** is any string value to use for the comparison or the variable name for the **\[EXIST\]** case.

**CompareType** may be one of the following:

| **Command Name** | **Description** |
| --- | --- |
| CMP\_Exist | True if variable name in MatchString is set. |
| CMP\_NotExist | True if variable name in MatchString is not set. |
| CMP\_Equal | True if variable name in MatchString is not set. |
| CMP\_NotEqual | True if SourceType not equal to MatchString. |
| CMP\_EqualIgnore | True if SourceType equals MatchString, ignoring case. |
| CMP\_NotEqualIgnore | True if SourceType does not equal Matchstring, ignoring case. |
| CMP\_Less | True if value of SourceType < value of MatchString. |
| CMP\_LessEqual | True if value of SourceType <= value of MatchString. |
| CMP\_Greater | True if value of SourceType > value of MatchString. |
| CMP\_GreaterEqual | True if value of SourceType >= value of MatchString |
| CMP\_Regex | True if regex in MatchString found in SourceType (matching group is available in SRC\_PreviousRegexMatch for additional condition checks) |

The following examples show how you might setup and use the Android Config Rules Commands in your UE4 projects:

The following code will set **myvar** to **arm64** if **isARM64** is **true**:

```
	`condition:((SourceType=isARM64,CompareType=CMP_EQUAL,MatchString="true")),(myvar="arm64")`
Copy full snippet
```
condition:((SourceType=isARM64,CompareType=CMP\_EQUAL,MatchString="true")),(myvar="arm64")

The following code will set **myvar** to **arm64** if **isARM64** is **true** and clears **notsupported**:

```
	`set:(notsupported=true) 	condition:((SourceType=isARM64,CompareType=CMP_EQUAL,MatchString="true")),(myvar="arm64"),(notsupported)`

Copy full snippet
```
set:(notsupported=true) condition:((SourceType=isARM64,CompareType=CMP\_EQUAL,MatchString="true")),(myvar="arm64"),(notsupported)

The following code uses **Regex** to extract the number in **Adreno (TM) 630** and compares it to see if it is less than **510** to flag an error.:

```
	`condition:((SourceType=SRC_GpuFamily,CompareType=CMP_Regex,MatchString="(?!Adreno \(TM\))([0-9][0-9]*)"),(SourceType=SRC_PreviousRegexMatch,CompareType=CMP_LessEqual,MatchString="510")), (error="CR_Info_UnsupportedGPU")`

Copy full snippet
```
condition:((SourceType=SRC\_GpuFamily,CompareType=CMP\_Regex,MatchString="(?!Adreno \\(TM\\))(\[0-9\]\[0-9\]\*)"),(SourceType=SRC\_PreviousRegexMatch,CompareType=CMP\_LessEqual,MatchString="510")), (error="CR\_Info\_UnsupportedGPU")

**chipset** is a shortcut to set a group of variables if the hardware string is equal to either ro.hardware or hardware. It sets useAffinity, chipset, GPU, processorCount, bigCoreMask, and littleCoreMask. useAffinity controls whether or not taskgroup threads are restricted to the little cores with the littleCoreMask.:

```
	`chipset: hardware string, useAffinity, part name, GPU name, processor count, big core mask, little core mask`

Copy full snippet
```
chipset: hardware string, useAffinity, part name, GPU name, processor count, big core mask, little core mask

Here are some examples:

```
`chipset:"Qualcomm Technologies, Inc MSM8929", true, "Snapdragon 415", "Adreno (TM) 405", 8, 0xf0, 0x0f chipset:"Qualcomm Technologies, Inc MSM8937", true, "Snapdragon 435", "Adreno (TM) 505", 8, 0xf0, 0x0f chipset:"Qualcomm Technologies, Inc MSM8940", true, "Snapdragon 435", "Adreno (TM) 505", 8, 0xf0, 0x0f chipset:"Qualcomm Technologies, Inc MSM8952", true, "Snapdragon 617", "Adreno (TM) 405", 8, 0xf0, 0x0f chipset:"Qualcomm Technologies, Inc MSM8953", true, "Snapdragon 625/626", "Adreno (TM) 506", 8, 0xf0, 0x0f chipset:"Qualcomm Technologies, Inc MSM8956", true, "Snapdragon 650", "Adreno (TM) 510", 6, 0x03, 0x0f chipset:"Qualcomm Technologies, Inc MSM8976", true, "Snapdragon 652/653", "Adreno (TM) 510", 8, 0xf0, 0x0f chipset:"Qualcomm Technologies, Inc SDM630", true, "Snapdragon 630", "Adreno (TM) 508", 8, 0xf0, 0x0f chipset:"Qualcomm Technologies, Inc SDM636", true, "Snapdragon 636", "Adreno (TM) 509", 8, 0xf0, 0x0f chipset:"Qualcomm Technologies, Inc SDM660", true, "Snapdragon 660", "Adreno (TM) 512", 8, 0xf0, 0x0f chipset:"Qualcomm Technologies, Inc SDM640", true, "Snapdragon 640", "Adreno (TM) 610", 8, 0xc0, 0x3f chipset:"Qualcomm Technologies, Inc SDM670", true, "Snapdragon 670", "Adreno (TM) 620", 8, 0xf0, 0x0f chipset:"Qualcomm Technologies, Inc SDM710", true, "Snapdragon 710", "Adreno (TM) 616", 8, 0xc0, 0x3f chipset:"Qualcomm Technologies, Inc SDM730", true, "Snapdragon 730", "Adreno (TM) 615", 8, 0xc0, 0x3f chipset:"Qualcomm Technologies, Inc MSM8992", true, "Snapdragon 808", "Adreno (TM) 418", 6, 0x30, 0x0f chipset:"Qualcomm Technologies, Inc MSM8994", true, "Snapdragon 810", "Adreno (TM) 430", 8, 0xf0, 0x0f chipset:"Qualcomm Technologies, Inc MSM8996", true, "Snapdragon 820/821", "Adreno (TM) 530", 4, 0x0c, 0x03 chipset:"Qualcomm Technologies, Inc MSM8998", true, "Snapdragon 835", "Adreno (TM) 540", 8, 0xf0, 0x0f chipset:"Qualcomm Technologies, Inc SDM845", true, "Snapdragon 845", "Adreno (TM) 630", 8, 0xf0, 0x0f chipset:"samsungexynos9810", true, "Samsung Exynos 9 Series (9810)", "Mali-G72 MP18", 8, 0xf0, 0x0f chipset:"samsungexynos8895", true, "Samsung Exynos 9 Series (8895)", "Mali-G71 MP20", 8, 0xf0, 0x0f chipset:"samsungexynos9610", true, "Samsung Exynos 7 Series (9610)", "Mali-G72 MP3", 8, 0xf0, 0x0f chipset:"samsungexynos7885", true, "Samsung Exynos 7 Series (7885)", "Mali-G71 MP2", 8, 0xc0, 0x3f chipset:"samsungexynos7880", false, "Samsung Exynos 7 Series (7880)", "Mali-T830 MP3", 8, 0xff, 0x00 chipset:"samsungexynos7882", true, "Samsung Exynos 5 Series (7872)", "Mali-G71 MP1", 6, 0x30, 0x0f`
Copy full snippet
```
chipset:"Qualcomm Technologies, Inc MSM8929", true, "Snapdragon 415", "Adreno (TM) 405", 8, 0xf0, 0x0f chipset:"Qualcomm Technologies, Inc MSM8937", true, "Snapdragon 435", "Adreno (TM) 505", 8, 0xf0, 0x0f chipset:"Qualcomm Technologies, Inc MSM8940", true, "Snapdragon 435", "Adreno (TM) 505", 8, 0xf0, 0x0f chipset:"Qualcomm Technologies, Inc MSM8952", true, "Snapdragon 617", "Adreno (TM) 405", 8, 0xf0, 0x0f chipset:"Qualcomm Technologies, Inc MSM8953", true, "Snapdragon 625/626", "Adreno (TM) 506", 8, 0xf0, 0x0f chipset:"Qualcomm Technologies, Inc MSM8956", true, "Snapdragon 650", "Adreno (TM) 510", 6, 0x03, 0x0f chipset:"Qualcomm Technologies, Inc MSM8976", true, "Snapdragon 652/653", "Adreno (TM) 510", 8, 0xf0, 0x0f chipset:"Qualcomm Technologies, Inc SDM630", true, "Snapdragon 630", "Adreno (TM) 508", 8, 0xf0, 0x0f chipset:"Qualcomm Technologies, Inc SDM636", true, "Snapdragon 636", "Adreno (TM) 509", 8, 0xf0, 0x0f chipset:"Qualcomm Technologies, Inc SDM660", true, "Snapdragon 660", "Adreno (TM) 512", 8, 0xf0, 0x0f chipset:"Qualcomm Technologies, Inc SDM640", true, "Snapdragon 640", "Adreno (TM) 610", 8, 0xc0, 0x3f chipset:"Qualcomm Technologies, Inc SDM670", true, "Snapdragon 670", "Adreno (TM) 620", 8, 0xf0, 0x0f chipset:"Qualcomm Technologies, Inc SDM710", true, "Snapdragon 710", "Adreno (TM) 616", 8, 0xc0, 0x3f chipset:"Qualcomm Technologies, Inc SDM730", true, "Snapdragon 730", "Adreno (TM) 615", 8, 0xc0, 0x3f chipset:"Qualcomm Technologies, Inc MSM8992", true, "Snapdragon 808", "Adreno (TM) 418", 6, 0x30, 0x0f chipset:"Qualcomm Technologies, Inc MSM8994", true, "Snapdragon 810", "Adreno (TM) 430", 8, 0xf0, 0x0f chipset:"Qualcomm Technologies, Inc MSM8996", true, "Snapdragon 820/821", "Adreno (TM) 530", 4, 0x0c, 0x03 chipset:"Qualcomm Technologies, Inc MSM8998", true, "Snapdragon 835", "Adreno (TM) 540", 8, 0xf0, 0x0f chipset:"Qualcomm Technologies, Inc SDM845", true, "Snapdragon 845", "Adreno (TM) 630", 8, 0xf0, 0x0f chipset:"samsungexynos9810", true, "Samsung Exynos 9 Series (9810)", "Mali-G72 MP18", 8, 0xf0, 0x0f chipset:"samsungexynos8895", true, "Samsung Exynos 9 Series (8895)", "Mali-G71 MP20", 8, 0xf0, 0x0f chipset:"samsungexynos9610", true, "Samsung Exynos 7 Series (9610)", "Mali-G72 MP3", 8, 0xf0, 0x0f chipset:"samsungexynos7885", true, "Samsung Exynos 7 Series (7885)", "Mali-G71 MP2", 8, 0xc0, 0x3f chipset:"samsungexynos7880", false, "Samsung Exynos 7 Series (7880)", "Mali-T830 MP3", 8, 0xff, 0x00 chipset:"samsungexynos7882", true, "Samsung Exynos 5 Series (7872)", "Mali-G71 MP1", 6, 0x30, 0x0f

## Config Rules Special Variables

There are two special variables which trigger actions if set:

```
	`set:(log="message for the logcat")`

Copy full snippet
```
set:(log="message for the logcat")

The value of log after any command is evaluated will be written to the logcat output and cleared.

```
	`set:(dumpvars=1)`

Copy full snippet
```
set:(dumpvars=1)

This will dump all the variables currently set and their values to logcat.

## Config Rules Profiles

You can set the **Profile** variable to override the device profile used instead of the one that would be picked by the **AndroidDeviceProfileMatchingRules** in **DefaultDeviceProfiles**.ini. If this value is not modified the normal rules will still apply. The following example would force the **Android\_Galaxy\_S9Plus\_Adreno** setting for **SM-G965** models:

```
	`condition:((SourceType=sammodel,CompareType=CMP_Regex,MatchString="SM-G965")), (Profile="Android_Galaxy_S9Plus_Adreno")`
Copy full snippet
```
condition:((SourceType=sammodel,CompareType=CMP\_Regex,MatchString="SM-G965")), (Profile="Android\_Galaxy\_S9Plus\_Adreno")

## Config Rules Dialog

You can customize the error and warning dialog messages that are displayed using the following variables:

-   caption
-   exitbutton
-   continuebutton
-   updatebutton
-   helpbutton

The value placed in the caption or buttons is looked up in the string table to get the localized text for the dialog. You should make these string names unique and place them in a **ConfigurationStrings.xml** file in your project's **Build/Android/res/values** directory for each localized language your project supports. (values-fr, for example, would be for French).

An example of where the ConfigurationStrings.xml file should be placed is shown below.

Click for full image.

-   **Error -** You can signal an **error** by setting the **error variable**. The dialog will show the string table entry for the value you assign to it. All processing of the configrules.txt will stop once this is set and the user will not be able to continue into your application.
-   **Warning** - A **Warning** dialog is triggered by setting the **warning variable**. The dialog will provide a continue option and optionally update and/or help buttons if the corresponding variables are set. The help button will launch an external browser to the URL specified by the link variable. Evaluation of configrules.txt will continue until the end or error is set before the dialog is shown so you can change it again with different conditions if necessary.

The following example code was setup to display an error is the user tried to use an Android device that does not support ARM64.

```
	`set:(caption="CR_Caption_DeviceNotSupported", exitbutton="CR_Button_Quit", continuebutton="CR_Button_Continue", helpbutton="CR_Button_Help") 	condition:((SourceType=isARM64,CompareType=CMP_EQUAL,MatchString="false")),(error="CR_Info_RequiresARM64")`

Copy full snippet
```
set:(caption="CR\_Caption\_DeviceNotSupported", exitbutton="CR\_Button\_Quit", continuebutton="CR\_Button\_Continue", helpbutton="CR\_Button\_Help") condition:((SourceType=isARM64,CompareType=CMP\_EQUAL,MatchString="false")),(error="CR\_Info\_RequiresARM64")

When the above example is encountered, the error message that is displayed will come from the following string table.

```
`<?xml version="1.0" encoding="utf-8"?> <resources>  <string name="CR_Button_Quit">Quit</string> <string name="CR_Button_Help">More Info</string> <string name="CR_Button_Continue">Continue</string> <string name="CR_Button_Update">Check for Update</string>  <string name="CR_Caption_DeviceNotSupported">Device Not Supported</string>  <string name="CR_Info_RequiresARM64">This game requires an ARM64-v8a processor.</string> </resources>`
Copy full snippet
```
<?xml version="1.0" encoding="utf-8"?> <resources> <string name="CR\_Button\_Quit">Quit</string> <string name="CR\_Button\_Help">More Info</string> <string name="CR\_Button\_Continue">Continue</string> <string name="CR\_Button\_Update">Check for Update</string> <string name="CR\_Caption\_DeviceNotSupported">Device Not Supported</string> <string name="CR\_Info\_RequiresARM64">This game requires an ARM64-v8a processor.</string> </resources>

## Config Rules Build Files

The following additions to your project are required for the configrules.txt file to be included in your APK by compressing, and optionally encrypting, it. Start by registering the following **Unreal Plugin Language** (UPL) code in your project's **Build.cs** file:

```
	`if (Target.Platform == UnrealTargetPlatform.Android) 	{ 	// Add UPL to add configrules.txt to our APK 	string PluginPath = Utils.MakePathRelativeTo(ModuleDirectory, Target.RelativeEnginePath); 	AdditionalPropertiesForReceipt.Add("AndroidPlugin", System.IO.Path.Combine(PluginPath, "MyGame_UPL.xml")); 	}`
Copy full snippet
```
if (Target.Platform == UnrealTargetPlatform.Android) { // Add UPL to add configrules.txt to our APK string PluginPath = Utils.MakePathRelativeTo(ModuleDirectory, Target.RelativeEnginePath); AdditionalPropertiesForReceipt.Add("AndroidPlugin", System.IO.Path.Combine(PluginPath, "MyGame\_UPL.xml")); }

Next you will want to create a new file called **MyGame\_UPL.xm****l** which is placed in the same directory with the **Build.cs** file.

Click for full image.

Open up the MyGame\_UPL.xml file and then add the following code, saving the file when done (change the ConfigRulesKey to contain your unique encryption key):

```
	`<?xml version="1.0" encoding="utf-8"?> 	<root xmlns:android="http://schemas.android.com/apk/res/android"> 		 		<init> 			 			<setString result="ConfigRulesKey" value="This is my encryption key"/> 		</init> 		 		<gradleCopies> 			<copyFile src="$S(BuildDir)/configrules.txt" 						dst="$S(BuildDir)/gradle/app/configrules.txt"/> 		</gradleCopies> 		<gradleProperties> 			<insertValue value="CONFIGRULESTOOL_KEY=$S(ConfigRulesKey)"/> 			<insertNewline/> 			<insertValue value="CONFIGRULESTOOL_JAR=$S(AbsEngineDir)/Build/Android/Prebuilt/ConfigRulesTool/bin/ConfigRulesTool.jar"/> 			<insertNewline/> 		</gradleProperties> 		<gameActivityClassAdditions> 			<insertValue value="public String CONFIGRULES_KEY = "$S(ConfigRulesKey)";"/> 			<insertNewline/> 		</gameActivityClassAdditions> 		<buildGradleAdditions> 			<insert> 			<![CDATA[ 	task ProcessConfigRules(type: JavaExec) { 		description 'Produces compressed and encrypted configules.bin.png in assets' 		inputs.file file('configrules.txt') 		outputs.file file('src/main/assets/configrules.bin.png') 		main = "-jar" 		args = [ 			"${CONFIGRULESTOOL_JAR}", 			'c', 			'configrules.txt', 			'src/main/assets/configrules.bin.png', 			"${CONFIGRULESTOOL_KEY}" 		] 	} 	tasks.whenTaskAdded { task -> 		if (CONFIGRULESTOOL_JAR != null) { 			if (task.name == 'assembleRelease') { 				task.dependsOn 'ProcessConfigRules' 			   } 			if (task.name == 'assembleDebug') { 				task.dependsOn 'ProcessConfigRules' 			} 		} 	} 			]]> 			</insert> 		</buildGradleAdditions> 	</root>`
Copy full snippet
```
<?xml version="1.0" encoding="utf-8"?> <root xmlns:android="http://schemas.android.com/apk/res/android"> <init> <setString result="ConfigRulesKey" value="This is my encryption key"/> </init> <gradleCopies> <copyFile src="$S(BuildDir)/configrules.txt" dst="$S(BuildDir)/gradle/app/configrules.txt"/> </gradleCopies> <gradleProperties> <insertValue value="CONFIGRULESTOOL\_KEY=$S(ConfigRulesKey)"/> <insertNewline/> <insertValue value="CONFIGRULESTOOL\_JAR=$S(AbsEngineDir)/Build/Android/Prebuilt/ConfigRulesTool/bin/ConfigRulesTool.jar"/> <insertNewline/> </gradleProperties> <gameActivityClassAdditions> <insertValue value="public String CONFIGRULES\_KEY = "$S(ConfigRulesKey)";"/> <insertNewline/> </gameActivityClassAdditions> <buildGradleAdditions> <insert> <!\[CDATA\[ task ProcessConfigRules(type: JavaExec) { description 'Produces compressed and encrypted configules.bin.png in assets' inputs.file file('configrules.txt') outputs.file file('src/main/assets/configrules.bin.png') main = "-jar" args = \[ "${CONFIGRULESTOOL\_JAR}", 'c', 'configrules.txt', 'src/main/assets/configrules.bin.png', "${CONFIGRULESTOOL\_KEY}" \] } tasks.whenTaskAdded { task -> if (CONFIGRULESTOOL\_JAR != null) { if (task.name == 'assembleRelease') { task.dependsOn 'ProcessConfigRules' } if (task.name == 'assembleDebug') { task.dependsOn 'ProcessConfigRules' } } } \]\]> </insert> </buildGradleAdditions> </root>