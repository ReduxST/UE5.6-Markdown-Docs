# Setting Up SMPTE 2110

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/setting-up-smpte-2110-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/setting-up-smpte-2110-in-unreal-engine)  
**Processed:** 2025-06-14 16:49:49

---

### Setting Up SMPTE 2110 in Unreal Engine

This page contains everything you need to know to set up and deploy SMPTE 2110 in Unreal Engine using Nvidia Rivermax. This guide is intended for users who require high bandwidth SMPTE 2110 functionality, including the Broadcast and Film industry.

## Prerequisites

The following are the hardware and licensing requirements to integrate SMPTE 2110 using NVidia Rivermax:

### Hardware

Rivermax is an SDK developed by NVIDIA that works with Mellanox Connect-X network cards.

Although there are other 2110 producers, Unreal Engine 5.4 SMPTE 2110 features (at the time of publication) specifically require NVIDIA Rivermax.

#### Supported Network Cards

Driving an LED wall requires Bluefield for PTP (precision time protocol) accuracy. The list below describes the network cards (NICs) currently supported by Unreal Engine:

| Network Card (NIC) | Information |
| --- | --- |
| 
Connect-X 6 BlueField-2

 | 

We recommend this family of supported NICs, as it has PTP (precision time protocol) accuracy on Windows systems. PTP is required if driving an LED wall.

 |
| 

Connect-X 6

 | 

This family of NICs is supported, but is limited because it does not have PTP accuracy on Windows systems.

 |
| 

Connect-X 5

 | 

This family of NICs is supported by Rivermax SDK, but we do not recommend it for new installations.

 |

For a more detailed view, see [the NVIDIA website](https://developer.nvidia.com/networking/rivermax-getting-started) (you need an NVIDIA account to view the site).

GPUDirect capabilities are restricted to professional GPUs starting from the 4000 class and up, and require [Ampere architecture](https://www.nvidia.com/en-us/data-center/ampere-architecture/) or a future architecture generation (for example, RTX 6000 Ada, RTX 5000 Ada, RTX 4500 Ada, or RTX 4000 Ada). For a full list of GPUs that support GPUDirect, please refer to [the NVIDIA website](https://developer.nvidia.com/gpudirectforvideo).

Additionally, you need a motherboard supporting a resizable bar option, which may require a BIOS firmware update.

### Software

To use Rivermax with Unreal Engine, we recommend you follow the deployment guide found on [the NVIDIA Rivermax website](https://developer.nvidia.com/networking/rivermax), Windows DPU Deployment (version 2.51).

| Unreal Engine Version | Rivermax SDK Version | WinOF-2 Version | DPU Version | BlueField-2 Firmware Version |
| --- | --- | --- | --- | --- |
| 
5.3

 | 

1.20.10

 | 

3.10.52010

 | 

2.21

 | 

24.35.1012

 |
| 

5.4

 | 

1.41.11

 | 

24.1.50000

 | 

2.51

 | 

24.40.1000

 |
| 

5.5

 | 

1.41.11

 | 

24.1.50000

 | 

2.51

 | 

24.40.1000

 |
| 

5.6

 | 

1.60.6

 | 

24.10.50010

 | 

2.51

 | 

24.43.1014

 |

#### Rivermax SDK Installation Path

The default installation path for the RIvermax SDK is ‘C:\\Program Files\\Mellanox\\Rivermax\\lib’.

In Unreal Engine **5.4** and onward, in addition to using the default path, you can specify the installation path for the Rivermax SDK using the environment variable `$RIVERMAX_PATH`.

Starting with Unreal Engine **5.6,** you must specify an explicit path to your version of the Rivermax SDK.

### License

You need a license to use NVIDIA’s Rivermax SDK with Unreal Engine. [Contact NVIDIA](https://developer.download.nvidia.com/networking/nvidia-rivermax-license-generation-procedure.pdf?t=eyJscyI6ImdzZW8iLCJsc2QiOiJodHRwczovL3d3dy5nb29nbGUuY29tLyJ9) to obtain a license.

By default, the system expects to find the license next to Rivermax DLL. You can use the environment variable `$RIVERMAX_LICENSE_PATH` to specify a different location (such as a network drive) to look for the license.

## Deployment Steps

When setting up your Rivermax deployment, please refer to Nvidia's official documentation provided with your DPU, and with the Rivermax SDK.

### Optional: GPUDirect Setup

When setting up GPUDirect, make sure that the GPU and the DPU (Mellanox card) are on the same root complex. If they aren't, the SMPTE 2110 packets can be lost, especially if there are multiple input streams.

1.  Enable the resizable bar option in your BIOS.
    
2.  For optimal performance, you should place the Network Card and GPU on the same root complex.
    
3.  Validate the BAR1 available memory.
    
    -   Use the *Nvidia Control Panel - System* information to validate it’s enabled.
        
4.  Create a new environment variable to use CUDA with Rivermax.
    
    -   `RIVERMAX_ENABLE_CUDA`
        
    -   Set its value to 1.
        
5.  During initialization, if the system finds a compatible GPUDirect device, it will initialize the library with this support. If not, it will fall back to the system memory path.