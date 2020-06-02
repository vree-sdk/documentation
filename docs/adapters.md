# Adapters

An adapter is a script that reads and/or modifies data from the VReeBodyModel.

Adapters are executed every frame, in order of priority. This priority is set using the reorderable list in the [Settings](vree-settings.md#player-settings)

## Creating an adapter

A new adapter can be created by extending from `AdapterBase`. Three methods can be overwritten:

```c#
public virtual void Init() { }
```

The `Init` method is called when the adapter is instantiated.

```c#
public virtual void Destruct() { }
```

The `Destruct` method is called when the adapter is destructed.

```c#
public virtual bool AdapterCallback(int pid, ref Body body)
{
    return false;
}
```

The `AdapterCallback` method is called every frame. This method gets a reference of the body. In this method, the adapter's logic is placed. For example:

```c#
// Move the hip bone up by 1 meter.
body.SetBonePosition(BoneType.Hips, new Vector3(0, 1, 0),  Player.GetNeutralBody());
```

### Modifying the body

Using the `Body` reference within the `AdapterCallback` allows for modification of it's bones using the `SetBonePosition` and `SetBoneRotation` methods.

There are two optional parameters in both of these calls, defining the `BoneTrackingSpace` and `BoneEditMode`.

`BoneTrackingSpace` defines whether the data is in world (global) or local space. `BoneEditMode` defines how to handle the data. The following options are available:

- **ReplaceData**
  Replaces the existing data in the bone with the supplied data, multiplied by the neutral of the avatar

- **ReplaceDataIgnoreNeutral**
  Replaces the existing data in the bone with the supplied data, ignoring the neutral of the avatar

- **ReplaceDataRecursively**
  Replaces the existing data in the bone and all of its children with the supplied data, multiplied by the neutral of the avatar

- **ReplaceDataRecursivelyIgnoreNeutral**
  Replaces the existing data in the bone and all of its children with the supplied data, ignoring the neutral of the avatar

- **CombineData**
  Combines the existing data in the bone with the supplied data, multiplied by the neutral of the avatar

- **CombineDataIngoreNeutral**

  Combines the existing data in the bone with the supplied data, ignoring the neutral of the avatar

- **CombineDataRecursively**
  Combines the existing data in the bone and all of its children with the supplied data, multiplied by the neutral of the avatar

- **CombineDataRecursivelyIgnoreNeutral**
  Combines the existing data in the bone and all of its children with the supplied data, ignoring the neutral of the avatar

- **Ignore**
  Do nothing

> Make sure that **exactly one** adapter uses the neutral after every `ReplaceData` for that bone. This makes sure the data is correct for the currently selected model.
