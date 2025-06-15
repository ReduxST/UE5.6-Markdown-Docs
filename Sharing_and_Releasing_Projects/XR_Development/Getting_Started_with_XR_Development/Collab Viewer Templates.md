# Collab Viewer Templates

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/collab-viewer-templates-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/collab-viewer-templates-in-unreal-engine)  
**Processed:** 2025-06-14 16:13:53

---

The Collab Viewer Templates join multiple people together in a shared experience of the same 3D content. They are intended to make it easier and quicker for your team to review and communicate about designs in realtime, so that you can identify problems and iterate on the content more efficiently.

## Industry-Specific Templates

Unreal Engine offers two Collab Viewer Templates to work with, that are customized for specific user needs.

-   OEM/Manufacturing: This template has custom content intended for automotive design. It includes different types of lights present in the scene to demonstrate effects on car surfaces under different conditions.
    
    Click image to expand.
    
-   AEC: This template has custom content intended for architecture, engineering, and construction, including a sample building to demonstrate how to set up an architectural mockup.
    
    Click image to expand.
    

Every participant in a Collab Viewer session can use a computer set up with a standard mouse and keyboard, or with a VR headset and motion controllers. The Templates offer a variety of built-in tools for interacting with the scene content at runtime. Every participant can move objects around, change objects to a see-through X-Ray material, play animations that "explode" content into different spatial arrangements, and more. Everyone sees an avatar of each other person in the session, and can use a laser pointer tool to point out features of the environment:

Click image to expand.

The Collab Viewer Templates handle most of the difficult problems inherent in multi-viewer experiences, including setting up connections and replicating presence information between multiple computers. Use one as a starting point for your design review experiences, so that you can spend less time setting up networking and more time thinking about your designs. And, while they are most useful for evaluating and communicating your designs in a team environment, they offer enough interaction and navigation controls to be a good a starting point even for single-person experiences around your 3D content.

All of the interaction and navigation controls are provided by Blueprint classes in the Project, so you can customize them, learn from them, or even copy them into your own Projects. For more about working with Blueprint, see [Blueprint Visual Scripting](/documentation/en-us/unreal-engine/blueprints-visual-scripting-in-unreal-engine).

The pages in this section describe everything you need to know to get started with the Collab Viewer Templates, and to use them for your own content.

For a video walkthrough of the Collab Viewer Templates that demonstrates many of the concepts and procedures described in this documentation, see the recorded webinar:

## Workflow

The typical usage pattern for a Collab Viewer Template is:

1.  Create a new Project from the Template, or bring the Template content into your own existing Project.
2.  Set up the Project with the content you want to share with others. This typically involves the same kinds of data import and look development tasks that you would do in any Unreal Engine Project. For details on specific considerations that you'll need to keep in mind when setting up your content, such as collisions and navigation meshes, see [Adding Your Own Content to the Collab Viewer](/documentation/en-us/unreal-engine/adding-your-own-content-to-the-collab-viewer-in-unreal-engine).
3.  Use the tools built in to the Unreal Editor to package your Project to an executable file.
4.  Share that file with the people who need to be part of the collaborative review.
5.  One person launches the packaged Unreal Engine application and starts it up in server mode.
6.  Each other person who wants to be part of the same viewing session launches their copy of the application on a separate computer and joins the server session.

For a detailed tutorial that walks you through the steps above using the default content in the Template, see the [Quick Start](/documentation/en-us/unreal-engine/collab-viewer-template-quick-start-in-unreal-engine).

## VR Support

The Collab Viewer Templates use the OpenXR plugin by default to support VR headset interactions. The custom plugins for individual platforms such as Oculus VR and Steam VR are still supported and can be re-enabled if necessary.

## Getting Started

## How-To Guides

## Reference