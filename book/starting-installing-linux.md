# Development Environment on Linux

We have standardized on Debian / Ubuntu LTS as the supported Linux distribution, but [boutique distribution instructions](starting-installing-linux-boutique.md) are available for Cent OS and Arch Linux.

## Permission Setup

<aside class="note">
Never ever fix permission problems by using 'sudo'. It will create more permission problems in the process and require a system reinstallation to fix them.
</aside>

The user needs to be added to the group "dialout":

<div class="host-code"></div>

```sh
sudo usermod -a -G dialout $USER
```

And then you have to logout and login again, as this is only changed after a new login.

## Installation

Update the package list and install the following dependencies for all PX4 build targets. PX4 supports four main families:

  * NuttX based hardware: [Pixhawk](hardware-pixhawk.md), [Pixfalcon](hardware-pixfalcon.md)
  * Snapdragon Flight hardware: [Snapdragon](hardware-snapdragon.md)
  * Raspberry Pi hardware: [Raspberry Pi 2](hardware-pi2.md)
  * Host simulation: [jMAVSim SITL](simulation-sitl.md) and [Gazebo SITL](simulation-gazebo.md)

<aside class="note">
Install the [Ninja Build System](http://dev.px4.io/starting-installing-linux-boutique.html#ninja-build-system) for faster build times than with Make. It will be automatically selected if installed.
</aside>

<div class="host-code"></div>

```sh
sudo add-apt-repository ppa:george-edison55/cmake-3.x -y
sudo apt-get update
sudo apt-get install python-argparse git-core wget zip \
    python-empy qtcreator cmake build-essential genromfs -y
# simulation tools
sudo apt-get install ant protobuf-compiler libeigen3-dev libopencv-dev openjdk-7-jdk openjdk-7-jre clang-3.5 lldb-3.5 -y
```

### NuttX based hardware

Ubuntu comes with a serial modem manager which interferes heavily with any robotics related use of a serial port (or USB serial). It can deinstalled without side effects:

<div class="host-code"></div>

```sh
sudo apt-get remove modemmanager
```

Update the package list and install the following dependencies. Packages with specified versions should be installed with this particular package version.

<div class="host-code"></div>

```sh
sudo add-apt-repository ppa:terry.guo/gcc-arm-embedded -y
sudo apt-get update
sudo apt-get install python-serial openocd \
    flex bison libncurses5-dev autoconf texinfo build-essential \
    libftdi-dev libtool zlib1g-dev \
    python-empy gcc-arm-none-eabi -y
```

If the resulting `gcc-arm-none-eabi` version produces build errors for PX4/Firmware master, please refer to [the bare metal installation instructions](http://dev.px4.io/starting-installing-linux-boutique.html#Toolchain Installation) to install version 4.8 manually.

### Snapdragon Flight

Developers working on Snapdragon Flight should request the Hexagon 7.2.10 Linux toolchain and 2.0 SDK for Linux from [here](https://developer.qualcomm.com/software/hexagon-dsp-sdk/application) and execute the commands below. The installation guide will come up, leave everything at default by just continuing to press enter.

Arm cross toolchain:

<div class="host-code"></div>

```sh
sudo apt-get install gcc-arm-linux-gnueabihf g++-arm-linux-gnueabihf -y
```

Hexagon SDK:

<div class="host-code"></div>

```sh
chmod u+x qualcomm_hexagon_sdk_2_0_eval.bin
./qualcomm_hexagon_sdk_2_0_eval.bin
```
### Raspberry Pi hardware
Developers working on Raspberry Pi hardware should download the RPi Linux toolchain from below. The installation script will automatically install the cross-compiler toolchain. If you are looking for the *native Raspberry Pi toolchain* to compile directly on the Pi, see [here](hardware-pi2.md)

<div class="host-code"></div>

```sh
git clone https://github.com/pixhawk/rpi2_toolchain.git
cd rpi2_toolchain
./install_cross <install location> #Leave blank for default install to /opt/rpi_toolchain
```

### Snapdragon Flight

Developers working on Snapdragon Flight should download the Hexagon Linux toolchain and execute the commands below. The installation guide will come up, leave everything at default by just continuing to press enter.

Hexagon Tools:
<div class="host-code"></div>

```sh
tar xf Hexagon.LNX.7.2\ Installer-07210.1.tar
chmod u+x Hexagon.LLVM_linux_installer_7.2.10.bin
./Hexagon.LLVM_linux_installer_7.2.10.bin
```

After this the tools and SDK will have been installed to "$HOME/Qualcomm/...". Append the following to your ~/.bashrc:

<div class="host-code"></div>

```sh
export HEXAGON_TOOLS_ROOT="$HOME/Qualcomm/HEXAGON_Tools/7.2.10/Tools"
export HEXAGON_SDK_ROOT="$HOME/Qualcomm/Hexagon_SDK/2.0"
if [[ ":$PATH:" != *":$HEXAGON_TOOLS_ROOT/bin/:"* ]]; then PATH="$PATH:$HEXAGON_TOOLS_ROOT/bin"; fi
```

Load the new configuration:

<div class="host-code"></div>

```sh
source ~/.bashrc
```

There is a an external guide for installing the toolchain at 
[GettingStarted](https://github.com/ATLFlight/ATLFlightDocs/blob/master/GettingStarted.md). The 
[HelloWorld](https://github.com/ATLFlight/HelloWorld) and [DSPAL tests](https://github.com/ATLFlight/dspal/tree/master/test/dspal_tester) can be used to validate your tools installation and DSP image.

Messages from the DSP can be viewed using mini-dm.

<div class="host-code"></div>

```sh
$HOME/Qualcomm/Hexagon_SDK/2.0/tools/mini-dm/Linux_Debug/mini-dm
```

Now continue to run the [first build](starting-building.md)!
