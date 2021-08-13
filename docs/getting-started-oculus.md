# Setup for Oculus Quest

[Video version](https://www.youtube.com/watch?v=rxiATOTKyqU)

## 1. Android Configuration

**Android Module**

  1. Open Unity Hub.
  1. Click on `Installs`
  1. Click on the three dots icon and select `Add Modules`
  1. Select `Android Build Support`
  1. Click `Done` to start the installation
  
**VRee SDK Settings**

  1. Open a Unity project with the VRee SDK installed
  1. Open the `VReeSDK` scene from `Assets > Scenes > VReeSDK`
  1. Go to `VReeSDK > Settings` to open the VRee SDK settings in the inspector
  1. In the `Settings` field, select the `Quest Settings`

**Build and Player Settings**

  1. Go to `File > Build Settings...`
  1. Select the `Android` Platform and click `Switch Platform`
  1. Click on `Player Settings`
  1. Under `Other Settings > Rendering` enable `Auto Graphics API`
  1. Under `Other Settings > Identification`
     - set `Minimum API Level` to `Android 7.1 'Nougat' (API level 25)`
     - set `Target API Level` to `Automatic (highest installed)`
  1. Under `XR Settings` enable `Virtual Reality Supported`
  1. In the `Virtual Reality SDKs` list, add `Oculus` by clicking on the plus icon

## 2. Building to Oculus Quest

1. Connect the Oculus Quest to the development PC
1. Go to `File > Build And Run`
1. Enter a file name and click `Save`

## 3. Server and Client connection

1. Connect the Oculus Quest and the development PC to the same network
2. Run the application on the development PC by clicking the play button in the Unity Editor
3. Run the application on the Oculus Quest
