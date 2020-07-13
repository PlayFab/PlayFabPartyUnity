# PlayFab Party SDK for Unity

## Overview
This is a PlayFab Party plugin for game development on Unity.

## Supported platforms:
- Microsoft Game Core (just "Game Core" below)

## Version
|Party Unity SDK (main)
|-|
|1.4.7.0-main.0

Officially supported versions of PlayFab Party binaries with this release, by platform:

Platform|Version
|-|-|
Game Core|1.4.7

## Prerequisites
- PlayFab account ([www.playfab.com](https://www.playfab.com)) registered and set up:
    - Studio and App configured, TitleID exists
    - Party feature enabled
    - Highly recommended: PlayFab Unity test app tried to ensure seamless PlayFab integration
- PlayFab Unity Editor Extensions plugin
- PlayFab (Core) SDK (installed via PlayFab Unity Editor extensions)
- If you are targeting Game Core platform (Xbox One, Scarlett and/or PC):
    - Have access to the [Microsoft Game Development Kit (GDK)](http://aka.ms/gdkdl)
    - GDK installed (with all optional components)
    - GDK Unity plugin installed (available in Add-ins download section on GDK portal)
    - If you are targeting Game Core Xbox or Game Core Scarlett:
        - Unity Game Core Scarlett Add-on installed (download from Unity)
        - Unity Game Core Xbox One Add-on installed (download from Unity)
        - Party on Xbox consoles requires Xbox Live authentication, and therefore make sure that:
            - Your Xbox app title is registered in Xbox Partner Center
            - Necessary SandboxID and developer Xbox Live account are created, and configured to work with the registered Xbox app title
    - If you are targeting Game Core PC:
        - Party Unity SDK is "Game Core PC ready", as soon as Unity build tools for Game Core PC are available

## What's inside
The SDK contains the following:
- `/PlayFabPartySDK` – This folder contains APIs that you will call from your game to take advantage of networking, in-game chat and other functionality offered by PlayFab Party.
- `/PlayFabPartySDK/Examples` – This folder contains a simple demo scene with a script that shows how to call the Party APIs.
- `/PlayFabPartySDK/Prefabs` – This folder contains the PlayFabMultiplayerManager prefab.
- `/PlayFanPartySDK/Setup/GameCore` – This folder contains set up scripts that need to be used once to prepare the SDK to build for Game Core.

## Getting Started
### Setting up your environment
- Create a new Unity project
- Open player settings from the Unity main menu: Edit > Project Settings...
- Next, select the 'Player' tab
- Scroll down and check the box: Allow 'unsafe' Code
- Close the Project Settings window
- Link your Unity project with PlayFab by installing the editor extensions: https://github.com/PlayFab/UnityEditorExtensions/releases
- Import this plugin
- Install latest version of PlayFabSDK plugin using PlayFab Unity Editor Extensions UI
- Log in to your PlayFab title using PlayFab Unity Editor Extensions UI
- Follow [README guidelines from PlayFabSDK](https://github.com/PlayFab/UnitySDK) to test basic PlayFab functionality
- If you are targeting Game Core:
    - Install GDK Unity plugin
    - If you are targeting Game Core Xbox One or Game Core Scarlett:
        - In Unity Project tree navigate to `Assets/XGamingRuntime` folder and enable "GameCoreScarlett" and "GameCoreXboxOne" platforms in Inspector panel for `XGamingRuntime.dll` and `XGamingRuntimeThunks.dll` files
- Create a new, empty scene
- Import PlayFab Party Unity SDK plugin (unity package)
- If you are targeting Game Core: 
    - Go to `/Assets/PlayFabPartySDK/Setup/GameCore` folder in File Explorer and run `install-party-game-core-libs.ps1` script, it will copy Party binaries installed with GDK to `PlayFabPartySDK` assets
- Go to the `/Assets/PlayFabPartySDK/Prefabs` folder and drag and drop the `PlayFabMultiplayerManager` prefab into your scene
- Note: Party SDK is x64, so when you build Standalone please build for x64.

For a detailed guide please check out [Quickstart: PlayFab Party Unity Plugin](https://docs.microsoft.com/en-us/gaming/playfab/features/multiplayer/networking/party-unity-plugin-quickstart)