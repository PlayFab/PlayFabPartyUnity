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





