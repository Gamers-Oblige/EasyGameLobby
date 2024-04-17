# Authentication

Easy Game Lobby uses Unity's built-in authentication system to manage users. This system allows you to authenticate users using different methods, we currently support Anonymous and Steam authentication.

All authentication methods can be accessed through the LobbyManager [`NetworkHelper`](lobby-manager.md#networkhelper) property.

Steam authentication methods are only available if [Steam is enabled](../enable-steamworks.md).

Refer to [Unity's documentation](https://docs.unity.com/ugs/en-us/manual/authentication/manual/use-anon-sign-in) for more information on how to implement other authentication methods.

## Methods

### `SignInAnonymously`{:.method}

**Declaration**

<span class="code"><span class="return">Task</span> <span class="method">SignInAnonymouslyAsync</span>( )</span>

**Description**

Sign in anonymously to the Unity Services.

### `SignInWithSteam`{:.method}

**Declaration**

<span class="code"><span class="return">Task</span> <span class="method">SignInWithSteamAsync</span>( )</span>

**Description**

Sign in with Steam to the Unity Services.

### `LinkSteamAccount`{:.method}

**Declaration**

<span class="code"><span class="return">Task</span> <span class="method">LinkSteamAccountAsync</span>( )</span>

**Description**

Link the Steam account to the anonymous account.

### `UnlinkSteamAccount`{:.method}

**Declaration**

<span class="code"><span class="return">void</span> <span class="method">UnlinkSteamAccount</span>( )</span>

**Description**

Unlink the Steam account from the anonymous account.
