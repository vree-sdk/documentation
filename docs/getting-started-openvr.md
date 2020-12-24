# Setup for OpenVR/SteamVR

[Video version](https://www.youtube.com/watch?v=n6IlzNkGBnw)

## 1. Settings

- Player Settings
  1. Go to `Edit > Player Settings`
  1. Under `XR Settings` enable `Virtual Reality Supported`
  1. In the `Virtual Reality SDKs` list, add `OpenVR` by clicking on the plus icon
- VRee SDK Settings
  1. Open a Unity project with the VRee SDK installed
  1. Open the `VReeSDK` scene from `Assets > Scenes > VReeSDK`
  1. Go to `VReeSDK > Settings` to open the VRee SDK settings in the inspector
  1. In the `Settings` field, select the `OpenVR Settings`

## 2. Local player (host-client mode)

1. In the VRee SDK Settings, enable `Create Local Server Player` and `Add Render Camera`
1. With SteamVR installed, enter play mode by clicking the play button in the Unity Editor

## 3. Server and Client mode

Ensure the server and client pc are connected to the same local network.

- On the server
  1. In the VRee SDK Settings, disable `Create Local Server Player`
  2. Enter play mode
- On the client
  1. In the VRee SDK Settings, set `Windows Role` to `Client`
  1. With SteamVR installed, enter play mode
