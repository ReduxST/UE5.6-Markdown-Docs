# Export Formats

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/cinematic-rendering-export-formats-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/cinematic-rendering-export-formats-in-unreal-engine)  
**Processed:** 2025-06-14 16:13:17

---

**Movie Render Queue** supports a variety of output formats for rendering to images or movies, and is capable of outputting different formats at the same time.

#### Prerequisites

-   You have completed the prerequisite steps from the Movie Render Queue section of the **[](/documentation/404)**page.

You can choose which formats you want to render in Movie Render Queue's **Settings** window by clicking the **\+ Setting** dropdown menu and selecting a format from the **Export** category. ![render export format](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4022a716-3deb-41c0-80b9-6e9e8a7247f2/addexportformat.png)

You can enable and disable output formats as you would with any other setting by clicking on the enable button next to their text. You can also select them to edit their properties, if available.

The following output formats are available:

| Name | Description |
| --- | --- |
| [**Command Line Encoder**](/documentation/en-us/unreal-engine/cinematic-rendering-export-formats-in-unreal-engine#commandlineencoder) | The Command Line Encoder can be used to create your own output format from third party software, such as FFmpeg. This setting requires an encoder executable and settings to be enabled in your Project Settings. |
| [**Final Cut Pro XML**](/documentation/en-us/unreal-engine/cinematic-rendering-export-formats-in-unreal-engine#finalcutproxml) | The Final Cut Pro XML format will output an XML file that can be read by Final Cut Pro and other video editing software that support this format. This is not supported in shipping builds. |
| **.bmp Sequence \[8bit\]** | Outputs the movie as a sequence of .bmp images. Pixel values are clamped in the \[0-1\] range, meaning that no HDR values are preserved. This applies sRGB encoding curve. |
| [**EXR Sequence**](/documentation/en-us/unreal-engine/cinematic-rendering-export-formats-in-unreal-engine#exrsequence) | Outputs the movie as a sequence of .exr images. HDR values are preserved but if the Tone Curve is enabled, linear values are scaled to approximately the \[0-1\] range with only the brightest highlights going above one. Disabling the Tone Curve writes linear values in the \[0-100\] range or more depending on the intensity of lights and other bright objects. No sRGB encoding curve is applied to .exr targets. |
| **.jpg Sequence \[8bit\]** | Outputs the movie as a sequence of .jpg images. Applies sRGB encoding curve. |
| **.png Sequence \[8bit\]** | Outputs the movie as a sequence of .png images. Applies sRGB encoding curve. Transparency is supported by enabling Enable Alpha Channel Support in Post Processing project setting. |
| [**WAV Audio**](/documentation/en-us/unreal-engine/cinematic-rendering-export-formats-in-unreal-engine#wavaudio) | Outputs a .wav audio file alongside any other output formats you have selected. |
| [**Apple ProRes Video Codecs**](/documentation/en-us/unreal-engine/cinematic-rendering-export-formats-in-unreal-engine#appleproresvideocodecs) | Outputs a .mov file using Apple ProRes, which is Apple's high-quality, lossy video compression codec. This requires the Apple ProRes Media plugin to be enabled. |
| [**Avid DNx Video Codecs**](/documentation/en-us/unreal-engine/cinematic-rendering-export-formats-in-unreal-engine#aviddnxvideocodecs) | Outputs a movie file using Avid DNx, which is a high-definition lossy video codec. This requires the Avid DNxHR/DNxMXF Media plugin to be enabled. |
| **Prestreaming Recorder** | The Prestreaming Recorder is used to create render caches for cinematics using **Virtual Textures** or **Nanite**. |

## Command Line Encoder

The Command Line Encoder can be used to create your own output format from 3rd party software, such as FFmpeg. To use Command Line Encoder, you must navigate to the **Movie Pipeline CLI Encoder** project setting to set up certain properties and settings.

If you use the Command Line Encoder, you must accompany it with an image sequence export format too, in order for it to create movie frames from those images. If you want to include audio, you must also include a **.wav Audio** export.

![command line encoder export](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0f2a549d-8660-4922-b407-d659c940ac42/clejoint.png)

### Export Details

Selecting Command Line Encoder will reveal the following details:

![command line encoder properties](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/93291ae4-9c80-4e51-9618-667655806b90/cledetails.png)

| Detail Name | Description |
| --- | --- |
| **File Name Format Override** | Overrides the **File Name Format** from the **Output** setting for the movie that the Command Line Encoder outputs. You can use this to generate a single master movie file, instead of individual shot movie files if you are rendering your image sequences to separate shot folders. |
| **Quality** | What encoding quality settings to use. These can be defined in the **Movie Pipeline CLI Encoder** project setting. |
| **Additional Command Line Args** | Any additional command line arguments to pass to the encoder for this job. |
| **Delete Source Files** | If enabled, deletes the source image sequence files after the movie encoding is completed. This will result in only the movie being exported, without the source images. |
| **Skip Encode on Render Canceled** | If enabled, the encoder will not attempt to encode whatever frames were rendered if the render was cancelled prematurely. |
| **Write Each Frame Duration** | Writes the duration for each frame into the generated texture file. This is needed for some input types on some CLI encoding software. |

### Project Settings

You will be required to set up certain project settings in order to use Command Line Encoder.

Click on **Edit > Project Settings** to open the project settings window and navigate to **Movie Pipeline CLI Encoder** in the **Plugins** category.

![command line encoder project settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cec8e9e3-2daa-4d81-8a65-c3bc66412e2a/cleps.png)

| Detail Name | Description |
| --- | --- |
| **Executable Path** | 
The path, including executable name, to the encoder executable file.

-   Can either be a direct path, such as `‪D:\ffmpeg\bin\ffmpeg.exe`.
-   Or, if you have designated your encoder's path in **Windows Environment Variables**, you can just specify your encoder executable.



 |
| **Codec Help Text** | Text for your project to paste into Unreal's console window to generate a list of valid audio and video codecs for your encoder. Requires the **Executable Path** to be set first as the command queries the executable. |
| **Video Codec** | Specify the video codec here. If using FFmpeg, you can see the list of codecs by executing **MovieRenderPipeline.DumpCLIEncoderCodecs** in Unreal's **Output Log** window. |
| **Audio Codec** | Specify the audio codec here. If using FFmpeg, you can see the list of codecs by executing **MovieRenderPipeline.DumpCLIEncoderCodecs** in Unreal's **Output Log** window. An audio codec must be specified if -acodec {AudioCodec} is being specified in the command line. |
| **Output File Extension** | Extension for the output file and should not include the period, such as **mp4**, **mkv**, or **webm**. Certain codecs support different containers and you should ensure you are using the correct container for your codec. |
| **Command Line Format** | 

The format string to use when building the final command line argument to launch. Uses `{tokens}` to insert arguments from your project setting or Command Line Encoder details.

-   `{AdditionalLocalArgs}`: Inserts arguments here from the Additional Command Line Args property in the Command Line Encoder details.
-   `{VideoInputs}`: Inserts argument here from the Video Input String Format project setting.
-   `{AudioInputs}`: Inserts argument here from the Audio Input String Format project setting.
-   `{AudioCodec}`: Inserts argument here from the Audio Codec project setting.
-   `{VideoCodec}`: Inserts argument here from the Video Codec project setting.
-   `{Quality}`: Inserts arguments here from the Quality property in the Command Line Encoder details, then defined by the Encode Settings project setting.
-   `{OutputPath}`: Inserts arguments here from the Output Directory property in the Movie Render Queue's output details.



 |
| **Video Input String Format** | 

The format string to use when building the video input argument. Uses `{tokens}` to insert arguments from your image sequence.

-   `{InputFile}`: When your render is occurring, a temporary text file is created which itemizes every frame being rendered in sequence. This token references that file in order to find the frames to produce the video. By default this text file is automatically deleted after encoding finishes. You can keep this text file by enabling the Write All Samples property from the Debug Options setting.
-   `{FrameRate}`: The frame rate from either the Level Sequence, or the Output Frame Rate if Use Custom Frame Rate is enabled from the job's Output.



 |
| **Audio Input String Format** | 

The format string to use when building the audio input argument. Uses `{tokens}` to insert arguments from your .wav file output.

-   `{InputFile}`: When your render is occurring, a temporary text file is created which itemizes the audio being created. This token references that file in order to find the audio to add to the video. This text file can be saved by enabling the Write All Samples property from the Debug Options setting.



 |
| **Encode Settings Low** | The encoding argument to use when **Low** is specified from the **Quality** property in the Command Line Encoder details. |
| **Encode Settings Med** | The encoding argument to use when **Med** is specified from the **Quality** property in the Command Line Encoder details. |
| **Encode Settings High** | The encoding argument to use when **High** is specified from the **Quality** property in the Command Line Encoder details. |
| **Encode Settings Epic** | The encoding argument to use when **Epic** is specified from the **Quality** property in the Command Line Encoder details. |

Your Encode Settings may need to be different depending on the codecs being used. The default values are considered a typical setting for the most common codecs you may use with FFmpeg. Only single pass encoding is supported with Command Line Encoder. You can reference **[FFmpeg Codec Documentation](https://ffmpeg.org/ffmpeg-codecs.html)** for more information on codecs and their encoding settings.

### Example Setup

The following shows an example of what details and project settings you can use if you want to set up your encoder to use ffmpeg with the open format VP9 codec.

Here you can see that the **Command Line Encoder** is being exported along with **.jpg Sequence** and **.wav Audio**.

![command line encoder export](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/16c4e193-82db-4f0b-908f-3904410cc466/examplecle.png)

In the Project Settings, the highlighted properties are the only ones that have been altered from their default values in order to support the codec. If you are not exporting a .wav audio pass, then it is not necessary to specify an Audio Codec.

![command line encoder project settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4714380f-d398-49c5-82ee-877e72e661e7/exampleps.png)

-   Video Codec: `libvpx-vp9`
-   Audio Codec: `libvorbis`
-   Output File Extension: `mkv`
-   Encode Settings Low: `-crf 28 -b:v 0`
-   Encode Settings Med: `-crf 23 -b:v 0`
-   Encode Settings High: `-crf 20 -b:v 0`
-   Encode Settings Epic: `-crf 16 -b:v 0`

## EXR Sequence

Unreal supports .exr image sequences as an output format for Movie Render Queue. These are compatible with a variety of visual effects packages, including Nuke, Tweak RV, IfranView, and Adobe Premiere with the ProEXR plugin.

![exr export details](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5ca14fa1-7eca-4de7-87fb-45be49a375a2/exrdetails.png)

Currently, EXR output supports the following compression settings:

| EXR | Description |
| --- | --- |
| **None** | Applies no compression to the render output for the .exr sequence. |
| **PIZ** | A lossless compression format that provides good quality for grainy images. |
| **ZIP** | A lossless compression format that provides good quality for images with low amounts of noise. |

Unreal also supports the use of **Multilayer** .exr output. If you enable multiple different **[Render Passes](/documentation/en-us/unreal-engine/cinematic-render-passes-in-unreal-engine)**, each of them will be embedded into your .exr sequence, and they will all be separately accessible in your external visual effects editing program.

Not all software supports multi-layered .exr files. In these cases, they will only show the default RGBA channels when you load the .exr. If you are using a program that does not support multi-layered .exrs, you can uncheck the **Multilayer** setting to write out each layer as an individual .exr file.

## Apple ProRes Video Codecs

Apple ProRes is Apple's high-quality, lossy video compression format for post-production and visual effects, which supports up to 8k video.

To use it, you must enable it's plugin. Navigate in the Unreal Engine menu to **Edit > Plugins**, locate **Apple ProRes Media** in the **Media Players** section, and enable it. You will need to restart the editor afterward. ![apple prores plugin](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b647df98-4e13-47a5-9caa-fa5bfc02ed4f/appleplugin.png)

**Apple ProRes \[10-12bit\]** will now be available in the **Settings** menu. When you select this output format, your render will output a video file using one of several codecs, each providing a different level of compression and quality. The video container will be **.mov**.

![render apple prores details](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/17820a35-4d81-4422-bd54-b56c746789c3/appledetails.png)

Click the **Codec** dropdown to select your desired codec for the output video file. The following codecs are available:

| Codec | Pixel depth | Estimated Bitrate at 1080p and 30 fps | Description |
| --- | --- | --- | --- |
| **Apple ProRes 422 Proxy** | 10 bit | 45 mbps | Highest compression. Intended for use in offline workflows that require low data rates but full-resolution video. |
| **Apple ProRes 422 LT** | 10 bit | 100 mbps | A more compressed version of Apple ProRes 422, estimated at roughly 30% smaller file size. Intended for environments with limited storage and data rate. |
| **Apple ProRes 422** | 10 bit | 150 mbps | High quality compression for full-width 4:2:2 video sources. Intended for multistream, real-time editing. |
| **Apple ProRes 422 HQ** | 10 bit | 220 mbps | A higher bit-rate version of Apple ProRes 422. Offers the same level of quality as ProRes 4444, but for 4:2:2 video sources. |
| **Apple ProRes 4444** | 12 bit | 330 mbps | High-quality compression format for 4:4:4:4 image sources. Provides an extremely high-quality image and supports alpha channels. Output files are very large. |
| **Apple ProRes 4444 XQ** | 12 bit | 500 mbps | Highest-quality storage with support for alpha channels. 12 bits of precision for RGB channels and 16 bits for alpha. Output files are extremely large. |

For more information about each of these codecs, see **[Apple's documentation on Apple ProRes](https://support.apple.com/en-us/HT202410)**.

The **Drop Frame Timecode** setting will set the timecode track to use the drop-frame format. This is only applicable if your sequence has a framerate of 29.97.

If you enable **Override Maximum Encoding Threads**, you can set the **Max Number of Encoding Threads** to a manual number. This sets the maximum number of CPU threads that you want to allow the codec to use in the encoding process for the video file. Using more threads will make encoding faster, but will result in a higher CPU usage.

Apple ProRes does not export any audio. Add a **.wav Audio** export setting to output a separate .wav file alongside your video so that you can combine them in post-production.

## Avid DNx Video Codecs

Avid DNxHR and DNxMXF are Avid's high-definition lossy video codecs for post-production, which support up to 8k video.

To use them, you must enable their plugin. Navigate in the Unreal Engine menu to **Edit > Plugins**, locate **Avid DNxHR/DNxMXF Media Plugin** in the **Media Players** section, and enable it. You will need to restart the editor afterward.

![avid dnx plugin](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/da00385f-e96a-443a-98ee-9203ef323a4c/avidplugin.png)

**Avid DNx \[8bit\]** will now be available as an output setting. When you select this setting, it will output your movie as a video file using Avid's DNx codec. The video container will be **.mxf**.

![render avid dnx details](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7c5ec9e6-f6ba-46a9-9bbd-510816dceeda/aviddetails.png)

Enabling **Use Compression** will output a lossy, compressed file, while disabling it will output a lossless, uncompressed file. You can change the **Number of Encoding Threads** to control how many CPU threads you want the codec to use for encoding. Using a higher number of threads will decrease the amount of time required to encode the file, but will result in a higher CPU usage.

Refer to **[Avid's documentation on the DNx video codecs](https://www.avid.com/products/avid-high-resolution-workflows)** for more information regarding this codec and its specifications.

Avid DNx does not export any audio. Add a **.wav Audio** export setting to output a separate .wav file alongside your video so that you can combine them in post-production. At this time, Avid DNx only supports 8-bit precision regardless of codec.

## Final Cut Pro XML

The Final Cut Pro XML format will output an XML file that can be read by Final Cut Pro and other video editors that support this format. Similar to Command Line Encoder, you are also required to specify an accompanying image sequence or video file output along side this export format.

![render xml details](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3abf615f-4293-432e-b64c-2ff11e1b9862/xmldetails.png)

Use the **File Name Format Override** field to specify a **{token}** for the name of your output files. These tokens are based on the ones from your **Output** settings.

The **Data Source** dropdown menu specifies the method for building the Final Cut Pro XML file, which in turn decides what data is embedded in the file and how it will be formatted.

| Data Source | Description |
| --- | --- |
| **Output Metadata** | Builds the XML file based on the files that were actually written to disk, instead of based on the original Level Sequence data. This will support time dilation tracks (which will cause shots to have more/less frames than the actual Shot section in Sequencer) and does not support being reimported back into Sequencer later. |
| **Sequence Data** | Builds the XML file directly from sequence data. Intended for use in re-importing. |

Final Cut XML is only supported as an output format for Unreal Editor. It is not available for use in shipping builds, as it depends on editor-only functionality.

## WAV Audio

You can export .wav audio of your sequences without needing an additional rendering pass. This enables you to output a movie's audio and combine it with your image sequences in post-production.

![export wav audio details](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fa06047b-8bc7-4852-ac5e-87cb6b83cc0f/wavdetails.png)

Use the **File Name Format Override** field to override the **File Name Format** from the **Output** setting for the exported .wav file.

The WAV Audio output format is experimental and may not be production ready. Because the movie renderer runs the engine between shots for warmup frames, audio that is not controlled by Sequencer will have gaps between shots. Additionally, there may be minor audio distortion on audio clips in Sequencer between shots.

## Custom Output Formats

You can create your own format by implementing the **UMoviePipelineOutputBase** class, which gives you a callback for each output frame containing all render passes rendered in that frame (such as burn-ins, UI widgets, and the final image). By implementing the class in your project's code, it will automatically show up in the Settings menu for use. You will need to link against the MovieRenderPipelineCore module.

If you want to ensure this output format is added to every new job created with the UI, you can adjust the **Default Job Setting Classes** specified in the Movie Render Pipeline Project settings.

## Prestreaming Recorder

The Prestreaming Recorder option is only available if you have enabled the **Cinematic Prestreaming** [Plugin](/documentation/en-us/unreal-engine/working-with-plugins-in-unreal-engine) and is used to create render caches for cinematics using [Virtual Textures](/documentation/en-us/unreal-engine/virtual-texturing-in-unreal-engine) and [Nanite](/documentation/en-us/unreal-engine/nanite-virtualized-geometry-in-unreal-engine).

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0173d6b8-275e-4ed8-ab75-1b41d6d6ed9c/prestreaming1.png)

Due to how Virtual Textures and Nanite stream their data, you must first render using the **Prestreaming Recorder** to build a cache for the Cinematic Prestreaming system to interpret. This cache automatically saves and gets referenced within the sequence being rendered. With it, Sequencer uses this data to inform the Virtual Texture and Nanite systems which content is required for a frame before it is needed, allowing the required data to already be on the GPU when the frame is rendered. Without it, Nanite and Virtual Textures will have a delay between being shown and reaching their target quality, potentially causing lower resolution or quality on textures and geometry during a cinematic.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1c1a8e66-d5c4-4e0e-87e7-ae453bdd0905/prestreaming2.png)

Building a prestreaming cache isn't only for MRQ renders. The Cinematic Presteaming track and its data cache can also inform streaming of Virtual Textures in real-time sequences. This requires your real-time cinematics to be mostly deterministic, as the cache only contains data for what was rendered at that time. When the cache has no data available, it reverts back to the regular runtime latency seen in these systems.

The Prestreaming Recorder contains the following properties:

| Data Source | Description |
| --- | --- |
| **Package Directory** | 
The directory, relative to your project root folder, to save the Cinematic Prestreaming data cache. This must start with `/Game/`, and it can also use normal [format strings](/documentation/en-us/unreal-engine/cinematic-rendering-image-quality-settings-in-unreal-engine#formatstringinformation).

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a1c3f967-b488-480d-929e-8ac2cf5e2849/prestreaming3.png)

 |
| **Virtual Textures** | Enables capture of Virtual Texture page requests. Disabling this prevents any Virtual Textures information from being gathered to build the Cinematic Prestreaming cache. |
| **Nanite** | Enables capture of Nanite requests. Disabling this prevents any Nanite information from being gathered to build the Cinematic Prestreaming cache. |
| **Modify Target Sequence** | Enables the Cinematic Prestreaming Recorder to automatically add the cache playback data to the Level Sequence after the render completes. |
| **Disable Advance Render Features** | 

If enabled, this disables several rendering features, such as lighting, post processing, reflections. Disabling these can speed up your render, but causes the actual output render images to be very basic and unusable.

It can be useful to enable this, since the primary purpose of the Prestreaming Recorder is to build the **Cinematic Prestreaming cache**, not render.



 |

Nanite and Virtual Textures are screen resolution dependent, which means you must render your cinematic with the Prestreaming Recorder at your target resolution to generate accurate cache data. It will also need to be re-rendered if your content changes drastically, such as the transforms of objects, edits to materials, or other changes.

You can also add the [VT Pending Mips (Debug)](/documentation/en-us/unreal-engine/cinematic-render-passes-in-unreal-engine#vtpendingmips) render pass, which exports additional frames to your output directory. These frames can be used to debug Virtual Texture mip information.