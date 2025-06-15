# Summary View Quick Start Guide

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/summary-quick-start-guide](https://dev.epicgames.com/documentation/en-us/unreal-engine/summary-quick-start-guide)  
**Processed:** 2025-06-14 16:53:02

---

## Overview

When building advanced visual effects in Unreal Engine, Niagara systems can become very complex. Each emitter may contain dozens, or even hundreds of parameters that control the final output. This is beneficial for visual effect artists and advanced users. However, it can become overwhelming to beginners or non-VFX artists.

Users can create a subset of parameters of an emitter by using the **Summary View**. This view is fully customizable and contains only the parameters selected by the user. This can help highlight key parameters that affect the simulation or expose certain parameters to non-technical users for ease of use.

You can create a Summary View per emitter in any Niagara system. For this example, you will use a fluid system that comes with an emitter that has a Summary View set up by default. Then, you will create one from scratch.

## Create a Niagara System

In this section you will create a new Niagara system and see its default Summary View.

1.  To open the **Plugins** window click **Settings > Plugins**. Go to the **FX** category and enable the **NiagaraFluids** plugin. Restart the Unreal Engine editor, if needed.
    
    ![Enable the NiagaraFluids plugin](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/18c19e7e-b047-428e-b315-076346cb427a/niagara-summary-1.png)
2.  In the **Content Browser**, right click and select **FX > Niagara System**.
    
    ![In the Content Browser, right click and select FX > Niagara System](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c92e3539-cd75-4430-828b-8764e20622b4/niagara-browser-1.png)
3.  Expand the **Niagara Fluids** category on the left and click **3D Gas**. Then select **Grid3D\_Gas\_ColoredSmoke** and click **Create**.
    
    ![Select New system from a template or behavior example and click Next](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4ad0f636-c5f0-4dff-bc08-a0820be74fd0/niagara-browser-2.png)
4.  Double click **NS\_ColoredSmoke** to open it. Select the **Grid3D\_Gas\_Master\_Emitter** and click **Emitter Summary**.
    
    ![Click Emitter Summary](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ba46ad9c-7228-470f-9546-aef7ba54cf8a/niagara-summary-6.png)
5.  Go to the **Details** panel to see the **Summary View** of this emitter.
    
    The Summary View consists of **Sections** (1) and individual **Parameters** (2). The Sections act as filters for the parameters being displayed. The parameters can be individual variables, entire modules, or even renderers with their properties. In addition, you can create Categories (not pictured) to further group parameters under specific Sections.
    
    ![The Summary View consists of Sections (1) and Parameters (2)](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b08c13d6-346f-4777-9289-746a598b8b29/niagara-summary-7.png)

## Create your First Summary View

In this section you will create a Summary View for one the emitters. You will also learn how to search for and add parameters.

1.  In **NS\_ColoredSmoke** select the **ParticleSourceEmitter** and click on **Emitter Summary**.
    
    ![Select the ParticleSourceEmitter and click on Emitter Summary](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8ee53317-ea00-4ff3-b6bc-95d514cc93f6/niagara-summary-8.png)
2.  Go to the **Details** panel and notice the **Summary View** is empty. Click on **Edit Summary** to open the **Edit Summary View** window.
    
    ![Click on Edit Summary to open the Edit Summary View window](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5da01663-5328-4cd7-aa9e-a05a36a16e3b/niagara-summary-9.png)
3.  The Edit Summary View window consists of the following areas:
    
    -   (1) The **Source List** area, where you can search for any source of information, including individual parameters, modules, renderers, and more. You select the source and drag it to a Category (2) to include it in your Summary View.
    -   (2) The **Section** and **Category** area. This is where you organize your parameters under Categories and Sections.
    -   (3) The **Details** area. This area will show the details of any selected element.
    
    ![The Edit Summary View window consists of the Source List area (1),  the Section and Category area (2), and the Details area (3)](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8273d3e3-f622-4e0e-a125-6fb18af37be4/niagara-summary-10.png)
4.  Click in the Search bar and type "Spawn Count." Then click and drag **Spawn Count** into the area below the **Add Category** button.
    
    ![Click in the Search bar and type ](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/15d9c6c9-2f0b-4125-a5c9-f9dba9b8e079/niagara-summary-11.png)
    
    Select the parameter to see the available information in the **Details** area. In this case, you can enter a **display name override** and a **tooltip override**. Also notice how the Summary View of the emitter is immediately updated and shows the Spawn Count parameter.
    
    ![Select the parameter to see the available information in the Details area](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e44ebd76-d40f-48ef-8c21-119815b521e3/niagara-summary-12.png)
5.  Following the steps above, add the following parameters to your summary: **Color**, **Noise Strength**, **Noise Frequency**, as seen below.
    
    ![Add the following parameters to your summary: Color, Noise Strength, Noise Frequency](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d391e987-04a1-493c-9cd4-ac5dae6f65ab/niagara-summary-13.png)
6.  Your Summary View should now look like the image below.
    
    ![You should see your parameters in the Summary View](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/acffef9b-c260-404c-a222-c1ad3acf673d/niagara-summary-14.png)

## Organize your Summary View

In this section you will create categories and sections for your Summary View. You will also use the Display Name Override for one of your parameters.

1.  In the **Edit Summary View** window, click **Add Category** and name your category **Particle Spawn**.
    
    ![Click Add Category](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/54a69838-7d72-4d4d-a691-8e3ed87ceb16/niagara-summary-15.png)
2.  Click and drag the **Spawn Count** parameter to the **Particle Spawn** category, nesting the parameter to the category.
    
    ![Click and drag the Spawn Count parameter to the Particle Spawn category](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/21d30851-edaa-4159-ba17-c23bce0bb1bc/niagara-summary-17.png)
3.  Add the category **Particle Color**, then add the **Color** parameter to it. Add the category **Particle Noise**, then add the parameters **Noise Strength** and **Noise Frequency**.
    
    ![Add categories Particle Color and Particle Noise. Add the Color, Noise Strength, and Noise Frequency parameters](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7216fda2-1c3d-4a82-85bd-7b416254f8f2/niagara-summary-18.png)
4.  Click **Add Section** and name your new section **Color**. Your new section is selected by default. Notice no parameters or categories are part of this new section.
    
    ![Click Add Section and name your new section Color](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8982883e-7814-40ae-9aa5-e27ec7d39ddd/niagara-summary-19.png) ![Notice that no parameters or categories are part of this new section](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/47bc1e9b-f8e0-4d17-aa00-2dcc59b921b4/niagara-summary-20.png)
5.  Click the **All** section. Select and drag the **Particle Color** category into the **Color** section.
    
    ![Select and drag the Particle Color category to the Color section](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5a2255ee-caf9-467c-8ed4-a19fc914202d/niagara-summary-21.png)
    
    Click the **Color** section to see the **Particle Color** category, along with the parameters associated with that category.
    
    ![Click the Color section to see the Particle Color category](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/18115cb4-eebe-482d-8082-8389f0100de7/niagara-summary-22.png)
6.  Go back to the **All** section and create a new section named **Forces**. Then select and drag the **Particle Noise** category to that section.
    
    ![Create a new section named Forces and drag the Particle Noise category to that section](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cbcc0a32-27ac-45ee-b35c-0982cac02340/niagara-summary-23.png)
7.  Go back to the **All** section and select the **Spawn Count** parameter. In the **Details** area, click the **Display Name Override** input box and enter **Particle Count**.
    
    ![Select the Spawn Count parameter. In the Details area, click the Display Name Override input box and enter Particle Count](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/19e3fe49-996a-4366-bb13-038a6583d6f6/niagara-summary-24.png)
8.  Your Summary View should now reflect all your sections and categories.
    
    ![Your Summary View should now reflect all your Sections and Categories](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b9edf09f-b790-4800-8bfc-8ef336adc567/niagara-summary-25.png)

## Add Parameters from the Emitter

In addition to using the Edit Summary View window, you can add parameters directly to Summary View while working inside your emitter. This makes it easier to build your Summary View as you work on your emitter.

To add parameters from your emitter, follow these steps:

1.  Exit the **Edit Summary View** window and click **Particle Update** in the emitter.
    
    ![click Particle Update in the emitter](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1aefcf3c-2c7b-4a6c-8baa-ddd53d4002bf/niagara-summary-26.png)
2.  Go to the **Details** panel and scroll down to the **Curl Noise Force** module. Right-click the **Noise Quality / Cost** parameter and select **Add to Emitter Summary**.
    
    ![Right click the Noise Quality / Cost parameter and select Add to Emitter Summary](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/37fc659d-4c6a-4040-845c-ebeb0a801835/niagara-summary-27.png)
3.  Scroll up to the **Spin Position** module. Right-click the module name and select **Add to Emitter Summary**. You can add individual parameters, entire modules, and more, to the Summary View.
    
    ![Scroll up to the Spin Position module. Right click the module name and select Add to Emitter Summary](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e9b67942-a3bd-4974-91f7-f517b1d570e9/niagara-summary-28.png)
4.  Click Summary View in the emitter to confirm you added your parameters.
    
    ![Click Summary View in the emitter to confirm your parameters have been added](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fbac3fa9-6de0-4eb1-bdca-f4814423bdce/niagara-summary-29.png)