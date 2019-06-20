This chapter explains what adapter do and how to use them.

#Adapters
An adapter is a script that modifies or reads data from the VReeBodyModel.

Adapters are executed every frame, in order of priority. This priority is set using the reorderable list in the [Settings](../vree-settings/#hardware-selection)

![Alt](../images/adapters/adapter-priority.jpg)

All adapters have extend from the IVReeAdapter interface which adds the following:
```c#
string AdapterName();
```
Name of the adapter.
```c#
int Priority { get; set; }
```
Priority of the adapter, used internally.
```c#
Player Player { get; set; }
```
Reference to the Player the adapter belongs to.
```c#
void Init();
```
Init is called after the adapter fully created, and fields like Player have been set.

#Defining an Adapter
Create a new script and make it extend from either `IVReeBodyAdapter` or `IVReeHandAdapter`

The only difference between the two is the signature of the `AdapterCallback` method. The IVReeBodyAdapter uses the entire body, where the hand adapter takes an array of floats indicating the bend of each finger.

After extending give the adapter a name:

```c#
public string AdapterName()
{
    return "ExampleAdapter";
}
```

Define both the Priority and the Player:
```c#
int Priority { get; set; }
Player Player { get; set; }
```

And run the any init code if required:
```c#
void Init()
{
    //do something, or not
}
```

Finally add your code to modify the bones as intended:

```c#
public bool AdapterCallback(int pid, ref Body body)
{
    //Let's move the hip bone 1m up
    body.SetBonePosition(BoneType.Hips, Player.GetNeutralBody(), new Vector3(0, 1, 0));
}
```

The SetBonePosition and SetBoneRotation calls of the Body class allows you to change the body's bone position and rotations.
There are two optional parameters in both of these calls, defining the `BoneTrackingSpace` and `BoneEditMode`.

`BoneTrackingSpace` defines wether the data is in world or local space. This defaults to world.
`BoneEditMode` defines how to handle the data. This defaults to CombineData.  

- ReplaceData

    >    *Replaces the existing data in the bone with the supplied data, multiplied by the neutral of the avatar*

- CombineData

    >    *Combines the existing data in the bone with the supplied data, multiplied by the neutral of the avatar*

- ReplaceDataRecursively

    >    *Replaces the existing data in the bone and all of its children with the supplied data, multiplied by the neutral of the avatar*

- CombineDataRecursively

    >    *Combines the existing data in the bone and all of its children with the supplied data, multiplied by the neutral of the avatar*

- ReplaceDataIngoreNeutral

    >    *Replaces the existing data in the bone with the supplied data, ingoring the neutral of the avatar*

- CombineDataIngoreNeutral

    >    *Combines the existing data in the bone with the supplied data, ingoring the neutral of the avatar*

- ReplaceDataRecursivelyIngoreNeutral

    >    *Replaces the existing data in the bone and all of its children with the supplied data, ignoring the neutral of the avatar*

- CombineDataRecursivelyIngoreNeutral

    >    *Combines the existing data in the bone and all of its children with the supplied data, ignoring the neutral of the avatar*

- Ignore

    >    *Do nothing*

Make sure that one, *and only one,* adapter uses the neutral after every `ReplaceData` for that bone. This makes sure the data is correct for the currently selected model.

#Using the adapter
To use an adapter it has to be added to the `Selected Input Devices`, as well as the `Supported Hardware Selection` in the Settings.

To be able to add it to these lists, first start by creating a new `AdapterDefinition` by going to `Assets -> Create -> VRee -> Adapters -> Add Adapter Definition`.
After naming the definition select it and add a new item to the `Input Adapters` list. Click the dropdown box and select the adapter by the name defined in the `AdapterName` method.

Go back to the settings and add the new definition to the Lists specified above.
If you want to change the priority you can now reorder it in the `Adapter Priority` part of the `Hardware Selection` segment of the settings.

#Bone Structure
The VRee Player Model structure looks as following:

 - [Player Prefab]
    - Root
        - Skeleton
            - [Prefabs Unity's Mecanim bones]

First, all bone data will be applied on the `hip bone` and all children of it.
This data is inserted as `Global` position and rotations.

Afterwards the data is put into the `Skeleton` and lastly into the `Root`. Because of this order of applying data, the data in the `Hips` and below are changed to `Local` positions and rotations relative to the `Skeleton` and `Root` bone.

An example of this system is action is showcased by the `PlayerFieldAdapter`, where rotating and moving the Player's field, moves and rotates the player accordingly.