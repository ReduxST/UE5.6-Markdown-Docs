# Set Spectator Screen Mode Texture Plus Eye Layout

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/set-spectator-screen-mode-texture-plus-eye-layout-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/set-spectator-screen-mode-texture-plus-eye-layout-in-unreal-engine)  
**Processed:** 2025-06-14 16:48:38

---

[![](https://dev.epicgames.com/community/api/documentation/image/f9613dbd-e740-454a-8207-16568e8247ce?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/f9613dbd-e740-454a-8207-16568e8247ce?resizing_type=fit)

This node sets up the layout for the `TexturePlusEye` function in `ESpectatorScreenMode`.

**Inputs**

| Pin Location | Name | Description |
| --- | --- | --- |
| 
[![](https://dev.epicgames.com/community/api/documentation/image/6c7c9c85-5fef-474b-b29a-c2c71b872732?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/6c7c9c85-5fef-474b-b29a-c2c71b872732?resizing_type=fit)



 | 

(In) Exec

 | 

Input execution pin.

 |
| 

[![](https://dev.epicgames.com/community/api/documentation/image/0dd93ce8-66e0-4f40-a79a-d359bf4ebcba?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/0dd93ce8-66e0-4f40-a79a-d359bf4ebcba?resizing_type=fit)



 | 

Eye Rect Min

 | 

A Vector 2D Structure, setting the minimum position of the screen rectangle that the Eye will be drawn in.

Values are normalized between `0.0` and `1.0`.



 |
| 

[![](https://dev.epicgames.com/community/api/documentation/image/bf69c778-1c19-4d85-81ac-87834b805f19?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/bf69c778-1c19-4d85-81ac-87834b805f19?resizing_type=fit)



 | 

Eye Rect Max

 | 

A Vector 2D Structure, setting the maximum position of the screen rectangle that the Eye will be drawn in.

Values are normalized between `0.0` and `1.0`.



 |
| 

[![](https://dev.epicgames.com/community/api/documentation/image/78c96e64-d93c-4cfc-b9ce-65b55621fa5e?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/78c96e64-d93c-4cfc-b9ce-65b55621fa5e?resizing_type=fit)



 | 

Texture Rect Min

 | 

A Vector 2D Structure, setting the minimum position of the screen rectangle that the Texture will be drawn in.

Values are normalized between `0.0` and `1.0`.



 |
| 

[![](https://dev.epicgames.com/community/api/documentation/image/602036bd-8d99-4c92-aa82-a06aa99d7174?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/602036bd-8d99-4c92-aa82-a06aa99d7174?resizing_type=fit)



 | 

Texture Rect Max

 | 

A Vector 2D Structure, setting the maximum position of the screen rectangle that the Texture will be drawn in.

Values are normalized between `0.0` and `1.0`.



 |
| 

[![](https://dev.epicgames.com/community/api/documentation/image/43566e83-18a0-43e5-81ab-28d06d9ccf01?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/43566e83-18a0-43e5-81ab-28d06d9ccf01?resizing_type=fit)



 | 

Draw Eye First

 | 

If this flag is set to `True`, the Eye is drawn before the Texture; however, if this flag is set to false, the Texture will be drawn before the Eye.

 |
| 

[![](https://dev.epicgames.com/community/api/documentation/image/8058fd85-bcce-433e-ae42-1b6a34c17452?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/8058fd85-bcce-433e-ae42-1b6a34c17452?resizing_type=fit)



 | 

Clear Black

 | 

If this flag is set to `True`, the Render Target will be drawn black before either rectangle is drawn.

 |

**Output**

| Pin Location | Name | Description |
| --- | --- | --- |
| 
[![](https://dev.epicgames.com/community/api/documentation/image/8e6f0e6d-c4fc-4c22-8fbb-330546d54a80?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/8e6f0e6d-c4fc-4c22-8fbb-330546d54a80?resizing_type=fit)



 | 

(Out) Exec

 | 

Output execution pin.

 |