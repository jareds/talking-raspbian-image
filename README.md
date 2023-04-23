currently it is impossible to boot the default Raspbian image to a desktop and enable speech using Orca with out a HDMI device hooked up. This is a packer build that fixes this by taking the default 64 bit Raspbian distribution, adding a headless x display driver, and loading a xorg.conf to enable the headless driver. The instructions I based this off can be found at
https://techesoterica.com/future-ready-vision-with-the-voice-and-the-raspberry-pi-4b/
This image ahs been tested on a Pi 4. It will likely work on a Pi 400 but I have not tested. It will not work on any Pi models that do not support a 64 bit OS.
The easiest way to build an image is to use Docker installed on either Linux or WSL2 on Windows. You can create a .img file with the following command and burn it to an SD card.

```docker run --rm --privileged -v /dev:/dev -v ${PWD}:/build mkaczanowski/packer-builder-arm build raspbian.json```

Once the card is burned plug it into your pi, attach a keyboard and headphones, power on your pi, and wait up to ten minutes for the prompt to install Orca.
It should be possible to build the image with out Docker if you have Packer and the required Packer-Arm plugin installed. This appeared to be a non-trivial amount of work though so I stuck with Docker.