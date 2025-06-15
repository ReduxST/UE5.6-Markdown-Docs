# Template Sequences

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/template-sequences-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/template-sequences-in-unreal-engine)  
**Processed:** 2025-06-14 16:53:41

---

Template Sequences enable the reuse of animation data created in Sequencer for Actors of a compatible class (same or inherited). Similar to how animation sequences can be played on any compatible Skeletal Mesh, Template Sequence animation can be played on any compatible Actor.

#### Prerequisites

-   You have an understanding of **[Sequencer](/documentation/en-us/unreal-engine/how-to-make-movies-in-unreal-engine)** and its **[Interface](/documentation/en-us/unreal-engine/sequencer-cinematic-editor-unreal-engine)**.
    
-   You have an understanding of **[Blueprints Visual Scripting](/documentation/en-us/unreal-engine/blueprints-visual-scripting-in-unreal-engine)**.
    

## Template Sequence Asset

To start using Template Sequences, you must first create a Template Sequence asset. Do this by right-clicking the **Content Browser** and selecting **Animation > Template Sequence**.

![create template sequence](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/051952c7-fd10-4b2d-82f2-e8c4806767b7/createts.png)

Next, select the root object class binding for the sequence.

![template sequence root binding](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8aa77f33-6d9c-411d-ac29-4511f2c2cda0/rootbinding.png)

Once created, double-click the asset to open the Template Sequence window. You should see your root object class added to the sequence as a **[Spawnable](/documentation/en-us/unreal-engine/spawn-temporary-actors-in-unreal-engine-cinematics)**.

![open template sequence](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8647f066-7765-4fa9-a290-bbce3f8e7c29/opents.png)

### Interface

The Template Sequence interface looks similar to Sequencer's interface, with the exception of certain unneeded items omitted from the toolbar.

A new **Bind Actor Class** button is added to the toolbar, which allows for rebinding the root Actor class.

![template sequence bind actor class button](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/877431a3-8867-45c0-912e-da7e237e0fff/tsbindbutton.png)

### Camera Animation Sequence

Template Sequences are commonly used for creating template camera animation. You can easily create a Template Sequence with a default binding to a camera by right-clicking the **Content Browser** and selecting **Animation > Camera Animation Sequence**.

Upon opening this Template Sequence, you will see a **[Cine Camera Actor](/documentation/en-us/unreal-engine/cinematic-cameras-in-unreal-engine)** added to the sequence. The **Bind Actor Class** button's behaviour has also changed to swap between the **Cine Camera Actor** and the **[Legacy Camera Actor](/documentation/en-us/unreal-engine/camera-actors-in-unreal-engine)**

![camera animation sequence](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/01bec604-abb4-40f4-9209-45dde42c2c3d/cameraanimseq.png)

## Usage

This section describes how to bind and rebind Actors to Template Sequences and assign your animations to other Actors of the same class.

### Binding Actors

Template Sequences require you bind your Actors as **[Spawnables](/documentation/en-us/unreal-engine/spawn-temporary-actors-in-unreal-engine-cinematics)** in order to animate. Therefore, you can bind or rebind Actors to your Template Sequence by dragging them from either the Content Browser or the **[Place Actors](/documentation/en-us/unreal-engine/placing-actors-in-unreal-engine)** panel.

![template sequence drag drop](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1ca7215a-68e3-4811-8f84-d46db6ba5e41/dragdropadd.png)

Only a single Actor can be added to a Template Sequence, as adding another Actor from a different class will change the current binding.

### Content Setup

If the content of your Template Sequence is meant to be additive, you will need to ensure your animation sections are set to **Additive**, **Relative**, or **Additive from Base**.

Do this by right-clicking the section keyframe area and selecting one of the **Additive** options from the **Blend Type** submenu.

![template sequence additive transform](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e70943ef-1fb0-4e4b-8c03-7f848a09f9d8/additivesetup.png)

You can then create your additive animation in the Template Sequence view. In this example the animation is of a simple bouncing ball, in which the ball hits the ground at the (0, 0, 0) coordinates.

![template sequence example](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/da9af773-df17-488d-8950-ee98a086973f/templateanim.gif)

### Apply Template Sequence Animation

Template Sequences are meant to be used on an Actor within a Level Sequence. The Actor's class must match the class that the Template Sequence was bound to.

In your Level Sequence, click the **\+ Track** button, navigate to **Template Sequence,** and select your **Template Sequence Asset**.

![template sequence track](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/db79f869-f5f6-48e5-9d8e-06372a4c7981/selectts.png)

You can apply your Template Sequence animation to any Actor of the same class. If your template is additive, the animation will apply additively to the Actor's current position.

![multiple template sequences](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2efd4202-66a5-4c14-b2e7-5c9179d32354/templateseqmulti.gif)

### Property Multipliers

Property Multipliers can be used on the Template Sequence instance as a way to modify the intensity of properties and transforms for each template instance. The multipliers available to add to a Template Sequence is based on the **[Property Tracks](/documentation/en-us/unreal-engine/cinematic-transform-and-property-tracks-in-unreal-engine)** that you have added to the Actor class in the Template Sequence.

To add a Property Multiplier, right-click the Template Sequence section and select your property from the **Property Multipliers** menu.

![template sequence property multiplier](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1520e804-04ec-47b2-bd4f-38bb84b6a5b3/multipliers1.png)

Once added, you can expand the **Template Animation** track and view the multipliers, which typically have a default value of **1**. You can change the value of a multiplier and set keyframes for it.

![template sequence property multiplier](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/eab19686-16fa-4521-8858-4c286e6e4642/multipliers2.png)

Using Property Multipliers, you can vary the intensities of each instance of your Template Sequence.

![property multiplier variation](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f40c8152-14b0-4256-b853-597a22e61ffe/templateseqmultiplier.gif)

## Blueprint Usage

Template Sequences can also be applied to Actors at runtime using the **Create Template Sequence Player** Blueprint node.

![create template sequence player](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b147740d-860b-42d1-830b-b867aab4b048/tsbp.png)

### Content Setup

1.  In your Blueprint, add the **Create Template Sequence Player** node. Once added, select your **Template Sequence** asset from the dropdown menu on the node.
    
    ![assign template sequence player](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8813b1f7-0f9d-46e9-aa19-f799ea937ba4/tsbp2.png)
    
2.  Call **Set Binding** from the **Template Sequence Player** node and connect the **Out Actor** pin from the **Template Sequence Player** node to the **Target** pin.
3.  Add a reference to the Actor you want to apply the template sequence animation to and connect it to the **Set Binding** node's **Actor** pin.
    
    ![template sequence blueprints](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1434beec-3357-463b-864b-870e11addb4a/setbinding.png)
    
4.  Lastly, add a **Play** node and connect from the **Create Template Sequence Player** node's **Return Value** pin.
    
    ![template sequence blueprints](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bf3c944a-6e44-4b0c-bf55-2dcdff664b05/playbp.png)