# Containers Overview

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/overview-of-containers-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/overview-of-containers-in-unreal-engine)  
**Processed:** 2025-06-14 16:40:54

---

Support for **containers** expands **Unreal Engine's** capabilities to support new cloud-based development workflows and deployment strategies. Unreal Engine containers can be used to enhance production pipelines, develop next-generation cloud applications, deploy enterprise solutions at unprecedented scale, and much more.

Although official support for containers in Unreal Engine is still a Beta feature, it is built upon the pre-existing open source infrastructure developed by [TensorWorks](https://tensorworks.com.au/) and the [Unreal Containers](https://unrealcontainers.com/) community initiative, which is already in production use by developers around the world today.

## Understanding Containers and Container Images

As described by the [What is a Container?](https://www.docker.com/resources/what-container) page on the Docker website, containers are a technology designed to package applications and their supporting dependencies into a single standard unit that is portable across computing infrastructure, both on-premises and in the cloud.

In a similar manner to virtual machines, containers are stored on disk as a **container image**, from which one or more containers can be run. Unlike virtual machines, containers share a single underlying operating system kernel and can share common data across separate container images. This makes them computationally lightweight and facilitates a larger number of concurrent deployments.

If you would like to learn more about containers, take a look at some of the resources available from various cloud providers:

-   [IBM: What are Containers](https://www.ibm.com/cloud/learn/containers)
-   [Red Hat: A Practical Introduction to Container Terminology](https://developers.redhat.com/blog/2018/02/22/container-terminology-practical-introduction)

## Development and Runtime Container Images

There are two types of container images that are included in Unreal Engine: **development images** and **runtime images**.

**Development images** contain the Unreal Editor and build tools. They are used for tasks that require the editor, such as building and packaging Unreal Engine projects and plugins, rendering cinematics created using [Sequencer](/documentation/en-us/unreal-engine/unreal-engine-sequencer-movie-tool-overview), or running commandlets. Distribution of development images is governed by the terms of the [Unreal Engine EULA](https://www.unrealengine.com/en-US/eula/publishing).

**Runtime images** contain only the dependencies required to run packaged Unreal Engine projects. Developers extend runtime images by adding files for their packaged Unreal Engine projects, and creating new container images that can be deployed to cloud environments. Since runtime images do not contain the editor or build tools, their distribution is less restricted than development images.

For a more detailed explanation of the differences between development images and runtime images, see the [Development images .vs. runtime images](https://unrealcontainers.com/docs/concepts/image-types) documentation page on the Unreal Containers community hub website.

## Available Container Images

Starting with Unreal Engine 4.27, official development and runtime container images are included with each Engine release. The source code for these container images can be found in the `Engine/Extras/Containers` directory of the Unreal Engine source code, which you can download from GitHub, or from Perforce if you are an Unreal Engine licensee. Prebuilt versions of all container images are published to [GitHub Container Registry](https://docs.github.com/en/packages/working-with-a-github-packages-registry/working-with-the-container-registry) and can be downloaded without requiring you to build them from source.

The following development images are provided:

| Development Image Type | Description |
| --- | --- |
| **dev** | This is the full Linux development image for Unreal Engine, which includes an Installed Build of Unreal Engine, template projects, and full debug symbols. |
| **dev-slim** | This is a smaller version of the Linux development image that excludes template projects and debug symbols. |

The following runtime images are provided:

| Runtime Image Type | Description |
| --- | --- |
| **runtime** | 
This is the streamlined Linux runtime image for running packaged Unreal Engine applications inside containers, with or without GPU acceleration. To minimize the image's size, this image does not include support for audio output.

This container image currently only supports GPU acceleration on machines using NVIDIA GPUs.



 |
| **runtime-pixel-streaming** | 

This image extends the streamlined Linux runtime image to add the dependencies required for Pixel Streaming applications, including support for audio output. As a result, this image is noticeably larger than the default runtime image, although it is still far smaller than the Windows runtime image.

This container image currently only supports GPU acceleration with NVIDIA GPUs.



 |
| **runtime-windows** | 

This is the Windows runtime image for running packaged Unreal Engine applications inside containers, with or without GPU acceleration. Since Windows container images are already significantly larger than their Linux counterparts, and the dependencies required for Pixel Streaming applications are relatively small compared to the size of the Windows operating system itself, this image includes those dependencies as well.

Support for running Pixel Streaming applications inside GPU accelerated Windows containers is experimental and is not recommended for production use.



 |

In addition to the development and runtime images, the following images are provided for specific use cases such as Pixel Streaming:

| Special Image Type | Description |
| --- | --- |
| **pixel-streaming-signalling-server** | This is a Linux container image that includes the Cirrus signalling and web server used by the Pixel Streaming system. |
| **multi-user-server** | This is a Linux container image that includes the server used by Unreal Engine's Multi-User Editing system. |

## Limitations

Official support for containers in Unreal Engine is still in Beta and is subject to a number of limitations. See the [Known Limitations](/documentation/en-us/unreal-engine/known-limitations-of-containers-in-unreal-engine) page for details.

## Available Resources

In addition to the official documentation for container support in Unreal Engine, the following resources are available:

-   The [Unreal Containers community hub](https://unrealcontainers.com/) maintains extensive written documentation with links to related videos and source code repositories. The community hub website is accompanied by a Discord server for community discussions about the use and development of Unreal Engine containers.