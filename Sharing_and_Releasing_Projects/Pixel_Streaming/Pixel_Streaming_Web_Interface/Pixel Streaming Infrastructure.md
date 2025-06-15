# Pixel Streaming Infrastructure

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/pixel-streaming-infrastructure](https://dev.epicgames.com/documentation/en-us/unreal-engine/pixel-streaming-infrastructure)  
**Processed:** 2025-06-14 16:43:16

---

The Pixel Streaming Infrastructure contains the servers and frontend components of the Pixel Streaming plugin. It contains the scripts needed to run Pixel Streaming (the Signalling Server, Matchmaker and SFU) and is designed to be both easy to access and modify. Additionally, it contains the foundation that developers can modify and extend to suit the needs of their Pixel Streaming experience. Previously, these scripts were found in the Samples/PixelStreaming directory of your project and engine. If you want to continue using Pixel Streaming moving forward, we recommend using the new infrastructure as all the latest frontend updates to Pixel Streaming will be made there.

## Why?

We moved the Pixel Streaming frontend to its own repository for a number of reasons:

1.  To improve the release cadence of Pixel Streaming. With the infrastructure existing in its own repository, it is not bound to updates to Unreal Engine.
    
2.  Encourage and allow easier contribution from Unreal Engine licensees and users.
    

## Acquiring the Infrastructure

There are **3 different ways** to acquire the Pixel Streaming infrastructure. The methods below are the most commonly used and should cover most use cases.

### Download the ZIP

You can directly download the infrastructure in ZIP format by heading to: [https://github.com/EpicGamesExt/PixelStreamingInfrastructure](https://github.com/EpicGamesExt/PixelStreamingInfrastructure). Navigate to the branch of the infrastructure you need and press the green code button. You should see the option to download ZIP.

### Use Git Command

If you have Git installed locally, you can acquire the infrastructure using the command line, for example:

`git clone --branch UE5.5 https://github.com/EpicGamesExt/PixelStreamingInfrastructure.git` in your preferred terminal (make sure you have git installed).

The git command mentioned above will pull the 5.5 branch of the infrastructure. If you need a different branch, please modify the git command accordingly.

### Use the Provided Scripts

With the Pixel Streaming plugin enabled, you will find scripts to automatically pull the required branch of the infrastructure.

Navigate to `\Engine\Plugins\Media\PixelStreaming\Resources\WebServers` and run the `get_ps_servers` command (make sure to use the `.bat` script for Windows and `.sh` script for Linux or Mac accordingly). This will automatically pull the relevant branch of the Pixel Streaming infrastructure into that folder.

This method is recommended because the downloaded infrastructure will be automatically packaged with your Pixel Streaming enabled project. If you don't use this method, you can still ensure the infrastructure packages with your project by manually placing the infrastructure in the above location.

## Infrastructure Layout

After pulling the infrastructure through one of the methods above, you'll end up with a local file setup as shown below. You can browse the infrastructure directly on GitHub as well.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5a6a1295-0674-4493-bf00-331550213bc4/infrastructurelocal.jpg)

The Pixel Streaming component locations are as follows:

1.  **Frontend**: This directory contains the HTML, CSS, images, and JavaScript / TypeScript code that runs in web browsers and allows them to connect to Unreal Engine Pixel Streaming applications and interact with them, as well as documentation on how to implement these interactions.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c44349a0-689a-4449-9467-a3f86ea24b33/frontendlocal.jpg)
2.  **Matchmaker**: This directory contains all the scripts required to configure and run the Matchmaker.
    
    The Matchmaker is being deprecated from Unreal Engine 5.5 onward. For users who require the matchmaker, you can use previous versions of the Pixel Streaming infrastructure.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/349d59ef-7c19-424f-873a-e623ba8b7cae/matchmakerlocal.jpg)
3.  **SFU**: This directory contains everything needed to configure and run the Selective Forwarding Unit.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/af84576e-9e7e-407e-82e6-131034511909/sfulocal.jpg)
4.  **SignallingWebServer**: This is the directory for your mandatory Pixel Streaming elements, such as the Signalling Server, Web Server and frontend.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f6f0177d-80f4-45c4-882c-e03527ac0e72/sslocal.jpg)

The `platform_scripts` directory is the go to location for all the scripts used to start each Pixel Streaming element. You will find scripts for Windows in `cmd` and scripts for Linux or Mac in `bash`.

For information about using the Matchmaker and the Selective Forwarding Unit, refer to the [Hosting and Networking Guide](/documentation/en-us/unreal-engine/hosting-and-networking-guide-for-pixel-streaming-in-unreal-engine).

For help setting up a basic Pixel Stream, refer to [Getting Started with Pixel Streaming](/documentation/en-us/unreal-engine/getting-started-with-pixel-streaming-in-unreal-engine).

For guidance on customizing the frontend, refer to the [Frontend/Docs/](https://github.com/EpicGamesExt/PixelStreamingInfrastructure/tree/master/Frontend) directory.

## Engine Versions

There are different branches of the Pixel Streaming Infrastructure for each different version of the engine. As the Pixel Streaming plugin has variances between each version of the engine, it's vital that you use the compatible version of the Pixel Streaming infrastructure (e.g. branch 5.0 for Unreal Engine 5.0) There is also a master branch available that is used for our active development. This will have the latest features, but is also experimental and is not guaranteed to be stable.

Refer to the versions section of the frontend repo for the list of Unreal Engine versions that are currently supported:

[](https://github.com/EpicGamesExt/PixelStreamingInfrastructure#versions)