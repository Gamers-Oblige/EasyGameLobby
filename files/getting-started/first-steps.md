# Getting started

<span class="text-center margin-top-40">
  <a href="https://assetstore.unity.com/packages/slug/282001" class="btn btn-primary" role="button">:simple-unity: Download Package</a>
</span>

## Importing the package

To begin using Easy Game Lobby, import the package into your Unity project.

When importing the files, the "Runtime/Templates" folder is optional. This folder contains a fully functional lobby template that you can use to jumpstart your game development. If you prefer to create your own lobby UI from scratch, you can skip importing this folder. However, we recommend checking the template to understand the system and utilize some of its scripts for your custom interfaces.

## Enabling Unity Services

After importing the Easy Game Lobby package into your Unity project, enable the necessary services:

1. [Unity Services](https://docs.unity3d.com/Manual/SettingUpProjectServices.html)
2. [Unity Lobby](https://docs.unity.com/ugs/en-us/manual/lobby/manual/get-started#Set_up_Lobby)
3. [Unity Relay](https://docs.unity.com/ugs/en-us/manual/relay/manual/get-started#Set_up_Relay)

## Loading the Template

If you imported the "Runtime/Templates" folder, choose one of the available templates. Add the scene to your build settings and open it to see the lobby in action. (You may need to import the TextMesh Pro package to display texts correctly, if not imported already. Reload the scene after importing.)

Create a new scene called "GameScene" and add it to the build, it's the default scene name to be loaded when starting a game on the lobby template, but you can change it in the [`GameStartManager`](../ui-scripts/components-and-prefabs/game-start-manager.md) script.

The basics functions of the lobby should already be functional, allowing you to start developing your game immediately using Netcode for GameObjects. However, you may need to adjust [certain settings](template-settings-and-concepts.md) to ensure full compatibility with your project.
