# Lenovo Thinkpad W520 Bumblebee configuration

configuration snippets that enable 'best of both worlds' behavior for the
Nvidia 2000M / Intel HD3000 combination:

- disable NVidia and work with the Intel GPU when on battery (no external monitor possible)
  - power consumption is identical to a Quad-Core T520 (intel only) (15W w/ medium brightness and light usage)
- enable NVidia when external monitor is required (25-30W power consumption)
- optirun <executable> works

Note that I'm not doing anything demanding extraordinary GPU power. I could
happily live with Intel-only if a T520 could handle more than 16GB memory.

Configuration has been tested on a recent up-to-date arch install with the
following software installed:

- bumblebee 3.2.1
- nvidia 361.28-4 (nvidia-settings, nvidia-utils)
- xf86-video-intel 1:2.99.917+587+gc186d4d-1 (yes, that's the version as reported by pacman)
- bbswitch 0.8-44

Additionally, bumblebee service must be enabled:
`sudo systemctl enable bumblebeed.service`

The `bin` directory contains some scripts I use to automate switching between modes.

## Resources

- [scyth's blog](http://www.unixreich.com/blog/2013/linux-nvidia-optimus-on-thinkpad-w520w530-with-external-monitor-finally-solved/)
  - gave me hope and made me by that W520 in the first place
  - provides the - IMHO essential - hint to set `PMMethod=none`
  - also important: `KeepUnusedXServer=true`
- [Arch Wiki](https://wiki.archlinux.org/index.php/NVIDIA_Optimus)
  - `Option "UseEDID" "true"` but I'm not sure that actually makes sense

## Issues

- `xrandr --output VIRTUAL6 --auto` doesn't select the highest available resolution.
  - explicitely request a certain mode
  - mode names are strange
- the mode names (`VIRTUAL6.738-3840x2160`) sometimes change, then the `4k` script doesn't work
- have to remember to call `mobile` to turn off nvidia or else your battery runtime sucks

