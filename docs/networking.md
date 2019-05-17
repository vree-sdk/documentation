This chapter will explain how to send and receive VRee data packets and everything network related.

TODO high level overview <<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<< 

# Defining a Packet

To create a packet simply create a new C# script and make it extend from either `PacketServerToClient` or `PacketClientToServer`. Packets can only be send one direction, trying to send it the wrong way will result in an exception being thrown.

In this example the packet will be send from Server to Client and it will contain a single integer. This example will be used to explain the different options and uses of the Networking System.

After extending from the PacketServerToClient we define a single integer parameter:

```c#
public class MyPacketServerToClient : PacketServerToClient<int> { }
```

Up to 8 parameters can be added this way. If more are required you can compile data into a struct and use the struct as a parameter.

Always try to keep the maximum data size of a packet under 1400 bytes, going over this value will cause the packet to be split up in multiple packets and increases packet droprate.

If a packet needs to be more likely to arrive it can be made Reliable.This is done by adding the isReliable override function to the class
public override bool isReliable()
    {
        return true;
    }
This should only be used for packet rarely send, as this puts a much bigger strain on the network. 

Please note, this does not guerantee packets arriving, but it will automatically resend it if the client does not send a proper reply. This is tried up to a maximum of default 50 times, and can be changed in the DataLogger Settings 
TODO move settings
