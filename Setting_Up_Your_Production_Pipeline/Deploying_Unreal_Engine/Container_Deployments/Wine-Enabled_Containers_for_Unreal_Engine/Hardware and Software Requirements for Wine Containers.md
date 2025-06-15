# Hardware and Software Requirements for Wine Containers

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/hardware-and-software-requirements-for-wine-containers-for-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/hardware-and-software-requirements-for-wine-containers-for-unreal-engine)  
**Processed:** 2025-06-14 16:27:14

---

## Requirements for Linux Containers

You can build and run the Wine-enabled container images for Unreal Engine on Windows, macOS, or Linux. To build or run the container images, your computer will need to meet the following hardware requirements:

-   A 64-bit CPU with support for [Second Level Address Translation (SLAT)](https://en.wikipedia.org/wiki/Second_Level_Address_Translation).
-   Hardware virtualization support enabled in the system BIOS.
-   Minimum of 4 GB of system RAM.

Your computer will also need to meet the following software requirements:

-   Windows: A 64-bit Windows 10 Home, Pro, Enterprise, or Education, version 1903 or newer with Docker Desktop for Windows installed. See the [Installing Docker](/documentation/en-us/unreal-engine/hardware-and-software-requirements-for-wine-containers-for-unreal-engine#installingdocker) section below for instructions on how to install Docker Desktop for Windows.
-   macOS: macOS version 10.14 or newer with Docker Desktop for Mac installed. See the [Installing Docker](/documentation/en-us/unreal-engine/hardware-and-software-requirements-for-wine-containers-for-unreal-engine#installingdocker) section below for instructions on how to install Docker Desktop for Mac.
-   Linux: A 64-bit version of CentOS 8 or newer, Debian 10 or newer, Fedora 32 or newer, Ubuntu 16.04 or newer, or any Linux distribution that meets [Docker's prerequisites](https://docs.docker.com/engine/install/binaries/#prerequisites) with Docker Engine installed. See the [Installing Docker](/documentation/en-us/unreal-engine/hardware-and-software-requirements-for-wine-containers-for-unreal-engine#installingdocker) section below for instructions on how to install Docker Engine.

## Installing Docker

Docker is the recommended tool for building and running container images with Wine and the Unreal Engine. The steps for installing Docker will depend on the operating system you are using. The links below provide instructions on how to do this on each platform it is available on:

-   Windows: [Install Docker Desktop on Windows](https://docs.docker.com/desktop/setup/install/windows-install/)
-   macOS: [Install Docker Desktop on Mac](https://docs.docker.com/desktop/setup/install/mac-install/)
-   Linux: Follow the appropriate instructions to install Docker Engine for your specific Linux distribution:
    -   [CentOS](https://docs.docker.com/engine/install/centos/)
    -   [Debian](https://docs.docker.com/engine/install/debian/)
    -   [Fedora](https://docs.docker.com/engine/install/fedora/)
    -   [Ubuntu](https://docs.docker.com/engine/install/ubuntu/)
    -   [Other Linux distributions](https://docs.docker.com/engine/install/binaries/)