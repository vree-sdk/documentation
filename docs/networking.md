This chapter will explain how to send and receive VRee data packets and everything network related.

# Packets

A VRee Packet is essentially a wrapper around user data that can be easily sent over the network. The VRee Platform provides two types of packets: `PacketServerToClient` and `PacketClientToServer`. Packets are one-way traffic, meaning that a `PacketServerToClient` can only be sent from the server to a client and a `PacketClientToServer` can only be sent from a client to the server.

A packet can contain up to eight parameters. However, a packet can contain more data by creating a struct that holds multiple fields. Keep in mind that the maximum data size of a packet is `1400 bytes`, going over this value causes the packet to be split into multiple packets which increases packet drop rate.

TODO high level overview <<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<< 

## Defining a Packet

A packet is defined by creating a new class which extends from the PacketServerToClient base class or the PacketClientToServer base class. In the example shown below, a PacketServerToClient is created with one integer parameter.

```c#
public class MyPacketServerToClient : PacketServerToClient<int> { }
```

If a packet is important and needs to be __more likely__ to arrive, the `IsReliable()` method can be overwritten to return true. This will tell the VRee Platform to try to send the packet until it is received by the client or until the `maximum reliable packet resend count`[^1] is reached. Remember that flagging a packet as reliable puts a bigger strain on the network.

[^1]: Refer to the [VRee Settings documentation](/vree-settings/) for more information.

```c#
public override bool IsReliable()
{
   return true;
}
```

