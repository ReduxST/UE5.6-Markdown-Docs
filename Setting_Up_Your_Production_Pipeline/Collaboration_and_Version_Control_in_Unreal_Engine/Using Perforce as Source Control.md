# Using Perforce as Source Control

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/using-perforce-as-source-control-for-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/using-perforce-as-source-control-for-unreal-engine)  
**Processed:** 2025-06-14 17:00:31

---

Unreal Engine (UE) comes with an integrated method that allows people to work together on their projects using version control software called Perforce. Source Control allows users on your team to share assets and code with one another, as well as providing a backup and history of changes so any files can be rolled back to an earlier version if something went wrong with the file.

## Workflow

In general and mostly for historical reasons, working with assets in the Unreal Editor follows the workflow of Perforce. Files known as Assets (extension .uasset and .umap) are mainly what the Editor works with. These files are binary, so cannot be opened as text or merged in a text-based merge tool. For this reason, when working on a file the Editor will lock that file (this is known as **Checking Out** in Perforce nomenclature) so that other users cannot concurrently edit it. When the user is done with editing the file(s) they have locked, they check in, or commit those files, uploading the changes to the server and releasing the lock on the file.

## Using Perforce with Unreal Engine

### Setting up a Perforce Server on your Local Machine

To avoid potential integration issues with our tools, such as [UnrealGameSync](/documentation/en-us/unreal-engine/unreal-game-sync-ugs-for-unreal-engine), we recommend running a **case-insensitive** Perforce server.

There are two ways of running the Perforce server, **P4D** and **P4S**. P4D runs while an instance of the command line is running, so it is usually only used for spot-maintenance tasks. P4S is the service-based equivalent of P4D as it allows you to run the server in the background. The service is usually installed and started when you install the Perforce server tools.

Sometimes the service does not get run automatically. To turn the service on in Windows, first go into the **Control Panel -> Administrative Tools ->Services applet**. Then find the Perforce service in the list and start it:

Once the service is running, you can connect to your server using **P4Admin**. If this is the first connection to your server, then you can make a new user in the initial connection dialog:

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f2813ba1-b031-4f07-9a9a-61f610aa8925/sc_p4_setup.png)

Fill in the connection information for your Perforce server and press okay. Once you have connected to the server in P4Admin, you can make new depots, users, and groups pretty easily. Use P4V and the Unreal Editor to connect to the server with the credentials you supplied in the initial connection dialog.

