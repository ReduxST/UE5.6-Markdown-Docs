# UnrealGameSync (UGS)

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/unreal-game-sync-ugs-for-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/unreal-game-sync-ugs-for-unreal-engine)  
**Processed:** 2025-06-14 16:57:24

---

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6d151ec0-7bab-45a4-af18-5eb83d3a82c7/deployment_banner-1.png "Deployment_Banner-1.png")

When a team is working on an **Unreal Engine (UE)** project, they're working in an environment where code and content is continuously developed and integrated into the project. Oftentimes, while working in a collaborative development environment, success depends on a team's ability to effectively collaborate and communicate on problems that might arise during the development and integration process.

This is where a sync tool can help.

## What is UnrealGameSync (UGS)?

Conceptually, **UGS** is a tool that promotes code and content integration in a collaborative development environment, enabling teammates distributed over time and distance to labor on the same project as it gets updated. Technically, UGS provides a graphical front-end to sync UE projects from **Perforce**, optionally building those projects with Microsoft's [Visual Studio](https://www.visualstudio.com/) Compiler.

When they're using this tool, an **Artist's** workflow typically involves UGS syncing their project files, resolving merge conflicts, syncing editor binaries, updating version files, and optionally running their Unreal project.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4004456c-baa6-4d11-98e8-ce6eb9c04e1b/artist_workflow.png "Artist_Workflow.png")

For **Programmers**, their workflow typically involves UGS syncing their project files, resolving merge conflicts, updating version files, generating project files, optionally building UE4, and optionally running their Unreal project.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cfe78d0f-3b18-4eb1-a175-750515c91792/programmerworkflow.png "ProgrammerWorkflow.png")

Resolving merge conflicts is enabled by default; however, you can disable this service in the **Options** shortcut menu. Additionally, disabling UGS from building your project precludes UGS from running it.

After installing UGS, members of any team will be able to quickly bootstrap and iterate on projects without the overhead that typically comes with using sync tools.

## Who Benefits from Using UGS?

Anyone wanting to gain insight into or contribute to a UE game project, but more specifically; Developers, Designers, and Artists. In general, for all team members, it's safe to submit changes containing assets and source code because UGS syncs both code and content with ease.

### Developers

-   Developers can sync to a changelist (CL) as soon as it's submitted, thereby enabling them to locally compile the source code matching the CL. Additionally, they can add comments to each change, flagging builds as good or bad for other developers.
    
-   When engineers are working on a fix for a broken build, they can notify the rest of the team that they're working on the fix by setting a flag.
    
-   Developers can safely make content changes from local builds without submitting unversioned assets because Engine version files (`Version.h` and `Build.version`) are updated to the synced CL.
    
-   Because UGS includes custom build steps, UGS enables developers to set up tools and utilities that are specific to their project.
    

Note that build system results can be surfaced alongside a list of submitted CLs (along with a link to build logs).

### Creatives

-   If creatives, such as artists or designers, don't have Visual Studio (or if they don't need to compile the Editor), they can get a compressed Editor build of the project, which is compiled by the **Continuous Integration System (CIS)**.
    
-   Getting a compressed Editor build of the project is particularly useful for artists because the compressed build can be synced and automatically decompressed.
    

Finally, it's important to note that other disciplines, such as Quality Assurance, Production, or Business units can also use UGS to gain insight into a project's status or collaborate with developers and creatives. If you're new to UGS and you want to start using it, check out the [UGS Quick Start](/documentation/en-us/unreal-engine/unreal-game-sync-quick-start-guide) guide.

## Unreal Game Sync Documentation