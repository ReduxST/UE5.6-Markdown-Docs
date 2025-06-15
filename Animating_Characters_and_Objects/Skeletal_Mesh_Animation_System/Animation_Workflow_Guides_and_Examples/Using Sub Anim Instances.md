# Using Sub Anim Instances

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/using-sub-anim-instances-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/using-sub-anim-instances-in-unreal-engine)  
**Processed:** 2025-06-14 17:01:09

---

As you start to create more and more complex Animation Blueprints for your characters, there may be times when you want to re-use portions of an Animation Blueprint within another Animation Blueprint. Rather than re-creating the node network, you can split that network off into its own Animation Blueprint and use a **Sub Anim Instance** to access the Animation Blueprint when it is needed.

In this how-to we create an Animation Blueprint with logic to affect our playable character, then use a Sub Anim Instance inside the template's Animation Blueprint to call that logic.

For this guide, we are using the **Blueprint Third Person** template with **Starter Content** enabled.

## Steps

1.  In the **Content/Mannequin/Animations** folder, **Right-click** on and **Duplicate** the **ThirdPerson\_AnimBP** and call it **AltAnimBP**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/82c90615-6efc-40d2-9358-906b0df4b294/subanimbp01.png)
    
    This AltAnimBP will be used as our Sub Anim Instance that will be called from the ThirdPerson\_AnimBP.
    
    When creating an Animation Blueprint to use as a Sub Anim Instance, you must use the same Skeleton Asset as the one in the Animation Blueprint you plan to incorporate it in. In our example, we duplicated the template's Animation Blueprint, however, when creating Animation Blueprints from scratch you will need to select a Skeleton.
    
2.  In the **AnimGraph** of **AltAnimBP**, **Right-click** and add a **Sub-Graph Input** node.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/60d2e7c8-8722-4fef-8ea7-23d40266c7a0/subanimbp02.png)
    
    This will create an **In Pose** on the Sub Anim Instance, allowing us to pass through external pose data to this Animation Blueprint.
    
3.  **Right-click** again and add a **FABRIK** skeletal control node.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fcc34bb5-52c7-4ab6-9edf-b2cce783bce8/subanimbp03.png)
    
    For this example, we will use IK to push the character's arms up into the air as they run around during gameplay.
    
4.  Assign the following settings to the **FABRIK** node from the **Details** panel.
    
    -   Uncheck the **(As Pin) Effector Transform**
    -   Set **Location** to **100, 0, 200**.
    -   Set **Tip Bone** to **index\_01\_l**.
    -   Set **Root Bone** to **clavicale\_l**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/91fd6a6b-e9ce-4b9f-9148-41bf3e9fb95f/subanimbp04.png)
5.  Copy the **FABRIK** node in the graph and make the following changes to it from the **Details** panel.
    
    -   Set **Location** to **\-100, 0, 200**.
    -   Set **Tip Bone** to **index\_01\_r**.
    -   Set **Root Bone** to **clavicale\_r**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/364cce05-96d1-42fb-8c8f-1396dd74121d/subanimbp05.png)
    
    This will ensure that both the Left and Right arms are affected.
    
6.  **Right-click** on the **Alpha** pin of a **FABRIK** node and **Promote to Variable** called **Effect Alpha**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2c2ce504-77d6-47d6-9ff8-b278884137bb/subanimbp05b.png)
7.  Recreate the node network shown below (the **Local to Component** and **Component to Local** nodes will be automatically created).
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/44f42885-08a9-443e-9e68-dee86285f153/subanimbp06.png)
    
    If you **Compile** the Animation Blueprint, the character in the preview window will put their arms up.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ba6066dc-83e2-4648-95bc-bf6671e3134d/compliedblueprint.png)
8.  Inside the **Content Browser** under **Content/Mannequin/Animations**, open the **ThirdPerson\_AnimBP**.
    
9.  Inside the **AnimGraph**, **Right-click** and add the **Sub Anim Instance** node.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b3bae8c6-7f25-4b3d-bd03-2a824294b4d8/subanimbp07.png)
    
    This is the node that we use to gain access to our Animation Blueprint we created.
    
10.  In the **Details** panel for the **Sub Anim Instance** node, set the **Instance Class** to **AltAnimBP**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8f4949aa-5875-4cce-abdc-100ffe514e93/subanimbp08.png)
11.  Click the **Expose** checkbox next to **EffectAlpha** to expose the property.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9a76ea9c-a435-452e-a936-440774906633/subanimbp09.png)
    
    By exposing properties, you can update those properties with data from the parent Animation Blueprint.
    
12.  From the **MyBlueprint** panel, drag in the **Speed** variable and divide it by **600** then plug that into the **Effect Alpha**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d344abc4-d626-45fb-834f-27b1358bce13/subanimbp10.png)
    
    Here we divide the character's movement speed by a value to produce a blend between the amount of Skeletal Control applied.
    
13.  **Compile** then **Play in the Editor**.
    

## End Result

Below, as our character's speed increases it is divided by the specified amount before being used to drive the amount of Skeletal Control applied inside our Sub Anim Instance network. In this example we used the **Sub-Graph** input node to determine the resulting pose data, however, you can create an Animation Blueprint with its own State Machine and logic to generate the resulting pose data as well.