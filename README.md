
## MirrorNetworkDiscovery

Network discovery for [Mirror](https://github.com/vis2k/Mirror).


## Features

- Simple. 1 script. 600 lines of code.

- Uses C#'s UDP sockets for broadcasting and sending responses.

- Independent of current transport. Although, [NetworkDiscoveryHUD](/NetworkDiscoveryHUD.cs) (example GUI) works only with Telepathy.

- Single-threaded.

- Tested on: Linux, Windows, Android.

- Can lookup specific servers on the internet (outside of local network).

- Has a separate [GUI script](/NetworkDiscoveryHUD.cs) for easy testing.

- Has support for custom response data.

- By default, server responds with: current scene, number of players, max number of players, game server port number, game signature.

- No impact on performance.


## Usage

Attach [NetworkDiscovery](/NetworkDiscovery.cs) script to NetworkManager's game object. Assign game server port number.

Now, you can use [NetworkDiscoveryHUD](/NetworkDiscoveryHUD.cs) script to test it (by attaching it to NetworkManager), or use the API directly:

```cs
// register listener
NetworkDiscovery.onReceivedServerResponse += (NetworkDiscovery.DiscoveryInfo info) =>
{
	// we received response from server
	// add it to list of servers, or connect immediately...
};

// send broadcast on LAN
// when server receives the packet, he will respond
NetworkDiscovery.SendBroadcast();

// on server side, you can register custom data for responding
NetworkDiscovery.RegisterResponseData("Game mode", "Deathmatch");
```

For more details on how to use it, check out NetworkDiscoveryHUD script.


## Inspector

![](/NetworkDiscoveryInInspector.png)


## Example GUI

![](/HUD.png)


## TODO

- Don't try to start/stop server socket every frame, but only when server status changes

- Measure ping - requires that all socket operations are done in a separate thread, or using async methods

- Add "Refresh" button in GUI next to each server

- Prevent detection of multiple localhost servers (by assigning GUID to each packet) ?

- Centered label ; join "Players" and "MaxNumPlayers" columns

