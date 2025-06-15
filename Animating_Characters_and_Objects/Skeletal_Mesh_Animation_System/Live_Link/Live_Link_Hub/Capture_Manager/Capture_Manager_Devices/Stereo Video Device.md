# Stereo Video Device

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/stereo-video-device](https://dev.epicgames.com/documentation/en-us/unreal-engine/stereo-video-device)  
**Processed:** 2025-06-14 16:52:39

---

The **Stereo Video** device enables the ingest of pairs of videos as stereo takes. An audio file (`.wav`) may also be provided alongside the video.

[![Device Details Stereo](https://dev.epicgames.com/community/api/documentation/image/efd248c9-f080-4336-b58f-d70478e126e4?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/efd248c9-f080-4336-b58f-d70478e126e4?resizing_type=fit)

-   **Display Name**: The name of the device as it will appear in the **Devices** list.
    
-   **Take Directory**: The path to the root folder containing pairs of video files. This folder can contain subfolders.
    
-   **Video Discovery Expression**: [Tokens](https://dev.epicgames.com/documentation/en-us/unreal-engine/stereo-video-device#discovery-expression-tokens) that can be extracted from the folder and file name of the video to identify the take.
    
-   **Audio Discovery Expression**: [Tokens](https://dev.epicgames.com/documentation/en-us/unreal-engine/stereo-video-device#discovery-expression-tokens) that can be extracted from the folder and file name of the audio file to identify the take.
    

A visual example of the content expected to be found by the Stereo Video device in the **Take Directory** is shown below:

Console Output

```code
`+-- take_1 |   +-- top.mov |   \-- bot.mov | +-- take_2 |   +-- audio.wav |   |-- top.mov |   \-- bot.mov | |-- top.mov`

```

Copy full snippet(11 lines long)

## Discovery Expression Tokens

The **Video Discovery Expression** and **Audio Discovery Expression** are used to define the naming convention for video and audio files in your takes. The available tokens are:

|  |  |
| --- | --- |
| 
`<Slate>`

 | 

The slate name.

 |
| 

`<Name>`

 | 

The identifier for the camera in the stereo pair.

 |
| 

`<Take>`

 | 

The take number.

 |
| 

`<Any>`

 | 

Any valid string.

 |
| 

`<Auto>`

 | 

Used without any other tokens to automatically identify takes based on the directory structure.

 |

Tokens can be separated using the following delimiters: `_-.\`

When not using the `<Auto>` token, both `<Slate>` and `<Name>` must be present.

For example, consider the following take: `MyTakeFolder/MySlate_MyName_SomeString-005.mov`. If the Video Discovery Expression is set to the default value of `<Auto>`, the following tokens will be identified:

|  |  |
| --- | --- |
| 
**Slate**

 | 

`MyTakeFolder`

 |
| 

Name

 | 

`MySlate_MyName_SomeString-005`

 |
| 

**Take**

 | 

`1`(the default value)

 |

However, if the Video Discovery Expression is set to `<Slate>_<Name>_<Any>-<Take>` the following tokens will be extracted instead:

|  |  |
| --- | --- |
| 
**Slate**

 | 

`MySlate`

 |
| 

**Name**

 | 

`MyName`

 |
| 

Take

 | 

`5`

 |
| 

**Any**

 | 

`SomeString`

 |

In both cases, the extension `.mov` is ignored.

The same applies for audio files, where any audio extension (such as `.wav`) is ignored.