Check out the [P4Admin Documentation](http://www.perforce.com/perforce/doc.current/manuals/p4admin/p4admin.pdf) for more in-depth information on the ins and outs of Perforce.

### P4 Typemap

Before you start adding files to your depot, you should set up your **P4 Typemap** so Perforce knows how to treat Unreal file types. Setting the typemap will affect how files get set to read only or writable inside of Perforce. However to do this, you will need to open a new command prompt and set up some p4 environment variables.

```
	`p4 set P4USER=your.username 	p4 set P4PORT=localhost:1666`
Copy full snippet
```
p4 set P4USER=your.username p4 set P4PORT=localhost:1666

Replace the values above with your respective username and connection address. Open the typemap by entering the following in the command prompt.

```
	`p4 -P <PASSWORD> typemap`
Copy full snippet
```
p4 -P <PASSWORD> typemap

You will then see a text window open; this is your server's typemap. The typemap below is an example that we have used in the past:

```
	`# Perforce File Type Mapping Specifications. 	# 	#  TypeMap:             a list of filetype mappings; one per line. 	#                       Each line has two elements: 	# 	#                       Filetype: The filetype to use on 'p4 add'. 	# 	#                       Path:     File pattern which will use this filetype. 	# 	# See 'p4 help typemap' for more information.  	TypeMap: 					binary+w //depot/....exe 					binary+w //depot/....dll 					binary+w //depot/....lib 					binary+w //depot/....app 					binary+w //depot/....dylib 					binary+w //depot/....stub 					binary+w //depot/....ipa 					binary //depot/....bmp 					text //depot/....ini 					text //depot/....config 					text //depot/....cpp 					text //depot/....h 					text //depot/....c 					text //depot/....cs 					text //depot/....m 					text //depot/....mm 					text //depot/....py 					binary+l //depot/....uasset 					binary+l //depot/....umap 					binary+l //depot/....upk 					binary+l //depot/....udk 					binary+l //depot/....ubulk`
Copy full snippet
```
\# Perforce File Type Mapping Specifications. # # TypeMap: a list of filetype mappings; one per line. # Each line has two elements: # # Filetype: The filetype to use on 'p4 add'. # # Path: File pattern which will use this filetype. # # See 'p4 help typemap' for more information. TypeMap: binary+w //depot/....exe binary+w //depot/....dll binary+w //depot/....lib binary+w //depot/....app binary+w //depot/....dylib binary+w //depot/....stub binary+w //depot/....ipa binary //depot/....bmp text //depot/....ini text //depot/....config text //depot/....cpp text //depot/....h text //depot/....c text //depot/....cs text //depot/....m text //depot/....mm text //depot/....py binary+l //depot/....uasset binary+l //depot/....umap binary+l //depot/....upk binary+l //depot/....udk binary+l //depot/....ubulk

Once edited, save the file by pressing **Ctrl+S** on your keyboard and then exit. The command prompt should then show **Typemap saved**.

### P4 Ignore

There might be files that you want ignored when addign client files to the depot or when reconciling client workspaces. To help with this, you can specify a **P4 Ignore** file. The default name for this file is `.p4ignore`.

The following is an example of Epic's `.p4ignore` file:

```
	`# Here you can specify files to ignore when adding files to the depot. 	# 	# The syntax for P4IGNORE files is not the same as Perforce syntax. 	# Instead, it is similar to that used by other versioning systems: 	# 	# - Files are specified in local syntax 	# - a # character at the beginning of a line denotes a comment 	# - a ! character at the beginning of a line excludes the file specification 	# - a * wildcard matches substrings. 	# 	# For example: 	# 	# foo.txt    Ignore files called "foo.txt" 	# *.exe      Ignore all executables 	# !bar.exe   Exclude bar.exe from being ignored 	# 	############################################################################### 	# Epic's P4IGNORE. 	# P4IGNORE doesn't work like GITIGNORE: 	# http://stackoverflow.com/questions/18240084/how-does-perforce-ignore-file-syntax-differ-from-gitignore-syntax 	############################################################################### 	# Ignore root Visual Studio solution files. We do check in some sln files in subdirectories, so only ignore 	# the ones found in the root. 	/*.sln 	/.p4sync.txt  	# Ignore all Visual Studio temp files. 	*.suo 	*.opensdf 	*.sdf 	/Engine/DerivedDataCache/* 	**/DerivedDataCache/Boot.ddc 	**/DerivedDataCache/**/*.udd  	# Ignore all Intermediate and Saved directories 	*/Intermediate/* 	*/Saved/* 	# Ignore UBT's configuration.xml 	Engine/Programs/UnrealBuildTool/* 	*.uatbuildrecord 	*.tmp  	# Ignore built binaries and temporary build files 	*/obj/* 	*.csprojAssemblyReference.cache  	# Ignore UBT's log output files 	/Engine/Programs/UnrealBuildTool/*.txt  	# Ignore Python cached files 	*.pyc  	# Ignore JetBrain's IDE folders 	.idea/ 	!.idea/runConfigurations 	.gradle/  	# Ignore autogenerated files from HoloLens WMRInterop 	/Engine/Source/ThirdParty/WindowsMixedRealityInterop/packages/* 	/Engine/Source/ThirdParty/WindowsMixedRealityInterop/MixedRealityInteropHoloLens/Generated Files/* 	/Engine/Source/ThirdParty/WindowsMixedRealityInterop/MixedRealityInteropHoloLens/x64/* 	/Engine/Source/ThirdParty/WindowsMixedRealityInterop/MixedRealityInteropHoloLens/ARM64/* 	/Engine/Source/ThirdParty/WindowsMixedRealityInterop/MixedRealityInterop/x64/* 	/Engine/Source/ThirdParty/WindowsMixedRealityInterop/MixedRealityInterop/ARM64/*  	# Ignore files added by Finder on Mac 	.DS_Store  	# Ignore all .code-workspace files 	*.code-workspace`
Copy full snippet
```
\# Here you can specify files to ignore when adding files to the depot. # # The syntax for P4IGNORE files is not the same as Perforce syntax. # Instead, it is similar to that used by other versioning systems: # # - Files are specified in local syntax # - a # character at the beginning of a line denotes a comment # - a ! character at the beginning of a line excludes the file specification # - a \* wildcard matches substrings. # # For example: # # foo.txt Ignore files called "foo.txt" # \*.exe Ignore all executables # !bar.exe Exclude bar.exe from being ignored # ############################################################################### # Epic's P4IGNORE. # P4IGNORE doesn't work like GITIGNORE: # http://stackoverflow.com/questions/18240084/how-does-perforce-ignore-file-syntax-differ-from-gitignore-syntax ############################################################################### # Ignore root Visual Studio solution files. We do check in some sln files in subdirectories, so only ignore # the ones found in the root. /\*.sln /.p4sync.txt # Ignore all Visual Studio temp files. \*.suo \*.opensdf \*.sdf /Engine/DerivedDataCache/\* \*\*/DerivedDataCache/Boot.ddc \*\*/DerivedDataCache/\*\*/\*.udd # Ignore all Intermediate and Saved directories \*/Intermediate/\* \*/Saved/\* # Ignore UBT's configuration.xml Engine/Programs/UnrealBuildTool/\* \*.uatbuildrecord \*.tmp # Ignore built binaries and temporary build files \*/obj/\* \*.csprojAssemblyReference.cache # Ignore UBT's log output files /Engine/Programs/UnrealBuildTool/\*.txt # Ignore Python cached files \*.pyc # Ignore JetBrain's IDE folders .idea/ !.idea/runConfigurations .gradle/ # Ignore autogenerated files from HoloLens WMRInterop /Engine/Source/ThirdParty/WindowsMixedRealityInterop/packages/\* /Engine/Source/ThirdParty/WindowsMixedRealityInterop/MixedRealityInteropHoloLens/Generated Files/\* /Engine/Source/ThirdParty/WindowsMixedRealityInterop/MixedRealityInteropHoloLens/x64/\* /Engine/Source/ThirdParty/WindowsMixedRealityInterop/MixedRealityInteropHoloLens/ARM64/\* /Engine/Source/ThirdParty/WindowsMixedRealityInterop/MixedRealityInterop/x64/\* /Engine/Source/ThirdParty/WindowsMixedRealityInterop/MixedRealityInterop/ARM64/\* # Ignore files added by Finder on Mac .DS\_Store # Ignore all .code-workspace files \*.code-workspace

For more information about ignore files, see the [P4IGNORE](https://www.perforce.com/manuals/cmdref/Content/CmdRef/P4IGNORE.html) documentation page on Perforce's documentation site.

### Server on your Local Network

You can set up a server on your local network for people to use to collaborate with one another. To do this, follow the steps above on the server and connect using the server's name or IP from your clients.

### Cloud Provider

There are various cloud providers that allow you to host Perforce servers off-site and to collaborate remotely. A quick search online for **Perforce Hosting** should turn up a few results. Each hosting provider is different, but all should end up with a set of credentials that you can use to connect. See also **Connecting from Unreal Editor** below for a note about connecting to Perforce cloud providers.

### Setting up a Local Workspace

To work with files that are under Perforce control, you will need to set up a Workspace so that the files can be managed on your local machine. You can do this via P4V by opening up the **Workspaces** tab in the **View** dropdown:

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d544e1be-4f40-408d-9223-95a02a193a1e/sc_view_workspace.png)

To create a new workspace, right-click in the Workspace window and select the **New Workspace** option. Then enter a name for your workspace and a location where you want the files to be on your local machine, the Workspace Root.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2cc26df6-cb18-474f-a33f-b49b09a61379/sc_new_workspace.png)

Once you have a server and a workspace, you will want to start adding files to it. For the moment, this needs to be done initially outside the Editor via P4V. If you already have a workspace that someone else has set up with some files already, you can skip ahead. When you create a new project, you can choose whether it incorporates C++ code and Blueprint elements. If you are using C++ code in your project, you will see a **Source/** directory as well. You should initially add only the following directories of your project:

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/02e528e0-2e04-4007-a4b2-5f77c40124c3/sc_p4_files_to_add.png)

Folders and files highlighted in **Green** should be added to your depot. The Binaries folder in **Yellow** is optional, depending on how your team wants to work together. It is not required if every team member is going to compile their editor/game themselves, but should be included in the **initial add** if any team members will just be grabbing a version from the depot to create content. Note that the server typemap setup above should mean that coders can compile their binaries without them being set to be **Read-Only** by Perforce.

### Adding Files to Perforce

Adding files to Perforce is something that can be accomplished in the few following steps.

1.  To add files/folders to Perforce, first select the files/folders in P4V and then right-click and select the **Mark For Add** option.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d1db3ebe-90e6-4571-803b-cc1b806c19ab/sc_p4_mark_for_add.png)
2.  This will add the files to your default change list. All files that you add can be seen in the Pending change lists tab:
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/353565a4-d74c-447f-a09a-8c77a33cf7aa/sc_view_pending_changelists.png)
3.  To submit something, first right-click on the change list and then select **Submit**. Then enter a change list description and click the Submit button.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/76c621ab-c205-4fe7-936e-0eb218adfce2/sc_p4_submit_files.png)

If you want to start work on a project that someone else has already started, you will need to get the latest revision from Perforce using P4V. To do this, find the project in the Depot View in P4V and then **Right-click** on the project you want to get and select **Get Latest Revision**. This will download all the files to the location you specified for your Workspace Root above.

### Connecting from Unreal Editor

You can connect to your Perforce server right from the Editor by clicking on the **Source Control** icon on the **Toolbar**:

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5ee7d8c5-dfd3-4471-a06e-c404cf8eda9e/sc_ue4_sc_enable.png)

Once open, choose Perforce as the provider from the Source Control Login dialog and enter your login credentials. If you have a workspace already set up (that the current project is inside of), your login credentials should be populated automatically.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c692d7f4-e9ec-4287-99b9-0854c1c16eec/sc_p4_ue4_setup.png)

When using some servers, including many cloud providers - you may need to enter the Host and Password to access your depot from the Editor. You can do this by opening the advanced field at the bottom of the Perforce login dialog:

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7e1e7c34-6940-4dc4-9fc6-5f157297c200/sc_p4_ue4_setup_advanced.png)