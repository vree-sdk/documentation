# Setup for Pico Interactive

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
  1. In the `Settings` field, select the `Pico Settings`

**Build and Player Settings**

  1. Go to `File > Build Settings...`
  1. Select the `Android` Platform and click `Switch Platform`
  1. Click on `Player Settings`
  1. Under `Other Settings > Rendering` enable `Auto Graphics API`
  1. Under `Other Settings > Identification`
     - set `Minimum API Level` to `Android 7.1 'Nougat' (API level 25)`
     - set `Target API Level` to `Automatic (highest installed)`
  1. Under `XR Settings` enable `Virtual Reality Supported`

## 2. Download
  1. Download the PicoVR Unity SDK from the [PicoVR download page](https://developer.pico-interactive.com/sdk "PicoVR Unity SDK download page")
  1. Import the Pico SDK package into your Unity project.

## 3. Settings

**VRee SDK Settings**

  1. Open the `VReeSDK` scene from `Assets > Scenes > VReeSDK`
  1. Go to `VReeSDK > Settings` to open the VRee SDK settings in the inspector
  1. In the `Settings` field, select the `Pico Settings`
  1. In the `Player Settings` verify that under `Scripting Define Symbols` "USEPICO" has been automatically entered.

## 4. Building to PicoVR

1. Connect the Pico VR headset to the development PC
1. Go to `File > Build And Run`
1. Enter a file name and click `Save`

## 5. Server and Client connection

1. Connect the PicoVR headset and the development PC to the same network
2. Run the application on the development PC by clicking the play button in the Unity Editor
3. Run the application on the PicoVR headset
