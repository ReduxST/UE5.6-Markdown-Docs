# Compositing Material Nodes Reference

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/compositing-material-nodes-reference-for-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/compositing-material-nodes-reference-for-unreal-engine)  
**Processed:** 2025-06-14 16:14:42

---

To make compositing easier, UE5 has a series of nodes to serve some of the most common compositing operations. Here, each one is briefly highlighted and has an explanation of its purpose.

Click image to expand.

The compositing material nodes expect a **float4** input, so make sure you're passing in **RGBA** and not just **RGB**.

## Over

This node layers one image (A) over another (B), using the alpha from input A.

![Over Node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/aa1a91a7-2377-492f-8a38-55cd7c98f259/02-over-node.png "Over Node")

This node expects that the input color channels are pre-multiplied with the image's alpha.

## In

This node returns the portion of A that is inside the shape of B.

![In Node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3454702c-2376-4d1d-8f18-62271e636f87/03-in-node.png "In Node")

## Out

This node returns the portion of A that is outside the shape of B.

![Out Node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/61f6c657-aaec-467b-9434-693d36143ed9/04-out-node.png "Out Node")

## PreMult

This node multiplies the input's RGBA channel by its alpha.

![PreMult Node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/426f6779-8b0f-40fc-ac87-9fe934365027/05-premult-node.png "PreMult Node")

## UnPreMult

This node divides the input's RGBA channel by its alpha.

![UnPreMult Node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/91da0193-ca1a-45dd-9d55-d551036345a1/06-unpremult-node.png "UnPreMult Node")

## KeyMix

This node layers two images together using a specified mask.

![KeyMix Node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9b3d39a7-dee5-4f0d-b10d-7c2839346a17/07-key-mix-node.png "KeyMix Node")