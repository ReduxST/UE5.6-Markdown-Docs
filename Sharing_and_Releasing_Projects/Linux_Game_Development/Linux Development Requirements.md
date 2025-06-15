# Linux Development Requirements

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/linux-development-requirements-for-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/linux-development-requirements-for-unreal-engine)  
**Processed:** 2025-06-14 16:33:41

---

This page contains the software development kit (SDK) and hardware requirements needed to develop Unreal Engine (UE) projects for Linux devices.

## Recommended Hardware

|  |  |
| --- | --- |
| 
**Recommended Operating System**

 | 

Ubuntu 22.04

 |
| 

**Processor**

 | 

Quad-core Intel or AMD, 2.5 GHz or faster

 |
| 

**Memory**

 | 

32 GB RAM

 |
| 

**Graphics Card**

 | 

GeForce 2080

 |
| 

**Graphics RAM**

 | 

8 GB or more

 |
| 

**RHI Version**

 | 

Vulkan: AMD (RADV minimum 24.2.8+, recommended 25.0.0+) and NVIDIA (570+)

 |

## Recommended Software for Developing on Linux

Minimum requirements for running the engine or editor are listed below.

| Running the Engine |   |
| --- | --- |
| 
**Operating System**

 | 

Rocky Linux 8 / Redhat Linux 8 or newer

 |
| 

**Linux Kernel Version**

 | 

kernel 4.18 or newer

 |
| 

**Additional Dependencies**

 | 

glibc 2.28 or newer

 |

If either Unreal Editor or installations of UE games take a very long time on startup, check that your `glibc` is version 2.35 or newer, as earlier versions have a slow implementation of `dlopen`.

The requirements for programmers developing with the engine are listed below.

| Developing with the Engine |   |
| --- | --- |
| 
**Operating System**

 | 

Ubuntu 22.04, Rocky Linux 8

 |
| 

**Compiler**

 | 

clang 18.1.0

 |
| 

Optional

 |  |
| 

**IDE**

 | 

Visual Studio Code, Rider

 |

## Cross-Compile Toolchain

