# qemu-aarch64
This simple tutorial helps get an ARMv8 emulated system up and
running on either RHEL 8 or OSX.

## Install QEMU
Clone this repository to your local host. You'll need to install
QEMU. Once installed, QEMU will place firmware files in
`/usr/local/share/qemu` with `.fd` extensions.

### Install QEMU on OSX
The easiest way to do this is to use [brew](https://brew.sh). Once
brew is enabled, type the following:

    brew install qemu

### Install QEMU on RHEL

On RHEL, you'll need to register and update the system. Edit
`setup-rhel8.sh` and set the `USERNAME` and `PASSWORD` to match
your [Red Hat Customer Portal](https://access.redhat.com) credentials.
Then,

    sudo ./setup-rhel8.sh

Next, you'll need to build QEMU as RHEL does not include the ability
to emulate aarch64 architectures OOTB. To download, build, and
install QEMU, do the following:

    ./build-qemu.sh

Provide your password for `sudo` when prompted.

## Installation
Adjust the various parameters in the `demo.conf` file. Obtain the
DVD ISO image for the operating system you'd like to install. This
defaults to RHEL 8.3 for aarch64 which can be downloaded from the
[Red Hat Customer Portal](https://access.redhat.com/downloads/content/419/ver=/rhel---8/8.3/aarch64/product-software).
Then,

    ./launch.sh

## Update the emulated system
Once the system starts you'll be prompted to go through the text
mode of the anaconda installer for RHEL. Make sure to configure the
various options including networking and a minimal install.

Immediately after installation, you can copy the `setup-rhel8.sh`
script to the emulated system to subscribe and pull updates from
Red Hat. From the host,

    scp -P 2222 setup-rhel8.sh rlucente@localhost:

Log on to the emulated system and edit `setup-rhel8.sh` and set the `USERNAME`
and `PASSWORD` to match your [Red Hat Customer Portal](https://access.redhat.com)
credentials. Then,

    ssh -p 2222 rlucente@localhost
    sudo ./setup-rhel8.sh

## Running
Once installed, the directory containing this repo will have several
`.img` files. To launch your system, simply run:

    ./launch.sh

