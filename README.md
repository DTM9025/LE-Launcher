Locale Emulator Launcher
========================

Launcher for Locale Emulator that is distributable and can be included in game packages.

By simply including `LELauncher.exe`, the configuration `le.config`, and the dlls `LoaderDll.dll` and `LocaleEmulator.dll`,
you can run any executable with the appropriate locale settings just like as you would with Locale Emulator. However,
this format makes it so you can package it with your game distributions or patches without needing to tell users to
install Locale Emulator (or manually switch locales). By simply editing `le.config` with the appropriate settings,
you can include those files and have the user just run it without needing to install Locale Emulator!

**NOTE:** The release binaries currently only work for 32-bit applications.

## Download

Download available at <https://github.com/DTM9025/LE-Launcher/releases>.

## Configuration

This launcher requires those four files to be located in the same directory. In addition, it requires `le.config` to
be properly configured to run the desired executable with the appropriate locale settings. An example `le.config` is
provided in this project and release. The fields that you should edit are in the `le.config` Profile and are as follows:

* `Parameter`: The relative path from the directory of `LELauncher.exe` to the target executable you want to run.
* `Location`: The locale you want to simulate. These are the same as the ones used in Locale Emulator. Common values include `ja-JP` and `zh-CN`. Available location codes can be found [here](https://learn.microsoft.com/en-us/openspecs/windows_protocols/ms-lcid/a9eac961-e77d-41a6-90a5-ce1a8b0cdb9c).
* `Timezone`: The timezone you want to simulate. These are the same as the ones in Locale Emulator. Examples are `Tokyo Standard Time` and `China Standard Time`.
* `RunAsAdmin`: Whether to run the target executable as Admin or not. Can be set `true` or `false`.
* `RedirectRegistry`: Whether to fake language-related keys in Registry. Can be set `true` or `false`. **Recommended to be true**.
* `IsAdvancedRedirection`: Whether to fake system UI language. Can be set `true` or `false`.
* `RunWithSuspend`: Whether to run the target executable with a suspended process. Can be set `true` or `false`. **Recommended to be false**.

Example configs for common profiles can be found in the `LEConfigs` folder.

## Requirements

This program requires the `.NET Framework 4.8 Runtime` to be installed. This should be included by default in updated Windows 10/11.
If this is not the case, then you can download the runtime (or tell users to download the runtime) from [here](https://dotnet.microsoft.com/en-us/download/dotnet-framework/net48).

Due to this, this program only works for Windows 7 and up. In addition, the release binaries only work for 32bit executables.

However, the code here should still compile in earlier versions up to `.NET Framework 4.0`. That version is end-of-life,
but if needed you can simply edit the project to use `.NET Framework 4.0` as in the original Locale Emulator program.

## Example Usage

Let's say you have a 32-bit game that you are translating. However, for some weird reason it doesn't work unless you are in
a Japanese locale, even after editing all file names, etc. (maybe text doesn't showup or it just refuses to run). You
can include this launcher in your patch and tell users to run `LELauncher.exe` to run the translated patched game, allowing
you to run the game with the Japanese locale.

For starters, let's say the directory structure of the patched game zip will be this:

```
<Translated Game Folder To Be Zipped>
├── resources
│   ├── blah
│   └── blah
|── assets
|   └── blah
|        └── blah.png
└── game.exe
```

Before you zip this up, you add `LELauncher.exe`, `le.config`, `LoaderDll.dll`, and `LocaleEmulator.dll` into the root folder
alongside `game.exe`.

To ensure it runs in the Japanese locale, you edit `le.config` and make the `Location` value to be `ja-JP` and make the
`Timezone` value to be `Tokyo Standard Time`. To ensure `LELauncher.exe` launches the game you also make the `Parameter` value
to be `game.exe`, as that is the relative path to that executable from `LELauncher.exe`'s directory. You set the other parameters
as appropriate.

If you want, you can also rename `LELauncher.exe` to whatever is best for you (like `game-en.exe` or something) to make it
more clear to users that they should run that executable to run the translated game. In addition, you could also change
the icon with external tools like Resource Hacker (instructions can be found [here](https://www.wikihow.com/Change-the-Icon-for-an-Exe-File#Editing-the-EXE-in-Resource-Hacker)).

Now you can just zip that up with the included laucnher in your patch distrubation, and tell users to run `LELauncher.exe`
(or whatever you renamed it to) to run the translated patched game and it will run in the Japanese locale! All without
needing to tell the user to install Locale Emulator or switch locales in Windows!

## Build

 1. Clone the repo using Git.
 2. Install Microsoft Visual Studio 2022. Make sure you have `.NET desktop development` checked.
 3. Open `LocaleEmulator.sln`.
 4. Perform Build action.
 5. Clone and build the core libraries: https://github.com/xupefei/Locale-Emulator-Core
 6. Copy LoaderDll.dll and LocaleEmulator.dll from Locale-Emulator-Core to Locale-Emulator build folder.
 7. Create a `le.config` file as appropriate and place into the build folder. (See `LEConfigs` folder for examples).

## License

![LGPL](https://www.gnu.org/graphics/lgplv3-147x51.png)

This program is free software; you can redistribute it and/or modify
it under the terms of the GNU Lesser General Public License as published by
the Free Software Foundation; either version 3 of the License, or
(at your option) any later version.

This library is distributed in the hope that it will be useful,
but WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
GNU Lesser General Public License for more details.

You should have received a copy of the GNU Lesser General Public License
along with this program.  If not, see <http://www.gnu.org/licenses/>

## Credit

This project is forked from [Locale Emulator](https://github.com/xupefei/Locale-Emulator) by [xupefei](https://github.com/xupefei/).
