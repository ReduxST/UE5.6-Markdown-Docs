# Wine-Enabled Containers Quick Start

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/wine-enabled-containers-quick-start-for-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/wine-enabled-containers-quick-start-for-unreal-engine)  
**Processed:** 2025-06-14 17:04:27

---

## Prerequisite Topics

In order to understand and use the content on this page, make sure you are familiar with the following topics:

-   [Installing Unreal Engine](/documentation/404)
-   [Building container images](https://docs.docker.com/get-started/docker-concepts/building-images/)
-   [Running containers](https://docs.docker.com/engine/containers/run/)
-   Using [Unreal Automation Tool](/documentation/en-us/unreal-engine/unreal-automation-tool-for-unreal-engine)

This Quick Start is designed to help you build Wine-enabled container images for use with the Unreal Engine, capable of running Windows development and cloud deployment workflows on Linux. The following topics will be covered in this guide:

-   Installing Docker on your computer.
-   Downloading the Wine Resources repository which contains scripts for building Wine-enabled container images.
-   Building a Linux container image that includes both Unreal Engine and Wine for running Windows workloads.

The container image built by following these instructions does not include a C++ compiler toolchain. As a result, it cannot be used to package Unreal Engine projects that include C++ code. The container image can be used to package projects that contain only Blueprint scripts.

## Requirements

To build and run the Wine container image for this Quick Start, your computer will need to meet the hardware and software requirements listed in the Linux containers section of the [Hardware and Software Requirements](/documentation/en-us/unreal-engine/hardware-and-software-requirements-for-wine-containers-for-unreal-engine) page.

Additionally, you will need the following software installed on your computer to follow this guide:

-   Docker with Docker Engine version 23.0.0 or newer. See [Installing Docker](/documentation/en-us/unreal-engine/wine-enabled-containers-quick-start-for-unreal-engine#installingdocker) below.
-   Python version 3.7 or newer. Visit [python.org](https://www.python.org/) to download and install Python.

## Installing Docker

Docker is the recommended tool for building and running container images with Wine and Unreal Engine. The steps for installing Docker will depend on the operating system that you are using. The links below provide instructions on how to do this on each platform it is available on:

-   Windows: [Install Docker Desktop on Windows](https://docs.docker.com/desktop/setup/install/windows-install/)
-   macOS: [Install Docker Desktop on Mac](https://docs.docker.com/desktop/setup/install/mac-install/)
-   Linux: Follow the appropriate instructions to install Docker Engine for your specific Linux distribution:
    -   [CentOS](https://docs.docker.com/engine/install/centos/)
    -   [Debian](https://docs.docker.com/engine/install/debian/)
    -   [Fedora](https://docs.docker.com/engine/install/fedora/)
    -   [Ubuntu](https://docs.docker.com/engine/install/ubuntu/)
    -   [Other Linux distributions](https://docs.docker.com/engine/install/binaries/)

## Download the Wine Resources Repository

Epic Games provides resources for building container images that encapsulate Wine with patches that improve compatibility for Unreal Engine workloads. These resources are publicly available on GitHub for use by Unreal Engine licensees.

Download the Wine Resources repository from [github.com/EpicGamesExt/WineResources](https://github.com/EpicGamesExt/WineResources) to your computer. If you have Git installed, you can simply clone the repository to a local directory. Alternatively, you can download a ZIP archive from the **Code** dropdown menu by selecting **Download ZIP**. When the download is complete, extract the the files to a local directory.

## Build the Wine Base Image

Open a Command Prompt (or Terminal) window and change your working directory to `WineResources/build`.

Run the appropriate wrapper script depending on the operating system:

-   Under Linux and macOS, run `./build.sh`
-   Under Windows, run `.\build.bat`

The wrapper script will automatically install the Python packages that the build script depends upon, and then run the Python build script itself. The Python build script will build the base image that contains the patched version of Wine. Once the build completes, the container image will be available with the tag `epicgames/wine-patched:9.0.0`.

To test the base image, run a container which prints the built version of Wine:

```shell
`docker run --rm "epicgames/wine-patched:9.0.0" wine --version`
Copy full snippet
```
docker run --rm "epicgames/wine-patched:9.0.0" wine --version

## Copy Unreal Engine into the Wine Container Image

Now you are ready to create a new container image, based on the one you created in the previous step, which contains an Installed Build of Unreal Engine.

For this step you will require a copy of Unreal Engine for Windows. The recommended way to obtain the required files is to download Unreal Engine using the [Epic Games Launcher](https://store.epicgames.com/en-US/download) on a Windows machine, by following the [official installation instructions](/documentation/404).

Copy the contents of Unreal Engine's root directory (which includes `Engine/`) to the `WineResources/examples/quickstart/wrap-installed-build/context/UnrealEngine/` directory.

When copying the Installed Build files under Windows, you may encounter an error if any of the destination file paths exceed the [maximum path length limit](https://learn.microsoft.com/en-us/windows/win32/fileio/maximum-file-path-limitation). To avoid this, either ensure the destination directory has a short path (for example, by storing the local copy of the Wine Resources repository in the root of a drive, such as `C:\WineResources`), or follow Microsoft's [instructions to enable long path support](https://learn.microsoft.com/en-us/windows/win32/fileio/maximum-file-path-limitation?#enable-long-paths-in-windows-10-version-1607-and-later).

Open a Command Prompt (or Terminal) window and change your working directory to `WineResources/examples/quickstart/wrap-installed-build/`. To build a new container image that includes both Wine and Unreal Engine, run the appropriate wrapper script depending on the operating system:

-   Under Linux and macOS, run `./build.sh`
-   Under Windows, run `.\build.bat`

The wrapper script will run the Python build script itself, using the appropriate commands for the operating system. The Python build script will verify that the Installed Build files have been copied to the correct location, and will then automatically detect the version of Unreal Engine that the files represent. The script will then build the container image.

Once the build completes, the container image will be available with the tag `epicgames/unreal-engine:dev-wine-blueprintonly-<VERSION>`, where `<VERSION>` is the version of Unreal Engine that the container image was built for.

The Dockerfile step that copies the Installed Build files into the container image may take a long time to complete (that is, over an hour on many systems, and potentially multiple hours under Windows when using Docker Desktop with WSL2). There is no output to indicate the progress of the copy operation, so it may appear to have frozen, but this is almost certainly not the case and you will simply need to wait for it to complete.

## Use the Wine-Enabled Unreal Engine Container Image

With the Wine-enabled Unreal Engine container image created, you can now package Unreal Engine projects for Windows. As noted above, the container image does not currently support packaging projects that include C++ code, so the image can only be used to package projects that contain Blueprint scripts.

The code below demonstrates how to package a project using Unreal Automation Tool in a Wine image built for Unreal Engine 5.5.0:

Replace `<PATH_TO_PROJECT>` with the path to the directory that contains the Unreal Engine project that you want to package (this is the directory that contains the `.uproject` file). Replace `<UPROJECT_FILE>` with the name of the `.uproject` file.

Choose your operating system

Windows macOS Linux

```
`docker run --rm -v "<PATH_TO_PROJECT>:/project" ^ "epicgames/unreal-engine:dev-wine-blueprintonly-5.5.0" ^     /bin/sh -c "wine ^     C:/UnrealEngine/Engine/Build/BatchFiles/RunUAT.bat ^     BuildCookRun ^     -noP4 -allmaps -build -cook -stage -pak ^     -project='Z:/project/<UPROJECT_FILE>' ^     -platform=Win64 ^     -clientconfig=Development ^     -archive -archivedirectory='Z:/project/archive'"`
Copy full snippet
```
docker run --rm -v "<PATH\_TO\_PROJECT>:/project" ^ "epicgames/unreal-engine:dev-wine-blueprintonly-5.5.0" ^ /bin/sh -c "wine ^ C:/UnrealEngine/Engine/Build/BatchFiles/RunUAT.bat ^ BuildCookRun ^ -noP4 -allmaps -build -cook -stage -pak ^ -project='Z:/project/<UPROJECT\_FILE>' ^ -platform=Win64 ^ -clientconfig=Development ^ -archive -archivedirectory='Z:/project/archive'"

If you are running the command in a PowerShell window rather than a Command Prompt window then you will need to replace the caret escape characters (`^`) at the end of each line with backtick escape characters instead (\`).

```
`docker run --rm -v "<PATH_TO_PROJECT>:/project" \ "epicgames/unreal-engine:dev-wine-blueprintonly-5.5.0" \     /bin/sh -c "wine \     C:/UnrealEngine/Engine/Build/BatchFiles/RunUAT.bat \     BuildCookRun \     -noP4 -allmaps -build -cook -stage -pak \     -project='Z:/project/<UPROJECT_FILE>' \     -platform=Win64 \     -clientconfig=Development \     -archive -archivedirectory='Z:/project/archive'"`
Copy full snippet
```
docker run --rm -v "<PATH\_TO\_PROJECT>:/project" \\ "epicgames/unreal-engine:dev-wine-blueprintonly-5.5.0" \\ /bin/sh -c "wine \\ C:/UnrealEngine/Engine/Build/BatchFiles/RunUAT.bat \\ BuildCookRun \\ -noP4 -allmaps -build -cook -stage -pak \\ -project='Z:/project/<UPROJECT\_FILE>' \\ -platform=Win64 \\ -clientconfig=Development \\ -archive -archivedirectory='Z:/project/archive'"

```
`docker run --rm -v "<PATH_TO_PROJECT>:/project" \ "epicgames/unreal-engine:dev-wine-blueprintonly-5.5.0" \     /bin/sh -c "wine \     C:/UnrealEngine/Engine/Build/BatchFiles/RunUAT.bat \     BuildCookRun \     -noP4 -allmaps -build -cook -stage -pak \     -project='Z:/project/<UPROJECT_FILE>' \     -platform=Win64 \     -clientconfig=Development \     -archive -archivedirectory='Z:/project/archive'"`
Copy full snippet
```
docker run --rm -v "<PATH\_TO\_PROJECT>:/project" \\ "epicgames/unreal-engine:dev-wine-blueprintonly-5.5.0" \\ /bin/sh -c "wine \\ C:/UnrealEngine/Engine/Build/BatchFiles/RunUAT.bat \\ BuildCookRun \\ -noP4 -allmaps -build -cook -stage -pak \\ -project='Z:/project/<UPROJECT\_FILE>' \\ -platform=Win64 \\ -clientconfig=Development \\ -archive -archivedirectory='Z:/project/archive'"