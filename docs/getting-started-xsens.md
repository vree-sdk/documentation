# Setup for Xsens

[Video version](https://www.youtube.com/watch?v=dzoXOrUPHjk)

## 1. Settings

- VRee SDK Settings
  1. Open a Unity project with the VRee SDK installed
  1. Open the `VReeSDK` scene from `Assets > Scenes > VReeSDK`
  1. Go to `VReeSDK > Settings` to open the VRee SDK settings in the inspector
  1. In the `Settings` field, select the preset matching your VR headset
  1. Set `Player Configuration` to `Full Body`
  1. Change the `First Person Player Model` to the `FirstPersonPlayer` model
  1. Change the `Third Person Player Model` to the `ThirdPersonPlayer` model
  1. Remove the `Controller Adapter` from the `Adapter Priority` list by selecting the adapter and clicking the minus button
  1. Add the `Xsens Adapter` to the `Adapter Priority` list by clicking the plus button
  1. Move the `Xsens Adapter` up in priority by drag and dropping it above the HMD Adapter

## 2. Full Body VR Avatar

1. Enter play mode with the Xsens motion capture suit connected to the same network as the server
1. Switch to the Game View
1. Select the player from the `Connected Players` list by clicking on the player name.
1. Click the `Calibrate` button to calibrate the suit and VR headset
