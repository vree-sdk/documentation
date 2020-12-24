# VRee player

## Player details

A VRee player is created for every user connected to the application. All information available for the player can be found in the Inspector by selecting the root for the player on the server. Each adapter can be expanded to display adapter specific information.

![Alt](./images/player/player-details.png "Player details.")

## Player model

A player model, defined in `VReeSDK > Settings > Player Settings`, is attached to the VRee Player. Any model can be used for the player as long as the model is in a valid Unity Mecanim Humanoid format.

> Note that the first and third person skeleton rig must be identical.

## Player avatar system

The player avatar system automatically synchronizes the player model's bones over the network using highly optimized data packets. This data may be modified before synchronization using [adapters](adapters.md).

### Bone Structure

The VRee Player Model structure is as follows:

- [Player Prefab]
  - Root
    - Skeleton
      - [Prefabs Unity's Mecanim bones]

First, all bone data will be applied on the `hip bone` and all children of it.
This data is inserted as `global` position and rotations.

Afterwards the data is put into the `Skeleton` and lastly into the `Root`. Because of this order of applying data, the data in the `Hips` and below are changed to `Local` positions and rotations relative to the `Skeleton` and `Root` bone.

An example of this system is action is showcased by the `PlayerFieldAdapter`, where rotating and moving the Player's field, moves and rotates the player accordingly.
