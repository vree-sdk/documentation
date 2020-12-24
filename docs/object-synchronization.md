# Object Synchronization

The VRee SDK for Unity allows developers to easily synchronize data using the provided synchronization system. The synchronization system automatically synchronizes when the data has changed and bundles the information to optimize the network traffic. Object synchronizers only work on objects that are in the scene on startup, instantiated objects will not be synchronized.

By default, two synchronizers are included:

- `TransformSynchronizer` - synchronizes the position, rotation and scale of the Unity Transform component.
- `EnabledStateSynchronizer` - synchronizes the enabled state of the GameObject.

## Using synchronizers

To synchronize an object, simply add the `SynchronizedObject` component to a GameObject. This component marks the GameObject as synchronized and gives it a unique Id. On this component, the rate at which the data should be synchronized can be defined. By default, the synchronization rate is set to synchronize every frame (0).

![Alt](./images/object-synchronization/synchronizedobject.png "GameObject with SynchronizedObject component added.")

With only a `SynchronizedObject`, the GameObject is marked as synchronized but nothing is being synchronized because the object has no `Synchronizer`. In the image below, a `TransformSynchronizer` is attached to the object.

![Alt](./images/object-synchronization/synchronizedobject-with-transformsynchronizer.png "Transform Synchronizer added to the synchronized object.")

## Creating Custom Synchronizers

Custom synchronizers can be created take advantage of the Synchronization system’s automatic data bundling. In this example, we’ll create a `CustomSynchronizer` that synchronizes an integer. The class diagram shown below explains how the Synchronization system connects the classes necessary for synchronization. For the `CustomSynchronizer`, three new classes will be created: `CustomSynchronizer`, `CustomSynchronizerDataBundler` and `CustomSynchronizerBundledDataPacket`.

![Alt](./images/object-synchronization/synchronization-class-diagram.png "Synchronization class diagram.")

- The `CustomSynchronizer`, this class extends from SynchronizerBase. This class defines the Data struct and is responsible for determining if the data has changed.
- The `CustomSynchronizerDataBundler`, this class extends from SynchronizerDataBundlerBase which handles the data bundling.
- The `CustomSynchronizerPacket`, this class extends from PacketServerToClient<CustomSynchronizer.Data[]> and contains the data bundled by the CustomSynchronizerDataBundler.

A couple of virtual methods have to be overwritten in the CustomSynchronizer script.

- The `Register()` method should call CustomSynchronizerData.RegisterSynchronizer() method with itself as parameter, this ensures that the data can arrive to the Client_Synchronize() method on the client.
- The `Server_DetectChange()` to set the Synchronize flag to true when the data has changed.
- The `Client_Synchronize()` method should validate the data type and update the local values with the data values.

The data struct must contain an integer field storing the Id and any optional data fields. In this case, the `IntegerData` field is added.

```
[DisallowMultipleComponent] // Make sure only one of this synchronizer can be added per GameObject.
public class CustomSynchronizer : SynchronizerBase
{
    /// <summary>
    /// Defines the data this Synchronizer will synchronize to the clients.
    /// </summary>
    public struct Data : ISynchronizerData
    {
        public int Id;
        public int IntegerData; // <- Added the integer data field.

        public int GetId()
        {
            return Id;
        }
    }

    /// <summary>
    /// Stores the previous state of the data.
    /// </summary>
    private int _previousIntegerData; // <- Store the previous integer data.

    /// <summary>
    /// Stores the current state of the data.
    /// </summary>
    [SerializeField] private int _integerData; // <- Store the current integer data.

    /// <summary>
    /// Checks for changes in data.
    /// </summary>
    protected override void Server_DetectChange()
    {
        base.Server_DetectChange();

        if (_integerData != _previousIntegerData) // <- Check if the integer data was changed.
        {
            Synchronize = true;
        }

        _previousIntegerData = _integerData; // <- Set the previous integer data.
    }

    /// <summary>
    /// Registers itself to the SynchronizerDataBundler.
    /// </summary>
    /// <param name="assignedId">The UniqueId assigned to the SynchronizedObject.</param>
    internal override void Register(int assignedId)
    {
        base.Register(assignedId);

        CustomSynchronizerDataBundler.Instance.RegisterSynchronizer(this); // <- Register the CustomSynchronizer.
    }

    /// <summary>
    /// Gets the current data.
    /// </summary>
    /// <returns>The current data struct.</returns>
    public override object GetData()
    {
        return new Data() // <- Return the Data struct with the current integer data.
        {
            Id = AssignedId, // This value must be the AssignedId of the Synchronizer.
            IntegerData = _integerData
        };
    }

    /// <summary>
    /// Bundles the data.
    /// </summary>
    public override void BundleData()
    {
        CustomSynchronizerDataBundler.Instance.Server_BundleData(this); // <- Bundle the data for the CustomSynchronizer.
    }

    /// <summary>
    /// Gets the data bundler for this synchronizer.
    /// </summary>
    /// <returns></returns>
    public override ISynchronizerDataBundler GetBundler()
    {
        return CustomSynchronizerDataBundler.Instance; // <- Return the CustomSynchronizer DataBundler.
    }

    /// <summary>
    /// Updates the synchronized data from the server.
    /// </summary>
    /// <param name="data">The data to be updated.</param>
    internal override void Client_Synchronize(ISynchronizerData data)
    {
        VReeSDK.ValidateClient(); // Validate the role.
        if (!(data is Data)) { return; } // Check if the data is the correct type.

        Data synchronizedData = (Data)data;

        // Update the synchronizedData on the client.
        _integerData = synchronizedData.IntegerData; // <- Set the current data.
    }
}
```

```
/// <summary>
/// The data bundler for this synchronizer.
/// </summary>
internal class CustomSynchronizerDataBundler : SynchronizerDataBundlerBase<
    CustomSynchronizer,
    CustomSynchronizer.Data,
    CustomSynchronizerBundledDataPacket>
{ }
```

```
/// <summary>
/// The synchronizer bundled data packet.
/// </summary>
internal class CustomSynchronizerBundledDataPacket : PacketServerToClient<CustomSynchronizer.Data[]> { }
```

To get a better understanding of how the synchronization system works internally, refer to the following sequence diagram.

![Alt](./images/object-synchronization/synchronization-sequence-diagram.png "Synchronization sequence diagram.")
