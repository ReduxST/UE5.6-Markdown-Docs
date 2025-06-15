# Hardware and Software Specifications

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/hardware-and-software-specifications-for-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/hardware-and-software-specifications-for-unreal-engine)  
**Processed:** 2025-06-14 16:27:16

---

Operating System

×Windows

Select an option from the dropdown to see content relevant to it.

This page covers the hardware and software requirements for Unreal Engine (UE5). 

## Recommended Hardware

|  |  |
| --- | --- |
| 
**Operating System**

 | 

Windows 10 64-bit version 1909 revision .1350 or higher, or versions 2004 and 20H2 revision .789 or higher.

Windows 11 is compatible with UE5 and fits in the recommended specs.



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

**Graphics RAM**

 | 

8 GB or more

 |
| 

**Graphics Card**

 | 

DirectX 11 or 12 compatible graphics card with the latest drivers.

 |

Although some features have a minimum requirement of DirectX 11, we recommend DirectX 12 for most games.

DirectX11 is better for older PCs, especially laptops with integrated graphics. However, DirectX12 provides a higher frame rate, multi-core processing support, and parallel and asynchronous computing.

To get the most out of rendering features of Unreal Engine 5, such as Nanite and Lumen, see the Requirements for UE5 Rendering Features section of this page.

## Minimum Software Requirements

Minimum requirements for running the engine or editor are listed below.

| Running the Engine |  |
| --- | --- |
| 
**Operating System**

 | 

Windows 10 version 1703 (Creators Update)

 |
| 

**DirectX Runtime**

 | 

[DirectX End-User Runtimes (June 2010)](https://www.microsoft.com/en-us/download/details.aspx?id=8109)

 |

The requirements for programmers developing with the engine are listed below.

| Developing with the Engine |  |
| --- | --- |
| 
**All 'Running the Engine' requirements (automatically installed)**

 |  |
| 

**Visual Studio Version**

 | 

Visual Studio 2022

 |
| iOS App Development |  |
| --- | --- |
| 

**iTunes Version**

 | 

[iTunes 12 or higher](http://www.apple.com/itunes)

 |

Although Visual Studio is recommended for Windows development, Unreal Engine also supports VS Code and Rider.

## Prerequisite Software Installers

Unreal Engine includes installers for everything you need to run the editor and engine, such as the **Microsoft Visual C++ 2015-2022 Redistributable**. 

When you install Unreal Engine through the Epic Games Launcher, the launcher automatically installs these prerequisites for you. However, you may need to run the installers yourself if you build Unreal Engine from source, or if you must prepare a computer with all the Unreal Engine prerequisites for a specific purpose. For example, if you are set up a fresh computer to act as a [Swarm Agent](https://dev.epicgames.com/documentation/en-us/unreal-engine/unreal-swarm-in-unreal-engine).

You can find the installers in the `Engine/Extras/Redist/en-us` folder under your Unreal Engine installation location.

Support for 32-bit platforms was removed in Unreal Engine 5.

If you use Perforce to get the Unreal Engine source code, you can find binaries in the `Engine/Extras/Redist/en-us` folder of the Perforce repository.

  To learn more about Visual Studio, see [Setting Up Visual Studio](https://dev.epicgames.com/documentation/en-us/unreal-engine/setting-up-visual-studio-development-environment-for-cplusplus-projects-in-unreal-engine).  

## Graphics Card Drivers

We currently recommend using the latest stable releases from each card manufacturer:

-   [Download NVIDIA drivers here](http://www.nvidia.com/Download/index.aspx)
    
-   [Download AMD drivers here](http://support.amd.com/us/gpudownload/Pages/index.aspx)
    
-   [Download Intel drivers here](https://www.intel.com/content/www/us/en/products/docs/arc-discrete-graphics/software/drivers.html)
    

## Performance Notes

The spec below represents a typical system used at Epic Games (a Lenovo P620 Content Creation Workstation, standard version). This provides a reasonable guideline for developing games with Unreal Engine 5.

-   Operating System: Windows 11
    
-   Power Supply: 1400W Power supply unit
    
-   RAM: 256 GB DDR5-4800MHz (RDIMM, ECC)
    
-   Processor: AMD Ryzen™ Threadripper™ PRO 7985WX Processor (3.20 GHz up to 5.10 GHz)
    
-   OS Drive: 2 TB SSD M.2 2280 PCIe Gen4 Performance TLC Opal
    
-   DATA Drive: 4 TB SSD M.2 2280 PCIe Gen4 Performance TLC Opal
    
-   GPU: NVIDIA RTX™ 4080 16GB GDDR6
    
-   NIC: AMD RZ616
    
-   TPM Compliant
    

If you don't have access to Xoreax Incredibuild (Dev Tools Package), we recommend compiling with a machine having 12 to 16 cores.

## Requirements for UE5 Rendering Features

Some rendering features of Unreal Engine have different requirements than the minimum specifications.

| UE5 Feature | System Requirements |
| --- | --- |
| 
**Lumen Global Illumination, Lumen Reflections, and MegaLights**

 | 

-   Windows 10 build 1909.1350 and newer with DirectX 12 support.
    
    -   **SM6** must be enabled in the Project Settings.
        
-   One of the following graphics cards:
    
    -   AMD RX-6000 series or newer.
        
    -   Intel® Arc™ A-Series Graphics Cards or newer.
        
    -   NVIDIA RTX-2000 series or newer.
        

Lumen Hardware Ray Tracing now requires SM6 to be set in Project Settings.

To learn more, see [Lumen Technical Details](https://dev.epicgames.com/documentation/en-us/unreal-engine/lumen-technical-details-in-unreal-engine).

 |
| 

**Nanite Virtualized Geometry and Virtual Shadow Maps**

 | 

-   All versions of Windows 10 build 1909.1350 and newer, and Windows 11 with support for [DirectX 12 Agility SDK](https://devblogs.microsoft.com/directx/gettingstarted-dx12agility) are supported.
    
    -   Windows 10 version 2004 and 20H2 — The revision number should exceed or be equal to .789.
        
    -   DirectX 12 (with Shader Model 6.6 atomics), or Vulkan (VK\_KHR\_shader\_atomic\_int64).
        
    -   **SM6** must be enabled in the Project Settings. (On by default in new projects.)  
        
    -   Windows 10 version 1909 — The revision number should exceed or be equal to .1350.
        
-   Latest graphics drivers.
    

To learn more, see [Nanite Virtualized Geometry](https://dev.epicgames.com/documentation/en-us/unreal-engine/nanite-virtualized-geometry-in-unreal-engine) and [Virtual Shadow Maps](https://dev.epicgames.com/documentation/en-us/unreal-engine/virtual-shadow-maps-in-unreal-engine).

 |
| 

**Temporal Super Resolution**

 | 

Runs on any video card that supports Shader Model 5, but the limit of 8UAVs per shader has performance implications. Temporal Super Resolution shaders compile with 16bit types enabled on D3D12 that supports Shader Model 6.

To learn more, see [Temporal Super Resolution](https://dev.epicgames.com/documentation/en-us/unreal-engine/temporal-super-resolution-in-unreal-engine).

 |