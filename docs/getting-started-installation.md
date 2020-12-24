# Installation and Prerequisites

[Video version](https://www.youtube.com/watch?v=pw_7XS6vc1A)

## 1. Unity Installation

1. Open Unity Hub.
1. From `Installs`, click on `Add` and choose Unity 2018.4 LTS or higher.
1. Click next.
1. If you're building to Android _(Oculus Quest)_, make sure `Android Build Support` is checked.
1. Click next and install.

## 2. Create a VRee account

1. In the browser, go to [VRee Developers](https://developer.vree.world/dashboard/register "VRee Developers") and register an account.

## 3. Project Creation

1. Open Unity Hub.
1. From `Projects`, click `New`.
1. Select a template (3D by default) and enter a Project Name.
1. Click `Create` to create the project.

## 4. Importing the VRee SDK

1. Login to your [VRee Developers dashboard](https://developer.vree.world/dashboard/login "VRee Developers dashboard")
1. Download the `VRee SDK for Unity`
1. In Unity, go to `Assets > Import Package > Custom Package...` and select the downloaded VRee SDK.
1. Click `Open` and import the package by clicking `Inport`

## 5. Activate VRee license

1. In Unity, go to `VReeSDK > Register license...`
1. Enter your account details and click `Register license for this device`.
1. Your account now has an active developer seat.

## 6. Installing Prerequisites

- Xsens license prerequisite
  1. In Unity navigate the Project files to `Assets > VReeSDK > Prerequisites`.
  1. Right click `SoftwareActivation.zip` and select `Show in Explorer`.
  1. In the explorer, copy and extract `SoftwareActivation.zip` somewhere outside of the project structure (e.g. on the Desktop).
  1. Open the extracted folder and double click `activateLicense.bat` to create an empty Xsens license.
- C++ Redistributable prerequisite
  1. Download and install the `vc_redist.x86.exe` C++ Redistributable from the [Microsoft downloads page](https://developer.vree.world/dashboard/login "Microsoft downloads page").
- Firewall exception for Unity
  1. In Windows, search for `Firewall` and select `Windows Defender with Advanced Security`
  1. Click on Inbound Rules.
  1. Right click the installed Unity Editor version and select `Properties`.
  1. Under `Action`, select `Allow the connection` and click `Ok`.