**Cross-compiling** makes it possible for game developers to target Linux from Windows. At this time, cross-compiling is only supported for Windows, and Mac users currently have to resort to [Native Compiling](https://dev.epicgames.com/documentation/en-us/unreal-engine/linux-development-requirements-for-unreal-engine?application_version=5.5#native-toolchain). Additionally, we support, test, and provide libraries and toolchains for the Linux-x86\_64 platform.

### Why Cross-Compilation

**Cross-compilation** makes it possible for game developers, working in a Windows-centric workflow, to target Linux. At this time, cross-compilation is only supported for Windows. Mac users currently have to resort to native compilation. We support, test, and provide the libraries and toolchains for the Linux-x86\_64 platform.

### Getting the Toolchain

To download the Cross-Compilation Toolchain, refer to the download links in the table in the [Version History](https://dev.epicgames.com/documentation/en-us/unreal-engine/linux-development-requirements-for-unreal-engine#version-history) section on this page.

### After Installing Cross-Compile SDK

You can verify your installation by doing `echo %LINUX_MULTIARCH_ROOT%`.

[![Verify Cross-Compile SDK Installation](https://dev.epicgames.com/community/api/documentation/image/28914333-7e58-464b-98ba-5020eee0b7f7?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/28914333-7e58-464b-98ba-5020eee0b7f7?resizing_type=fit)

## Native Toolchain

Unreal Engine's setup shell script (`Setup.sh`) automatically downloads a native toolchain, which guarantees your compiler and linker to work with our codebase. With the native toolchain, you compile against a fixed sysroot (`glibc` at the very least), so that, for example, if you compile a game on Ubuntu 22.04, you will be able to start the binary on Rocky Linux 8.

## Performance Notes

The spec below represents a typical system used at Epic (a Lenovo P620 Content Creation Workstation, standard version). This provides a reasonable guideline for developing games with Unreal Engine 5:

-   Operating System: Ubuntu 22.04
    
-   Power Supply: 1000W power supply unit
    
-   RAM: 128GB DDR4-3200
    
-   Processor: AMD Ryzen Threadripper Pro 3975WX Processor - 128MB Cache, 3.5 GHz base / 4.2 GHz turbo, 32 Cores / 64 Threads, 280w TDP
    
-   OS Drive 1 TB M.2 NVMe3 x4 PCI-e SSD
    
-   DATA Drive 4 TB Raid Array - 2 x 2TB NVMe3 x4 PCI-e SSD in Raid 0
    
-   GPU: Nvidia RTX 3080 - 10GB
    
-   NIC 1GBPS on-board + Intel X550-T1 10G PCI-e Ethernet adapter
    
-   TPM Compliant
    

## Requirements for UE5 Rendering Features

| UE5 Feature | System Requirements |
| --- | --- |
| 
**Lumen Global Illumination, Lumen Reflections, and MegaLights**

 | 

-   **SM6** must be enabled in the Project Settings.
    
-   One of the following graphics cards:
    
    -   NVIDIA RTX-2000 series or newer.
        
    -   AMD RX-6000 series or newer.
        
    -   Intel® Arc™ A-Series Graphics Cards or newer.
        

Lumen Hardware Ray Tracing now requires SM6 to be set in Project Settings.

To learn more see, [Lumen Technical Details](https://dev.epicgames.com/documentation/en-us/unreal-engine/lumen-technical-details-in-unreal-engine).

 |
| 

**Path Tracing**

 | 

-   **SM6** must be enabled in the Project Settings.
    
-   One of the following graphics cards:
    
    -   NVIDIA RTX-2000 series or newer.
        
    -   AMD RX-6000 series or newer.
        

To learn more, see [Path Tracer](https://dev.epicgames.com/documentation/en-us/unreal-engine/path-tracer-in-unreal-engine).

 |
| 

**Nanite Virtualized Geometry and Virtual Shadow Maps**

 | 

-   GPU which supports the VK\_KHR\_shader\_atomic\_int64 Vulkan extension.
    
    -   **SM6** must be enabled in the Project Settings. (On by default in new projects.)
        
-   Latest Graphics Drivers.
    

To learn more see, [Nanite Virtualized Geometry](https://dev.epicgames.com/documentation/en-us/unreal-engine/nanite-virtualized-geometry-in-unreal-engine) and [Virtual Shadow Maps](https://dev.epicgames.com/documentation/en-us/unreal-engine/virtual-shadow-maps-in-unreal-engine).

 |

## Version History

If you migrate your 5.5 project to 5.6, you must update the cross-compile toolchain to v25 to avoid dependency issues. In addition, we don't recommend v24 (clang 19) for 5.6 due to undefined behaviors. 

| UE Version | Recommended Operating System | Recommended IDE | Compiler | Cross-Compile Toolchain | Native Toolchain |
| --- | --- | --- | --- | --- | --- |
| 
5.6

 | 

Ubuntu 22.04, Rocky Linux 8

 | 

Visual Studio Code, Rider

 | 

clang 18.1.0

 | 

  v25 [clang-18.1.0-based](https://cdn.unrealengine.com/CrossToolchain_Linux/v25_clang-18.1.0-rockylinux8.exe)

 | 

  v25 [clang-18.1.0-based](https://cdn.unrealengine.com/Toolchain_Linux/native-linux-v25_clang-18.1.0-rockylinux8.tar.gz)

 |
| 

5.5

 | 

Ubuntu 22.04, Rocky Linux 8

 | 

Visual Studio Code, Rider

 | 

clang 18.1.0

 | 

**v23** [clang-18.1.0-based](https://cdn.unrealengine.com/CrossToolchain_Linux/v23_clang-18.1.0-rockylinux8.exe)

 | 

**v23** [clang-18.1.0-based](https://cdn.unrealengine.com/Toolchain_Linux/native-linux-v23_clang-18.1.0-rockylinux8.tar.gz)

 |
| 

5.3-5.4

 | 

Ubuntu 22.04, CentOS 7

 | 

Visual Studio Code, Rider

 | 

clang 16.0.6

 | 

**v22** [clang-16.0.6-based](https://cdn.unrealengine.com/CrossToolchain_Linux/v22_clang-16.0.6-centos7.exe)

 | 

**v22**[clang-16.0.6-based](https://cdn.unrealengine.com/Toolchain_Linux/native-linux-v22_clang-16.0.6-centos7.tar.gz)

 |
| 

5.2

 | 

Ubuntu 22.04, CentOS 7

 | 

Visual Studio Code, Rider

 | 

clang 15.0.1

 | 

**\-v21** [clang-15.0.1-based](https://cdn.unrealengine.com/CrossToolchain_Linux/v21_clang-15.0.1-centos7.exe)

 | 

**\-v21** [clang-15.0.1-based](http://cdn.unrealengine.com/Toolchain_Linux/native-linux-v21_clang-15.0.1-centos7.tar.gz)

 |
| 

5.1

 | 

Ubuntu 22.04, CentOS 7

 | 

Visual Studio Code, Rider

 | 

clang 13.0.1

 | 

**\-v20** [clang-13.0.1-based](https://cdn.unrealengine.com/CrossToolchain_Linux/v20_clang-13.0.1-centos7.exe)

 | 

**\-v20** [clang-13.0.1-based](https://cdn.unrealengine.com/Toolchain_Linux/native-linux-v20_clang-13.0.1-centos7.tar.gz)

 |
| 

5.0.2+

 | 

Ubuntu 22.04, CentOS 7

 | 

Visual Studio Code, Rider

 | 

clang 13.0.1

 | 

**\-v20** [clang-13.0.1-based](https://cdn.unrealengine.com/CrossToolchain_Linux/v20_clang-13.0.1-centos7.exe)

 | 

**\-v20** [clang-13.0.1-based](https://cdn.unrealengine.com/Toolchain_Linux/native-linux-v20_clang-13.0.1-centos7.tar.gz)

 |
| 

5.0

 | 

Ubuntu 20.04, CentOS 7

 | 

Visual Studio Code, Rider

 | 

clang 11.0.1

 | 

**\-v19** [clang-11.0.1-based](https://cdn.unrealengine.com/CrossToolchain_Linux/v19_clang-11.0.1-centos7.exe)

 | 

**\-v19** [clang-11.0.1-based](https://cdn.unrealengine.com/Toolchain_Linux/native-linux-v19_clang-11.0.1-centos7.tar.gz)

 |