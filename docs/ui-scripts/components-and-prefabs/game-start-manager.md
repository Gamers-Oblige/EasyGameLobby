# Game Start Manager

The Game Start Manager is singleton component that manages all players ready status and starts the game when the conditions are met.

It's located in the Lobby Panel GameObject.

## Inspector Options

- **Should Everyone Be Ready**: If true, all players must be ready to start the game.
- **Should Lock Lobby**: If true, the lobby will be locked when the game starts, preventing new players from joining.
- **Min Players To Start**: The minimum number of players required to start the game.
- **Game Scene Name**: The name of the scene to load, if left empty the event [`OnGameStart`](#events) will be triggered.

Note that if the lobby is not locked, players can still join the lobby after the game has started and it's up to you to sync the game state with the new player.

## Properties

- **Instance**: The singleton instance of the Game Start Manager.
- **ReadyPlayers**: A network list of players IDs that are ready to start the game.

## Events

- **OnGameStart**: Triggered when the game starts. Only triggered if the `Game Scene Name` is empty.
- **OnNetworkSpawned**: Triggered when the player is connected in the network. (Triggered by the [`NetworkBehaviour`](https://docs-multiplayer.unity3d.com/netcode/current/basics/networkbehavior/) inherited class).
