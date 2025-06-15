# Google Play Asset Delivery Reference

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/using-google-play-asset-delivery-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/using-google-play-asset-delivery-in-unreal-engine)  
**Processed:** 2025-06-14 16:59:16

---

**Google Play Asset Delivery (GooglePAD)** is the Google Play Store's solution for delivering asset packs to applications once they are installed on a device. This solution is intended for use alongside the **Android App Bundle** distribution format. While the App Bundle distributes a customized .apk to the end user, handling code and binaries for the initial installation, the Play Asset Delivery system provides models, textures, sounds, shaders, and other large asset files separately from the .apk. This makes it possible for apps distributed through Google Play to manage the space taken up by content by delivering content as it is needed.

For more general information about Google Play Asset Delivery, refer to the (official Android documentation)\[https://android-developers.googleblog.com/2020/06/introducing-google-play-asset-delivery.html\].

**Unreal Engine** includes GooglePAD integration through a plugin, making this system simple to implement in your own projects. This plugin provides a function library with calls for managing downloads and requesting information from the Play Asset Delivery system. `UGooglePADFunctionLibrary` is available in both C++ and Blueprint.

For additional information on shipping with Android App Bundles, see the page on [Packaging Android Projects](/documentation/en-us/unreal-engine/packaging-android-projects-in-unreal-engine).

## Enabling the GooglePAD Plugin

The GooglePAD plugin is enabled by default, but if you want to disable it, you can find it in the Unreal Editor's **Plugins** window, under the **Android** section. To use GooglePAD, you must also use Android App Bundles as your packaging format.

![GooglePAD Plugin](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b2b33628-0487-42cc-b23e-323cc0f0844b/googlepadplugin.png)

To fully enable the plugin, open **Project Settings** and navigate to **Plugins** > **GooglePAD** > **Packaging**. Click the **Enable Plugin** checkbox, and the module will be available on startup for Android projects.

![GooglePAD Plugin Options](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ff8110cc-e5bd-410b-8111-1b8505275e40/googlepadplugin_2.png)

If you want to use GooglePAD for **install-time** assets, you also need to navigate to **Platforms** > **Android** > **APK Packaging** and disable **Package Data inside APK**. The main .obb file will then be delivered as an install-time asset pack automatically.

Click to enlarge image

## Creating Asset Packs

**Asset packs** for GooglePAD are packaged inside Android App Bundle builds, and managed by the Google Play Store when they are uploaded. This section explains how to package and organize asset packs for inclusion in your App Bundle.

### Asset Pack Delivery Modes

**Chunks** are Unreal Engine's format for organizing external assets. Chunk 0 represents the base installation of the game, while all other chunks are .pak files containing assets outside of the game's main installation.

To use GooglePAD, you must group your game's assets into chunks, and you must group those chunks into asset packs based on the delivery mode you want to use for them. Google Play Asset Delivery supports the following delivery modes for asset packs:

| Delivery Mode | File Size Limitation (Per Asset Pack) | Description |
| --- | --- | --- |
| **Install-Time** | 1 GB | Asset pack that is delivered at the time of installation. The main .obb from your project is automatically bundled into this asset pack. |
| **Fast-Follow** | 512 MB | Asset pack downloaded automatically after the app is installed. The app does not need to be open for this to download. Only one Fast-Follow asset pack is allowed per project. |
| **On-Demand** | 512 MB | Asset packs downloaded when the app is running. |

You can create a total of **50** asset packs per application. You can only have one Install-Time and one Fast-Follow asset pack per project, but can use as many On-Demand asset packs as you want as long as you do not exceed this limit.

### Creating Chunks

Open your **Project Settings** and navigate to **Project** > **Packaging** and make sure **Generate Chunks** is enabled.

![Activate Generate Chunks in the Project > Packaging section](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6578c34f-3c0d-4514-885b-263b99992376/generatechunks.png)

Now you can organize assets into chunks using the **asset manager** or **primary asset labels**. Refer to [Cooking and Chunking](/documentation/en-us/unreal-engine/cooking-content-and-creating-chunks-in-unreal-engine) page for more details on how to use these features.

Once you have designated which assets belong to specific chunks, **packaging** your project will output your chunks as **.pak** files. You can find them in your project folder under `Saved\StagedBuilds[PlatformName][ProjectName]\Content\Paks`.

Click to enlarge image.

### Including Chunks in your App Bundle Build

Each delivery mode for Play Asset Delivery has different requirements for incorporating chunks into App Bundles.

For Install-Time assets, you do not need to make any changes.

For Fast-Follow or On-Demand assets, select the .pak files you want to include and move them to your project's `Build/Android/gradle/assetpacks` directory. Each delivery mode has a different subfolder:

-   Fast-Follow asset packs must be placed in `Build/Android/gradle/assetpacks/fast-follow/[assetpackname]/src/main/assets`
    
-   On-Demand asset packs must be placed in `Build/Android/gradle/assetpacks/on-demand/[assetpackname]/src/main/assets`
    

Replace \[assetpackname\] with the name of the asset pack that the chunks will be bundled into. You can create multiple different named asset packs with different sets of .pak files. However, the names of your asset packs must be unique, and they may not be re-used between fast-follow and on-demand. This name will be the one that you use when querying for asset packs with the API.

Finally, you need to add a build.gradle file in the asset pack folder containing the following code:

```
	`apply plugin: 'com.android.asset-pack'  	def fileparts = projectDir.absolutePath.replaceAll('\\\\', '/').tokenize('/') 	def assetPackName = fileparts[fileparts.size()-1] 	def assetPackType = fileparts[fileparts.size()-2]  	assetPack { 		packName = assetPackName 		dynamicDelivery { 			deliveryType = assetPackType 			instantDeliveryType = assetPackType 		} 	}`

Copy full snippet
```
apply plugin: 'com.android.asset-pack' def fileparts = projectDir.absolutePath.replaceAll('\\\\\\\\', '/').tokenize('/') def assetPackName = fileparts\[fileparts.size()-1\] def assetPackType = fileparts\[fileparts.size()-2\] assetPack { packName = assetPackName dynamicDelivery { deliveryType = assetPackType instantDeliveryType = assetPackType } }

After you have met these requirements, package the project as an app bundle again, and it will include each of these asset packs in your build. When you upload the App Bundle to the Google Play Store, the asset packs will be available for download using the GooglePAD API.

This workflow will be streamlined further in Unreal Engine 4.26.

## Excluding Chunks From the OBB File

By default, .pak files are included in the OBB file generated alongside your project. To exclude them, you need to open your `DefaultEngine.ini` file and filter them using OBB filters under Android Runtime Settings.

```
	`[/Script/AndroidRuntimeSettings.AndroidRuntimeSettings] 	+ObbFilters="-*pakchunk1*" 	+ObbFilters="-*pakchunk2*" 	+ObbFilters="-*pakchunk3*" 	+ObbFilters="-*pakchunk4*" 	+ObbFilters="-*pakchunk5*" 	+ObbFilters="-*pakchunk6*" 	+ObbFilters="-*pakchunk7*" 	+ObbFilters="-*pakchunk8*" 	+ObbFilters="-*pakchunk9*"`

Copy full snippet
```
\[/Script/AndroidRuntimeSettings.AndroidRuntimeSettings\] +ObbFilters="-\*pakchunk1\*" +ObbFilters="-\*pakchunk2\*" +ObbFilters="-\*pakchunk3\*" +ObbFilters="-\*pakchunk4\*" +ObbFilters="-\*pakchunk5\*" +ObbFilters="-\*pakchunk6\*" +ObbFilters="-\*pakchunk7\*" +ObbFilters="-\*pakchunk8\*" +ObbFilters="-\*pakchunk9\*"

In the example above, the OBB filters will catch any .pak files containing any of the text provided. For instance, `+ObbFilters="-*pakchunk1*"` will omit any pak file whose name contains "pakchunk1".

## API Reference

The following sections detail the available functions in the GooglePAD function library and their usage.

### Requests and Error Handling

All requests in the GooglePAD function library return an `EGooglePADErrorCode` denoting whether or not the operation succeeded and, if not, what specific error prevented the request from being completed. The possible error codes are as follows:

| EGooglePADErrorCode | Description |
| --- | --- |
| `AssetPack_NO_ERROR` | No error with the request. Proceed with the requested information as normal. |
| `AssetPack_APP_UNAVAILABLE` | The requesting app is unavailable. |
| `AssetPack_UNAVAILABLE` | The requested asset pack is not available for your app's current version. |
| `AssetPack_INVALID_REQUEST` | The request is invalid. |
| `AssetPack_DOWNLOAD_NOT_FOUND` | The requested download has not been found. |
| `AssetPack_API_NOT_AVAILABLE` | The Asset Pack API is not available. |
| `AssetPack_NETWORK_ERROR` | Unable to obtain details about an Asset Pack due to a timeout or other network error. |
| `AssetPack_ACCESS_DENIED` | The download is not permitted due to current device circumstances, usually because the user is not signed into a Google account. |
| `AssetPack_INSUFFICIENT_STORAGE` | An asset pack download failed due to insufficient storage. |
| `AssetPack_PLAY_STORE_NOT_FOUND` | The Play Store app is either not installed on this device or not the official version. |
| `AssetPack_NETWORK_UNRESTRICTED` | Returned if `ShowCellularDataConfirmation` is called but no Asset Packs are waiting for wi-fi. This means that downloads can proceed without waiting for confirmation from the user. |
| `AssetPack_INTERNAL_ERROR` | An unknown error occurred in downloading an asset pack. |
| `AssetPack_INITIALIZATION_NEEDED` | `AssetPackManager_init` has not yet been called, therefore the API has not been enabled yet. |
| `AssetPack_INITIALIZATION_FAILED` | There was an error initializing the Asset Pack API. |

In addition to this return value, request functions will have an out variable providing the requested information. If you get a result of `AssetPack_NO_ERROR`, you can proceed with the provided information normally. Otherwise, you should use flow control to react to the provided error code appropriately.

### Getting the Location of Downloaded Files

The function `GetAssetPackLocation` fetches the location of an asset pack that has been downloaded and caches information about it locally. If the asset is available, it will output an integer handle that can be used to access the cached information as needed.

Calling `GetAssetsPath` and providing the location handle will output a string with the asset path for the desired asset pack. `GetStorageMethod` will output an `EGooglePADStorageMethod` stating the way the asset pack is stored on the user's device. Once you know the asset path and storage method, you can then use appropriate calls to access the assets.

The possible storage methods are as follows:

| EGooglePADStorageMethod | Description |
| --- | --- |
| `AssetPack_STORAGE_FILES` | The asset pack is unpacked into a folder containing individual asset files. These assets can be accessed via standard file APIs. |
| `AssetPack_STORAGE_APK` | The asset pack is installed as an APK containing packed asset files. These assets can be accessed via the Asset Manager. |
| `AssetPack_STORAGE_UNKNOWN` | No information is available about the asset pack, most likely due to an error. |
| `AssetPack_STORAGE_NOT_INSTALLED` | The asset pack is not installed, and is therefore unavailable. |

Once you are done using the above information, you must pass the location handle to `ReleaseAssetPackLocation` to free the cached location info.

If `GetAssetPackLocation` returns an error code of `AsetPack_UNAVAILABLE` or `AssetPack_DOWNLOAD_NOT_FOUND`, then the desired asset pack is unavailable and must be downloaded.

### Requesting Information about Asset Packs

The function `RequestInfo` takes in a `TArray` of asset pack names and returns an `EGooglePADErrorCode` denoting their current status. RequestInfo is not required to initiate a download, but can be used to determine whether remote asset packs are valid.

### Requesting or Cancelling a Download

The function `RequestDownload` takes in a `TArray` of strings representing the names of the asset packs you would like to download, then sends a request to the remote service to begin downloading those asset packs. If `RequestDownload` shows no errors, the asset packs will be downloaded and transferred to the app asynchronously in the background.

Because this functionality is asynchronous, the `RequestDownload` function does not return information about the downloaded asset pack, other than an error code denoting whether the request was successful. You must use the functions detailed in the [Monitoring Download Status](/documentation/en-us/unreal-engine/using-google-play-asset-delivery-in-unreal-engine#monitoringdownloadstatus) section below to check for the download's current status, and to access the asset pack itself you must use `GetAssetPackLocation` once the download is complete.

The function `CancelDownload` also uses a list of asset pack names, and will cancel downloading the designated asset packs.

### Getting Cellular Data Status

The function `ShowCellularDataConfirmation` will prompt the user for whether they want to download data using their cellular network. If the prompt is already present, you can use GetShowCellularDataConfirmationStatus to return an `EGooglePADCellularDataConfirmStatus` stating whether or not the user has approved the download.

Results of `AssetPack_CONFIRM_UNKNOWN` and `AssetPack_CONFIRM_PENDING` mean the user has not given approval yet, and the application should stand by until approval is given.

A result of `AssetPack_CONFIRM_USER_CANCELLED` means that the user has chosen not to allow the use of cellular data, and downloads should not be permitted at this time.

A result of `AssetPack_CONFIRM_USER_APPROVED` means that the user has given express approval to use cellular data and downloads should be allowed to proceed. Additionally, If this function returns an `EGooglePADErrorCode` with a result of `AssetPack_NETWORK_UNRESTRICTED`, the user is on their wi-fi network and does not need to use cellular data, therefore downloads should be permitted without the need to continue checking this function.

### Monitoring Download Status

`GetDownloadState` will locally cache the download status of an asset pack and return a download handle providing access to the cached information. This function takes in the name of the asset pack that you want to download and outputs the handle as an integer. You should keep the download handle cached so that you can continue to monitor the download, otherwise, you will need to re-acquire it.

With a valid download handle, you can call `GetDownloadStatus` to return the status of the desired asset pack as an `EGooglePADDownloadStatus`. This enum represents the status of a download as one of several possible states, which are as follows:

| EGooglePADDownloadStatus | Description |
| --- | --- |
| `AssetPack_UNKNOWN` | Nothing is currently known about the asset pack. |
| `AssetPack_DOWNLOAD_PENDING` | An async request to download the asset pack has been made and is currently pending. |
| `AssetPack_DOWNLOADING` | The asset pack download is currently in-progress. |
| `AssetPack_TRANSFERRING` | The asset pack is being transferred to the app. |
| `AssetPack_DOWNLOAD_COMPLETED` | Download and transfer are both complete, and the assets are now available to the app. |
| `AssetPack_DOWNLOAD_FAILED` | The request to download the asset pack has failed. |
| `AssetPack_DOWNLOAD_CANCELED` | The request to download the asset pack has been cancelled. |
| `AssetPack_WAITING_FOR_WIFI` | The asset pack download is waiting for wi-fi bandwidth to proceed. |
| `AssetPack_NOT_INSTALLED` | The asset pack is not currently installed. |
| `AssetPack_INFO_FAILED` | A request for information about the asset pack has failed. |
| `AssetPack_REMOVAL_PENDING` | An async request to remove the asset pack has been made and is currently pending. |
| `AssetPack_REMOVAL_FAILED` | An async request to remove the asset pack has failed. |

You can also use the download state handle to call `GetBytesDownloaded`, which will return the number of bytes currently downloaded to the user's device, and `GetTotalBytesToDownload`, which will return the total target size of the download.

Once you have finished using the download status information, you must call `ReleaseDownloadState` and provide the handle to release the cached download information from memory.

### Removing Asset Packs

The function `RequestRemoval` takes in an asset pack name and removes the specified asset pack from the user's device asynchronously. The asset pack's removal status can be monitored with `GetDownloadStatus` as above.

## Recommended Implementation

Implementation of the GooglePAD API can be modeled as a cycle of different states for each download.

| State | Description |
| --- | --- |
| **Accessing Asset Pack** | 
-   Use `GetAssetPackLocation` to check if you already have an asset pack downloaded. You should run this first to avoid attempting to download assets you already have.
-   Use `GetAssetsPath` and `GetStorageMethod` to determine the file path and access method appropriate for the asset pack.
-   You must call `ReleaseAssetPackLocation` to free the memory for the cached location of the asset pack.



 |
| **Initiating Download** | 

-   If the desired asset pack isn't available locally, call `RequestDownload` to initiate the download.
-   In case of connectivity issues, you may need to repeat `RequestDownload` until it is successful.



 |
| **Checking for Cellular Data Confirmation** | 

-   Use `ShowCelllarDataConfirmation` to ensure that the application has permission to continue the download.
-   After the initial cellular data confirmation prompt, use `GetShowCellularDataConfirmationStatus` to output the current state of the prompt. This should occur continuously on a `Tick` function until the prompt is either canceled or confirmed.



 |
| **Monitoring Download Status** | 

-   Once `RequestDownload` has run successfully, use `GetDownloadState` to cache the download state and obtain a handle to access it with. This needs to be called only once, and you should cache the handle as long as you need it.
-   Use `GetBytesDownloaded` and `GetTotalBytesToDownload` to check the progress of the download. `GetBytesDownloaded` should run continuously on tick until you stop monitoring progress.
-   Use `GetDownloadStatus` to determine the exact state the download is in. This should also be monitored continuously on tick. When the state returns as `AssetPack_DOWNLOAD_COMPLETED`, you can stop monitoring the status of the download and access the asset pack.
-   When you are finished, you must call `RelaseDownloadState` to free the memory for the cached download state.



 |

Implementing your solution in a custom **GameState** class will enable you to track a download continuously even as you change scenes and game modes. Alternatively, you may want to implement your solution in a front-end game mode that loads on startup so that you can perform necessary patches and updates before starting the game. The exact details of your solution will depend on your project's specific needs for updating assets.