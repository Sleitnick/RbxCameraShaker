# RbxCameraShaker

RbxCameraShaker is a port of the free Unity3D [EZ Camera Shake](https://assetstore.unity.com/packages/tools/camera/ez-camera-shake-33148) asset. The Unity3D asset had no licensing information, so I received written permission from the original authors of EZ Camera Shake to port their asset to Roblox.

This module is available from the [Roblox library](https://www.roblox.com/library/1461025953/Camera-Shaker).

## Purpose

RbxCameraShaker is a module that lets developers easily add realistic camera shake effects to Roblox games. The module is easy to use and performs well.

## Basic Use

Simple example:
```lua
local function ShakeCamera(shakeCf)
	-- shakeCf: CFrame value that represents the offset to apply for shake effect.
	-- Apply the effect:
	camera.CFrame = camera.CFrame * shakeCf
end

-- Create CameraShaker instance:
local renderPriority = Enum.RenderPriority.Camera.Value + 1
local camShake = CameraShaker.new(renderPriority, ShakeCamera)

-- Start the instance:
camShake:Start()

-- Apply explosion shakes every 5 seconds:
while (true) do
	wait(5)
	camShake:Shake(CameraShaker.Presets.Explosion)
end
```

## API

### CameraShaker

**Static Fields:**
```lua
CameraShaker.CameraShakeInstance
CameraShaker.Presets
```

**Constructor:**
```lua
camShaker = CameraShaker.new(renderPriority, bindFunction)
```

**Object Methods:**

| Method | Description |
| ------ | ----------- |
| `camShaker:Start()` | Start the camera shaker |
| `camShaker:Stop()` | Stop the camera shaker |
| `camShaker:StopSustained([fadeOutTime])` | Stop all sustained shakes |
| `camShaker:Shake(shakeInstance)` | Apply the shake effect once |
| `camShaker:ShakeSustain(shakeInstance)` | Apply the shake effect coninuously |
| `camShaker:ShakeOnce(magnitude, roughness [, fadeInTime, fadeOutTime, posInfluence, rotInfluence])` | Apply the custom shake effect once |
| `camShaker:StartShake(magnitude, roughness [, fadeInTime, posInfluence, rotInfluence])` | Apply the custom shake effect continuously |

### CameraShakeInstance
This is mostly used internally, but is still exposed for use.

**Static Fields:**
```lua
CameraShakeInstance.CameraShakeState
  - FadingIn
  - FadingOut
  - Sustained
  - Inactive
```

**Constructor:**
```lua
instance = CameraShakeInstance.new(magnitude, roughness, fadeInTime, fadeOutTime)
```

**Object Methods:**

| Method | Description |
| ------ | ----------- |
| `instance:UpdateShake(deltaTime)` | Update the shake |
| `instance:StartFadeOut(fadeOutTime)` | Fade out effect |
| `instance:StartFadeIn(fadeInTime)` | Fade in effect |
| `instance:IsShaking() ` | Returns `true` if shaking |
| `instance:IsFadingOut()` | Returns `true` if fading out |
| `instance:IsFadingIn()` | Returns `true` if fading in |
| `instance:GetState()` | Returns the current CameraShakeState |

### CameraShakePresets

| Preset | Description | Ideal Type |
| ------ | ----------- | ---------- |
| Bump | A high-magnitude, short, yet smooth shake | Once |
| Explosion | An intense & rough shake | Once |
| Earthquake | Continuous, rough shake | Sustained |
| BadTrip | Bizarre shake with high magnitude & low roughness | Sustained |
| HandheldCamera | A subtle, slow shake | Sustained |
| Vibration | Rough but low magnitude | Sustained |
| RoughDriving | Slightly rough and medium magnitude | Sustained |

These presets are easy to modify and use. For an example of using one of the presets, look at the Basic Use section.