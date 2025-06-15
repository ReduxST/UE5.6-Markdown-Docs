# DMX Quick Start

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/dmx-quick-start-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/dmx-quick-start-in-unreal-engine)  
**Processed:** 2025-06-14 16:21:09

---

This Quick Start guide describes how to use the basic DMX features to help you get started creating your own visual installation or live event using Unreal Engine.

## Enabling the DMX Plugins

To fully leverage the whole DMX feature set, you need to navigate to **Edit > Plugins** and enable the following plugins in your project.

### Base Plugins

The following are the main DMX plugins that you need to enable to use DMX in your project.

-   **DMX Engine:** Enables the core DMX engine functionality.
    
-   **DMX Protocol:** Enables the DMX communication protocols.
    

### Extra Plugins

The following are optional plugins that provide extra features and functionality.

-   **DMX Fixtures:** Provides example content of DMX-enabled light fixtures Blueprints you can use to spawn MVR.
    
-   **DMX Control Console:** Enables a DMX control console that sends DMX to a specific patch or raw DMX address.
    
-   **DMX PixelMapping:** Converts pixel information from Textures, Materials, Render Targets, or UMG widgets into DMX signals.
    
-   **Datasmith MVR:** Provides MVR support for Datasmith importers.
    
-   **DMX Display Cluster:** Enables proper synchronization of DMX data, and Lightcard control across your nDisplay cluster.
    
-   **DMX** **Remote Control Protocol:** Enables DMX support for the Remote Control plugin.
    

## Project Settings

When you look at the DMX section under **Edit > Project Settings**, you will see we categorized them in two sections.

