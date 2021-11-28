# jornada-dosbox
dosbox 0.74-3 fork with patches to be useful on Jornada 7xx running Linux:
- VGA code changed to output every 2nd scanline only in VGA mode to support half VGA screen
- VGA ROM font changed to look acceptable on half VGA screen
- Works on the commandline framebuffer device, doesn't require X11 overhead. Should work with X11 also though.
- Supports sound on the Jornada by using the snd-jornada720 driver from the kernelpatches repo.

## Dependencies
apt-get install the below packages to your Jornada Linux CF card:

- automake
- autotools-dev
- libsdl1.2debian 
- libsdl1.2-dev
- build-essential
- manpages-dev
- libevdev-dev
- libsdl-mixer(-dev) for ALSA sound support

`apt-get install automake autotools-dev libsdl1.2debian libsdl1.2-dev build-essential manpages-dev libevdev-dev`
 
## Building
I'd suggest to use the desktop PC and QEMU running on the CF card, running this on the Jornada should also be possible but might take some serious time.

- Make sure dependencies are installed
- git clone this repo: `git clone https://github.com/timob0/jornada-dosbox.git /opt/jornada-dosbox`
- `cd /opt/jornada-dosbox`
- `./configure`
- `make`
- `make install`

## Running
`dosbox` from the commandline. If you see a garbled screen, thats because of permissions to the framebuffer device. Try to run as root then.

On the first run, it will create a .dosbox folder in your home drive and create a config file in there which you can tweak
Some settings you would want to adjust:
- `fullscreen=true`
- `frameskip=6`
- `scaler=none`
- `core=auto`
- `cputype=auto`
- `cycles=max`
- Set the audio emulation to your liking, suggest to go with 22kHz or maybe even 11kHz sind it's quite heavy on the CPU. Be sure to use the snd-jornada720 from my kernelpatches repo and configure ALSA properly.

If you have a DOS folder on the FAT partition of your CF card for use with PocketDOS you can just mount it fine and use the programs from Linux. Add a mount C: /mnt/boot/YOURDOSFOLDER to the autoexec section of the config file

## Limitations
- Only every 2nd scanline is being rendered to scale down standard VGA to the Jornada screen
- Emulation is not exactly quick, maybe at PC-XT level
- Sound not working (due to no sound support in the Linux kernel for Jornada)
- Touchscreen -> Mouse translation is ... not good
- dosbox relies on its own keyboard mapping, the console keyboard map is ignored
