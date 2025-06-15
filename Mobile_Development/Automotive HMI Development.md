# Automotive HMI Development

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/automotive-hmi-development-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/automotive-hmi-development-in-unreal-engine)  
**Processed:** 2025-06-14 16:09:32

---

**Automotive Human-Machine Interface** **(HMI)** projects in **Unreal Engine** **(UE)** are highly-optimized mobile applications with many unique considerations. Vehicle controls and displays demand a high level of responsiveness, stability, and reliability, as failures in any of these areas can result in both frustration and safety issues for users. Additionally, HMI teams have a unique cross-disciplinary makeup, with developers from different industries and working environments all contributing to a project.

This section of the UE documentation provides guides tailored for automotive HMI projects, including:

-   Onboarding resources for HMI developers new to working with UE
    
-   Guidelines for achieving the high level of optimization and performance required for an HMI product
    
-   Guidelines for scaling an HMI project and collaborating between the unique disciplines and working environments that make up its industry
    

## Roles and Environments on an HMI Project

HMI projects for Unreal Engine (UE) have a unique cross-disciplinary environment. Your own organization's preferences may vary, but the following chart generalizes the typical UE HMI project's makeup:

[![A chart that shows the development teams in a typical UE HMI project and how they interact.](https://dev.epicgames.com/community/api/documentation/image/15e26ce7-b2c6-497b-b572-c45c2742d8d3?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/15e26ce7-b2c6-497b-b572-c45c2742d8d3?resizing_type=fit)

| Development Team | Number of Personnel | Discipline/Industry | Preferred Environment | Description |
| --- | --- | --- | --- | --- |
| 
Technical Artists

 | 

2-5

 | 

Technical art, 3D art, CAD, DCC through Unreal Engine

 | 

Windows

 | 

Primarily works on visual assets, such as car models. This can include Rigging, Animation, Materials, effects, Blueprinting, UI/UMG, Rendering, Lighting,  Profiling, and other related work.

 |
| 

UI/UX Developers

 | 

2-5

 | 

UI design, web design, User Experience design

 | 

MacOS, Figma

 | 

Builds the UI and menus for the vehicle.

 |
| 

Integration Developers

 | 

10-15

 | 

Computer science, software development

 | 

Linux

 | 

Integrates the vehicle's systems with the UE application.

 |
| 

Quality Assurance Testers

 | 

\-

 | 

Computer science, software development

 | 

\-

 | 

Tests the application and provides feedback about bugs and features to the team.

 |

The general workflow for these teams is as follows:

1.  Technical and 3D artists develop the art assets for the project, most especially car models, which are often displayed alongside technical information. This involves taking development assets and converting them into performance-focused models for a real-time application.
    
2.  UI and UX developers build the frontend UI for the project using Unreal Motion Graphics (UMG), UE's UI editor. This typically involves prototyping in Figma or another UI design suite, then re-creating the team's designs inside UMG.
    
3.  Integration developers work on the backend systems for the project, tying together the vehicle's systems, the project's application flow, and the assets provided by the UI and technical art teams. They also profile and debug the application, and provide technical feedback to the other teams so they can tweak their assets. This makes integration developers the central pillar of an HMI project's iterative workflow.
    
4.  The quality assurance team tests builds of the application and provides feedback about performance, bugs, and the overall user experience.
    
5.  Each of these teams continuously iterates on their respective pieces based on feedback from one another, correcting issues as they arise, tweaking the experience, and then testing again.
    

This makeup of teams introduces unique challenges for a UE project, as each of their industries prefers different operating systems and suites of software when working in other types of projects. Fortunately, UE supports each of these environments, and it is possible for this diverse group to collaborate.

## Onboard Your Organization

To set up your project for success, follow these guides to get your development environment set up and prepare to distribute projects to your team:

-   [Non-Game Licensee Onboarding Guide](https://dev.epicgames.com/documentation/en-us/unreal-engine/onboarding-guide-for-unreal-engine-nongames-licensees?application_version=5.5)
    
-   [Resources for Scaling Your Team](https://dev.epicgames.com/documentation/en-us/unreal-engine/resources-for-scaling-your-unreal-engine-team)
    
-   [Source Control in Unreal Engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/source-control-in-unreal-engine)
    
-   [Create an Installed Build](https://dev.epicgames.com/documentation/en-us/unreal-engine/create-an-installed-build-of-unreal-engine)
    

## Manage Your Application's Performance

Automotive HMI projects must hit a high bar of reliability, responsiveness, and performance to ensure the smoothest and safest user experience possible. The resources in this section provide an introduction to the concepts governing performance in UE, and the tools you can use to profile and configure performance.

### Basics

These pages provide an overview of the concepts behind performance profiling as well as overviews of optimization considerations in a variety of contexts.

-   [Introduction to Performance Profiling and Configuration](https://dev.epicgames.com/documentation/en-us/unreal-engine/introduction-to-performance-profiling-and-configuration-in-unreal-engine)
    
-   [Common Performance Considerations](https://dev.epicgames.com/documentation/en-us/unreal-engine/common-memory-and-cpu-performance-considerations-in-unreal-engine)
    
-   [Rendering Optimization on Mobile](https://dev.epicgames.com/documentation/en-us/unreal-engine/optimization-and-development-best-practices-for-mobile-projects-in-unreal-engine)
    
-   [Optimization Guidelines for UMG](https://dev.epicgames.com/documentation/en-us/unreal-engine/optimization-guidelines-for-umg-in-unreal-engine)
    

### Profiling Tools

These pages provide guides for each of the tools you can use to analyze your project's performance.

-   [Unreal Insights](https://dev.epicgames.com/documentation/en-us/unreal-engine/unreal-insights-in-unreal-engine)
    
-   [RenderDoc](https://dev.epicgames.com/documentation/en-us/unreal-engine/using-renderdoc-with-unreal-engine)
    
-   [Stat Commands](https://dev.epicgames.com/documentation/en-us/unreal-engine/stat-commands-in-unreal-engine)
    

### Performance Scaling Resources

These pages provide information about systems you can use to fine-tune performance for your application, including how to do so on individual devices.

-   [Scalability Settings](https://dev.epicgames.com/documentation/en-us/unreal-engine/scalability-in-unreal-engine)
    
-   [Customizing Android Device Profiles](https://dev.epicgames.com/documentation/en-us/unreal-engine/customizing-device-profiles-and-scalability-in-unreal-engine-projects-for-android)
    

## Technical Art

This section contains resources tailored to technical artists working on models, materials, and other assets for HMI projects. It is especially important to consider your project's **shading mode** in the mobile renderer, as this impacts both the lighting quality and the way UE processes materials.

-   [Mobile Previewer](https://dev.epicgames.com/documentation/en-us/unreal-engine/using-the-mobile-previewer-in-unreal-engine)
    
-   [Mobile Shading Modes](https://dev.epicgames.com/documentation/en-us/unreal-engine/mobile-rendering-and-shading-modes-for-unreal-engine)
    
-   [Mobile Deferred Shading Mode](https://dev.epicgames.com/documentation/en-us/unreal-engine/using-the-mobile-deferred-shading-mode-in-unreal-engine)
    
-   [Rendering Optimization on Mobile](https://dev.epicgames.com/documentation/en-us/unreal-engine/optimization-and-development-best-practices-for-mobile-projects-in-unreal-engine)
    

## UI Development

This section contains resources tailored for UI developers working on the frontend for HMI projects, including resources for macOS users.

### Working With UMG

-   [UMG Quickstart Guide](https://dev.epicgames.com/documentation/en-us/unreal-engine/umg-ui-designer-quick-start-guide-in-unreal-engine)
    
-   [UMG Editor Reference](https://dev.epicgames.com/documentation/en-us/unreal-engine/umg-editor-reference-for-unreal-engine)
    
-   [Animating UMG Widgets](https://dev.epicgames.com/documentation/en-us/unreal-engine/animating-umg-widgets-in-unreal-engine)
    
-   [UMG Viewmodel Plugin](https://dev.epicgames.com/documentation/en-us/unreal-engine/umg-viewmodel-for-unreal-engine)
    

### Improving UI Performance

-   [Optimization Guidelines for UMG](https://dev.epicgames.com/documentation/en-us/unreal-engine/optimization-guidelines-for-umg-in-unreal-engine)
    

### MacOS

-   [Xcode](https://dev.epicgames.com/documentation/en-us/unreal-engine/using-the-xcode-ios-simulator-with-unreal-engine-projects)
    
-   [Modern Xcode Workflow](https://dev.epicgames.com/documentation/en-us/unreal-engine/using-modern-xcode-in-unreal-engine)
    
-   [Supporting Mac Workflows from Windows](https://dev.epicgames.com/documentation/en-us/unreal-engine/working-on-ios-projects-using-a-windows-machine-in-unreal-engine)
    

## HMI Engineering and Debugging Resources

This section contains resources tailored for integration engineers working on the backend for HMI projects, including resources for Linux users.

### Linux Development Environment

-   [Visual Studio Code](https://dev.epicgames.com/documentation/en-us/unreal-engine/setting-up-visual-studio-code-for-unreal-engine)
    

### Debugging Resources

-   [Debugging in Android Studio](https://dev.epicgames.com/documentation/en-us/unreal-engine/debugging-unreal-engine-projects-for-android-using-android-studio)
    
-   [Setting Up Your Android Device for Development](https://dev.epicgames.com/documentation/en-us/unreal-engine/setting-up-your-android-device-for-developing-applications-in-unreal-engine)
    
-   [Using the Android Emulator With Unreal Engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/debugging-unreal-engine-projects-with-virtual-devices-using-the-android-emulator)
    
-   [Automated Testing](https://dev.epicgames.com/documentation/en-us/unreal-engine/automation-test-framework-in-unreal-engine)