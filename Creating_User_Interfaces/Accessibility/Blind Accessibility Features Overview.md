# Blind Accessibility Features Overview

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/blind-accessibility-features-overview-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/blind-accessibility-features-overview-in-unreal-engine)  
**Processed:** 2025-06-14 16:10:18

---

Visual interfaces can pose significant barriers for people who find it hard to see them. There are a number of strategies you can use to make your interfaces more accessible, including size and contrast, but there's one in particular that is essential for people with no vision: **text-to-speech**.

This means the visual information about your interfaces is communicated by synthesized speech, ideally covering both the text within the interface and also information about types of interface element and what state they're in.

This functionality is standard in other industries and rapidly spreading in game development. It is useful for blind gamers, gamers with low vision (e.g. wanting to save their eye strain for gameplay), and people with some cognitive conditions, and can help to meet some areas of CVAA compliance too.

CVAA is accessibility legislation that applies to all games for sale in the USA that have voice, text, and/or video chat functionality.

To learn more about the legal requirements of CVAA, refer to the [Demystifying CVAA](https://igda-gasig.org/what-and-why/demystifying-cvaa/) page on the IGDA Game Accessibility SIG (IGDA-GASIG) website.

**Unreal Engine 5** provides three plugins to assist developers in complying with CVAA requirements for blind users. These plugins are:

-   Text To Speech
    
-   Screen Reader
    
-   Slate Screen Reader
    

## Text To Speech Plugin

Text to speech (TTS) is a software technology that is used to provide auditory output in the form of a digital, synthesized, spoken voice. An example of TTS is a GPS device where the digital voice calls out directions when navigating to a destination. Another example is a smart assistant on your phone who reads out answers to you .

Unreal Engine's **Text To Speech** plugin provides basic functionality that supports accessibility for blind users by vocalizing text strings in your project. For example, you can use this plugin to read out the label, type and of an interface element (for example, "volume, slider, 30%"), or to vocalize the incoming messages in a text chat for an online game.

Currently, the TTS plugin only supports English across all platforms. We plan to support additional languages in the future.

## Screen Reader Plugin

A screen reader is a piece of assistive technology that helps blind users interact with a software application. It conveys visual information on screen, such as text or images, using non-visual means such as text to speech or Braille. It also offers blind users alternative means of interacting with user interface (UI) elements on-screen. For example, instead of using a mouse, a blind user can use special key combinations on a keyboard to change the focused object on the screen.

Screen readers can simulate actions that could be difficult for a blind user to do, such as right-clicking a UI element or scrolling the mouse wheel while inside the bounds of a UI element.

Unreal Engine's **Screen Reader** plugin takes text to speech functionality and expands it to provide a richer set of features. It offers a base framework that you can use to implement your own custom screen reader solution.

Features of this plugin include:

-   Requests for text to be vocalized via TTS.
    
-   Queueing a series of accessible announcements to be vocalized via TTS.
    
-   Requesting the contents of accessible UI elements be vocalized to the user.
    

When this plugin is enabled, the Text To Speech plugin is automatically enabled as well.

If you are using [Slate](/documentation/en-us/unreal-engine/slate-overview-for-unreal-engine) to implement your UI, consider using the Slate Screen Reader plugin instead.

## Slate Screen Reader Plugin

The **Slate Screen Reader** plugin is built on the base framework provided by the Screen Reader plugin. You can refer to this plugin as a sample for how to implement a screen reader for your own custom UI solution, or use it as-is if you are using Slate to implement your UI.

The goal of the plugin is to be "plug-and-play" for accessibility. When the plugin is enabled, all currently supported accessible Slate and UMG UI elements will have their contents vocalized when a user focuses on a UI element.

When this plugin is enabled, the Text to Speech and Screen Reader plugins are automatically enabled.

The plugin currently supports the following types of widgets:

-   Button
    
-   Check box
    
-   Combo box
    
-   Hyperlink
    
-   Image
    
-   Layout
    
-   Scroll bar
    
-   Slider
    
-   Text
    
-   Text (editable)
    
-   Window
    
-   List
    
-   List item
    
-   Unknown
    

## Choosing Which Plugin to Use

Use the information below to choose the right accessibility plugin for your project.

-   If you use a simple UI that doesn't require complex user interaction, consider the **Text To Speech** plugin as a lightweight solution to provide basic accessibility for blind users.
    
-   If you use Slate as your UI solution, use the **Slate Screen Reader** plugin.
    
-   If you use a UI solution other than Slate, you may need to implement your own custom screen reader. Use the **Screen Reader** plugin as a base framework for this.
    

You can refer to the Slate Screen Reader plugin for a sample implementation to guide your own custom screen reader development.

## Enabling the Plugins

You can enable all three plugins from the main menu (**Edit > Plugins**). If you need more information about how to enable plugins, refer to the [Working with Plugins](/documentation/en-us/unreal-engine/working-with-plugins-in-unreal-engine) page.

Before you can enable the **Screen Reader** and **Slate Screen Reader** plugins, you need to enable accessibility features for your project and / or Unreal Engine installation.

The steps to do this are the same, but the configuration file you need to edit are different based on whether you want to enable accessibility features for one specific project or for all of UE:

-   Project only: Open the `Config\DefaultEngine.ini` file.
    
-   All of UE: Go to the `C:\Program Files\Epic Games\UE_[Version]\Engine\Config` folder, then open either `BaseEditorSettings.ini` or `BaseEngine.ini`.
    

Add the following line to the `.ini` file you opened:

`Accessibility.Enable=1`

Save and close the file. If Unreal Engine is running, you may have to restart it before your changes take effect.