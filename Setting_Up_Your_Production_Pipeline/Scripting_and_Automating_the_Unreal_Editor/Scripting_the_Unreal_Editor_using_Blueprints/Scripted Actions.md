# Scripted Actions

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/scripted-actions-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/scripted-actions-in-unreal-engine)  
**Processed:** 2025-06-14 16:48:05

---

**Scripted Actions** are **Editor Utility Blueprints** that you launch in the **Unreal Editor** by right-clicking Assets in the **Content Browser**, or by right-clicking Actors either in the **Level Viewport** (shown above) or in the **World Outliner**.

This kind of workflow is especially useful any time you need your Blueprint logic to have contextual awareness about a certain set of **Assets** or **Actors**. Typically, a **Scripted Action** gets the list of Assets or Actors that are selected at the time you run the action, then modifies those objects or otherwise takes them into consideration in its graph.

The instructions on this page show you how to create and launch these kinds of Editor Utility Blueprints, and how you can customize them to apply only to specific types of Assets or Actors.

## Steps

In this procedure, we'll create a new Editor Utility Blueprint class from one of the parent classes that support Scripted Actions, and we'll set up a new event graph for that class that will show up as a Scripted Action.

1.  In the **Content Browser**, right-click the folder where you want to create your new class, and choose **Editor Utilities > Editor Utility Blueprint** from the context menu.
    
    ![Create Editor Utility Blueprint](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a673671a-4578-4920-b580-27693d770084/01_createeubp.png "Create Editor Utility Blueprint")
2.  Decide whether you want your Scripted Action to operate on Assets that you select in the **Content Browser**, or on Actors that you select in the **Level Viewport** or **World Outliner**.
    
    -   If you want your Scripted Action to operate on Assets, choose **AssetActionUtility** as the parent class, then press **Select**.
        
    -   If you want your Scripted Action to operate on Actors, choose **ActorActionUtility** as the parent class, then press **Select**.
        
    
    ![Choose ActorActionUtility or AssetActionUtility](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/391df744-dc58-4783-b094-0f4ffb1d21e8/02_chooseparentclasseubp.png "Choose ActorActionUtility or AssetActionUtility")
3.  Give your new class a descriptive name in the **Content Browser**.
    
    ![Name your new class](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1ee561f9-c685-4397-8767-afde996ac868/03_renameeubp.png "Name your new class")
    
    You won't see this class name when you run its Scripted Actions. You'll need it only to distinguish this class from the other Blueprint classes in your Project if you need to modify your Scripted Actions or add new ones later.
    
4.  Double-click your new class to open it in the Blueprint Editor.
    
5.  To create a Scripted Action for this class, you can either create a new function, or create a new **Custom Event** node in the Event Graph for the class.
    
    Make sure that the **Call In Editor** box is checked on the function entry node or the Custom Event node. This is automatically done for you when you create a new function, but you'll have to do it yourself if you choose to use a Custom Event.
    
    For example, this new function on an **AssetActionUtility** iterates through the list of Assets that are selected in the Content Browser, and prints the name of each one in the **Level Viewport**.
    
    The image below shows a similar function implemented on an **ActorActionUtility**.
    
    You'll find some useful Blueprint nodes for your Scripted Actions under the **Development > Editor** category, including the nodes shown in the examples above that return a list of the objects selected at the time your Scripted Action is run: **Get Selected Assets**, which returns an array of references to all the Assets selected in the **Content Browser**, and **Get Selection Set**, which returns an array of Actors that are currently selected in the Level.
    
    You also will want to install the **Editor Scripting Utilities** Plugin, if you haven't already, to get access to additional function libraries for working with Assets and Level Actors. See [Scripting and Automating the Editor](/documentation/en-us/unreal-engine/scripting-and-automating-the-unreal-editor).
    
6.  **Save** and **Compile** your Blueprint class.
    

## End Result

Once your Blueprint class is saved and compiled, you should see a new **Scripted Actions** sub-menu in the context menu for either Assets or Actors, depending on the parent class you chose for your Blueprint class. This sub-menu contains each of the functions or Custom Events that you set up in your Blueprint class.

For example, when you right-click one or more Assets in the **Content Browser**:

![Run a Scripted Action on selected Assets](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6f75e1fe-2aee-4064-9002-04beccb0deef/06_scriptedactionsrunassets.png "Run a Scripted Action on selected Assets")

Or when you right-click one or more Actors in the **Level Viewport** or **World Outliner**:

![Run a Scripted Action on selected Actors](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e6313032-187b-4e7e-9db8-c5d8ce35a85a/07_scriptedactionsrunactors.png "Run a Scripted Action on selected Actors")

Each function and Custom Event that you set up on your **AssetActionUtility** or **ActorActionUtility** class becomes available as a separate option in the context menu. You can create as many different Scripted Actions as you need within a single Blueprint class, or you can create multiple Blueprint classes and distribute your Scripted Actions across those classes.

## Restricting an Action to a Specific Class

If you compile and save your Blueprint, and then begin right-clicking actors in the level, you may notice the **Scripted Actor Actions** option appear in the context menu. The script is available for any actor class, which can cause confusion if the script is not designed for multiple classes. To control what actors artists can affect, you can restrict the scripted action to a specific class.

To adjust the supported class:

1.  In the top toolbar, click **Class Defaults**.
2.  On the **Supported Classes** bar, click the plus **(+)** icon.
3.  Search for and click **Static Mesh Actor**.
    
    ![Class Defaults](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/064f7a46-cc7c-487a-8eb1-0c72c951fc17/class-defaults.png)
4.  **Compile** (Ctrl + Alt) and **Save** (Ctrl + S).

## Dynamic Inputs

You can set up your Scripted Actions to require information from the user who invokes them. If you add one or more **Inputs** to your function entry node or Custom Event node, you'll be prompted to supply that input each time you run the Scripted Action in the editor. This can be useful any time your script needs some extra information that may be different each time you call the action.

For example, this function has three inputs: a string, an Actor Object Reference, and a Material Object Reference:

![A function with inputs](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/70d8c186-cbdb-42bb-b1a7-69a2e942ceac/12_funcwithinputnode.png "A function with inputs")

When you run the Scripted Action for this function, the editor pops up a small window for you to set these input values:

![Set input values](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ceaba71c-d668-47a7-bbe6-e421a375288c/13_setinputvsluewindow.png "Set input values")

The editor validates that each input matches the type of value it is supposed to be. However, it doesn't guarantee that the inputs will have values at all, or that those values will make sense in any particular context. Keep in mind that your script should handle unspecified input values and validate the input values the user does provide.