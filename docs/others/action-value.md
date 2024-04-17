# Action Value and Lobby Action Value

## Action Value

The `ActionValue` class is a generic class that allows you to create a value that can be updated and listened to.

### Properties

#### `Value`

Type: `T`
{:.info .under-title-h3}

#### `OnChanged`

Type: `event<T value, T oldValue>`
{:.info .under-title-h3}

Event only triggered when the value is updated, sending the new and old value.

### Methods

#### `SetValueWithoutNotify`

**Declaration**

<span class="code"><span class="return">void</span> <span class="method">SetValueWithoutNotify</span>(<span class="param">T</span> <span class="param-name">value</span>)</span>

**Parameters**

| Parameter | Type | Description |
| --- | --- | --- |
| **value**<span class="required">\*</span> | *T* | The new value to be set. |

*<span class="required">\*</span> Required parameter.*
{:.info .under-table}

**Description**

Sets the `Value` of the action value without triggering the `OnChanged` event.

## Lobby Action Value

The `LobbyActionValue` class is a generic class that implements the `ActionValue` class and the [`ILobbyValue`](custom-value-types.md#ilobbyvalue-interface) interface. It has the same properties and methods as the `ActionValue` class, but it also enables the [`LocalPlayer`](../managing-lobbies/local-player.md) and [`LocalLobby`](../managing-lobbies/local-lobby.md) classes to use it as a custom value, detecting changes and sending them to the server.
