# jail

Simple script that wraps the `bwrap` binary to isolate your $HOME directory.

## What

`bwrap` is the namespace system that powers things like flatpak. It is powerful,
and can be used to namespace arbitrary programs that do NOT have flatpaks.

The ONLY GOAL of this project is to isolate your EXISTING USER HOME DIRECTORY
from the running program - the program will see a UNIQUE HOME DIRECTORY
that does not contain your potentially personal or sensitive data.

Things like audio/themes/icons/graphics will hopefully "just work"

This is the primary goal of the project. IS IT NOT A SECURITY SOLUTION.

## How

### jail

See the `--help` for more details, but essentially

```sh
$ jail     --name my-jail    --   bash    --bind "${HOME}/hello" "${HOME}/world"  --        -c  ls
# jail  <-- jail options --> -- <command> <---------- bwrap options ----------->  -- <-- command options -->
```

#### Option and Parameter Format

The format of the arguments is specific and important:
First arguments are "jail options"
Then a '--'. This is REQUIRED in ALL CASES, even with no "jail options"
Then the COMMAND you wish to run. This is REQUIRED in ALL CASES and MUST come after the first '--'
Anything that follows will now be options passed directly to `bwrap`
Then if another '--' is found, `bwrap` option processing will stop
Any further options are passed to the COMMAND

All `bwrap` options and COMMAND options are supported.
It is up to you to craft jails specific to your COMMAND

#### Configuration

By default your jail directory will live in `${HOME}/.local/etc/jails/<COMMAND>`
though you can change this directory name from `<COMMAND>` to something else via the `--name` "jail option"

#### Shortcuts

Shortcut options exist to do things like

- Launch a bash shell in a jailed environment
- Bind the host X11 environment to the jail for X11 graphical programs
- Bind the host Wayland environment to the jail for Wayland graphical programs

### listjails

`listjails` is a simple script that when called will list out all currently running jails

```sh
[<user>] <PID> <COMMAND> (<NAME>)
```

For example

```sh
[pyamsoft] 1267458 /bin/bash (my-jail-bash)
```

## Issues

Check the issues page on GitHub for any notes about outstanding or existing
issues. If you encounter a problem with `jail` of which no such
issue already exists please feel free to help the developer by creating an
issue ticket.

## License

GPLv2

```
  The GPLv2 License

    Copyright (C) 2025 pyamsoft

    This program is free software; you can redistribute it and/or modify
    it under the terms of the GNU General Public License as published by
    the Free Software Foundation; either version 2 of the License, or
    (at your option) any later version.

    This program is distributed in the hope that it will be useful,
    but WITHOUT ANY WARRANTY; without even the implied warranty of
    MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
    GNU General Public License for more details.

    You should have received a copy of the GNU General Public License along
    with this program; if not, write to the Free Software Foundation, Inc.,
    51 Franklin Street, Fifth Floor, Boston, MA 02110-1301 USA.
```
