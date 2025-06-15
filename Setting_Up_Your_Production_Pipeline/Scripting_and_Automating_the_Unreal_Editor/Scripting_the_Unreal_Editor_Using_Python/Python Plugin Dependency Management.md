# Python Plugin Dependency Management

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/python-plugin-dependency-management-for-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/python-plugin-dependency-management-for-unreal-engine)  
**Processed:** 2025-06-14 16:45:13

---

Many plugins using the Unreal Engine (UE) **Python Script Plugin** depend on Python code packages, such as those available through the **Python Package Index** ([PyPI](https://pypi.org/)). [Python Environment and Paths in the Unreal Editor](/documentation/en-us/unreal-engine/scripting-the-unreal-editor-using-python) discusses methods to make Python scripts and libraries available to the Unreal Editor Python environment. In addition to those methods, Unreal Editor supports two other methods for packaging plugins and their Python dependencies so that they are accessible to the embedded Unreal Editor Python environment.

## Special Subdirectories of /Content/Python

For each enabled plugin, Unreal Editor automatically adds the following paths for plugin dependencies to the Python `sys.path` list. Each of these paths is added only if they exist.

-   `<PluginDir>/Content/Python/Lib/site-packages`
    
-   `<PluginDir>/Content/Python/<CurrentPlatform>/Lib/site-packages`
    

To package pure-Python libraries with a plugin, copy or install the library into `<PluginDir>/Content/Python/Lib/site-packages`.

If the library also contains compiled binaries (For example, C/C++ libraries with Python bindings), then you should copy or install it into `<Plugin>/Content/Python/<CurrentPlatform>/Lib/site-packages` for each supported platform (Linux, Mac, and/or Win64).

## Plugin Pip Install Dependencies

Unreal Editor supports using **pip** to download and install all Python dependencies of enabled plugins upon launch, or through a special Unreal Build Tool (UBT) mode. To use this feature, you must add the `PythonRequirements` to each `.uplugin` descriptor file that requires installed dependencies.

You can only install binary packages (wheels) with pip.

### Pip Installer Settings

Project-specific settings for the pip installer are found in your **Project Settings** under the **Plugins - Python** section.

![The Project Settings for Pip Installer in Unreal Editor](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/96cb2fea-1fcc-43c8-81fe-5f433e141359/image1.png)

| **Parameter** | **Description** |
| --- | --- |
| **Run Pip Install on Startup** | Enables the pip installer to run on editor startup. |
| **Advanced - Pip Strict Hash Checking** | 
Ensures that only the valid packages are installed all Epic enabled plugins use pip strict hash checking. This is particularly important if you provide an untrusted Override Index Url (supply chain attacks). Strict hash checking requires all packages be version pinned and have hashes listed. If you are creating your own plugins with python dependencies, you may wish to disable this option for simplicity during development.

When this option is disabled, plugins that have python dependencies may not run correctly unless all packages are already installed.



 |
| **Advanced - Offline Only** | Offline-only mode will run the pip install tool to check that all dependencies are available, but will simply fail with a log message if dependencies are not already installed. |
| **Advanced - Override Index URL** | 

Force use of only the specified index URL. This is particularly useful for restrictive firewall scenarios where all necessary packages and versions may be cached in a local devpi or similar package index cache server.

This setting also overrides any ExtraIndexUrls specified in plugin descriptors (see Pip Install Plugin Descriptor Configuration below), so all packages from all indexes must be cached.



 |

### Disable Pip Install on Startup

If it is guaranteed that python dependencies are already installed, or if they are not necessary for a particular commandlet or editor instance, the running the pip install on editor startup can be disabled in two ways. First, as discussed above the **Run Pip Install on Startup** setting can be unchecked to disable the installer. Additionally, the pip install can be disabled with the command-line flag `-DisablePipInstall`.

### Run Pip Install with Unreal Build Tool (UBT)

For plugin developers and advanced users, it can be useful to test the pip installer using Unreal Build Tool (UBT). The `-Mode=PipInstall` UBT flag runs the pip installer from the command line. The following example shows a pip install for the `EngineTest` project, assuming that the user is running from the UE root directory.

Command Line

```
	`Engine\Build\BatchFiles\RunUBT.bat EngineTestEditor Win64 Development -Project=..\..\EngineTest\EngineTest.uproject -Mode=PipInstall` 
Copy full snippet
```
Engine\\Build\\BatchFiles\\RunUBT.bat EngineTestEditor Win64 Development -Project=..\\..\\EngineTest\\EngineTest.uproject -Mode=PipInstall

### Offline Installation

The pip install tool requires internet access to download Python packages from the Python package index. If an online install is not possible because of restrictive firewall rules or similar, you can download all necessary dependencies on another computer with internet connectivity, then copy the downloaded packages into the pip install site-packages for the target machine.

1.  On a machine with internet access, run the same editor project or pip install UBT mode, and allow the package dependencies to download.
    
2.  Zip the `site-packages` folder (see Where Packages Are Installed).
    
3.  Copy this zip file to the target machine and unpack into the appropriate project `site-packages` directory (see Where Packages Are Installed).
    

### Where Packages Are Installed

All Python dependencies are installed at:

-   **Windows**: `<ProjectDir>/Intermediate/PipInstall/Lib/site-packages`
    
-   **Linux/MacOS**: `<ProjectDir>/Intermediate/PipInstall/lib/python3.11/site-packages`
    

## Pip Install Plugin Descriptor Configuration

The `PythonRequirements` in the plugin descriptor file contains a JSON array of objects, one object per platform. Each JSON object specifies:

-   A `Platform` (All, Linux, Mac or Win64).
    
-   An array of `Requirements` lines in pip `requirements.txt` line format.
    

Each object may optionally also contain an `ExtraIndexUrls` array with a list of additional urls for other package indexes (PyPI is always included).

While UE supports most common pip requirements' line specifiers, it ignores command flags (for example, `--force index-url`).

Below is an annotated excerpt from the engine `PythonFoundationPackages.uplugin` file showing the use of the `PythonRequirements` field to install `numpy 1.24.4` , `scipy 1.11.0` , and `torch 2.1.0` . The `torch` requirement is set for each platform so that the Windows/Linux platforms install CUDA-enabled package versions.

If strict hash checking is enabled then each requirement line must contain hashes for all supported wheels.

PythonFoundationPackages.uplugin

```
	`{  		"FriendlyName": "Python Foundation Packages",  		...  		"PythonRequirements":  		[  			{   				// The requirements listed under "All" will be installed for every platform  				"Platform": "All", // "All", "Linux", "Mac", or "Win64"  				"Requirements":  				[  					"numpy==1.24.4 --hash=sha256:9667575fb6d13c95f1b36aca12c5ee3356bf001b714fc354eb5465ce1609e62f --hash=sha256:7ffe43c74893dbf38c2b0a1f5428760a1a9c98285553c89e12d70a96a7f3a4d6 --hash=sha256:7215847ce88a85ce39baf9e89070cb860c98fdddacbaa6c0da3ffb31b3350bd5 --hash=sha256:ed094d4f0c177b1b8e7aa9cba7d6ceed51c0e569a5318ac0ca9a090680a6a1b1 --hash=sha256:befe2bf740fd8373cf56149a5c23a0f601e82869598d41f8e188a0e9869926f8 --hash=sha256:b4bea75e47d9586d31e892a7401f76e909712a0fd510f58f5337bea9572c571e --hash=sha256:f136bab9c2cfd8da131132c2cf6cc27331dd6fae65f95f69dcd4ae3c3639c810 --hash=sha256:c0bfb52d2169d58c1cdb8cc1f16989101639b34c7d3ce60ed70b19c63eba0b64 --hash=sha256:d11efb4dbecbdf22508d55e48d9c8384db795e1b7b51ea735289ff96613ff74d --hash=sha256:2541312fbf09977f3b3ad449c4e5f4bb55d0dbf79226d7724211acc905049400 --hash=sha256:e2926dac25b313635e4d6cf4dc4e51c8c0ebfed60b801c799ffc4c32bf3d1254 --hash=sha256:b7b1fc9864d7d39e28f41d089bfd6353cb5f27ecd9905348c24187a768c79694",   					"scipy==1.11.0 --hash=sha256:ee410e6de8f88fd5cf6eadd73c135020bfbbbdfcd0f6162c36a7638a1ea8cc65 --hash=sha256:6550466fbeec7453d7465e74d4f4b19f905642c89a7525571ee91dd7adabb5a3 --hash=sha256:028eccd22e654b3ea01ee63705681ee79933652b2d8f873e7949898dda6d11b6 --hash=sha256:f3cd9e7b3c2c1ec26364856f9fbe78695fe631150f94cd1c22228456404cf1ec --hash=sha256:36750b7733d960d7994888f0d148d31ea3017ac15eef664194b4ef68d36a4a97 --hash=sha256:2c6ff6ef9cc27f9b3db93a6f8b38f97387e6e0591600369a297a50a8e96e835d --hash=sha256:933baf588daa8dc9a92c20a0be32f56d43faf3d1a60ab11b3f08c356430f6e56 --hash=sha256:acf8ed278cc03f5aff035e69cb511741e0418681d25fbbb86ca65429c4f4d9cd --hash=sha256:530f9ad26440e85766509dbf78edcfe13ffd0ab7fec2560ee5c36ff74d6269ff --hash=sha256:f313b39a7e94f296025e3cffc2c567618174c0b1dde173960cf23808f9fae4be --hash=sha256:cf00bd2b1b0211888d4dc75656c0412213a8b25e80d73898083f402b50f47e41 --hash=sha256:91af76a68eeae0064887a48e25c4e616fa519fa0d38602eda7e0f97d65d57937 --hash=sha256:ad669df80528aeca5f557712102538f4f37e503f0c5b9541655016dd0932ca79 --hash=sha256:1b7c3dca977f30a739e0409fb001056484661cb2541a01aba0bb0029f7b68db8 --hash=sha256:6e619aba2df228a9b34718efb023966da781e89dd3d21637b27f2e54db0410d7 --hash=sha256:bc9a714581f561af0848e6b69947fda0614915f072dfd14142ed1bfe1b806710"  				]   			},  			{  				"Platform": "Linux",  				// CUDA-based torch requires an additional index to search for wheels 				"ExtraIndexUrls":  				["https://download.pytorch.org/whl/"],  				"Requirements":  				[  					"torch==2.1.0+cu118 --hash=sha256:bcb17e2de6ca634d326203694d0bfb552587335e536c1917be3f28c5664b5506 --hash=sha256:8ecf52ba49cfd3b7303d4e57e7b5c2106b77dbc9bdeaf880870162138bc70e18 --hash=sha256:a81b554184492005543ddc32e96469f9369d778dedd195d73bda9bed407d6589"  				]  			},  			{  				"Platform": "Mac",  				"ExtraIndexUrls":  				["https://download.pytorch.org/whl/"],  				"Requirements":  				[  					"torch==2.1.0 --hash=sha256:3cd1dedff13884d890f18eea620184fb4cd8fd3c68ce3300498f427ae93aa962 --hash=sha256:601b0a2a9d9233fb4b81f7d47dca9680d4f3a78ca3f781078b6ad1ced8a90523 --hash=sha256:05661c32ec14bc3a157193d0f19a7b19d8e61eb787b33353cad30202c295e83b --hash=sha256:101c139152959cb20ab370fc192672c50093747906ee4ceace44d8dd703f29af --hash=sha256:421739685eba5e0beba42cb649740b15d44b0d565c04e6ed667b41148734a75b --hash=sha256:a6b7438a90a870e4cdeb15301519ae6c043c883fcd224d303c5b118082814767 --hash=sha256:c8bf7eaf9514465e5d9101e05195183470a6215bb50295c61b52302a04edb690 --hash=sha256:6ad491e70dbe4288d17fdbfc7fbfa766d66cbe219bc4871c7a8096f4a37c98df"  				]  			}  		]  	}` 

Copy full snippet
```
{ "FriendlyName": "Python Foundation Packages", ... "PythonRequirements": \[ { // The requirements listed under "All" will be installed for every platform "Platform": "All", // "All", "Linux", "Mac", or "Win64" "Requirements": \[ "numpy==1.24.4 --hash=sha256:9667575fb6d13c95f1b36aca12c5ee3356bf001b714fc354eb5465ce1609e62f --hash=sha256:7ffe43c74893dbf38c2b0a1f5428760a1a9c98285553c89e12d70a96a7f3a4d6 --hash=sha256:7215847ce88a85ce39baf9e89070cb860c98fdddacbaa6c0da3ffb31b3350bd5 --hash=sha256:ed094d4f0c177b1b8e7aa9cba7d6ceed51c0e569a5318ac0ca9a090680a6a1b1 --hash=sha256:befe2bf740fd8373cf56149a5c23a0f601e82869598d41f8e188a0e9869926f8 --hash=sha256:b4bea75e47d9586d31e892a7401f76e909712a0fd510f58f5337bea9572c571e --hash=sha256:f136bab9c2cfd8da131132c2cf6cc27331dd6fae65f95f69dcd4ae3c3639c810 --hash=sha256:c0bfb52d2169d58c1cdb8cc1f16989101639b34c7d3ce60ed70b19c63eba0b64 --hash=sha256:d11efb4dbecbdf22508d55e48d9c8384db795e1b7b51ea735289ff96613ff74d --hash=sha256:2541312fbf09977f3b3ad449c4e5f4bb55d0dbf79226d7724211acc905049400 --hash=sha256:e2926dac25b313635e4d6cf4dc4e51c8c0ebfed60b801c799ffc4c32bf3d1254 --hash=sha256:b7b1fc9864d7d39e28f41d089bfd6353cb5f27ecd9905348c24187a768c79694", "scipy==1.11.0 --hash=sha256:ee410e6de8f88fd5cf6eadd73c135020bfbbbdfcd0f6162c36a7638a1ea8cc65 --hash=sha256:6550466fbeec7453d7465e74d4f4b19f905642c89a7525571ee91dd7adabb5a3 --hash=sha256:028eccd22e654b3ea01ee63705681ee79933652b2d8f873e7949898dda6d11b6 --hash=sha256:f3cd9e7b3c2c1ec26364856f9fbe78695fe631150f94cd1c22228456404cf1ec --hash=sha256:36750b7733d960d7994888f0d148d31ea3017ac15eef664194b4ef68d36a4a97 --hash=sha256:2c6ff6ef9cc27f9b3db93a6f8b38f97387e6e0591600369a297a50a8e96e835d --hash=sha256:933baf588daa8dc9a92c20a0be32f56d43faf3d1a60ab11b3f08c356430f6e56 --hash=sha256:acf8ed278cc03f5aff035e69cb511741e0418681d25fbbb86ca65429c4f4d9cd --hash=sha256:530f9ad26440e85766509dbf78edcfe13ffd0ab7fec2560ee5c36ff74d6269ff --hash=sha256:f313b39a7e94f296025e3cffc2c567618174c0b1dde173960cf23808f9fae4be --hash=sha256:cf00bd2b1b0211888d4dc75656c0412213a8b25e80d73898083f402b50f47e41 --hash=sha256:91af76a68eeae0064887a48e25c4e616fa519fa0d38602eda7e0f97d65d57937 --hash=sha256:ad669df80528aeca5f557712102538f4f37e503f0c5b9541655016dd0932ca79 --hash=sha256:1b7c3dca977f30a739e0409fb001056484661cb2541a01aba0bb0029f7b68db8 --hash=sha256:6e619aba2df228a9b34718efb023966da781e89dd3d21637b27f2e54db0410d7 --hash=sha256:bc9a714581f561af0848e6b69947fda0614915f072dfd14142ed1bfe1b806710" \] }, { "Platform": "Linux", // CUDA-based torch requires an additional index to search for wheels "ExtraIndexUrls": \["https://download.pytorch.org/whl/"\], "Requirements": \[ "torch==2.1.0+cu118 --hash=sha256:bcb17e2de6ca634d326203694d0bfb552587335e536c1917be3f28c5664b5506 --hash=sha256:8ecf52ba49cfd3b7303d4e57e7b5c2106b77dbc9bdeaf880870162138bc70e18 --hash=sha256:a81b554184492005543ddc32e96469f9369d778dedd195d73bda9bed407d6589" \] }, { "Platform": "Mac", "ExtraIndexUrls": \["https://download.pytorch.org/whl/"\], "Requirements": \[ "torch==2.1.0 --hash=sha256:3cd1dedff13884d890f18eea620184fb4cd8fd3c68ce3300498f427ae93aa962 --hash=sha256:601b0a2a9d9233fb4b81f7d47dca9680d4f3a78ca3f781078b6ad1ced8a90523 --hash=sha256:05661c32ec14bc3a157193d0f19a7b19d8e61eb787b33353cad30202c295e83b --hash=sha256:101c139152959cb20ab370fc192672c50093747906ee4ceace44d8dd703f29af --hash=sha256:421739685eba5e0beba42cb649740b15d44b0d565c04e6ed667b41148734a75b --hash=sha256:a6b7438a90a870e4cdeb15301519ae6c043c883fcd224d303c5b118082814767 --hash=sha256:c8bf7eaf9514465e5d9101e05195183470a6215bb50295c61b52302a04edb690 --hash=sha256:6ad491e70dbe4288d17fdbfc7fbfa766d66cbe219bc4871c7a8096f4a37c98df" \] } \] }

## Pip Strict Hash Checking

**Strict hash checking** ensures that downloaded packages exactly match the expected content, and is enabled by default in new projects and plugins. Strict hash checking requires you to list the exact version and hash info for all packages in your `.uplugin file` under `Requirements`. See the previous section for an example of a .uplugin file with hashes listed in the `Requirements` block.

### How to Disable Strict Hash Checking

If you are creating your own plugins with Python dependencies, you may wish to disable strict hash checking during development for simplicity's sake. To disable strict hash checking, follow these steps:

1.  Open Project Settings > Plugins > Python.
2.  Unfold the **Advanced** settings for Python Pip Install.
3.  Un-check **Pip Strict Hash Check**

![Uncheck Pip Strict Hash Check in the Python Plugins settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/46ef3eef-d44f-4a3b-aa3e-bb10d826f0bd/stricthashcheck.png)