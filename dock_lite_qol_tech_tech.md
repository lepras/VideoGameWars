this is the descriptin of the video, for safe keeping.

[DOCK Nintendo Switch Lite on TV with Raspberry Pi (2021 HOW TO) SysDVR
](https://www.youtube.com/watch?v=mJ4-HXS2H74)
---

Finally, a Switch Lite Dock solution! Play your Nintendo Switch Lite on TV, with Raspberry Pi 4 and SysDVR. I'll show you how to use SysDVR on Raspberry Pi, in 4 hopefully simple steps.

Can Switch Lite connect to TV? As a Switch Lite owner, the ability to dock to TV would be nice. With the Raspberry Pi Switch Lite Dock, yes you can. 

Chapters:
0:00 Intro
0:30 Can you connect a Switch Lite to TV?
0:56 Features of Raspberry Pi Switch Lite Dock
1:46 How to install SysDVR on Raspberry Pi 4
3:59 Limitations of Raspberry Pi Switch Lite Dock
5:22 Nintendo Switch vs. Switch Lite vs. Switch Pro?

Get the same Nintendo Switch Lite Dock for charging and USB: https://amzn.to/34Qfyy0
Control your Nintendo Switch using a Dualshock or Xbox controller: https://amzn.to/3gbVhIu
Get started with Raspberry Pi 4 FULL Starter Kit: https://amzn.to/3g5PRPr
DIY Raspberry Pi 4 Board: https://amzn.to/3fReGjj
Check out this NEW 8bitdo gaming controller!: https://amzn.to/34LLNyt
Get the NEW Nintendo Switch Lite!: https://amzn.to/3z1gH40

Step 1: Flash Gentoo64 Lite Image to an SD card
Download Gentoo64 Lite from their Github
(https://github.com/sakaki-/gentoo-on-...)
You can use the Raspberry Pi Imager to flash
(https://www.raspberrypi.org/software/)
Once you have Gentoo64 up and running, type "nmtui" into the command line prompt to setup wifi.

The next steps will have a lot of command line inputs if you're new to Pi projects or Linux. I suggest you access the Pi through SSH using an SSH client such as (https://mobaxterm.mobatek.net/)

Step 2: Compile and Install SDL2 on Pi
(https://github.com/midwan/amiberry/wi...)
You can follow the instructions above if you know your way around Linux, else you can copy paste the lines below in your SSH session

wget https://www.libsdl.org/release/SDL2-2... &&
wget https://www.libsdl.org/projects/SDL_t... &&
wget https://www.libsdl.org/projects/SDL_i... &&
mkdir -p $HOME/sdl2_sources && tar xvf SDL2-2.0.14.tar.gz -C $HOME/sdl2_sources && tar xvf SDL2_ttf-2.0.15.tar.gz -C $HOME/sdl2_sources && tar xvf SDL2_image-2.0.5.tar.gz -C $HOME/sdl2_sources && sudo emerge -C media-libs/libsdl2

the line below will take a while, have a coffee break while it's compiling and installing
cd $HOME/sdl2_sources/SDL2-2.0.14 &&
./configure --enable-video-kmsdrm --disable-video-rpi &&
make -j4 && sudo make install &&
cd $HOME/sdl2_sources/SDL2_image-2.0.5 &&
./configure && make -j4 && sudo make install &&
cd $HOME/sdl2_sources/SDL2_ttf-2.0.15 &&
./configure && make -j4 && sudo make install

use line below in each session before launching SysDVR, or include in a bash script
export LD_LIBRARY_PATH="/usr/local/lib" 

Step 3: Install .NET 5.0 on Pi
(https://dotnet.microsoft.com/download...)

wget https://download.visualstudio.microso... && 
mkdir -p $HOME/dotnet && tar zxf dotnet-sdk-5.0.202-linux-arm64.tar.gz -C $HOME/dotnet && 
export DOTNET_ROOT=$HOME/dotnet && 
export PATH=$PATH:$HOME/dotnet && 
sudo ln -s /home/demouser/dotnet/dotnet /usr/bin/dotnet

Step 4: Extract SysDVR to Pi and Switch
(https://github.com/exelix11/SysDVR)
Follow the instructions on their github to extract and install.
