# Contributing to Unreal Engine

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/contributing-to-the-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/contributing-to-the-unreal-engine)  
**Processed:** 2025-06-14 16:15:30

---

If you have made a fix or new feature in the **Unreal Engine (UE)** source code, you can contribute your changes back to **Epic Games** and get them published into the next release of Unreal Engine.

Over the years, we've already welcomed thousands of contributions from the community. There are many good reasons to join in, for example:

-   Merging your fixes and features into the main source code repository can make it easier for you to pick up the latest changes to Unreal Engine. You won't have to keep merging your local changes with newer engine source, or risk that your custom fixes might not compile or work as expected against the latest engine code.
    
-   Improving the Unreal Engine and editing tools helps to strengthen the wider Unreal community, which makes your knowledge and expertise even more valuable.
    
-   If we accept your changes, we'll also list your name and GitHub handle in our Release Notes as a contributor.
    

We use the GitHub Pull Request mechanism to manage, track, and evaluate submissions. This page tells you everything you need to know to get started.

## Plan Your Submission

It's easy to create a pull request in **GitHub**, but it takes a little forethought to create a pull request that we can evaluate easily and integrate quickly into our own repository.

Keep the following suggestions in mind if you want to increase the chances of your submission being accepted, and to avoid us asking you to do any extra work or changes. 

-   **Keep it focused.** Each pull request should ideally fix a single specific bug, or add a single, self-contained feature. Your pull request may involve changes to multiple files, and it may be made up of any number of commits, but all of those changes should be made to achieve a single aim.  
    If you have multiple things you want to contribute at the same time, don't hesitate to create multiple pull requests. It's easier for us to validate and bring in multiple separate requests than to break one large submission down into separate component parts.
    
-   **Start from release.** Although it's possible for us to merge in changes that you make on top of other branches, it's easiest if you make your changes in a clean, new branch that you create in your fork from a **release** branch that is even with the original Unreal Games repository.
    
-   **Keep it universal.** The Unreal Engine and editing tools are used across a potentially limitless spectrum of real-time content projects in a variety of industries and use cases. When you design a new feature, it's important to give some thought to making it as generic as possible, so that it will be useful to the widest possible audience. Avoid making assumptions about specific types of gameplay or content. 
    
-   **Follow our coding standard.** The [Unreal Engine Coding Standard](/documentation/en-us/unreal-engine/epic-cplusplus-coding-standard-for-unreal-engine) describes the conventions that we try to adhere to when writing our own code. Please do your best to follow these conventions in the code you submit. If you don't, it may take us longer to integrate your fixes, or we may ask you to go back and update your pull request to make it conform.
    
-   **Describe your changes well.** Give some thought in advance to the best way to tell us about the intent of your changes. Don't wait until you're filling out the pull request form on the GitHub web page to start getting your thoughts down into words.  
    If your changes fix a bug, how would we reproduce it? How can we tell if your change fixes the problem? Why did you choose this approach over other possible fixes?  
    If you want to add a new feature, who is it for? How is it supposed to work? Is it entirely your own work, or is it derived from another product or the work of another developer? 
    

Keep in mind that we don't guarantee that we'll accept your submission, even if you've done everything right on your side. The Epic engineers who review your submission often have inside knowledge about upcoming development plans, other engine subsystems or plugins that might be affected, third-party considerations, and so on. If they determine that we can't accept your submission for some reason, they'll let you know why in the pull request conversation.

## Set Up your Branch

Use the following steps to get your changes applied to a new branch in your fork.

1.  Update the release branch in your fork with the latest changes in the release branch of the original Epic Games Unreal Engine repository.  
    For details, see [Updating to the Latest Changes from Epic](/documentation/en-us/unreal-engine/updating-to-the-latest-changes-from-epic-in-unreal-engine).
    
2.  Create a new branch in your fork to hold your changes, based on the release branch. You can do this on the GitHub page for your fork, or you can do it on your local computer using the Git command-line tool or any visual Git tool.
    
3.  On your local computer, fetch the latest changes from your fork if necessary, and checkout your new branch.
    
4.  Make your changes in your local copy of the Unreal Engine source code.
    
5.  Compile the Unreal Engine and test to make sure your fix or feature is working as intended.
    
    Please do not skip this step! It may be tempting, especially if you're making a very small fix. But the release branch receives frequent updates, and any of them could potentially interfere with the changes you want to make.
    
6.  Commit your changes to your local branch, then push them back up to your GitHub repository.
    

## Start your Pull Request

Once you have your changes in a new branch in your fork, you can create a new pull request on the GitHub web site to ask us to merge those changes back into the original Unreal Engine repository.

1.  In a web browser, go to your repository's home page on [github.com](http://www.github.com).  
    This typically follows the format `https://github.com/<username>/UnrealEngine`, where `<username>` is your GitHub user name.
    
2.  You may see a notification that your new branch was recently modified. If so, you can click the green **Compare & pull request** button.
    
    ![Compare and pull request](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/114ef19f-2096-4121-9e8b-19f7d63888b6/contributing-github-1-recent.png "Compare and pull request")
    
    If not, select the branch that contains your changes from the **Branch** drop-down list, and click **New Pull Request**.
    
    ![New pull request](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3597fa62-641d-4558-972c-03251f31c506/contributing-github-2-new-pr.png "New pull request")
3.  On the Open a Pull Request page, click the **base** drop-down list and select the **release** branch. This sets the branch you want to merge your changes into.
    
4.  With the release branch selected, you should see that your branch is **Able to merge** (1), and the list of commits at the bottom of the page (2) should contain only the changes that you have made in your branch.
    
5.  This is your opportunity to tell us everything we need to know about the intent and scope of your changes. Set a brief description for your pull request, and use the text box to provide more detailed information.
    
6.  When you're satisfied that you've given us all the information we'll need in order to understand your changes, click **Create pull request**.
    

You'll be taken to a page for your new pull request, which is assigned a unique number. You can edit your title or description here, or add new comments in the conversation history. If you make any more commits to your custom branch, your pull request is automatically updated to include those changes too.

To get back here easily in future, either:

-   bookmark the URL, or
    
-   go to the [Pull Requests](https://github.com/EpicGames/UnrealEngine/pulls) tab on the Epic Games Unreal Engine repository page. You can use the **Filters** drop-down list to easily find the pull requests you've created in the list.
    

## Next Steps

The Epic engineering team will look over your new pull request as soon as possible, but your part is not necessarily done yet.

We may need to ask you some follow-up questions, or request that you make some additional changes. If so, we'll use the Conversation tab of your pull request to communicate. Keep an eye on the pull request, or subscribe to e-mail notifications from the GitHub site, so that you don't miss any messages from us.

If we do integrate your fix into our repository, your pull request will be set to **Closed** rather than **Merged**. This is normal and to be expected. The commit that integrates your changes will normally tag your pull request, so that there will be a record of your contribution.