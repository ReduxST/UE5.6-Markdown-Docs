# Advanced Multi-User Networking

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/advanced-multi-user-networking-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/advanced-multi-user-networking-in-unreal-engine)  
**Processed:** 2025-06-14 16:05:10

---

The instructions in the [Multi-User Editing Quick Start](/documentation/en-us/unreal-engine/getting-started-with-multi-user-editing-in-unreal-engine) show how to work with the **Multi-User Editing** system in a simple Local Area Network (LAN), where clients can automatically discover the Multi-User Editing server. However, automatic server discovery is not always possible. Sometimes, you may need to do some extra configuration on the computers that you want to connect through Multi-User Editing.

This page contains some strategies that may help you successfully establish a connection when the **Unreal Editor** cannot automatically discover your Multi-User Editing server.

## Same LAN, Same Subnet

If the Unreal Editor and the Multi-User Editing server are on the same LAN and the same subnet, but they aren't able to discover each other automatically, the cause might be that one or both of them is not set to broadcast or listen to multicast traffic on the correct network interface of the computer. To force Unreal Engine to use a specific network interface, you'll need to specify it as the unicast endpoint IP.

### Configuring the Editor

To set the unicast endpoint IP address in the Unreal Editor:

1.  From the main menu, select **Edit > Project Settings**.
    
2.  In the **Project Settings** window, go to the **Plugins > UDP Messaging** section, and find the **Transport > Unicast Endpoint** setting.
    
    ![Unicast Endpoint](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fe9bcb53-8165-44a5-9b3d-5e50a6cfdc56/01-multiuserediting-network-unicastendpoint.png "Unicast Endpoint")
3.  Set the value of this property to the IP address of the network interface you want the Unreal Editor to use. Always use port **0**. For example, `192.168.10.73:0`.
    

### Configuring the Server

To set the unicast endpoint IP address for the Multi-User Editing server, you can follow the instructions given above to set up the unicast endpoint for the Unreal Editor, then launch the server from the **Toolbar** in the Editor. If you launch the server this way, it will automatically use the same unicast IP address as the editor that launched it.

Alternatively, you can follow the instructions below to configure the IP address manually:

1.  If your server is already running, shut it down.
    
2.  In your Unreal Engine installation folder, go to the `Engine/Programs/UnrealMultiUserServer/Saved/Config/<platform>` folder, and open the `Engine.ini` file in a text editor. If that file doesn't already exist, create it.
    
3.  Add the following block of settings to the file:
    
    ```
            `[/Script/UdpMessaging.UdpMessagingSettings]         EnableTransport=True         UnicastEndpoint=192.168.0.73:0         MulticastEndpoint=230.0.0.1:50000         MulticastTimeToLive=1         EnableTunnel=False         TunnelUnicastEndpoint=         TunnelMulticastEndpoint=`
    Copy full snippet
    ```
    \[/Script/UdpMessaging.UdpMessagingSettings\] EnableTransport=True UnicastEndpoint=192.168.0.73:0 MulticastEndpoint=230.0.0.1:50000 MulticastTimeToLive=1 EnableTunnel=False TunnelUnicastEndpoint= TunnelMulticastEndpoint=
4.  Set the value of the `UnicastEndpoint` setting to the IP address of the network adapter you want the Unreal Editor to use. Always use port **0**.
    
5.  Save the file and restart your server.
    

## Same LAN, Different Subnet

If you want to connect an instance of the Unreal Editor to a server that is not on the same subnet, you will need to do some extra configuration for both the server and the Editor. This involves setting up the server with a port for its unicast endpoint, then setting up the Unreal Editor to connect to the server's unicast IP address and port as a static endpoint.

### Configuring the Server

You need to configure your Multi-User server to use a pre-defined port for its unicast endpoint. There are several ways you can accomplish this:

-   If you want to launch your Multi-User server manually, you can follow the same procedure given in the previous section for setting up the unicast endpoint in the configuration file. However, instead of port `0`, use a different port number in the range `50000` - `60000`.
    
-   If you want to launch your Multi-User server from the Unreal Editor, the easiest approach is to set the port number you want to use in the **Server Port** setting that you can find in the **Project Settings** window under the **Plugins > Multi-User Editing** section. This value will automatically override any port value you set for the unicast endpoint in the **Plugins > UDP Messaging** section.
    
    See also the [Multi-User Editing Reference](/documentation/en-us/unreal-engine/multi-user-editing-reference-for-unreal-engine#multi-usereditingsettings)
    
-   Alternatively, you could follow the procedure given in the previous section for setting up the unicast endpoint in the **Project Settings** window under the **Plugins > UDP Messaging** section. However, instead of port `0`, use a different port number in the range `50000` - `60000`.
    
    If you choose this third approach, the server will always use a port number one higher than the one you set. This ensures that there won't be a conflict between the Editor and the server when they run on the same machine. When you configure the static endpoint for your other Unreal Editor instances in the following section, you will need to remember to add one to the port number you set in the **Project Settings**. For example, if you set `50000` as the port number for the unicast endpoint in the Editor that you use to launch the server, you will need to configure other instances of the Editor to connect to the static endpoint with port `50001`.
    

### Configuring the Editor

To make an instance of the Unreal Editor on a different subnet capable of connecting to the server, you need to specify the IP address and port of the server as a static endpoint.

To set up a static endpoint in the Unreal Editor:

1.  From the main menu, select **Edit > Project Settings**.
    
2.  In the **Project Settings** window, go to the **Plugins > UDP Messaging** section. Expand the advanced settings under the **Transport** section and find the **Static Endpoints** setting.
    
    ![Static Endpoints list](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a35d08ba-3f86-4744-8258-d9e4a9902f8f/02-multiuserediting-network-staticendpoints.png "Static Endpoints list")
3.  Press **+** to add a new item to the list, and set the value of the new item to the IP address and port that you set up for your server's unicast endpoint.
    
    ![Set the server's IP address](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b268b2fd-e6e3-4c6a-a8e2-ff080400e715/03-multiuserediting-network-staticendpoints-added.png "Set the server's IP address")