-   [Communication Settings](/documentation/en-us/unreal-engine/dmx-quick-start-in-unreal-engine#communicationsettings)
    
-   [Fixture Settings](/documentation/en-us/unreal-engine/dmx-quick-start-in-unreal-engine#fixturesettings)
    

![The DMX project settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c2bf707f-7213-4b26-9663-b08c017faf6d/dmx-project-settings.png)

### Communication Settings

We consolidated the DMX protocol, adapter, and universe configuration settings under a concept called **Ports**, which applies to both DMX input and output data. There are no limits to the quantity of ports you can create, which means you can use ports to easily and properly separate various universes across multiple protocols and adapters.

#### Shared Settings

Most of the Ports settings function the same way for both input and output ports. These are defined in the table below.

| **Setting** | **Description** |
| --- | --- |
| Port Name | Define a custom name for easy identification. |
| Protocol Name | Choose between Art-Net or sACN. |
| Auto Complete Network Interface Card IP Address | Automatically selects an appropriate IP address. [See below for details.](/documentation/en-us/unreal-engine/dmx-quick-start-in-unreal-engine#autoip) |
| Network Interface Card IP Address | Specify the IP of the particular network adapter you are using. |
| Local Universe Start | 
The ID number for the first Universe where Unreal Engine should start listening or writing.

We start at Universe 1 for both supported protocols. Should you want to send to Universe 0, this is only possible for Art-Net and you can achieved this by setting the External Universe Start to 0.



 |
| Amount of Universes | How many Universes to set up. |
| Extern Universe Start | An offset value you can apply to Universes externally. For example, a value of 100 here would mean that Universe 1 was numbered as Universe 100 in the external output. |

##### Auto-selection of IP addresses based on string search

You can auto-select IP addresses by enabling the **Auto Complete Network Interface Card IP Address** checkbox.

![The autocomplete checkbox and options.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/668e8ba4-12a2-43e8-a40f-2b443f27b041/dmx-autocomplete.png)

The system selects the most appropriate IP Address based on the input in the IP address field. This feature supports wildcards.

Examples:

'192'

'192.\*'

'192.168.?.\*'

#### Input Ports

The Input Ports section is where you define the configuration for your local inputs. By default, this is an array with 3 elements, but you can add or remove elements as needed.

![Define the DMX input ports.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b1a08ca4-dd68-43bc-927c-df44aa459818/dmx-input-ports.png)

#### Output Ports

The Output Ports section is where you define your output configuration. Like the Input Ports section, by default this is an array with 3 elements that you can add or remove elements from as needed. However, the Output Ports section also has unique settings.

![Define the DMX output ports.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c930c4f5-08d8-4332-b758-403b8f5e57bf/dmx-output-ports.png)

The following properties are unique to the Output Ports settings.

| **Setting** | **Description** |
| --- | --- |
| Communication Type | Provides a choice between broadcast and unicast output. |
| Input into Engine | Enabling this checkbox sends the output internally to Unreal Engine as well. This does not show as input in the Activity Monitor. |
| Delay | Adds a time delay to output. [See below for details.](/documentation/en-us/unreal-engine/dmx-quick-start-in-unreal-engine#outputdelay) |

##### Output delay

You can use the Output delay functionality to add a fixed time delay to your output. The default time scale is in seconds, but you can set the delay according to various fps options instead.

![Set up your output delay.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/736a7009-8a86-4eb3-801a-bf0fc8acf52d/dmx-output-delay.png) ![The output delay options.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/08149d0e-f5a6-4eb8-b3f5-f1ad11707028/dmx-output-delay-options.png)

#### Console Commands

You can change any of the Ports settings using console commands.

For example, the following command sets the delay of OutputA to 5 seconds: `DMX.SetOutputPortDelay OutputA 5`

You can set all the Ports properties this way:

![The DMX port properties list.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9da5d04e-ca9c-497f-a6ae-51dff402752f/dmx-port-properties.png)

Check the the DMX namespace in the console to get help using these commands:

For example, if you enter `DMX.SetInputPortDeviceAddress`, the system prompts a question mark, which implies that `DMX.SetInputPortDeviceAddress ?` is the correct syntax.

You can specify this further. Entering `DMX.SetInputPortDeviceAddress MyInputPort` logs your current settings for the port.

#### General Ports Settings

In addition to the specific Input and Output Ports settings, there are general settings that apply to all ports.

![DMX general port settings.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4004edcb-77a6-49ed-9f05-93793fbd5ede/dmx-general-port-settings.png)

| **Setting** | **Description** |
| --- | --- |
| DMX Send Rate | The rate in Hertz (Hz) at which DMX data is sent. |
| Send DMX by default | Determines whether DMX data is sent to the network. |
| Receive DMX by default | Determines whether DMX data is received from the network. |
| All Fixture Patches receive DMX in Editor | When enabled, all fixture patches receive DMX data in the Editor, overriding their local settings. |

### Fixture Settings

DMX fixture settings are categorized in two sections.

-   Fixture Categories
    
-   Fixture Attributes
    

Both sections are arrays with set elements you can add or remove as necessary

![DMX fixture settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b1ba9be9-eb2d-4f15-9bde-a0fa4a99931f/dmx-fixture-settings.png)

#### Fixture Categories

The DMX Fixture Categories can be referenced in the DMX Library for convenience, which helps you better organize your various fixtures.

![DMX fixture categories](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2153db7d-ce90-4af5-91f9-2f6d572f1145/dmx-fixture-categories.png)

#### Fixture Attributes

We organized the DMX Fixture Attributes in a user-defined lookup table that provides us with a way to match the existing fixture terminology from the GDTF specifications to our internal functions.

![DMX fixture attributes](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ef092254-1588-4588-abc8-5df8ca90017d/dmx-fixture-attributes.png)

## Dropdown Menu

The DMX dropdown menu consolidates the DMX UI panels and features for quick and easy access.

![DMX UI and features dropdown menu](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6f439eb4-39bd-49a6-9803-55889c955212/dmx-dropdown.png)

### Channel Monitor

The DMX Channel Monitor is a debugging tool for visualizing DMX input and output for a specific Universe.

### Activity Monitor

The DMX Activity Monitor is a debugging tool for visualizing DMX input and output across all Universes at once. It displays all incoming and outgoing data.

### Control Console

The DMX Control Console is an editor tool for setting, testing and sending DMX data for a given selection of DMX Libraries and Patches through the use of easy to use faders.

### Patch Tool

The DMX Patch Tool is a small utility widget that conveniently allows you to batch patch a selection of Actors in your level.

### Receive DMX

Sets whenever DMX is received from the Network.

### Send DMX

Sets whenever DMX is sent to the Network.

## DMX Assets

### DMX Library

This asset consolidates all data related to DMX and MVR, such as manually created or GDTF imported fixtures, attribute or channel settings, and finally patching information.

![DMX Library option in the menu.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d22d39fe-d692-4d31-ab54-67f2cded6b6a/dmx-library.png)

### DMX Pixel Mapping

This asset consolidates all data related to Pixel Mapping, such as input binding, referenced DMX Library and patches, 2D positioning grid, color management, and various other settings.