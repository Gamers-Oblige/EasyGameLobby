# Local Player

Implemented in: `EasyGameLobby`
{:.info .under-title}

Wraps around Player instances, providing an interface for easy management and listening to player values and events. Most data fields utilize either a [`LobbyActionValue`](../others/action-value.md#lobbyactionvalue) or an [`ActionValue`](../others/action-value.md) to facilitate value changes and event listening (Refer to their respective pages for more information). While any player can modify values locally, only the player represented by the instance can send changes to the server using the {{[`UpdatePlayerData`](#updateplayerdata)}}{{< mdl-disable "<!-- markdownlint-disable MD051 -->" >}} method. Do not modify any data if the current player is not the player represented by the instance.

Any [custom player value](../getting-started/lobby-settings.md#custom-lobby-and-player-values) can be easily accessed by its name, as shown in the example below:

```csharp
Debug.Log(LobbyManager.Instance.CurrentPlayer.MyCustomPlayerValue.Value);
```

Or accessed using a string:

```csharp
// Casting is required to access the correct value type, otherwise it will always return the value as a string.
Debug.Log(
  (PlayerActionValue<int>)LobbyManager.Instance.CurrentPlayer["MyCustomPlayerValue"].Value
);
// Or
Debug.Log(
  (PlayerActionValue<int>)LobbyManager.Instance.CurrentPlayer.CustomDataMap["MyCustomPlayerValue"].Value
);
```

## Player Data

- **`Id`** - *string* Read-Only
- **`ClientId`** - *ulong* Read-Only  
Only visible to the host.

- **`IsHost`** - [LobbyActionValue](../others/action-value.md)<bool\>
- **`IsConnected`** - [LobbyActionValue](../others/action-value.md)<bool\>  
True if the player is connected to the relay.
Only visible to the host.

- **`Any Custom Player Value`** - [LobbyActionValue](../others/action-value.md)<T\>
- **`CustomDataMap`** - *Dictionary<string, [ILobbyValue](../others/custom-value-types.md#illobbyvalue-interface)\>*

```csharp title="Reading player values"
Debug.Log(LobbyManager.Instance.CurrentPlayer.IsHost.Value);
Debug.Log(LobbyManager.Instance.CurrentPlayer.MyCustomPlayerValue.Value);
```

```csharp title="Listening to player value changes"
LobbyManager.Instance.CurrentPlayer.IsHost.OnValueChanged += (oldValue, newValue) =>
{
  Debug.Log($"Is host changed from {oldValue} to {newValue}");
};
// Or
void OnIsHostChanged(bool oldValue, bool newValue)
{
  Debug.Log($"Is host changed from {oldValue} to {newValue}");
}

LobbyManager.Instance.CurrentPlayer.IsHost.OnValueChanged += OnIsHostChanged;
```

Refer to [Action Value](../others/action-value.md) for more information.

## Methods

### `UpdatePlayerData`{:.method}

**Declaration**

<span class="code"><span class="return">Task</span> <span class="method">UpdatePlayerData</span>( )</span>

**Description**

Updates the player data on the server. Only the player represented by the instance can send changes to the server.
