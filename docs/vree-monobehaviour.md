# VReeMonoBehaviour

The `VReeMonoBehaviour` script extends the standard Unity `MonoBehaviour` with useful features when developing with the VRee SDK. These scripts are automatically attached to a player when a player connects and has a reference to the player it is attached to.

## Creation

The VReeMonoBehaviour can be created by right-clicking in the Project window and selecting `Create > VRee > VReeMonoBehaviour Script`. Alternatively, a script can extend `VReeMonoBehaviour`.

The following method has to be implemented for the script to function properly.

```c#
public abstract SelectedBones AttachTo()
```

The AttachTo method should return which bone(s) the script should attached to. When the script is not reliant on placement to a specific bone SelectedBones.Root can be used.
If the script should be placed on multiple bones the OR operator can be used:
return SelectedBones.LeftHand | SelectedBones.RightHand;

## Utilization

The `VReeMonoBehaviour` is useful for placing logic on specific bones in the player body. For example, a script that logs the position of the hands can be created as follows.

1. Create the script.

   ```c#
   public class HandPositionLogger : VReeMonoBehaviour { }
   ```

1. Override the `AttachTo()` method to attach the script on the left and right hand.

   ```c#
   public override SelectedBones AttachTo()
   {
       return SelectedBones.LeftHand | SelectedBones.RightHand;
   }
   ```

1. Create an `Update()` method to log the position.

   ```c#
   private void Update()
   {
       string attachedTo = GetAttachedBone() == BoneType.LeftHand ? "left" : "right";
       Debug.Log($"[Player {Player.Id}] The position of the {attachedTo} hand is {transform.position}");
   }
   ```
