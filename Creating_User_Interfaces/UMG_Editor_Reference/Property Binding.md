# Property Binding

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/property-binding-for-umg-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/property-binding-for-umg-in-unreal-engine)  
**Processed:** 2025-06-14 16:45:01

---

One of the most useful aspects inside UMG is the ability to bind properties of your Widgets to Functions or Properties inside the Blueprint. By binding a property to a Function or Property Variable in your Blueprint, anytime that Function is called or Property is updated, it will be reflected in the Widget.

## Function Binding

Say for instance you had a **Progress Bar** Widget and you wanted to update it to reflect a player's health at all times. Under **Appearance** for the Progress Bar you will notice a **Percent** option with the option to **Bind** the Percent value to a Function or Property.

![Select Bind for the Percent value](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d63fd643-cb38-4605-b18d-0509b3eb80f3/ue5_1-01-bind-percent.png "Select Bind for the Percent value")

After clicking the **Bind** button and selecting the **Creating Binding** option, a new Function will be created and open up.

![New Function for binding](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e559e84a-6609-496f-bf71-f2a0ed09298a/ue5_1-02-new-function.png "New Function for binding")

The **Return Value** is tied to the Percent's Value, so you can plug in a value to feed your Progress Bar data.

![Script for binding function](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/65d2f506-cf96-41f4-8e04-ffd9fde6107e/ue5_1-03-function-script.png "Script for binding function")

Above, the Function gets a variable called **Player Health** from inside our Character Blueprint. Anytime the Player Health variable is updated, it is automatically passed to and reflected as the Percent Value on the Progress Bar.

## Property Binding

**Property Binding** consists of specifying a Property Variable that is bound to a Widget's property. When the Property Variable is updated, the setting that is bound to it is automatically updated and reflected in the Widget.

An example of binding a Property Variable for a button is illustrated below.

![Widget Blueprint layout](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/44e596ec-a91e-4156-a8cd-b06bdc3255c3/ue5_1-04-layout.png "Widget Blueprint layout")

In the image above, you can see three button for a Main Menu: **Continue**, **Start**, and **Quit**. You can make **Continue** button to only be enabled if the player has a Save Game. Under the **Behavior** section for the **Continue** button, you can un-check **IsEnabled** (so the button is not enabled by default) and then click the **Bind** button.

![Un-check IsEnabled option under Behavior](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c05fad1a-6d88-4834-8c74-06c190e975d0/ue5_1-05-uncheck-isenabled.png "Un-check IsEnabled option under Behavior")

On the **Graph** tab for this Widget Blueprint, you could then create a **Boolean** variable and once it has been created, can assign it via the Bind button (below we have created a Boolean called **DoesSaveExist?**).

![Assign variable via the Bind button](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/deaa77ab-4c82-4a22-82ab-92ae1f3261f3/ue5_1-06-select-variable.png "Assign variable via the Bind button")

With this variable bound to the **IsEnabled** Behavior, you could then set this whenever your game is started by checking if a save file is present and if so, Casting to this Widget Blueprint to access and set the **DoesSaveExist** variable to *True* which would then enable the button.

If you bind a property of a Widget and then directly call the **Set** function on that Widget, it will break the binding.