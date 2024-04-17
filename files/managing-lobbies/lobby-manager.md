# Lobby Manager

Implemented in: `EasyGameLobby`
{:.info .under-title}

The Lobby Manager is the main class that you will interact with when working with lobbies, it's a singleton and won't be destroyed on load. It is responsible for managing all lobby functionalities such as creating and keeping the lobby active sending [`Heartbeats`](../getting-started/lobby-settings.md#lobby-settings) and everything you may need while working with lobbies.

Unless you are creating your own lobby UI from scratch or modifying the existing one, you will not need to interact with the Lobby Manager directly. However, it is important to understand its properties and methods.

## Properties

### `LobbyManager.Instance`

Type: LobbyManager
{:.info .under-title-h3}

The singleton instance of the Lobby Manager. You can access it from any script by calling `LobbyManager.Instance` and access its properties and methods.

### `CurrentLobby`

Type: [LocalLobby](local-lobby.md)
{:.info .under-title-h3}

The current lobby the player is in. Instance of the [`LocalLobby`](local-lobby.md) class, which contains all the information about the lobby. If the player is not in a lobby, it will be `null`.

### `CurrentPlayer`

Type: [LocalPlayer](local-player.md)
{:.info .under-title-h3}

Instance of the [`LocalPlayer`](local-player.md) class, which contains all the information about the player. Even if the player is not in a lobby, this property will always be available.

### `NetworkHelper`

Type: [NetworkHelper](authentication.md)
{:.info .under-title-h3}

Instance of the [`NetworkHelper`](authentication.md) class, which contains all the methods for authenticating the player.

## Methods

### `CreateLobby`{:.method}

**Declaration**

<span class="code"><span class="return">Task</span> <span class="method">CreateLobby</span>(<span class="param">bool</span> <span class="param-name">isPrivate</span>, <span class="param">string</span> <span class="param-name">lobbyName</span>, <span class="param">string</span> <span class="param-name">password</span> = null, <span class="param">int</span> <span class="param-name">maxPlayers</span> = DEFAULT_MAX_PLAYERS)</span>

<span class="code"><span class="return">Task</span> <span class="method">CreateLobby</span>([LocalLobby](local-lobby.md) <span class="param-name">newLobby</span>, <span class="param">string</span> <span class="param-name">lobbyName</span>, <span class="param">int</span> <span class="param-name">maxPlayers</span> = DEFAULT_MAX_PLAYERS)</span>

**Parameters**

| Parameter | Type | Description |
| --- | --- | --- |
| **isPrivate**<span class="required">\*</span> | *bool* | Determines if the lobby is private. |
| **lobbyName**<span class="required">\*</span> | *string* | The name of the lobby. |
| **password** | *string* | The password to join the lobby. |
| **maxPlayers** | *int* | The maximum number of players allowed in the lobby. |
| **newLobby**<span class="required">\*</span> | [LocalLobby](local-lobby.md) | New instance of the LocalLobby class with the lobby settings. |

*<span class="required">\*</span> Required parameter.*
{:.info .under-table}

**Description**

Creates a new lobby with the specified settings. If a LocalLobby instance is provided, it will use its settings instead of the parameters. The player will automatically join the lobby after creation and trigger the [`OnLobbyJoinedOrCreated`](#onlobbyjoinedorcreated) event.

### `JoinLobby`{:.method}

**Declaration**

<span class="code"><span class="return">Task</span> <span class="method">JoinLobbyById</span>(<span class="param">string</span> <span class="param-name">id</span>, <span class="param">string</span> <span class="param-name">password</span> = null)</span>

<span class="code"><span class="return">Task</span> <span class="method">JoinLobbyByCode</span>(<span class="param">string</span> <span class="param-name">code</span>, <span class="param">string</span> <span class="param-name">password</span> = null)</span>

**Parameters**

| Parameter | Type | Description |
| --- | --- | --- |
| **id**<span class="required">\*</span> | *string* | The ID of the lobby to join. |
| **code**<span class="required">\*</span> | *string* | The code of the lobby to join. |
| **password** | *string* | The password to join the lobby. |

*<span class="required">\*</span> Required parameter.*
{:.info .under-table}

**Description**

Joins a lobby by its ID or code. If the lobby is private, the password must be provided. The player will automatically join the lobby and trigger the [`OnLobbyJoinedOrCreated`](#onlobbyjoinedorcreated) event.

### `QuickJoinLobby`{:.method}

**Declaration**

<span class="code"><span class="return">Task</span> <span class="method">QuickJoinLobby</span>(<span class="param">[QueryBuilder](filtering-lobbies/query-builder.md)</span> <span class="param-name">queryBuilder</span>)</span>

**Parameters**

| Parameter | Type | Description |
| --- | --- | --- |
| **queryBuilder**<span class="required">\*</span> | [QueryBuilder](filtering-lobbies/query-builder.md) | The query builder to filter the lobbies to join. |

*<span class="required">\*</span> Required parameter.*
{:.info .under-table}

**Description**

Joins a random lobby that matches the query builder filters. The player will automatically join the lobby and trigger the [`OnLobbyJoinedOrCreated`](#onlobbyjoinedorcreated) event.

### `GetLobbies`{:.method}

**Declaration**

<span class="code"><span class="return">Task</span>&lt;<span class="return">List</span>&lt;[LocalLobby](local-lobby.md)&gt;&gt; <span class="method">GetLobbiesAsLocal</span>(<span class="param">[QueryBuilder](filtering-lobbies/query-builder.md)</span> <span class="param-name">queryBuilder</span>)</span>

<span class="code"><span class="return">Task</span>&lt;<span class="return">List</span>&lt;<span class="return">Lobby</span>&gt;&gt; <span class="method">GetLobbies</span>(<span class="param">[QueryBuilder](filtering-lobbies/query-builder.md)</span> <span class="param-name">queryBuilder</span>)</span>

**Parameters**

| Parameter | Type | Description |
| --- | --- | --- |
| **queryBuilder**<span class="required">\*</span> | [QueryBuilder](filtering-lobbies/query-builder.md) | The query builder to filter the lobbies to get. |

*<span class="required">\*</span> Required parameter.*
{:.info .under-table}

**Description**

Returns a list of lobbies that match the query builder filters. The lobbies can be returned as a list of `Lobby` or [`LocalLobby`](local-lobby.md) instances.

### `TryToReconnectLastJoinedLobby`{:.method}

**Declaration**

<span class="code"><span class="return">Task</span>&lt;<span class="return">bool</span>&gt; <span class="method">TryToReconnectLastJoinedLobby</span>( )</span>

**Description**

Tries to reconnect to the last lobby the player was in. Returns `true` if the reconnection was successful, `false` otherwise.

As Easy Game Lobby does not handle the game's networking or gameplay logic, be aware that even though the reconnection was successful, it's up to you to sync the current game state with the reconnected player.

### `LeaveLobby`{:.method}

**Declaration**

<span class="code"><span class="return">Task</span> <span class="method">LeaveLobby</span>(<span class="param">string</span> <span class="param-name">reason</span> = null)</span>

**Parameters**

| Parameter | Type | Description |
| --- | --- | --- |
| **reason** | *string* | The reason for leaving the lobby. |

**Description**

Leaves the current lobby. If a reason is provided, an [`OnMsgPopup`](#onmsgpopup) event will be triggered with the reason with the type `Info`.

### `RemovePlayer`{:.method}

**Declaration**

<span class="code"><span class="return">Task</span> <span class="method">RemovePlayer</span>(<span class="param">string</span> <span class="param-name">playerId</span>)</span>

**Parameters**

| Parameter | Type | Description |
| --- | --- | --- |
| **playerId**<span class="required">\*</span> | *string* | The ID of the player to remove from the lobby. |

*<span class="required">\*</span> Required parameter.*
{:.info .under-table}

**Description**

Removes a player from the current lobby. Only the lobby owner can remove players from the lobby.

## Events

### `OnLobbyJoinedOrCreated`

**Parameters**

| Parameter | Type | Description |
| --- | --- | --- |
| **joinedLobby** | [LocalLobby](local-lobby.md) | The lobby that was joined or created. |

**Description**

Triggered when the player joins or creates a lobby, providing the LocalLobby instance of the lobby.

### `OnMsgPopup`

**Parameters**

| Parameter | Type | Description |
| --- | --- | --- |
| **text** | *string* | The message to display. |
| **msgType** | *MessageType* | The type of the message. |

**Description**

Triggered when a message popup is requested, providing the message text and type.

Message types enum:

- `Ignorable`
- `Info`
- `Warning`
- `Error`
- `Critical`

### `OnLobbyLeft`

**Description**

Triggered when the player leaves the lobby.

## Request Cooldown

Every Lobby request has it's [rate limits](https://docs.unity.com/ugs/en-us/manual/lobby/manual/rate-limits), [`RequestCooldown`](../others/request-cooldown.md) is a class that helps managing the rate limit of the requests. All RequestCooldown are static readonly fields that can be accessed from the `LobbyManager` class.

**Available RequestCooldown:**

- `QueryCooldown`
- `CreateLobbyCooldown`
- `JoinLobbyCooldown`
- `QuickJoinCooldown`
- `LeaveOrRemovePlayerCooldown`
- `UpdatePlayerCooldown`
- `UpdateLobbyCooldown`
- `GetJoinedLobbiesCooldown`
- `ReconnectCooldown`
- `HeartbeatCooldown`

See more about the [RequestCooldown](../others/request-cooldown.md) class.
