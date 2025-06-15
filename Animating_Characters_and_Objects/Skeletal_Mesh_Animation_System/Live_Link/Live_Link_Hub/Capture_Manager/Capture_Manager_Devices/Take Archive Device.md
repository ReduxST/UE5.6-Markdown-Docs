# Take Archive Device

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/take-archive-device](https://dev.epicgames.com/documentation/en-us/unreal-engine/take-archive-device)  
**Processed:** 2025-06-14 16:53:27

---

The **Take Archive** device enables the ingest of arbitrary video, audio, depth, and calibration data identified using a take metadata file (`.cptake`). It can be used if you would like more control over how the data is represented or the contents of the take are not compatible with the other **Capture Manager** devices. This device is backwards compatible with takes created for use with Capture Manager and **MetaHuman Animator** in **Unreal Engine** 5.5 and earlier.

[![Device Manager Take Archive Ingest](https://dev.epicgames.com/community/api/documentation/image/abea22e4-241f-45b8-9382-b698ad1f1c4a?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/abea22e4-241f-45b8-9382-b698ad1f1c4a?resizing_type=fit)

-   **Display Name**: The name of the device as it will appear in the **Devices** list.
    
-   **Take Directory**: the path to the root folder containing the `.cptake` metadata file. This folder can contain subfolders.
    

A visual example of the content expected to be found by the **Take Archive** device in the **Take Directory** is shown below:

Console Output

```code
`+-- take_1 |   +-- top.mov |   |-- bot.mov |   \-- metadata.cptake | |-- metadata.cptake \-- take_2.mov`
```

+-- take\_1 | +-- top.mov | |-- bot.mov | \\-- metadata.cptake | |-- metadata.cptake \\-- take\_2.mov

Copy full snippet(7 lines long)

## Take Metadata Files (.cptake)

Take metadata files (`.cptake`) are created by the user to describe the contents of a take. They allow Capture Manager to work with data that does not meet the expectations of the other devices or if you would like more control.

The information in a take metadata file is encoded using the JSON format, and adheres to a schema which can be found in `\Engine\Plugins\VirtualProduction\CaptureManager\CaptureManagerCore\Content\TakeMetadata\Schema`. Based on the schema, each take must have a `UniqueId` (specified as a GUID), `TakeNumber`, `Slate`, and `Device`section. Each take may optionally have an array of `Video`, `Depth`, `Audio`, or `Calibration` media content.

Below is a minimal example `.cptake` file for a mono video take:

Console Output

```code
`{   "Version": {     "Major": 4,     "Minor": 2   },   "UniqueId": "2b42db4d-11e5-49ab-8a4d-a78212345597",   "TakeNumber": 1,   "Slate": "MySlateName",   "Device": {     "Name": "MyDeviceName",`

```

Copy full snippet(21 lines long)

### Supported Device types

The supported device types compatible with MetaHuman Animator are:

-   StereoHMC
    
-   iPhone
    

If converting a **Live Link Face** take into the `.cptake` format, set the `Model` to the numerical component of the `deviceModel`found in the original `take.json` file. For example, if the `deviceModel`in the `take.json` file is `iPhone14`,`3`, set `Model`in the new `.cptake` metadata file to `14`,`3`.

### Supported Formats

The supported `Format` values for a `Video` section are:

-   mov
    
-   mp4
    
-   png
    
-   jpg
    
-   jpeg
    

The supported `Format` values for a `Depth` section are:

-   mha\_depth
    
-   exr
    

The supported `Format` values for an `Audio` section are:

-   wav
    
-   mov
    
-   mp4
    

The supported `Format` values for a `Calibration` section are:

-   opencv
    
-   mhaical