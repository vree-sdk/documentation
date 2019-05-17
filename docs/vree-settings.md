Using the VRee -> Settings button the Settings window will be opened. This chapter will walk through all the different options and their functions.
All settings shown in the first ScriptableObject (DefaultSettings) are saved in an xml file and can be changed after making a build. – Check with Jesse

# Networking
![Alt] (/images/settings/networking.png "Networking.")
## Platform Id
The platform id is used in network identification. A server running with ID 0 will accept all incoming connections, any other ID up to 255 can be used to only allow certain clients to connect. If the client and server agree on this ID the connection will be established, if these ID’s are different the connection request is ignored.
## Port
UDP port which is used for the communication handshake.
All networking traffic after the connection has been set up will be done for each player on the 'Selected Port + PlayerId'.
##Override Server Ip
If this field is filled in clients will attempt to connect to the server running on the provided IP. If the field is left empty the client will attempt to discover the server in the LAN.

# Networking Roles
This role determines wether the application acts as a Server or Client. 
![Alt] (/images/settings/networking-roles.png "Networking Roles.")
The options for the roles are:
###Server
The server connecting all clients
###Client
A user in the application
###AdminClient
A user without in-game model
###WatchClient
Similar to AdminClient but can be used for permission reasons

The other roles are implemented for future proofing, but have no current purpose.
# Build Targets
![Alt] (/images/settings/build-targets.png "Build Targets.")
##HMD Build Targets
The target of the build. Make sure you import/delete the hardware SDK's accordingly after switching target.
Below this field the custom editor for the HMD Target is shown, if present.

##Selected Input Devices
A list of 'Adapter Definitions'. These adapters are added onto the player after it connects, and determines how to the player controls it's avatar.
Below this list the custom editor for each adapter is shown, if present.

# Player Settings
![Alt] (/images/settings/player-settings.png "Player Settings.")
##Player Configuration
Is the player using a full-body or hands-only set up.

##Auto Correct Glovse
When enabled this option will automatically correct invalid rotations on the wrists using IK.

##First Person Prefab
Prefab to instantiate for the local player, usually this will be a model without a head to prevent camera clipping

##Third Person Prefab
Prefab to instantiate for all other players.

##Override HandsOnly Model
Enabling this boolen will allow attaching prefabs to the specified bones. Usually used to put different models on hands/head (i.e. Headset and Controller models)

##Override HMD, LeftHand, RightHand
Prefabs to use for the override flag above.

# Server Camera Configuration
![Alt] (/images/settings/server-camera-configuration.png "Server Camera Configuration.")
##Server Ui Camera Configuration
Prefab created on the server when a client connects. This camera will move accordingly with the user, and is displayed in the VRee UI.

# Hardware Selection
![Alt] (/images/settings/hardware-selection.png "Hardware Selection.")
##Supported Hardware Selection
2List that should contain all hardware and HMD's any of the users will be using. This list is futureproofing for when users have individual hardware in future versions.

##Adapter Priority
This reorderable List determines in which order adapters are ran. This way later adapters get the option to use the information of earlier ones, or overwrite them.

# Local Server Player
![Alt] (/images/settings/local-server-player.png "Local Server Player.")
##Create Local Server Player
When enabled a player is created for the server, switching from dedicated server to host.
##Add Render Camera
When enabled a camera is created for the server in the UI. Can be left off to reduce performance impact.
Recommended to be enabled when Create Local Server Player is enabled as well.

# General
![Alt] (/images/settings/general.png "General.")
##Calibration Delay
Time in seconds before the calibration is started after giving a calibration command.
##Allow Body Dimension Scaling
When enabled the bones position of the bones in the avatar can be changed. When disabled only the Hip bone's position can be changed.

# Data Logger
![Alt] (/images/settings/data-logger.png "Data Logger.")
##Suppress Reliable Message Dropped Log
When enabled no logs will be shown if a reliable packet was dropped.
##Data Logger Settings
Contains settings describing what and how much the data logger should log.

# User Settings
![Alt] (/images/settings/user-settings.png "User Settings.")
An optional list where developers can add their own ScriptableObjects. These can be retrieved through code by using 
```c#
VReePlatform.GetSettings<T>
```
where T is the type of the developers's ScriptableObject.

# Events
![Alt] (/images/settings/events.png "Events.")
##VRee Platform Initialized Event
This event is raised when the platform finished initialization.
##VRee Player Connected Event
This event is raised when a player has successfully connected.
##VRee Calibration Started Event
This event is raised when a calibration command is given for a player.
##VRee Calibration Finished Event
This event is raised when a player has finished the calibration procedure

# Player Fields
![Alt] (/images/settings/player-fields.png "Player Fields.")
This list of GameObjects is refered in the UI, and functions as the center of a users world.
When this GameObject is moved, the users connected to this field will move with it.