# Localization Key Debugging

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/debugging-localization-keys-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/debugging-localization-keys-in-unreal-engine)  
**Processed:** 2025-06-14 16:19:23

---

The **localization key debug culture** is a special [localization culture](/documentation/en-us/unreal-engine/managing-the-active-culture-at-runtime) that helps you debug localized text. If you set the culture for your application to a value of `keys`, any localized text in your UI displays its localization key rather than the display text. This includes both text that is localized using [string tables](/documentation/en-us/unreal-engine/using-string-tables-for-text-in-unreal-engine) as well as text localized through the `LOCTEXT` macro in C++. This makes it easier to determine localized text that may have problems, especially for complex UI, as you can observe the keys directly in the context of the displayed text and match them to the table quickly.

To use the Localization Key debug culture, follow these steps:

1.  Do one of the following:

-   Run a **Development** or **Debug** build of your application. See the \[Packaging\] section for more details.
    
-   Run your application in **Unreal Editor** using **Play In Editor**.
    
    Changing the localization culture in the console in Unreal Editor will change the language used for the editor's text as well as text inside your preview. We recommend using a Development or Debug build rather than in Unreal Editor to keep your environment clean and avoid confusion.
    

1.  Tap the tilde (**~**) key to bring up the **console**.
    
2.  Type the following command and press Enter:
    
    ```
         `-culture=keys`
    Copy full snippet
    ```
    \-culture=keys

After you input this command, any localized text in your UI will shows its key instead of the normal text.

![The Lyra sample project with the Keys culture active. ](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/29d18cf3-fb25-40dc-8f6d-c55a99400540/debug_keys_editor.png)

Example of the Lyra main menu with the Keys debug culture active. Slate.LogPaintedText is set to true, so the log displays the full localization keys of painted text in the preview.

### Displaying Full Localization Keys

You can set `Slate.LogPaintedText` to 1 or `true` to have the log print any text currently painted onscreen. This makes it possible to see the full localization key without any UI clipping issues.