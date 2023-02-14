# PlayFab Party SDK for Unity

## Overview
This is a PlayFab Party plugin for game development on Unity.

_(Please use Git client with Large File Storage (LFS) support to work with this repo)_

## Supported platforms:
- Windows
- Microsoft Game Core (just "Game Core" below)
- Linux
- iOS
- Android
- macOS

## Version
|Party Unity SDK (main)
|-|
|1.7.6.0-main.0

Officially supported versions of PlayFab Party binaries with this release, by platform:

Platform|Version|Notes
|-|-|-|
Windows|1.7.11
Game Core|1.7.* (distributed with Microsoft GDK)|Compatible with GDK 2021.04 or later
Linux|1.7.14 Tested with Ubuntu 20.04 and 22.04
iOS|1.7.6
Android|1.7.6
macOS|1.7.16

## Prerequisites
- PlayFab account ([www.playfab.com](https://www.playfab.com)) registered and set up:
    - Studio and App configured, TitleID exists
    - Party feature enabled
    - Highly recommended: PlayFab Unity test app tried to ensure seamless PlayFab integration
- PlayFab Unity Editor Extensions plugin (recommended)
- PlayFab (Core) SDK (installed via PlayFab Unity Editor extensions)
- If you are targeting iOS:
    - Unity iOS Build Support Add-on installed
- If you are targeting Android:
    - Unity Android Build Support Add-on installed with additional components:
        - Android SDK and NDK tools
        - OpenJDK
- If you are targeting Windows:
    - Unity Windows Build Support (IL2CPP) Add-on installed
- If you are targeting Game Core platform (consoles and/or PC):
    - Have access to the [Microsoft Game Development Kit (GDK)](http://aka.ms/gdkdl)
    - GDK installed (with all optional components)
    - Party on Game Core platform requires Xbox Live authentication, and therefore make sure that:
        - Your Xbox app title is registered in Xbox Partner Center
        - Necessary SandboxID and developer Xbox Live account are created, and configured to work with the registered Xbox app title
    - If you are targeting Game Core on Xbox consoles:
        - Unity Game Core Add-on for a necessary console installed (download from Unity)
        - Unity Game Core Package compatible with this version of GDK installed (download from Unity, then install using Package Manager in Unity Editor)
    - If you are targeting Game Core PC:
        - [GDK Unity plugin package](https://github.com/microsoft/gdk-unity-package) for this version of GDK installed

## What's inside
The SDK contains the following:
- `/PlayFabPartySDK` – This folder contains APIs that you will call from your game to take advantage of networking, in-game chat and other functionality offered by PlayFab Party.
- `/PlayFabPartySDK/Examples` – This folder contains a simple demo scene with a script that shows how to call the Party APIs.
- `/PlayFabPartySDK/Prefabs` – This folder contains the PlayFabMultiplayerManager prefab.
- `/PlayFabPartySDK/Setup/GameCore` – This folder contains set up scripts that need to be used once to prepare the SDK to build for Game Core.
- `/PlayFabPartySDK/Source/DLLs` – This folder contains the underlying Party C++ library binaries for each supported platform.

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
- If you are targeting Game Core on:
    - Xbox consoles:
        - Add macro definition (Scripting Define Symbol) `UNITY_GAMECORE` in Project Settings
    - PC:
        - Add macro definition (Scripting Define Symbol) `MICROSOFT_GAME_CORE` in Project Settings
        - To build for Game Core on PC use top menu command in Unity Editor: GDK > PC > Build and Run
    - Note that these macros should not be set at the same time, they are mutually exclusive.
- Create a new, empty scene
- Import PlayFab Party Unity SDK plugin (unity package)
- If you are targeting Game Core: 
    - Go to `/Assets/PlayFabPartySDK/Setup/GameCore` folder in File Explorer and run `install-party-game-core-libs.ps1` script, it will copy Party binaries installed with GDK to `PlayFabPartySDK` assets
- Go to the `/Assets/PlayFabPartySDK/Prefabs` folder and drag and drop the `PlayFabMultiplayerManager` prefab into your scene
- Note: Party SDK is x64, so when you build Standalone (Windows) please build for x64.
- If you are targeting iOS:
    - Enable 'Prepare iOS for Recording' (set checkbox) in iOS Player Settings
    - Two PlayFabParty.framework libraries are provided: one for real iOS devices and another one for iOS Simulator (x64). Make sure to enable only one of them for iOS platform before building. The framework for a device is enabled by default (see Inspector settings for PlayFabParty.framework folders)
- If you are targeting Android: please make sure to allow your app to use microphone on the device.

For a detailed guide please check out [Quickstart: PlayFab Party Unity Plugin](https://docs.microsoft.com/en-us/gaming/playfab/features/multiplayer/networking/party-unity-plugin-quickstart)

## Error Handling
The error callbacks used in `PlayFabMultiplayerManager` API may return error data which includes `PlayFabMultiplayerManagerErrorType`. It can be used to determine a type of the error that the user app may act on.

In addition to error types, there are also specific Party error codes. They are intended for diagnostics and logging, not for programmatic error handling.

### Error Codes
The underlying Party C++ library may return error codes that Party Unity plugin will pass on to the user app. All possible Party error codes and their descriptions are listed in `PartyErrors.md` file which is distributed with a public Party C++ library NuGet package, e.g.:
https://www.nuget.org/packages/Microsoft.PlayFab.PlayFabParty.Cpp.Windows/

It is located at the root of the NuGet package content.

## Logging
The underlying Party C++ library includes logging capabilities with a configurable verbosity level. Logging configuration is defined in `PlayFabPartyLogger.json` file which can be deployed as an asset along with the application. An example of configuration file:

```json
{
    "enabled": false,
    "bufferSize": 16384,
    "maxNumberOfItemsInBatch": 100,
    "maxBatchWaitTimeInSeconds": 1,
    "readBufferWaitTimeInMilliseconds": 1,
    "logFolder": "/platform-specific-path/",
    "logLevel": "VERBOSE",
    "xrnLogEnabled": false,
    "maxLogFileSizeInMegabytes": 0
}
```

When this file is detected by the application in runtime it will use it to enable logging as configured. The following verbosity levels are currently supported:
1. `VERBOSE` - everything
2. `INFO` - less than everything, only important messages and errors
3. `ERROR` - only errors

The logging is disabled by default, but can be enabled with "enabled" property set to `true`.

Instructions to enable logging for specific platform.
Platform|Where to put PlayFabPartyLogger.json (permission needed)|`logFolder` value|How to view logs
|-|-|-|-|
iOS|Inside the application folder (Set UIFileSharingEnabled to true in the Info.plist of the app)|/app_sandbox_storage/Documents/|Copy logs from `logFolder` to PC
Android|Create a folder "\sdcard\PlayFabParty\config" (External storage folder requires READ_EXTERNAL_STORAGE permission)|/sdcard/PlayFabParty/log/|Copy logs from `logFolder` to PC and open in NotePad++
macOS|~/Documents (Set UIFileSharingEnabled to true in the Info.plist of the app)|~/Documents|Open logs directly in `logFolder`

## Troubleshooting
###Expired Tokens:
PlayFab party unity plugin uses the entity token of the logged-in user to access PlayFab services such as creating a network, speech-to-text and text-to-speech.
However this Entity token has a finite expiration time typically 24 hrs after which the Party Unity plugin might experience issues accessing these services.

One symptom of the expired token is that the player is unable to create a new party network.

The game is responsible for monitoring the expiration of the entity token and provide an updated token to the Party Unity plugin using the following API available in PlayFabMultiplayerManager:
```json
public void UpdateEntityToken(string entityToken)
```
