# Working with Plugins

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/working-with-plugins-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/working-with-plugins-in-unreal-engine)  
**Processed:** 2025-06-14 17:04:53

---

A **plugin** is an optional software component that adds specific functionality to **Unreal Engine**. Plugins can add entirely new features and modify built-in functionality without modifying the Unreal Engine code directly. For example, a plugin might add new menu items and toolbar commands to the editor, or even add entirely new features and editor sub-modes.

You can enable or disable plugins independently for each project, depending on your needs.

There are two types of plugins available in Unreal Engine:

-   Unreal Engine plugins.
    
-   Third-party plugins.
    

## Enabling a Plugin

To enable an Unreal Engine plugin, follow these steps:

1.  From the main menu, go to **Edit > Plugins**. This opens the **Plugins** window.
    
    [![Plugins window in Unreal Engine 5](https://dev.epicgames.com/community/api/documentation/image/dba988ca-aac7-4828-96ca-5fc2b81ed8c9?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/dba988ca-aac7-4828-96ca-5fc2b81ed8c9?resizing_type=fit)
    
    Plugins window in Unreal Engine 5.
    
2.  Find the plugin you want to enable using the list on the left of the screen. Alternatively, enter a term in the **Search** box to search for all plugin names and descriptions that contain this term.
    
    [![Searching for a plugin by name](https://dev.epicgames.com/community/api/documentation/image/800c9461-5550-4dfd-8711-0d4926c767c3?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/800c9461-5550-4dfd-8711-0d4926c767c3?resizing_type=fit)
    
    This example shows all search results for the term "xr". Note that the search term is highlighted everywhere it appears.
    
3.  To enable a plugin, click the checkbox next to it.
    
    [![Enabling a plugin.](https://dev.epicgames.com/community/api/documentation/image/b2e0efa1-48e5-4a2a-bae2-fb2af3e72558?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/b2e0efa1-48e5-4a2a-bae2-fb2af3e72558?resizing_type=fit)
    
    Enabling a plugin.
    
    For plugins that are not production-ready, such as beta plugins, you might see a warning asking you to confirm that you want to enable that plugin.
    
4.  Save your work, then restart Unreal Engine.
    

Third-party plugins might require additional steps before you can enable them. For more information, refer to the documentation for the third-party plugin you want to install. Note that Epic Games is not responsible for the contents of third-party plugins.

## Disabling a Plugin

To disable a plugin, follow these steps:

1.  From the main menu, go to **Edit > Plugins**. This opens the **Plugins** window.
    
    [![Plugins window in Unreal Engine 5](https://dev.epicgames.com/community/api/documentation/image/cd625ff4-2bdf-420f-8c13-97788f71866d?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/cd625ff4-2bdf-420f-8c13-97788f71866d?resizing_type=fit)
    
    Plugins window in Unreal Engine 5.
    
2.  Find the plugin you want to disable using the list on the left of the screen. Alternatively, enter a term in the **Search** box to search for all plugin names and descriptions that contain this term.
    
    [![Searching for a plugin by name](https://dev.epicgames.com/community/api/documentation/image/65648dec-3ca3-413a-9dee-96cde9be0111?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/65648dec-3ca3-413a-9dee-96cde9be0111?resizing_type=fit)
    
    This example shows all search results for the term "xr". Note that the search term is highlighted everywhere it appears.
    
3.  To disable a plugin, clear the checkbox next to it.
    
    [![Disabling a plugin](https://dev.epicgames.com/community/api/documentation/image/cc700ea6-babc-4fa9-96f6-ad3a8fda2ada?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/cc700ea6-babc-4fa9-96f6-ad3a8fda2ada?resizing_type=fit)
    
    Disabling a plugin.
    
    If the plugin you want to disable is a *dependency* for other plugins (that is, other plugins require it to function), you will see a notification asking you if you want to disable those plugins as well. Note that this might break existing functionality in your project if you used any of those plugins to implement it.
    
4.  Save your work, then restart Unreal Engine.
    

## Installing Plugins from Fab

While Unreal Engine contains plugins that offer many different kinds of functionality, you can also install additional plugins from [Fab](https://www.fab.com), using the methods described below. The examples shown here use the free glTF Exporter plugin by Epic Games.

### Downloading Plugins from the Fab Website

You can browse and download plugins for Unreal Engine directly from the Fab site. You can also access Fab directly through a link in the Epic Games Launcher.

To download plugins from the site, follow these steps:

1.  In the **Epic Games Launcher**, navigate to the **Unreal Engine** tab, select **Fab** and click **Start exploring**.
    
    [![Fab tab in the Epic Games launcher](https://dev.epicgames.com/community/api/documentation/image/a79cc1fe-0257-4a9a-8983-c4adacf06145?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/a79cc1fe-0257-4a9a-8983-c4adacf06145?resizing_type=fit)
    
2.  You are redirected to the Fab site.
    
    [![The Fab website](https://dev.epicgames.com/community/api/documentation/image/a1417038-b9a0-4583-a1e0-c90b1b15f6d8?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/a1417038-b9a0-4583-a1e0-c90b1b15f6d8?resizing_type=fit)
    
3.  Search for the plugin you want to install and click the thumbnail to open the listing
    
    [![Searching for a plugin on Fab](https://dev.epicgames.com/community/api/documentation/image/afa87840-0309-472c-8048-816080861736?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/afa87840-0309-472c-8048-816080861736?resizing_type=fit)
    

The next step depends on whether you selected a [free plugin](https://dev.epicgames.com/documentation/en-us/unreal-engine/working-with-plugins-in-unreal-engine) or a [paid plugin](https://dev.epicgames.com/documentation/en-us/unreal-engine/working-with-plugins-in-unreal-engine).

The following information is adapted from the [Acquiring Products section of the Purchasing and Downloading Products](https://dev.epicgames.com/documentation/en-us/fab/purchasing-and-downloading-assets-in-fab#acquire-products) page in the Fab documentation. Refer to that page for more information.

#### Free Plugin

To download a free plugin, follow these steps:

1.  On the plugin's listing click **Add to My Library**.
    
    [![Adding a plugin to your library](https://dev.epicgames.com/community/api/documentation/image/96ddc93b-0f39-41f9-9bf2-d855068b996d?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/96ddc93b-0f39-41f9-9bf2-d855068b996d?resizing_type=fit)
    
2.  Accept the Fab EULA.
    
    [![Accept the Fab EULA](https://dev.epicgames.com/community/api/documentation/image/82d70f60-a69c-40b3-b089-0a296fc80d38?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/82d70f60-a69c-40b3-b089-0a296fc80d38?resizing_type=fit)
    
3.  Your free plugin is now available in your Fab library on the Fab site and in the Epic Games launcher.
    
    [![Plugin saved in my library notification](https://dev.epicgames.com/community/api/documentation/image/756cdbaf-961b-4aba-8cb7-cedb875473b5?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/756cdbaf-961b-4aba-8cb7-cedb875473b5?resizing_type=fit)
    

#### Paid Plugin

To download a plugin for sale, follow these steps:

1.  Click the **Select a License** dropdown to view the available licenses. Select a license type if applicable. This can vary depending on the size of your organization.
    
    [![Select a license](https://dev.epicgames.com/community/api/documentation/image/889c8cfe-3e21-4a90-8664-3468ea6671c5?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/889c8cfe-3e21-4a90-8664-3468ea6671c5?resizing_type=fit)
    
2.  Select either **Buy now** or **Add to cart**.
    
    1.  If you select Buy now, you are shown the checkout screen where you can pay for your selected plugin directly. Go to step 4.
        
    2.  If you select Add to cart, your plugin is added to your cart. Continue to step 3.
        
3.  Click **View in cart**, then click the **Checkout** button to pay for your selections once you have all the plugins (and any other Fab products) you want to buy.
    
    [![Checking out](https://dev.epicgames.com/community/api/documentation/image/71c307e5-377b-4ba2-81e3-dd12b64f553e?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/71c307e5-377b-4ba2-81e3-dd12b64f553e?resizing_type=fit)
    
4.  Complete the checkout process, and you will see the same notification as for free plugins.
    
    [![Plugin saved in my library notification](https://dev.epicgames.com/community/api/documentation/image/beacad57-0055-48ce-9375-78387691c9b7?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/beacad57-0055-48ce-9375-78387691c9b7?resizing_type=fit)
    

#### Install your Plugin

After you have added your new plugin to your Fab library, you need to install it to Unreal Engine.

1.  Go to the Library tab in the launcher, then scroll down to the Fab Library section. Search for your new plugin, then click **Install to Engine**.
    
    [![Install to Engine button for a plugin](https://dev.epicgames.com/community/api/documentation/image/9d8e3466-0bed-4b91-9688-25704dee6674?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/9d8e3466-0bed-4b91-9688-25704dee6674?resizing_type=fit)
    
    If you can't find your new plugin, refresh the Fab Library.
    
    [![Refresh the Fab Library](https://dev.epicgames.com/community/api/documentation/image/71a9db6f-66e6-4154-8e73-a0a0c6eb7747?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/71a9db6f-66e6-4154-8e73-a0a0c6eb7747?resizing_type=fit)
    
2.  Select the engine version for the plugin installation, then click **Install**.
    
    [![Selecting an Unreal Engine version](https://dev.epicgames.com/community/api/documentation/image/599ed67a-7e6b-4109-95c7-aa77e41b4416?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/599ed67a-7e6b-4109-95c7-aa77e41b4416?resizing_type=fit)
    
    When installing a plugin or other asset, only supported versions of Unreal Engine are available, even if you have other Unreal Engine versions installed.
    
3.  After the installation completes, open the version of Unreal Engine you installed the plugin for, and **enable** the plugin following the instructions in the [Enabling a Plugin](https://dev.epicgames.com/documentation/en-us/unreal-engine/working-with-plugins-in-unreal-engine) section on this page.
    

### Downloading Plugins From Fab Inside Unreal Engine

You can download plugins (and other content) using the Fab plugin while you are working inside Unreal Engine. Before you can install additional plugins from Fab, you must first [enable the Fab plugin](https://dev.epicgames.com/documentation/en-us/unreal-engine/working-with-plugins-in-unreal-engine).

[![Fab plugin in Unreal Engine](https://dev.epicgames.com/community/api/documentation/image/ca1654b2-ea91-40ff-9a32-31263690f99e?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/ca1654b2-ea91-40ff-9a32-31263690f99e?resizing_type=fit)

After you install the plugin, you can access it from the following options in Unreal Engine:

-   In the **Windows** menu, scroll down to the **Get Content** section and click **Fab**.
    
    [![Fab in the Unreal Engine Windows menu](https://dev.epicgames.com/community/api/documentation/image/672ad83c-949c-41f8-94df-e147b1b6e7b6?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/672ad83c-949c-41f8-94df-e147b1b6e7b6?resizing_type=fit)
    
-   In the **Content Drawer**, click the **Fab** button right next to the **+Add** button.
    
    [![Fab in the Content Drawer](https://dev.epicgames.com/community/api/documentation/image/026c9952-126d-47d3-b168-e09eaef73fb2?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/026c9952-126d-47d3-b168-e09eaef73fb2?resizing_type=fit)
    

In the Fab window, you can search for and acquire plugins (both free or paid) in the same way as on the Fab site.

[![Fab window in Unreal Engine](https://dev.epicgames.com/community/api/documentation/image/d344d342-197b-4829-8fee-60dc9630787a?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/d344d342-197b-4829-8fee-60dc9630787a?resizing_type=fit)

Only plugins usable with Unreal Engine appear in the Fab window inside Unreal Engine. Content for other platforms is not available.

After you add a plugin to your library, you must download and install it to use it. To install your new plugin, quit out of Unreal Engine, and find the plugin in your Fab Library. Click **Install to Engine**, and proceed as previously described above.

[![Install to Engine button for a plugin](https://dev.epicgames.com/community/api/documentation/image/d2be7027-7099-42b1-87c5-b9b9d0ea91a8?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/d2be7027-7099-42b1-87c5-b9b9d0ea91a8?resizing_type=fit)

[![Selecting an Unreal Engine version](https://dev.epicgames.com/community/api/documentation/image/e322b603-96b8-4b2f-9dfa-f9cec9933eaa?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/e322b603-96b8-4b2f-9dfa-f9cec9933eaa?resizing_type=fit)

## Plugin Installation Locations

Unreal Engine stores all plugins at the following locations:

-   `C:\Program Files\Epic Games\UE_[version]\Engine\Plugins` on Windows
    
-   `/Users/Shared/Epic Games/UE_[version]/Engine/Plugins` on macOS