# Updating to the Latest Changes from Epic

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/updating-to-the-latest-changes-from-epic-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/updating-to-the-latest-changes-from-epic-in-unreal-engine)  
**Processed:** 2025-06-14 16:57:42

---

One of the biggest benefits of working from source is that you always have access to the very latest improvements and new features that our team adds to **Unreal Engine (UE)**. As we make changes in the source code and issue new official releases, we continuously update the various branches of the [Unreal Engine GitHub repository](https://github.com/EpicGames). You will probably want to pick up these changes periodically: perhaps every time we publish a new official release, or any time there is an update relevant to your needs.

This page describes two different approaches you can use to update a branch of your fork so that it matches the latest changes in the main Unreal Engine repository.

## Use an Upstream Remote

In this approach, you add the original Epic Games Unreal Engine repository to your local copy of your fork as a new remote repository. This is usually referred to as the **upstream remote**. You pull changes from that upstream remote into your local branch. Then you can push those changes back up to your own fork on GitHub, usually referred to as the **origin remote**.

Although this may at first seem trickier than using a GitHub pull request as described below, we recommend this approach. It has a couple of advantages:

-   Once you have set up your upstream remote, you never have to set it up again as long as you keep using the same local clone of your fork. This makes it convenient to pick up new changes as frequently as you feel is necessary for your project.
-   Each time you use a GitHub pull request to update your fork, you create a new commit in your branch and a new pull request in your project's history. This is usually harmless, but it is better to avoid these unnecessary entries.

The instructions below show you how to use the Git command-line tools to add the new remote and pick up changes. If you use a Graphical User Interface (GUI) Git client, the steps should be roughly the same. Refer to your tool's documentation for details.

If you use [GitHub Desktop](https://desktop.github.com/), the upstream remote is automatically created for you when you clone your fork. You only need to merge the changes from the upstream branch into your local branch, then push those changes up to your origin repository.

### Set up an Upstream Remote

1.  If you have not already done so, clone your fork to your computer.
2.  Open a command prompt, and navigate to the folder that contains your repository.
3.  Add the base Epic Games repository as a new remote, named `upstream`.
    
    ```
            `> git remote add upstream https://github.com/EpicGames/UnrealEngine`
    		
    Copy full snippet
    ```
    \> git remote add upstream https://github.com/EpicGames/UnrealEngine

### Bring Changes Into Fork

1.  Checkout the branch you want to update. For example:
    
    ```
            `> git checkout ue5-main`
    		
    Copy full snippet
    ```
    \> git checkout ue5-main
2.  Pull the changes from the upstream remote into your local branch.
    
    ```
            `> git fetch upstream         > git merge upstream/ue5-main`
    		
    Copy full snippet
    ```
    \> git fetch upstream > git merge upstream/ue5-main
3.  Push the changes up to your origin remote.
    
    ```
            `> git push origin ue5-main`
    Copy full snippet
    ```
    \> git push origin ue5-main

## Use a GitHub Pull Request

1.  In a web browser, go to your repository's home page on [GitHub](http://www.github.com). This typically follows the format `https://github.com/<USERNAME>/UnrealEngine`, where `<USERNAME>` is your GitHub user name.
    
2.  Choose the branch you want to update from the **Branch** menu. The Epic Games Unreal Engine GitHub page `README.md` contains information about the available branches.
    
    ![Select the ue5-main branch](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/83372137-abff-4b92-bfd5-02406607c30f/git-branch.png "Select the ue5-main branch")
3.  Typically, as long as you have not made changes to this branch in your fork, GitHub informs you that the Epic Games repository already has all the commits from your repository.
    
    ![Contribute changes to upstream](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ad1ffe63-a4f0-4fd7-87b0-6896475aea6e/git-contribute.png "Contribute changes to upstream")
4.  Selecting **Sync Fork** informs you of any changes that exist in the Epic Games repository that have not been synced to your fork. To inspect the changes, click **Compare**.
    
    ![Comparing changes between branches](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/af150c7a-0793-4601-9800-a7ddc98c317a/git-sync-fork.png "Comparing changes between branches")
    
    If you know that there are no changes in your fork and you do not wish to review the changes that are available for sync from the Epic Games repository, but you simply wish to update to all of the latest changes, click **Update Branch**.
    
5.  After you have selected **Compare**, GitHub displays the commits that are present in the Epic Games repository, but are missing from your fork. If there are no changes that have conflicts, the branches are able to be automatically merged. To begin the process of merging changes, click **Create Pull Request**.
    
    ![Compare branches](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bcaf4b9b-9417-4b3d-9903-d120251268dd/git-compare-branches.png "Compare branches")
6.  Enter a brief description to indicate what branch your pull request is updating. When you are done, click **Create Pull Request**.
    
    ![Open a new pull request](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1ecf724d-06f2-4e91-8064-9b77a10f3cd1/git-create-pull-request.png "Open a new pull request")
7.  GitHub displays the changes contained in this pull request. At the bottom of the list of changes, click **Merge Pull Request**.
    
    ![Merge pull request](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8fa5b384-3a0d-42a7-bb98-70523f524665/git-merge-pull-request.png "Merge pull request")
8.  Click **Confirm Merge**.
    
    ![Confirm merge](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7ec840de-52cb-4f68-a7da-b6fa459a82fc/git-confirm-merge.png "Confirm merge")

When the merge is done, your fork's branch will be up-to-date on GitHub. You can now use the Git command line or your choice of visual tools to checkout the branch and pull the latest changes to your local computer.