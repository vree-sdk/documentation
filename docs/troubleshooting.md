# Troubleshooting

## General

**The VRee settings window is blank**  
The VRee settings window only works when the `[VReeSDK]` prefab is placed in your scene.

**There's no UI when I start the application**
Make sure that the `[VReeSDK]` and `[VReeSDK_UI]` prefabs are in the scene.

**Client does not connect to the Server**  
Confirm that the `Connection id` match on the server and client and check if the server and client are connected to the same network.

**Client's screen stays back but a player appears on server**  
Verify that a firewall exception has been made for Unity. Refer to [firewall exceptions](getting-started.md/#firewall) for more information.

**Server ceases to respond when started**  
Run the software activation as explained here in the [getting started guide](getting-started.md/#installing-prerequisites)

**My HMD positional tracking does not work**  
Confirm that the `Target Hmd` matches your HMD. View our setup [videos](http://developer.vree.world/trainingvideos) for more information.

## Licensing & Accounts

**No license found pop-up**
The `No License found!` pop-up is shown when the application is started without a valid license in the application root.

To resolve this issue, make sure the license path contains the license file which may be [generated](getting-started.md#generating-a-license) or [downloaded](#license-management).

![Alt](./images/license/no-license-found.png "No license found.")
![Alt](./images/license/license-not-found.png "License not found!")

A new license may also be generated using the [VRee Standalone License Request Tool](https://developer.vree.world/Downloads).

**License Request Failed pop-up**
When generating a new license, the request may fail. This can be due to several issues:

- Incorrect user information - Make sure the Username and Password field contain the correct VRee account information. `Uppercase I’s` may be confused with `lowercase L’s` and vice versa.
- The machine already has a license key generated. - Remove the license key using the VRee License web interface before generating the license. - Download the license key and manually merge the license.
- No internet connection is available. - Generating the license requires the VRee SDK to communicate with the VRee License Server. Make sure the machine is connected to the internet.
- The VRee License is unavailable. - Confirm that the server cannot be reached by going to the VRee License Page. - Contact VRee if the License Server is unavailable.

![Alt](./images/license/license-request-failed.png "License not found!")
