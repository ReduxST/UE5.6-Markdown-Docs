# Containers Quick Start

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/quick-start-guide-for-using-container-images-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/quick-start-guide-for-using-container-images-in-unreal-engine)  
**Processed:** 2025-06-14 16:45:30

---

The Containers Quick Start is designed to help you access the official container images for Unreal Engine and use them to run a simple container. This guide will walk you through the following tasks:

-   Install Docker on your computer.
    
-   Log in to GitHub Container Registry so that you can use Docker to download prebuilt Unreal Engine container images.
    
-   Download the prebuilt Linux development container image for Unreal Engine.
    
-   Start a container using the development image.
    
-   Build and package a project inside the container.
    

## 1\. Requirements

To run the Unreal Engine container image for this Quick Start, your computer will need to meet the hardware and software requirements listed in the Linux containers section of the [Hardware and Software Requirements](/documentation/en-us/unreal-engine/hardware-and-software-requirements-for-container-deployments-in-unreal-engine) page.

## 2\. Verifying GitHub Access

Verify that you can access the Unreal Engine source code repository on GitHub: [https://github.com/EpicGames/UnrealEngine](https://github.com/EpicGames/UnrealEngine). If you cannot access the repository then you will need to [link your GitHub account with your Epic Games Account](https://www.unrealengine.com/en-US/ue-on-github).

## 3\. Installing Docker

Docker is the recommended tool for building and running the container images that are included with Unreal Engine. The steps for installing Docker will depend on the operating system that you are using. The links below provide instructions on how to do this on each platform it is available on:

-   **Windows:** [Install Docker Desktop for Windows](https://docs.docker.com/docker-for-windows/install/)
    
-   **macOS:** [Install Docker Desktop for Mac](https://docs.docker.com/docker-for-mac/install/)
    
-   **Linux:** Follow the appropriate instructions to install Docker Engine for your specific Linux distribution:
    
    -   [CentOS](https://docs.docker.com/engine/install/centos/)
        
    -   [Debian](https://docs.docker.com/engine/install/debian/)
        
    -   [Fedora](https://docs.docker.com/engine/install/fedora/)
        
    -   [Ubuntu](https://docs.docker.com/engine/install/ubuntu/)
        
    -   [Other Linux distributions](https://docs.docker.com/engine/install/binaries/)
        

## 4\. Authenticating with GitHub Container Registry

To download container images from GitHub Container Registry using Docker you will need to authenticate using a personal access token. If you do not already have a personal access token with the `read:packages` scope then you will need to [follow the steps to create one](https://docs.github.com/en/github/authenticating-to-github/keeping-your-account-and-data-secure/creating-a-personal-access-token).

Once you have created a personal access token with the required scope, use the `docker login` command to authenticate with GitHub Container Registry as described in the [instructions from GitHub](https://docs.github.com/en/packages/working-with-a-github-packages-registry/working-with-the-container-registry#authenticating-to-the-container-registry). This command will need to be run from the command-line interface, which is accessed differently depending on the operating system that you are using.

-   **Windows:** Open the Start menu and type "cmd" in the search box. The application "Command Prompt" should be displayed as the first search result. Open the Command Prompt by either clicking on it or pressing the Enter key.
    
-   **macOS:** Open Spotlight search by pressing Command + Space and type "terminal" in the search box. The application "Terminal" should be displayed as the first search result. Open the Terminal by either clicking on it or pressing the Enter key.
    
-   **Linux:** Open the search feature of your desktop environment (typically accessed by pressing the Super key) and type "terminal" in the search box. A terminal application should be displayed as the first search result. Open the terminal by either clicking on it or pressing the Enter key.
    

Once you have opened the command-line prompt then run the command shown below, replacing `ACCESS_TOKEN` with your personal access token and `USERNAME` with your GitHub username:

```
	`echo ACCESS_TOKEN | docker login ghcr.io -u USERNAME --password-stdin`
Copy full snippet
```
echo ACCESS\_TOKEN | docker login ghcr.io -u USERNAME --password-stdin

If the authentication process was successful then you should see the message *"Login Succeeded"* displayed.

## 5\. Pulling Prebuilt Container Images

The official prebuilt container images for Unreal Engine are stored as image tags in the [ghcr.io/epicgames/unreal-engine](https://ghcr.io/epicgames/unreal-engine) repository. To download the Linux development image for Unreal Engine 4.27, use the `docker pull` command shown below:

```
	`docker pull ghcr.io/epicgames/unreal-engine:dev-4.27`
Copy full snippet
```
docker pull ghcr.io/epicgames/unreal-engine:dev-4.27

This will download a container image that encapsulates the files for Unreal Editor and build tools, which are quite large. Depending on the speed of your internet connection, the download process may take some time. When the download is complete, you should see the message *"Status: Downloaded newer image for ghcr.io/epicgames/unreal-engine:dev-4.27"* displayed.

## 6\. Building a Project in a Development Container

If you do not have an Unreal Engine project available for testing purposes then you will need to [follow the steps to create a new project](/documentation/en-us/unreal-engine/creating-a-new-project-in-unreal-engine). You can use any project to test the development container image so long as that project does not use any code plugins which are incompatible with Linux.

Open a command-line prompt and run the command shown below to start a new container using the development image, replacing `PROJECT_PATH` with the path to the directory that contains the `.uproject` file for your project:

```
	`docker run --rm -ti -v "PROJECT_PATH:/project" ghcr.io/epicgames/unreal-engine:dev-4.27`
Copy full snippet
```
docker run --rm -ti -v "PROJECT\_PATH:/project" ghcr.io/epicgames/unreal-engine:dev-4.27

This will start a container with access to the files for your project. Since the container is running Linux, it can be used to build and package the project for Linux devices. To package the project, run the command shown below, replacing `PROJECT_NAME` with the name of your project:

```
	`/home/ue4/UnrealEngine/Engine/Build/BatchFiles/RunUAT.sh \ 	BuildCookRun \ 	-utf8output \ 	-platform=Linux \ 	-clientconfig=Shipping \ 	-serverconfig=Shipping \ 	-project=/project/PROJECT_NAME.uproject \ 	-noP4 -nodebuginfo -allmaps \ 	-cook -build -stage -prereqs -pak -archive \ 	-archivedirectory=/project/Packaged`
Copy full snippet
```
/home/ue4/UnrealEngine/Engine/Build/BatchFiles/RunUAT.sh \\ BuildCookRun \\ -utf8output \\ -platform=Linux \\ -clientconfig=Shipping \\ -serverconfig=Shipping \\ -project=/project/PROJECT\_NAME.uproject \\ -noP4 -nodebuginfo -allmaps \\ -cook -build -stage -prereqs -pak -archive \\ -archivedirectory=/project/Packaged

The C++ code modules for the project will be compiled, if the project is not a Blueprint-only project, and the project's assets will then be cooked and packaged. The packaged files will be placed in a subdirectory called `Packaged` inside the directory that contains the `.uproject` file.

To stop the container, run the command shown below:

```
	`exit`
Copy full snippet
```
exit

## Next Steps

Now that you are familiar with the basics of working with prebuilt container images, you can continue learning more about using Unreal Engine containers with the following resources:

-   In addition to downloading prebuilt container images, all images that are included with Unreal Engine can also be customized and built from source:
    
    -   How-To: [Building the Linux Container Images from Source](/documentation/en-us/unreal-engine/building-the-linux-container-images-from-source)
        
    -   How-To: [Building the Windows Container Images from Source](/documentation/en-us/unreal-engine/building-the-windows-container-images-from-source)
        
-   If you're unsure whether you need a development image or a runtime image, take a look at the interactive [Quickstart Guide](https://unrealcontainers.com/docs/preliminaries/quickstart) on the Unreal Containers community hub.
    
-   Explore the [list of use cases](https://unrealcontainers.com/docs/use-cases/) that can benefit from Unreal Engine containers.