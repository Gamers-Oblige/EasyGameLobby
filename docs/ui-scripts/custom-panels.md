# Custom Panels

The template panels system handles what is displayed to the player in the UI. To extend this system, you can create custom panels by creating a script that extends the `BasePanel` or `SubPanelBase` class.

## BasePanel

The `BasePanel` class is the base class for all custom panels. It provides a custom inspector that allows you to easily see the panel in the editor and set the panel as the default panel.

It automatically listens for the `ActivePanelId.OnChanged` event of the [PanelsManager](#panelsmanager) and will automatically show or hide the panel based on the active panel id.

By default, it associates the `gameObject.GetInstanceId()` as the panel id. You can override the `BasePanel` methods to customize the panel id.

## SubPanelBase

It's a basic class that extends `MonoBehaviour` and provides a reference to the MainPanel it belongs to.

## PanelsManager

It's a simple class that listen to the LobbyManager events [`OnLobbyJoinedOrCreated`](../managing-lobbies/lobby-manager.md#onlobbyjoinedorcreated) and [`OnLobbyLeft`](../managing-lobbies/lobby-manager.md#onlobbyleft) events, showing the LobbyPanel when the player joins a lobby and showing the SearchPanel when the player leaves the lobby.

The script is located inside the root `UI` game object and can be deleted if you want to handle the panels change yourself.

Has a static field `ActivePanelId` that can be used to change the active panel id.

Type: [ActionValue](../others/action-value.md)<int\>
{:.info .under-title-h3}
