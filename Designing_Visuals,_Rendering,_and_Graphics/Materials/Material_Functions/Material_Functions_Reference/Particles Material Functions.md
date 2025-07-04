# Particles Material Functions

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/particles-material-functions-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/particles-material-functions-in-unreal-engine)  
**Processed:** 2025-06-14 16:42:11

---

Particle functions are designed to aid in complex material generation for particle systems.

## Particle Functions

The following is a list of all the functions underneath the Particles category.

### 3dParticleOpacity

The purpose of this function is to help setup particles such that they fade away as they move away from the camera.

| Item | Description |
| --- | --- |
| Inputs |   |
| **Depth Texture (Scalar)** | Takes in an inverted z-depth render (black near the camera and white values in the background). Be sure that the texture's SRGB switch is disabled in the texture properties window. |
| Depth Texture Options |   |
| **Use dynamic or explicit texture depth settings (StaticBool)** | The default setting (true) is dynamic texture depth. Using explicit texture settings (false) will allow you to specify exactly how many world units your depth texture represents. For example, 512 units would make the texture 512 units deep. The dynamic texture depth option will use the ratio between the particle's size and its depth to scale the depth for differently scaled particles. For example, if your ratio was set to 1, a square particle that was 512 units would set the 512 unit depth texture. A ratio value of 0.5 would generate a texture depth of 256. This helps the effect scale properly with various particle sizes. |
| **Dynamic Texture Depth Ratio (Scalar)** | Enter the ratio of the height texture's depth to the height texture's width (use 3ds Max world unit measurements). For instance, if you create a plane in a 3D application that is 512x512 and you render a height texture from that plane that represents 256 units away from the plane then you would calculate this number by dividing 256/512, which would be a ratio of 0.5. |
| **Explicit Texture Depth Ratio (Scalar)** | World space scale of the depth texture. A value of 256 will make the depth texture 256 units deep. |
| **Depth Texture Falloff Softness (WS)(1/n) (Scalar)** | The distance in world space units across which the object's opacity gradually fades. Enter 1 divided by the number of world space units across which you would like the transition to take place. For instance, enter 1/16 in the input field and Unreal will convert that number to 0.062500. Doing this ahead of time removes an instruction from the effect. |
| Camera Falloff Group |   |
| **Use Near Camera Falloff (StaticBool)** | Setting this to *true* makes the particles falloff as they approach the camera. The default value is *false*. |
| **Near Camera Falloff Start Distance (Scalar)** - | The distance in world space units from the camera where the object maintains its remains transparent. |
| **Near Camera Fade Distance (1/n) (Scalar)** | The distance from the camera where the opacity fades to 0. Enter the reciprocal of the target distance. For example, to fade the particle out over 256 units enter 1/256, which Unreal will convert into 0.003906. |
| **Use Depth In Camera Falloff Calculation (StaticBool)** | Makes closer pixels (according to the depth map) fade out before farther pixels. The default value is *false*. |
| Particle Alpha Group |   |
| **Use Particle Alpha (StaticBool)** | Multiplies the result by the particle color alpha channel. The default value is *false*. |
| WPO Group |   |
| **Camera Offset (Scalar)** | This value should be the same value as *Texture Depth*. The *Texture Depth* value is used as this input's default value. |
| Outputs |   |
| **Opacity** | Provides the final opacity calculation after falloff. |
| **World Position Offset** | Emulates what camera offset does in the Particle Editor. |

![3dParticleOpacity](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/07f38083-2a9c-4024-8086-63e4f1317f78/3dparticleopacity.png)

Any input prefixed by "--------" is intended to be a separator in the input list and is not meant to receive actual inputs.