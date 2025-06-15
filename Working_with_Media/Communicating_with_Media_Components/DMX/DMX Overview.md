# DMX Overview

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/dmx-overview](https://dev.epicgames.com/documentation/en-us/unreal-engine/dmx-overview)  
**Processed:** 2025-06-14 16:21:04

---

## What is DMX?

[DMX](https://en.wikipedia.org/wiki/DMX512) stands for "Digital Multiplex" and is a standard for digital communication networks commonly used in the Live Events space to control simple to complex stage lighting and effects. It was originally intended as a standardized method for controlling light dimmers, which, prior to DMX512, had employed various incompatible proprietary protocols. It soon became the primary method for linking controllers (such as a lighting console) to dimmers and special effects devices such as fog machines and intelligent lights.

DMX has also expanded to uses in non-theatrical interior and architectural lighting, at scales ranging from strings of Christmas lights to electronic billboards. DMX can now be used to control almost anything, reflecting its popularity in theaters and venues. DMX is used throughout the industry to control various devices such as lighting fixtures, lasers, smoke machines, mechanical devices, among many others.

Now, in the context of Virtual Production, DMX is gaining momentum and being used both ways. First, to control and trigger events in Unreal using a lighting desk. Second, to drive large sets of DMX enabled lighting fixtures and devices, for example, through the means of the Pixel Mapping tool where the generated image and pixels are used to drive fixtures RGB values. Finally, another important use-case to highlight is high quality previs of DMX powered shows, projects and virtual production setup, inside UE.

## Protocols

We added DMX functionality by supporting both **[Art-Net](https://en.wikipedia.org/wiki/Art-Net)** and **[sACN](https://en.wikipedia.org/wiki/Architecture_for_Control_Networks)** industry variants.

Art-Net and sACN are network protocols allowing to aggregate and send DMX data over Ethernet (IP). Art-Net allows sending 32,768 universes down a single network cable. Although it is an older protocol, it is supported by more gear and devices. sACN (streaming architecture for control networks), currently appears more popular and allows you to run 63,999 universes of DMX data down a single network cable.

## DMX Data

DMX can be thought of as a package of digital information that is being sent from one location (our source) to a different location (or destination). Each package is created at some source with specific information that should be received and read by some recipients. Each packet is structured in a very intentional way and if you would like to know more about how this works on the hardware level, please read the **[ESTA standards](https://tsp.esta.org/tsp/documents/docs/ANSI-ESTA_E1-11_2008R2018.pdf)**. For our purposes, we are only concerned with the contained data. Each package contains an array of 512 bytes, each of which has a value that ranges from 0-255.

![DMX data structure](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e4d0202e-24c5-41f1-8f67-b825f9389902/dmx-data.png)

Each byte is commonly referred to as a **Channel**. A transmitted package consisting of 512 channels is commonly referred to as a **Universe**.

## DMX Using Unreal Engine

Using Unreal Engine, you can control your fixtures directly using DMX over ethernet using an interface device. UE can act as the signal source, transmitting data using the Art-Net or sACN protocols to DMX and then on to the daisy-chained fixtures that make up your installation, and also directly receive and interpret DMX messages sent back from your fixtures.

You can also use UE to work with a lighting console, either interpreting and passing along DMX instructions sent by a lighting console for connected DMX fixtures, or sending DMX data about a scene rendered in UE to a lighting console.

![Fixtures networked to a computer acting as a DMX console](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ca2e2b95-c9f3-4017-8331-7ef28194fb84/console-organization.png)

Here, Unreal Engine would be running on the computer acting as the source of the DMX data. To view the image source, click here.

Support for USB interfaces is not implemented in this Engine version.

## DMX Fixtures

DMX fixtures are the devices actually responsible for receiving and executing commands based on the data received. This could mean turning a light on or off or rotating the device 90 degrees. There are many sorts of DMX fixtures from standard stage lights that simply turn on and off to intelligent lights that have multi-directional rotation and lighting filters.

Each fixture has a set of attributes/commands that are predefined on the hardware level. These attributes are organized into various functionality groups called **Modes**. Often fixtures contain multiple modes which predefine the available attributes the fixture will respond to and enable or disable certain features.

Fixture manufacturers give the user different mode options so that they can cater to a large range of use cases, including as many features as possible while allowing the user to pick and choose which are the most important to them. This results in the simplest, smallest channel count mode; a complex, huge channel mode; and some in-between modes. A lot of the time in professional lighting practice, the intermediate modes are chosen for their balance between features and ease of control, along with more frugal use of the DMX channel count.

Each mode contains a set of attributes. Attributes are responsible for telling the hardware how to respond to the received DMX data. In most cases, you can find all attributes for a particular fixture outlined in the fixture manual provided with the device.

![DMX light fixtures](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d7b39136-e9f0-4108-b251-6bd65d513228/dmx-light-fixtures.png "DMX light fixtures")

## Signal Communication

Let us next consider how UE and fixtures talk to each other using DMX. UE can drive one or many universes, each of which has multiple fixtures daisy-chained in a long string. You can think of a universe as a form of identification for a group of addressed fixtures. To send data to the proper fixture, you need to also send it to the correct universe.

Once you command UE to distribute a DMX packet, UE locates the proper universe and sends a packet of data down the string for each connected fixture to receive and interpret. Each fixture receives the same packet of data and executes an internal command if the packet contains any data meant for that fixture. Once the fixture reads the data, the data is then passed down the chain onto the next fixture to repeat the process. For the fixture to receive the proper information, it must be listening for the right data at the right address. This introduces the concept of fixture addressing or "patching", covered more in the next section.

Below you can see an overview of the signal hierarchy and data usage.

![The logical organization of a DMX network](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/82ec3773-b235-49c9-9dbd-933e758d65a6/dmx-network-org.png)

| **Name** | **Description** |
| --- | --- |
| Universe | Each universe can contain many fixtures daisy-chained together up to 512-bytes each. |
| Fixture | Each fixture occupies one or more addresses inside a universe. |
| Starting Address | A fixture's starting address determines how the fixture should interpret the received DMX data packet (a single index in the byte array). |
| Attribute | A fixture contains a set of attributes defined by its current mode which each take on an address determined by their attribute number (channel) plus the starting address (see the diagram below under Fixture Patching for an example). |

## Fixture Patching

The concept of fixture patching comes from the idea that you need to be able to virtually position your fixtures along a communication chain for them to receive the proper data. Since UE uses DMX to send full packets of data to be read by multiple fixtures, it is important to have a way for fixtures to identify exactly which bytes in the packet they should read and interpret, and which ones they should ignore.

You can do this by assigning each fixture at a specific starting address in a universe. A starting address can be anywhere between 1 and 512 (the maximum number of values in your DMX packet). When you assign a fixture to a specific starting address, it then occupies a range of addresses from the assigned starting address through the starting address plus the number of attributes the fixture contains in its current mode.

See the example below:

![Address ranges in an example universe.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/eef7fdc2-6d4d-44fb-b9bc-ef4ae2c7ff6f/universe-addresses.png)

**Fixture 2** current mode = 8ChannelMode (contains **8** attributes)

1.  Red (address 8)
    
2.  Green (address 9)
    
3.  Blue (address 10)
    
4.  Strobe (address 11)
    
5.  Pan (address 12)
    
6.  Tilt (address 13)
    
7.  Macro (address 15)
    

**Starting Address** = 8

**Address Range** = 8 - 15

Using the example above, in order to pan, the fixture will be listening on address 12 for a byte value between 0-255 which will ultimately control the amount the fixture will pan within its defined rotation range.

#### Attribute Resolution

Most commonly an attribute will operate with an input range of a single byte (for example, 0-255). Occasionally, higher resolution is needed to achieve more precision in movements or lighting control. If this is the case, attributes take on larger input ranges constructed of multiple bytes instead of just one. The combination of multiple bytes results in higher possible values for controlling a particular attribute. Below you can see the possible attribute signal types.

1.  **8 Bit Attribute** - Min: 0, Max: 255 - Occupies 1 address
    
2.  **16 Bit Attribute** - Min: 0, Max: 65,536 - Occupies 2 addresses
    
3.  **24 Bit Attribute** - Min: 0, Max: 16,777,215 - Occupies 3 addresses
    
4.  **32 Bit Attribute** - Min: 0, Max: 4,294,967,296 - Occupies 4 addresses
    

When an attribute using more than 8 bits is needed, that attribute occupies more than one address in the universe. Depending on the resolution, it can occupy multiple consecutive addresses. You can see the number of addresses an attribute will occupy in the list above.

## DMX Communication Over Network

Over the past few years, network communication methods for sending DMX data have become increasingly more popular and important. As shows get larger and the number of fixtures increases, addressing more fixtures in a fast, efficient, and reliable way becomes critical.

To overcome the channel restriction of DMX while still using its structure, ethernet protocols were developed. These protocols allow transmitting data from multiple DMX universes over a single Cat5 cable. The UE DMX plugin supports the two most widely-used ethernet protocols, Art-Net and sACN.

### Art-Net

Art-Net is a royalty-free communications protocol for transmitting the DMX512-A lighting control protocol and Remote Device Management (RDM) protocol over UDP. It is used to communicate between "nodes" (for example, intelligent lighting instruments) and a "server" (a lighting desk or general-purpose computer running lighting control software, in this case UE).

More detailed information about the Art-Net protocol can be found on the [Art-Net site](https://art-net.org.uk/structure/the-technology/).

### sACN

Streaming Architecture for Control Networks(sACN) is a standard protocol developed by ESTA to efficiently transmit DMX universe data over the network. It is comparable to Art-Net in many aspects. One advantage it offers is the multicast option allowing very easy configuration. sACN is a popular protocol for controlling large numbers of RGB LEDs.

# Protocol Integration

In the Unreal Engine DMX Plugin, cross-platform support for both receiving and sending DMX data through sACN and Art-Net protocol variants is included. Since both Art-Net and sACN are UDP network protocols, Unreal Engine's pre-existing network messaging features now natively implement each protocol built on top of the Unreal Engine architecture.

For this plugin, the most recent version of the Art-Net protocol, Art-Net 4, is integrated. Art-Net 4 has a theoretical limit of 32,768 universes or Port-Addresses (that is, 32 kiloverses) as opposed to Art-Net 3's universe limit of 256.

For the full Art-Net 4 protocol specification, you can find the official documentation [here](https://artisticlicence.com/WebSiteMaster/User%20Guides/art-net.pdf).

For published documentation on the sACN protocol visit this [link](https://tsp.esta.org/tsp/documents/published_docs.php).