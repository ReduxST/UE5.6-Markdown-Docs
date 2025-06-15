# GPUDump Viewer Tool

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/gpudump-viewer-tool-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/gpudump-viewer-tool-in-unreal-engine)  
**Processed:** 2025-06-14 16:26:15

---

**DumpGPU** is a platform-agnostic console command that dumps the intermediary rendering resource binaries of a captured frame to disk. The dump is stored with .json and .bin files that can then be browsed using a lightweight webpage viewer.

![gpu dump viewer](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5ee66270-b67e-4ae6-9405-c8aba15d6e91/gpu-dump-viewer.png)

This command serves several purposes:

-   It is available for all builds without the need to install a third party GPU debugging tool or restart the editor.
-   Dumps can come from any supported platforms:
-   Windows D3D11, D3D12, Vulkan
-   Linux Vulkan
-   Mac Metal, AGX
-   PlayStation 4 and PlayStation 5
-   XboxOne, Xbox Series X/S
-   Nintendo Switch
-   iOS and Android
-   The interface is browsable from any platform that supports Chrome and a WebGL 2.0-capable GPU.
-   Simple and platform-agnostic, which enables anyone to produce a GPU dump when encountering an artifact.
-   Ideal for artists that run into unexpected and hard-to-reproduce problems while working in the editor.
-   Minimizes frictions of browsing a resources binary.
-   Platform GPU captures often require the correct SDK, and a dev kit to be able to analyze the resource. The GPUDump viewer enables developers to better triage bugs, but also to look at resources from any platforms with the required context of an issue.
-   For graphics programmers writing new renderer functionality, this tool provides a faster iterative workflow for analyzing what may be happening.

## Dumping Process

