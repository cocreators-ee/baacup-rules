# Game rules for Baacup

Baacup monitors the savegame folders for your games for changes, and creates backups of your
savegames. This repository contains rules for different games Baacup supports.

Check out Baacup at [cocreators-ee/baacup](https://github.com/cocreators-ee/baacup).

## Rule files path

The data files for Baacup will be stored under the appropriate `BASE_PATH` depending on the
platform:

- For \*nix: `$HOME/Baacup`
- For Windows: `My Documents\Baacup`

The Rules belong in the `rules` subdirectory below that.

- For \*nix: `$HOME/Baacup/rules`
- For Windows: `My Documents\Baacup\rules`

### Rules

Stored in `{BASE_PATH}/rules/{game}-{variant}.yaml`, e.g. `Baldurs Gate 2 - Steam.yaml`.

Contains the following:

```yaml
name: Baldur's Gate 2
issues: Optional explanation of any issues with these rules.
platforms:
  windows:
    executable: "*\\bg2.exe"
    savegames:
      - "${LOCALAPPDATA}\\SomePublisher\\BG2\\quicksave.sav"
      - "${LOCALAPPDATA}\\SomePublisher\\BG2\\autosave.sav"
      - "${LOCALAPPDATA}\\SomePublisher\\BG2\\saves\\*.sav"
  linux:
    executable: "*/bg2.bin"
    savegames:
      - "${HOME}/.local/savegames/BG2/*.sav"
  macos:
    executable: "*/bin/bg2"
    savegames:
      - "${HOME}/Save Games/Baldur's Gate 2/*.macsav"
```

## Using these rules

If you want to manually use the contents of this repository, you can
[download the contents](https://github.com/cocreators-ee/baacup-rules/archive/refs/heads/main.zip)
and then copy the contents of the `rules` folder in the archive to the "rule files path" as
explained above.

## Contributing

See [CONTRIBUTING.md](./CONTRIBUTING.md) for general guidelines.

In the configuration files you can refer to various locations using
[environment variables](https://www.howtogeek.com/787217/how-to-edit-environment-variables-on-windows-10-or-11/),
and you should generally do so whenever possible.

E.g. on Windows you will find that savegames often are under your user account's profile, meaning
the username is a part of the path, and changes for every user of Baacup. We want the rules to work
for _everyone_, so we need to use environment variables to determine the correct path instead.

When referring to environment variables, you should use the syntax `${NAME}` on ALL PLATFORMS.
Common environment variables you would use are then as follows:

- Windows:
  - `${APPDATA}` - `C:\Users\username\AppData\Roaming`
  - `${LOCALAPPDATA}` - `C:\Users\username\AppData\Local`
  - `${ProgramData}` - `C:\ProgramData`
  - `${ProgramFiles}` - `C:\Program Files`
  - `${ProgramFiles(x86)}` - `C:\Program Files (x86)`
  - `${USERPROFILE}` - `C:\Users\username`
  - `${MyDocuments}` - Added by Baacup at runtime, normally `C:\Users\username\My Documents`, but
    determined via Windows "known folder" system so if it is moved, it should still work
- \*nix based systems:
  - `${HOME}` - The home folder of your user account. E.g. `/home/username/` or `/Users/username/`

For the rules to detect the game executable you can use wildcards at the start fairly freely, but it
is preferred if you would try to be as exact as possible - so e.g. if the game is normally installed
on `C:\Program Files (x86)\Steam\steamapps\common\Game` and then has under that
`bin\Windows\Game.exe`, you should use `*\\bin\\Windows\\Game.exe` so it will not be confused with
other `Game.exe` files in the system as easily.

## License

The code is released under the GPL v3 license. Details in the [LICENSE.md](./LICENSE.md) file.

# Financial support

This project has been made possible thanks to [Cocreators](https://cocreators.ee) and
[Lietu](https://lietu.net). You can help us continue our open source work by supporting us on
[Buy me a coffee](https://www.buymeacoffee.com/cocreators).

[!["Buy Me A Coffee"](https://www.buymeacoffee.com/assets/img/custom_images/orange_img.png)](https://www.buymeacoffee.com/cocreators)
