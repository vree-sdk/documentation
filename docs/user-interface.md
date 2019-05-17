The VRee platform comes with an example interface that can be used for basic application testing. This UI is generated using MarkLight and does not scale with resolution. Because of this it’s recommended to set the game resolution scale to `1920x1080`.

![Alt](/images/user-interface/full-hd-resolution.png "Setting the Unity game view to Full HD.")

The UI consists of four tabs: Configuration, Admin, Interact and Watch.

![Alt](/images/user-interface/overview.png "User interface overview.")

The left side displays a list of currently `Connected Players` (figure above - 1). The list is automatically updated whenever a player connects. For each player, the `name`, `body controller`, `hand controller` and `player field` are displayed. Next to each of those, the battery level is shown if the battery level is under 20%. The battery icon next to the player name corresponds with the battery level of the client device.

The `Calibrate` and `Recenter` buttons are activated when one or multiple players are selected from the `Connected Players` list (figure above - 2). The calibrate button starts the calibration process and the recenter button sets the position of the player back to the selected `player field` defined in the [VRee Settings](/vree-settings).

On the right side of the user interface, the `Player Configuration` is displayed (figure above - 3). The layout of this screen can be adjusted to your own personal liking using the buttons on the top right of the screen (figure above - 4). By default, the automatic layout is selected. This will automatically adjust the layout to the number of connected players.

![Alt](/images/user-interface/colormapped-settings.png "Settings mapped by color.")

Clicking on one of the color-coded icons shows the available options as seen in the figure above. These colorcodings are set configured in the `ColorMappings.txt` file in the `VRee Platform/Prerequisites` folder. Make sure to use `VRee -> Refresh Prerequisites` to copy the updated file to the root of the project. 