To initiate the process of creating a GPU dump of the frame, enter the command `DumpGPU` into the console window, or use the keyboard shortcut **CTRL + Shift + /**.

Once the command is initiated, it needs to copy the intermediary rendering resources to disk. To handle this, capture speed is traded for memory to limit out of memory failures from occurring. This ensures that the dump can reliably gather data of artifacts that are rare or difficult to reproduce without crashing a process that was able to reproduce it.

The amount of persistent memory needed for a dump to know whether a resource has been already dumped or not is negligible.

If the amount of memory required to dump a resource is larger than the available memory in the system, the resource will not be dumped. Instead, a warning is placed in the log.

The `DumpGPU` command is available on **Debug**, **DebugGame**, **Development**, and **Test** builds, but it can be enabled on **Shipping** builds with the `Project.Target.cs`.

```
	`GlobalDefinitions.Add("ALLOW_CONSOLE_IN_SHIPPING=1"); 	GlobalDefinitions.Add("ALLOW_DUMPGPU_IN_SHIPPING=1");`

Copy full snippet
```
GlobalDefinitions.Add("ALLOW\_CONSOLE\_IN\_SHIPPING=1"); GlobalDefinitions.Add("ALLOW\_DUMPGPU\_IN\_SHIPPING=1");

These should be used for debugging testing purposes shipping only rendering problems and **should not** be enabled when actually shipping the project.

### Save Location of GPU Dumps

When a GPU dump is performed, it is stored in the project's root directory under the `Saved/GPUDumps` by default. On Desktop platforms, the file explorer will open a window to this dump location automatically on completion.

![gpu dump viewer windows file explorer](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/36e41aa0-906a-4d2e-ae93-5eaed0d89a2b/gpu-dump-viewer-file-explorer.png)

For **Staged** builds, they are saved in the Stage's Saved directory, with the path format: **\[Staged Directory\] / \[Platform Name\] / \[Project Name\] / Saved / GPUDumps**.

All dumps are uncompressed raw resources, which means they can take up a lot of disk space. However, it is highly compressible as a Zip file. For example, the Matrix: Awakens technical demo produced dumps that were approximately 8Gb uncompressed, and 2.2Gb once zipped.

Zipping dumps can be useful when sharing data with others.

#### Mobile Platform Dump Save Location

For Mobile platforms, the GPU dumps are saved in the following locations:

| Mobile Platform | Save Location File Path |
| --- | --- |
| **iOS** | `[Path to App Container]/Documents/[ProjectName]/Saved/GPUDumps/` |
| **Android** | 
`/storage/emulated/0/UnrealGame/[ProjectName]/[ProjectName]/Saved/GPUDumps/`

Stencil buffer will be empty on Android OpenGL.



 |

### Dump Settings

The GPU dumps created can be tailored to your needs with the following commands:

| Console Variable | Description |
| --- | --- |
| `r.DumpGPU.Root` | Selects a subset of Render Dependency Graph (RDG) passes to dump based on their draw events and the parent scopes they belong to. Enabling this can significantly speed up the dumping process by only dumping the passes you need when iterating on isolated rendering functionality. For example, to only dump post processing passes, enter `r.DumpGPU.Root="PostProcessing"`. |
| `r.DumpGPU.Viewer.Visualize` | Automatically opens a specific resource based on its name in the viewer. For example you would enter \`r.DumpGPU.Viewer.Visualize "" |
| `r.DumpGPU.Directory` | GPU dumps can take up large amounts of disk space. You can specify the directory to save all GPU dumps in a single location using this command in your `ConsoleVariables.ini` configuration file. You would specify the location like so, \`r.DumpGPU.Directory="\[X:/File/Path/Name\]". |

### How the DumpGPU Command Copies the GPUDumpViewer

The GPUDumpViewer source code is available with the engine source and can be found in `/Engine/Extras/GPUDumpViewer`.

On non-Shipping builds, the GPUDumpViewer is automatically copied into the staging directory. Then, when the DumpGPU command is called to dump the frame, the files are copied from the staged directory to the dumping directory.

If you have a Shipping staged build, the GPUDumpViewer's HTML source may not be copied into the dumping directory because it is missing in the staged directory. In this case, you can copy your repository's `//Engine/Extras/GPUDumpViewer` application into your dumping directory to open the dump.

## The GPU Dump Viewer

The GPU Dump Viewer is an HTML web-based application. From this viewer, you can access information about how the Unreal Engine renderer works.

To get started, once a GPU dump has occurred, the operating system will open the folder location of the saved dump. The viewer can be opened in Chrome by double-clicking the `OpenGPUDumpViewer.bat` file.

![windows file explorer gpudumpviewer bat file](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c43ba530-a55e-47f6-9355-45ad04d046a1/gpu-dump-viewer-file-explorer-bat-file.png)

Once initiated, a new Chrome window will open with the **GPUDumpViewer** running.

![gpu dump viewer](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/43ef720c-0152-44d9-a454-dc136c255854/gpu-dump-viewer.png)

GPUDumpViewer web application opens in a new Chrome Incognito window.

The GPUDumpViewer is a web application and functions similarly to any browser-based page or application. The following are some quick tips about working in the GPUDumpViewer:

-   Any link is clickable and can be opened in its own tab for quick access.
-   Navigation with the forward and back buttons will move between any previously viewed pages.
-   If sharing a capture with someone, you can share the link after the # part to link them directly to a panel and part of the dump. For example, `#display_output_resource(96,'0000000067e1bfa0.mip0');`

When you open GPUDumpViewer, you can cycle through a bunch of tips and tricks in the main viewing area.

![gpu dump viewer highlighted sections](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/eebae2cc-5858-4b87-90eb-0c11a903c011/gpu-dump-viewer-sections.png)

1.  Title Bar and Panels
2.  Pass and Resource Tree
3.  Viewer

### Title Bar and Panels

The main title bar provides quick reference information about the name of the project, operating system, RHI, and build that was used when the dump was created. It also includes clickable information panels for general information about the project, console variables used, and a copy of the project's log.

![gpu dump viewer title bar](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cb6066e4-d2e6-4f74-983c-20e94bad918a/gpu-dump-viewer-title-bar.png)

#### Infos Panel

The **Infos** panel contains a summary of the GPU Dump. You'll find useful information about the system, drivers, and engine build, along with a screenshot of the final image from the back buffer.

![gpu dump viewer infos panel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2eb702c1-e30e-4e0b-96a7-a7040413ad59/gpu-dump-viewer-infos-panel.png)

#### CVars Panel

The **CVars** panel includes a searchable list of any rendering console variables — ones that begin with `.r.*` or `.sg.*`, or contain the RHI keyword — that were run before the dump occured.

![gpu dump viewer cvars panel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/35fa84e6-ff09-4941-8fab-9b1f54a395ca/gpu-dump-viewer-cvars-panel.png)

Console variables are captured at the beginning of the frame. Therefore, some might be subject to changes if gameplay toggles cvars at runtime.

#### Log Panel

The **Log** panel provides a copy of the project's log, which gets saved along with the dump once the dump is completed. This is where you can also inspect whether there has been any warning issued in the dumping process.

![gpu dump viewer log panel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/160dbb48-2df6-4b66-8a33-1354c5771651/gpu-dump-viewer-log-panel.png)

### Viewers

The viewing area displays information about the different Passes, Textures, and Buffers when selected.

#### Pass Viewer

When clicking on a **Pass** in the draw event hierarchy, only the resources that the pass reads and modifies will be shown. It automatically opens up the first output resource, whether it's a texture or the buffer.

![gpu dump viewer pass viewer](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/aa92a76c-bbeb-41c5-84ba-b91d9ddda4d7/gpu-dump-viewer-pass-viewer.png)

Next to the pass name (at the top of the viewer), you will find the **Pass Parameters** button.

![gpu dump viewer pass parameters button](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d4c6f732-6350-43b1-b6b5-941dd7c11446/gpu-dump-viewer-pass-parameters.png)

Clicking this will display the raw pass parameters. More often than not, the pass parameters are shader parameters. For example, when `FComputerShaderUtils::AddPass()` or `FPixelShaderUtils::AddPass()` are used.

Pass Parameters enable you to verify that no instances of NaN from the CPU affects your shader through the shader parameters.

![gpu dump viewer pass parameters panel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7aa14227-25a1-44be-b1fe-b6516c4be2bf/gpu-dump-viewer-pass-parameters-panel.png)

#### Texture Viewer

When a **Texture** is selected in the Pass view's **Input Resources** or **Output Resources** list, you can visualize its pixels in the viewer.

![gpu dump viewer texture viewer](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/86da928c-229a-4431-823b-437c24d7da5e/gpu-dump-viewer-texture-viewer.png)

WebGL 2.0's canvas makes it possible to view textures by loading the raw resource binary (the RHI has copied into the dump's directory), and displaying it using a simpler WebGL pixel shader. For formats not supported by WebGL, such as 32 bit UINT textures, additional work behind the scenes is done to accurately simulate the pixel format.

The Texture Viewer includes several buttons along the top of the displayed texture:

![gpu dump viewer texture viewer buttons](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/30a5520d-5cda-4229-8e75-e37b9b255ddb/gpu-dump-viewer-texture-viewer-buttons.png)

-   Set the size of the texture being displayed in the viewer or simply fit it to the window.
-   Use **Copy to clipboard** to copy the currently displayed texture and relevant resource information to your clipboard. When you paste it into a text editor, or email, you should see something like this:
    
    ![copy to clipboard example](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/82047058-9f52-4383-9d70-8c3ba0e4abbd/gpu-dump-viewer-copy-to-clipboard-example.png)
-   There are three buttons to change the texture view mode: **Visualization** for standard texture view mode, or **NaN** (not a number) and **Inf** (infinity) viewing modes for identifying those types of pixel errors.

Hovering the mouse over the texture returns the current RGBA values of the cursor texel position. Left-clicking the mouse will capture and hold the texel RGBA position value.

The value displayed for the Cursor Texel Pos and Selected Texel Pos includes many more digits than the precision allowed by the pixel format encoding. This is because the webpage decodes the texel in javascript using [double precision floating point format](https://en.wikipedia.org/wiki/Double-precision_floating-point_format).

For parts of the texture you want to examine more closely, you can use the mouse wheel to zoom in and out of the texture. When zoomed in, you can right-click and drag to move around the texture.

![gpu dump viewer texture viewer texels selection](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b51e2768-d9c7-40bb-8ffd-a95f84ac4876/gpu-dump-viewer-texture-viewer-texels.png)

The area below the displayed texture provides key information about the texture and how it is being rendered.

![gpu dump viewer-texture-viewer-information panels](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/40cd4416-a3d6-4569-8023-cd40808fcd6f/gpu-dump-viewer-texture-viewer-infopanels.png)

1.  Texture Descriptor
2.  WebGL 2.0 visualization shader to customize
3.  Passes that modify the resource
4.  Passes that read the resource

##### Texture Descriptor

The **Texture Descriptor** displays information about the currently displayed texture. This is the one set up on `FRDGBuilder::CreateTexture()`.

![gpu dump viewer texture descriptor](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/063986ed-8fde-469f-9f77-77722400f1f5/gpu-dump-viewer-texture-descriptor.png)

At this time, the `DumpGPU` command only dumps `FRDGTexture` and only supports non-MSAA Texture2D. This includes depth, stencil, and mip levels. Texture2DArray, Texture2DMS, Texture3D, TextureCube, TextureCubeArray are metadata like HTILE, CMask & cie are not supported yet

##### WebGL 2.0 Visualization Shader

The **WebGL 2.0 Visualization Shader** displays the code fragment that gets compiled to display the texture in the top window. Below it, the compilation log window displays any compilation errors that may occur.

![gpu dump viewer webgl 2.0 visualization shader](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2f361f24-d6be-4116-9a14-b42cf43e6af2/gpu-dump-viewer-texture-webgl-glsl.png)

The WebGL 2.0 canvas window is an editable text box that can be used to write any WebGL 2.0 GLSL. It can be customized to visualize and decode the texture, like when your image is compressing multiple bits of information per channel, or using a different color space. Any code typed in this field will automatically recompile and display any errors.

The syntax for WebGL 2.0 shaders differs from those that Unreal Engine uses with its Unreal Shader Format (.*usf) and Unreal Shader Header (*.ush) files used to write internal rendering code with HLSL. A link to the [WebGL 2.0 quick reference card](https://www.khronos.org/files/webgl20-reference-guide.pdf) for GLSL syntax is linked at the bottom of the compilation window.

The `fetchTexel(uv)` is not standard GLSL. Instead, it is a custom function that automatically handles pixel formats that are not normally supported by WebGL2.0.

##### Passes being Modified and Read

At the very bottom are two windows, one for the Passes that are modifying the selected resource and Passes that are reading from the selected resource. In either Passes list, click on any Pass to display them in the viewer.

![gpu dump viewer modified and read passes panels](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/eeadd03a-78f4-47cc-993d-96bb10ef67d8/gpu-dump-viewer-texture-pass-modify-read.png)

#### Buffer Viewer

Once a texture is selected for viewing in the Pass **Input Resources** or **Output Resources** lists, the **Buffer** view will list its descriptor and visualization contents.

![gpu dump viewer buffer viewer](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c883d074-318a-4cd0-a154-69927977063d/gpu-dump-viewer-buffer-viewer.png)

The **Buffer Descriptor** lists general information about the selected resource, such as its name, size, description, usage, and more.

![gpu dump viewer buffer descriptor](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5383dd37-444a-431b-b371-d098db708f98/gpu-dump-viewer-buffer-descriptor.png)

The **Buffer Visualization** lists addresses in the buffer with decimal or 0x prefix hexadecimal values.

![gpu dump viewer buffer visualization](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0521556d-35a1-4183-97ab-f201e6836912/gpu-dump-viewer-buffer-visualization-panel.png)

Use the **Address** text field to jump to a specific address that is either decimal or with a 0x prefix.

![gpu dump viewer buffer visualization address search field](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5afd2d74-ad51-445b-aea6-2d4e1391d3d8/gpu-dump-viewer-buffer-visualization-panel-address.png)

The format of the list can be customized and supports the following:

-   Float, Half
-   Int, short, char
-   Uint, ushort, char
-   Hex(), or bin(), which displays any of the above formats in hexadecimal or binary.

Because the GPUDumpViewer doesn't know how the data should be interpreted, the buffer defaults to data visualization using the `hex(uint)` format unless it has the `DrawIndirect` usage flag, in which case the `Uint` format is used.

The templated `FRDGBufferDesc::Create*()` function can be used to create your `FRDGBuffer` with a shader parameter structure, making it more convienent to browse the buffer's content.

![gpu dump viewer create buffer code snippet](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ea29e80e-9542-4d40-8c49-573062a4e137/gpu-dump-viewer-create-buffer-code-snippet.png) ![gpu dump viewer create buffer in viewer](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4b98e781-11fa-457c-985f-61a14973cc37/gpu-dump-viewer-create-buffer-code-snippet-1.png) 

The buffer automatically switches to displaying members per-column instead of per-row when the descriptor `NumElements` is greater than 1.