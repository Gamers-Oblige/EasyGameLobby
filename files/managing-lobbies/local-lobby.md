# Local Lobby

Implemented in: `EasyGameLobby`
{:.info .under-title}
<!-- markdownlint-disable MD051 -->
Local Lobby wraps around Lobby instances, providing an interface for easy management and listening to lobby values and events. Most data fields utilize either a [`LobbyActionValue`](../others/action-value.md#lobby-action-value) or an [`ActionValue`](../others/action-value.md) to facilitate value changes and event listening (Refer to their respective pages for more information). While any player can modify values locally, only the host can send changes to the server using the [`UpdateLobbyData`](#updatelobbydata) method. Do not modify any data if the current player is not the host.
<!-- markdownlint-enable MD051 -->
All data of joined lobbies are automatically synchronized with the server, and the host is responsible for updating the lobby data.

Any [custom lobby value](../getting-started/lobby-settings.md#custom-lobby-and-player-values) can be easily accessed by its name, as shown in the example below:

```csharp
Debug.Log(LobbyManager.Instance.CurrentLobby.MyCustomValue.Value);
```

Or accessed using a string:

```csharp
// Casting is required to access the correct value type, otherwise it will always return the value as a string.
Debug.Log(
  (LobbyActionValue<int>)LobbyManager.Instance.CurrentLobby["MyCustomValue"].Value
);
// Or
Debug.Log(
  (LobbyActionValue<int>)LobbyManager.Instance.CurrentLobby.CustomDataMap["MyCustomValue"].Value
);
```

A new instance of a local lobby can be created and provided to the [`CreateLobby`](../managing-lobbies/lobby-manager.md#createlobby) method to create a lobby with updated values before creation.

```csharp title="Local Lobby Constructor"
// The relay code is always automatically generated, providing it will have no effect.
public LocalLobby(bool isPrivate, string password = null, string relayCode = null)
```

```csharp
// Password is optional
LocalLobby newLobby = new LocalLobby(true, "password123");
newLobby.MyCustomValue.Value = 10;
await LobbyManager.Instance.CreateLobby(newLobby, "My Lobby", 4);
```

## Lobby Data

- **`Id`** - *string* Read-Only
- **`Code`** - *string* Read-Only
- **`Name`** - [LobbyActionValue](../others/action-value.md#lobby-action-value)<string\>
- **`MaxPlayers`** - [LobbyActionValue](../others/action-value.md#lobby-action-value)<int\>
- **`IsPrivate`** - [LobbyActionValue](../others/action-value.md#lobby-action-value)<bool\>
- **`IsLocked`** - [LobbyActionValue](../others/action-value.md#lobby-action-value)<bool\>
- **`HostId`** - [LobbyActionValue](../others/action-value.md#lobby-action-value)<string\>
- **`Password`** - [LobbyActionValue](../others/action-value.md#lobby-action-value)<string\>  
Only visible to the host.

- **`HasPassword`** - [ActionValue](../others/action-value.md)<bool\>
- **`Players`** - *List<[LocalPlayer](local-player.md)\>*
- **`ClientIdToPlayer`** - *Dictionary<ulong, [LocalPlayer](local-player.md)\>*  
Maps the Netcode client id to the [LocalPlayer](local-player.md).
Only visible to the host.

- **`RelayCode`** - [LobbyActionValue](../others/action-value.md#lobby-action-value)<string\>
- **`Any Custom Lobby Value`** - [LobbyActionValue](../others/action-value.md#lobby-action-value)<T\>
- **`CustomDataMap`** - *Dictionary<string, [ILobbyValue](../others/custom-value-types.md)\>*

```csharp title="Reading lobby values"
Debug.Log(LobbyManager.Instance.CurrentLobby.Name.Value);
Debug.Log(LobbyManager.Instance.CurrentLobby.MyCustomValue.Value);
```

```csharp title="Listening to lobby value changes"
LobbyManager.Instance.CurrentLobby.Name.OnValueChanged += (oldValue, newValue) =>
{
  Debug.Log($"Lobby name changed from {oldValue} to {newValue}");
};
// Or
void OnNameChanged(string oldValue, string newValue)
{
  Debug.Log($"Lobby name changed from {oldValue} to {newValue}");
}

LobbyManager.Instance.CurrentLobby.Name.OnValueChanged += OnNameChanged;
```

Refer to [Action Value](../others/action-value.md) for more information.

## Methods

### `UpdateLobbyData`{:.method}

**Declaration**

<span class="code"><span class="return">Task</span> <span class="method">UpdateLobbyData</span>( )</span>

**Description**

Sends all updated lobby values to the server. Only the host can send changes to the server.

Example:

```csharp
LobbyManager.Instance.CurrentLobby.MyCustomValue.Value = 99;
LobbyManager.Instance.CurrentLobby.Name.Value = "New Lobby Name";
await LobbyManager.Instance.CurrentLobby.UpdateLobbyData();
```

## Events

### `OnPlayerJoined`

**Parameters**

- **[`LocalPlayer`](local-player.md)** - The player that joined the lobby.

**Description**

Event that is called when a player joins the lobby.

### `OnPlayerRemoved`

**Parameters**

- **[`LocalPlayer`](local-player.md)** - The player that left the lobby.
- **`int`** - The index of the player in the player list (Do not use this index to access the player in the [player list](#lobby-data) as it will be unavailable).

**Description**

Event that is called when a player leaves the lobby.
