# VRee Settings

The VRee Settings window can be opened from the Unity menu `VReeSDK > Settings`. This window only functions properly when the `[VReeSDK]` prefab is placed in the scene.

The VReeSDK uses Unity's Scriptable Object system to save the settings for different build targets. By default, the `OpenVR Settings` is used as it works with some of the most common HMDs.

A new settings scriptable object can be created by going to `Create > VReeSDK > VReeSDK Settings`.

Folding out the selected settings reveals the following fields:

## Networking

**Connection Id**
The Connection Id is used in network identification. A server running with connection ID 0 will accept all incoming connections from clients, IDs 1-255 can be used to only allow clients with matching connection Ids to connect.

**Port**  
The UDP port which is used for the communication handshake. Each connected player will receive their own communication port with `Port + PlayerId` where `PlayerId` is the ID assigned to the player, starting with 1 and incrementing by 1 for each new player.

When using a server outside your local network enable router port forwarding on server and client side. Port `9999` should be forwarded for the communication handshake. Additionally 1 increment of `9999` should be forwarded for each expected player connection.

> For example, 4 expected players. Port forward `9999-10004`.

If the amount of expected players is unclear, a high number of ports can be forwarded to ensure all players can connect.

Refer to manual of your router to setup port forwarding on your specific device or contact support@vree.world.

**Override Server IP**  
If this field is filled in clients will attempt to connect to the server running on the provided IP. If the field is left empty the client will attempt to discover the server in the LAN as usual.

**Reliable Packet Send Attempts**
How often a reliable packet should be resent before finally dropping it. Increasing this number may decrease network performance.

## Networking Roles

Networking roles determine how the application should behave. The following networking roles are available:

- Server: The server connecting all clients
- Client: A client (player) connecting to the server
- AdminClient: A client without in-game model
- ViewerClient: Similar to AdminClient but can be used to distinguish users

**Windows Role**
The role assigned when launching the application from a windows device.

**Android Role**
The role assigned when launching the application from an android device.

## Build Targets

**Target Hmd**  
The target of the build. This determines how the clients behave. Target HMDs can be switched by drag-and-dropping a camera prefab `VReeSDK > Hardware > OpenVR > Prefabs > OpenVrHmd` to the field.

> Make sure to import/delete the hardware SDKs accordingly after switching targets.

## Player Settings

**Player Configuration**  
Is the player using a full-body or hands-only set up.

**Auto Correct Hand Rotation**  
When enabled this option will automatically correct invalid rotations on the wrists using IK.

**First Person Prefab Model**  
Prefab to instantiate for the local player, usually this will be a model without a head to prevent camera clipping

**Third Person Prefab Model**  
Prefab to instantiate for all players other than the local player.

**Allow Body Dimension Scaling**
If enabled, allows bones in the avatar to be scaled.

**Override HandsOnly Model**  
Enabling this will allow attaching prefabs to the specified bones. This will disable the body model specified in `First/Third Person Prefab Model`.

**Override Hmd Model**
Prefab to instantiate on the head bone. Usually used to display the HMD the player is using.

**Override Left Hand Model**
Prefab to instantiate on the left hand bone. Usually used to display the controller the player is using.

**Override Right Hand Model**
Prefab to instantiate on the right hand bone. Usually used to display the controller the player is using.

**Adapters**
In this list, adapters can be added, removed or reordered to change what code influences the player body. Refer to [Adapters](adapters.md) for more information.

**Calibration Order**
The order in which hardware should calibrate, this list is automatically populated if a hardware adapter can be calibrated.

**Calibration Delay**
How many seconds to wait before calibrating.

## Server Camera Configuration

**Server Camera**  
Prefab created on the head bone of a player. This camera renders the player's first-person view in the [VRee User Interface](user-interface.md).

## Local Server Player

**Create Local Server Player**  
Whether to create a player for the `Server` role, essentially switching from dedicated server to host.

**Add Render Camera**  
When enabled a prettier camera is created for the server in the UI. Enabling this will impact performance.

**Render Camera**
The render camera to use.

## Network Packet Logger

**Suppress Reliable Message Dropped Log**  
When enabled no logs will be shown when a reliable packet was dropped.

**Data Logger Settings**  
Contains settings describing what and how much the data logger should log.

## Recording & Playback

**Playback mode**
Enable to start the server in playback mode, this allows for playback of recorded sessions.

## User Settings

An optional list where developers can add their own ScriptableObjects. These can be retrieved through code by using

```c#
VReeSDK.GetSettings<T>
```

where `T` is the type of the user setting ScriptableObject.

## Editor Settings

Defines the behaviour of the VRee SDK when running in the Unity Editor.

**Log Events**
Log when a [VRee Event](vree-events.md) is raised.
