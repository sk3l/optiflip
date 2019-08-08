# optiflip - Nvidia <~> Intel Hybrid Graphics Helper Scripts

This repo contains some helper scripts and sample X11 configs to assist in manually changing the active graphics card in an Optimus hybrid graphics machine, switching back/forth between Nvidia and Intel. The process relies on the bbswitch kernel module for toggling the active graphics card.

The inspiration of these tools is [this documentation](https://wiki.archlinux.org/index.php/Lenovo_ThinkPad_P1#Hybrid_graphics_with_bbswitch_only) from Arch Linux on the Lenovo Thinkpad P1 laptop.

## DISCLAIMER

Use of these instructions and this code IS AT-WILL; USE AT YOUR OWN RISK. I am not responsible for any issues or problems you incur in using the code, configuration or following these instructions. 

## Installation

1. Copy the contents of `/scripts` folder to a location in your $PATH, e.g. /usr/local/sbin

```
│mskelton@panther ~ $ sudo cp scripts/* /usr/local/sbin
```

2. Copy the contents of `/conf` folder to `/etc/X11`. **IMPORTANT**, you should consider backing up any existing xorg.conf you already have in place.

```
│mskelton@panther ~ $ sudo cp /etc/X11/xorg.conf /etc/X11/xorg.conf.BAK
│mskelton@panther ~ $ sudo cp /conf/* /etc/X11
```

## Use

1. You can call the `lsgfx` helper script to let you know which card your hybrid graphics is currently using:

```
mskelton@panther ~ $ lsgfx
OpenGL vendor string: VMware, Inc.
OpenGL renderer string: llvmpipe (LLVM 8.0, 256 bits)
```

2. Open a new TTY using <ctl+alt+F2> (F3, F4, etc. can be used instead)

3. Execute the script for the graphics card you wish to activate e.g. gfxnvidia

** !!! BEWARE !!! this will TERMINATE your current X11 session in order to switch the graphics card and start a new X11 session. ** You should back up any work you wish to not lose at this point in running GUI apps.

```
mskelton@panther ~ $ gfxnvidia
ON
```

4. Your desktop manager will have been restarted (assuming your using e.g. SDDM or another modern variety). Log back into an X11 session.

5. Confirm that the active graphics card has alternated.

```
mskelton@panther ~ $ lsgfx
OpenGL vendor string: NVIDIA Corporation
OpenGL renderer string: Quadro P2000 with Max-Q Design/PCIe/SSE2
``` 
