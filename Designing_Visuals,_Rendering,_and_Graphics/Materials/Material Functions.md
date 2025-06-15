# Material Functions

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/material-functions-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/material-functions-in-unreal-engine)  
**Processed:** 2025-06-14 16:35:14

---

**Material Functions** let you package parts of a Material graph into a reusable asset that you can share to a library and easily insert into other Materials. Their purpose is to streamline Material creation by giving instant access to commonly used networks of Material nodes. Material Functions allow you to abstract complex Material logic into a single node, making Material creation easier for artists.

A secondary benefit of Material Functions is that edits to a single function propagate throughout all Material networks which use it. So if you need to make a fix or change how a Material Function works, you will not have to make further edits to the many Materials which may be using that function. These two pages provide information about how to create and use Material Functions in Unreal Engine.

## Functions Reference

The reference pages below provide information and usage examples for all the default Material Functions included with Unreal Engine. These are organized according to the categories in the [Material Editor](/documentation/en-us/unreal-engine/unreal-engine-material-editor-ui) palette.