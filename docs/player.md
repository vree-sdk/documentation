#VRee Player
A VRee player is created for every user connected to the application. The following diagram shows the connection protocol after the PlatformId was confirmed.

![Alt](../images/player/player-connection-diagram.jpg "Player Connection.")

All information available for the player can be found in the Editor by selecting the root for the intended player on the server.

![Alt](../images/player/player-editor.png "Player Editor.")

Each player has an body which is controller by Adapters as explain in [here](../adapters.md).  
Furthermore some general information about the player and his configuration is available.
##Player Models
The player model a player is given is defined in the VReeSettings. The player is always controlled using a VRee Body Model. For any player configuration all bones are send over the network, as a complete body model has been optimized to fit within a single UDP packet.

Any model can be used for the player as long as the model fits in Unity’s Mecanim Humanoid format. The data is automatically converted to be used with the currently selected rig.
The rig for the First person and Third person players must be identical.

 
##VReeMonoBehaviour
These scripts are automatically placed upon every player when a player connects. If preferred this option can be disabled as explained in the VReeMonoBehaviour Features chapter.
This chapter will walk through the process of creating a new VReeMonoBehaviour as well as some of the notable features.

__Creating a new VReeMonoBehaviour__  
The VReeMonoBehaviour can be created by Right clicking in the Project window and selecting Create -> VRee -> VReeMonoBehaviour Script

Alternatively, create a new C# script and replace the MonoBehaviour extension with the VReeMonoBehaviour extension. The following methods will have to be overridden:

```c#
public override void Init()
public override SelectedBones SelectedBoneIds()
```


Their functionality is explained in the next chapter.

__VReeMonoBehaviour features__  

```c#
public Player Player;
```

The Player field is a reference to the player this script was placed upon.

```c#
public BoneType GetAttachedBone()
```

The GetAttachedBone method can be called to retrieve the BoneType on which this script was placed.

```c#
public override void Init()
```

The Init method is called after the script was placed on the player and initialized. At this point the Player and AttachedBone will be set and can be used. This is a mandatory function to be implemented.

```c#
public override SelectedBones SelectedBoneIds()
```

The SelectedBoneIds method has to be implemented and should return which bone the script should be placed upon. When the script is not reliant on placement to a specific bone SelectedBones.Root can be used. 
If the script should be placed on multiple bones the OR operator can be used:
return SelectedBones.LeftHand | SelectedBones.RightHand;

```c#
public override bool PutOnPlayer()
```

The PutOnPlayer method is an optional override, when not overridden this will return true. Can be changed to return false if the script should not be automatically added to the Player on connection.

__MonoBehaviour__  
The VReeMonoBehaviour in turn extends from the traditional MonoBehaviour, so any normal MonoBehaviour methods like Start and Update will be available.
