# Jetson setup through a VM without a GUI

## Requirements

- [Vagrant](vagrantup.com)
- An NVidia developer account to download the SDK and firmware

## Instructions

1. Download the SDK manager from [NVidia](https://developer.nvidia.com/embedded/jetpack) and
put the deb package in the root directory of this repo.

2. Setup the VM using

        vagrant up

3. SSH into the VM and launch the SDK manager through xvfb with

        vagrant ssh
        xvfb-run sdkmanager --cli install --query --user NVIDIA_USERNAME

   Or, using the response file after having set your credentials in the [sdkm_responsefile.ini](./sdkm_responsefile.ini):

        xvfb-run sdkmanager --cli install --responsefile /vagrant/sdkm_responsefile.ini

   The process will ask you to put the Jetson in Recovery mode before flashing
   the firmware.

   Alternatively, to only download the firmware and install the dependencies
   without flashing the board, run one can use:

        vagrant provision --provision-with install

4. To only (re)flash the Jetson after having downloaded the necessary doodah:

        cd ~/nvidia/nvidia_sdk/JetPack_4.3_Linux_P3310/Linux_for_Tegra
        sudo ./flash.sh 'jetson-tx2' mmcblk0p1

   Check out the [documentation for the flash.sh script](https://docs.nvidia.com/jetson/l4t/index.html#page/Tegra%2520Linux%2520Driver%2520Package%2520Development%2520Guide%2Fflashing.html%23wwpID0E0QJ0HA) for further details.
