---
hide:
  - navigation
  - toc
---
# Enabling Steamworks

1. [Install the Steamworks Package](https://steamworks.github.io/installation/#unity-instructions) (Installing using the .unitypackage is easier)
2. A new script will be created at `Assets/Scripts/Steamworks.NET/SteamManager.cs`, move it to `Assets\com.rlabrecque.steamworks.net\Runtime`
3. Create a new GameObject in the scene and add the `SteamManager` script to it
4. Create your app and note down the app ID following the [Steamworks documentation](https://partner.steamgames.com/doc/store/application#creating_applications).
5. Create the Publisher Web API key following the [Authentication using Web API Keys](https://partner.steamgames.com/doc/webapi_overview/auth) documentation.
6. Configure your ID provider to be Steam for Unity Authentication:
      1. In the Unity Editor menu, go to Edit > Project Settings…, then select Services > Authentication from the navigation menu.
      2. Set ID Providers to Steam, then select Add.
      3. Enter the app ID in the App ID text field.
      4. Enter the Publisher Web API Key in the Key text field, then select Save.
7. On the Project Settings and go to the `Player` > `Other Settings` > `Script Compilation` and add a new define symbol `ENABLE_STEAM`

Now Steamworks API is enabled and Unity services are configured to use Steam as an authentication provider.

Easy Game Lobby, only uses Steam to authenticate and get the Steam profile name, refer to the [Steamworks.NET documentation](https://steamworks.github.io/) and [Steamworks oficial documentation](https://partner.steamgames.com/doc/api) for more information on how to further use the Steamworks API.
