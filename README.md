lightHost installation guide
=====================
Guide on installing `lightHost.exe` on linux with `wine` and `winetricks`.

Dependencies
------------------
### Wine
This installation guide was tested on `wine-6.13` from `winehq-devel` package.

[Install wine](https://wiki.winehq.org/Download)

### Winetricks
This installation guide was tested on `winetricks 20210206-next` 
from [github repository](https://github.com/Winetricks/winetricks).

[Install winetricks](https://github.com/Winetricks/winetricks#installing)

### LightHost
Download latest lightHost release for `win64` 
from [github](https://github.com/rolandoislas/LightHost/releases) and 
extract `Light Host.exe` to whatever directory you want.

### PulseAudio and Pactl
To create virtual audio in/out i use `pactl` command 
if your system does not use [PulseAudio](https://www.freedesktop.org/wiki/Software/PulseAudio/) 
install it or edit `lightHost` file: comment `pactl` lines with `#`.

Installation
--------------
1. Install dependencies listed above.
2. Create new `wineprefix` and setup it for lightHost:
```bash
# This will create new wineprefix in "$HOME/.local/share/wineprefixes/lighthost"
# and install needed by lightHost and most VST3 plugins components to it.
winetricks prefix=lighthost d3dcompiler_43 d3dx9 d9vk dotnet40 gdiplus mfc42 arial tahoma dxvk
```
3. _Only if you are using WAYLAND or lightHost does not appear in taskbar:_
```bash
# Run this command and in opened window check Graphics -> Emulate a virtual desktop
winetricks prefix=lighthost winecfg
```
4. Download `lightHost` file from this repository and then run following commands:
```bash
# Go to directory where file was downloaded
cd ~/Downloads
# Open file and edit its environment variables
nano lightHost
# Make file executable
sudo chmod +x lightHost
# Move it to PATH dir
sudo mv lightHost /usr/bin/
```
5. _Optionally:_ download lightHost.desktop file and then run following commands:
```bash
# Go to directory where file was downloaded
cd ~/Downloads
# Make file executable
sudo chmod +x lightHost.desktop
# Move it to applications dir
sudo mv lightHost.desktop /usr/share/applications/
```
6. Now you should be able to start lightHost by `lightHost` command. 
Feel free to install windows VST3 plugins to your lighthost wineprefix.

Running
----------
1. Start lightHost with `lightHost` command or desktop entry.
2. Run `pavucontrol` command to enter audio configuration, go to `Playback` tab and 
change device for `lightHost.exe` audio stream to `lighthost Audio/Sink sink`.
3. Then on `Recording` tab you should be able to select `Monitor of lighthost Audio/Sink sink` as source. 
