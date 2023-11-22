# Welcome to Power Supply Firmware repository

The code that runs on the power supply hardware is maintained in this repository.
## How do I develop this code?

Before starting, you need to install some tools. 

 1. Follow this [installation guide from modm](https://modm.io/guide/installation/) to install it and its dependencies. 
 2. Next, install [Visual Studio Code](https://code.visualstudio.com/) as IDE. It will allow you to build and debug the code without the need of a terminal.
 3. Inside Visual Studio Code, install the following plugins:
    1. C/C++ 
    2. C/C++ Extension Pack
    3. C/C++ Themes
    4. Cortex-Debug

## How to clone and initialize

Run the following commands to initialize the repository.

    $ git clone https://github.com/power-devices/power-supply-firmware.git
    $ cd power-supply-firmware
    $ git submodule update --init --recursive --jobs 8

Finally, instruct Visual Studio Code to open the **power-supply-firmware/src** folder. To build the code you needto press **Ctrl + Shift + B** and select one of the options.

## modm configuration

The [documentation](https://modm.io/reference/build-systems/) of modm states:

> The modm:build:scons build system generator is our preferred and
> recommended one

So, we are using scons. The automatic configuration files are almost fine. The Visual Studio Code required some tunning:

 1. gdb was unhappy because "openocd_gdbinit" doesn't exist: the solution is create a symbolic link to gdbinit_openocd
 2. debugger doesn't start: just remove the following line (twice) from **src/.vscode/launch.json**:

> "runToMain": true,

 3.  debugger still doesn't start: the openocd configuration in **src/.vscode/launch.json** is loading files in reverse order. Make it looks like:

            "configFiles": [
                "openocd.cfg",
                "modm/openocd.cfg",
            ],

 4.  compiling takes too long: edit the **src/.vscode/tasks.json** to look like:

            "command": "scons build profile=release -j$(nproc)",


## modm documentation

It is available [here](https://docs.modm.io/develop/api/blue-pill-f103/index.html).

