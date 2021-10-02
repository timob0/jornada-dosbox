# jornada-dosbox
dosbox 0.74-3 fork with patches to be useful on Jornada 7xx running Linux:
- VGA code changed to output every 2nd scanline only in VGA mode to support half VGA screen
- VGA ROM font changed to look acceptable on half VGA screen

## Dependencies
- automake
- autotools-dev
- libsdl1.2debian libsdl1.2-dev

## building
I'd suggest to use the desktop PC and QEMU running on the CF card

- Make sure dependencies are installed, apt-get install them
- git clone this repo, maybe to /opt/jornada-dosbox
- cd /opt/jornada-dosbox
- ./configure
- ./make
