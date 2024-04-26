# dc-cmake-example

Small example of a project using cmake for dreamcast
- For now the content of the example is copied from a cpp example provided in the kallistiOS repo (https://github.com/KallistiOS/KallistiOS)
- The goal of this example is to illustrate using cmake for dreamcast programming.
- When building the app1, a cdi image of is created

# Prerequisites

1. KOS toolchains: https://github.com/KallistiOS/KallistiOS 
2. Kos-ports: https://github.com/KallistiOS/kos-ports
3. mkdcdisc: https://gitlab.com/simulant/mkdcdisc
    - Note that it is expected to be placed at /opt/mkdcdisc
    - Used to build the cdi image
4. A `bin/` directory is expected at the root of the project

# Launch the emulator

After the build, a cdi image is created in the `bin/` directory. for use with emulators.

### Flycast 
You can install flycast via flatpak ( See https://github.com/flathub/org.flycast.Flycast)
And then run it.
```
flatpak run org.flycast.Flycast ${workspaceFolder}/bin/app1.cdi
```