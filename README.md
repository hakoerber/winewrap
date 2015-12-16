# winewrap
Script to handle multiple wine prefixes for games.

It expects a specific directory structure which each folder containing a
`prefix` directory and an `info` file.

```
wine
├── game1
│   ├── prefix
│   │   ├── dosdevices
│   │   └── drive_c
│   └── info
├── game2
│   ├── prefix
│   │   ├── dosdevices
│   │   └── drive_c
│   └── info
├── ...
```

## Usage

```
winetricks <action> <game>
```

### Actions

Action | Description
--- | ---
`start` | Start the specified game
`setup` | Sets up a new clean wineprefix and installs requirements
`getenv` | Prints the necessary environment variables to stdout

### Expected environment variables

`WINEPATH`: Must point to the folder containing the games. Would be `wine` in the above directory tree.

## Info file

The `info` file is a simple bash file that contains variables that describe
certain aspects of the game and is sourced by winewrap. Refer to `info.sample`
for an example. The required variables are the following:

Variable | Description
--- | ---
`_ARCH` | The architecture to use for the wineprefix, either `win32` or `win64`. Refer to `WINEARCH` in `wine(1)`
`_DLL_OVERRIDES` | A list of DLL overrides. Refer to `WINEDLLOVERRIDES` in `wine(1)`
`_EXE` | The path to the `.exe` to run when starting the game, relative to the wineprefix. Usually starts with `drive_c` which maps to `C:\`
`_WINEOPTIONS` | Options to directly pass to wine
`_REQUIREMENTS` | Array of required components that will be installed via `winetricks(1)`
