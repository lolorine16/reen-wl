# wlroots-tinywl

This is the "minimum viable product" Wayland compositor based on wlroots. It
aims to implement a Wayland compositor in the fewest lines of code possible,
while still supporting a reasonable set of features. Reading this code is the
best starting point for anyone looking to build their own Wayland compositor
based on wlroots.

## Building TinyWL

TinyWL is disconnected from the main wlroots build system, in order to make it
easier to understand the build requirements for your own Wayland compositors.
Simply install the dependencies:

- wlroots
- wayland-protocols

And run `make`.

## Running TinyWL

You can run TinyWL with `./tinywl`. In an existing Wayland or X11 session,
tinywl will open a Wayland or X11 window respectively to act as a virtual
display. You can then open Wayland windows by setting `WAYLAND_DISPLAY` to the
value shown in the logs. You can also run `./tinywl` from a TTY.

In either case, you will likely want to specify `-s [cmd]` to run a command at
startup, such as a terminal emulator. This will be necessary to start any new
programs from within the compositor, as TinyWL does not support any custom
keybindings. TinyWL supports the following keybindings:

- `Alt+Escape`: Terminate the compositor
- `Alt+F1`: Cycle between windows

## Limitations

Notable omissions from TinyWL:

- HiDPI support
- Any kind of configuration, e.g. output layout
- Any protocol other than xdg-shell (e.g. layer-shell, for
  panels/taskbars/etc; or Xwayland, for proxied X11 windows)
- Optional protocols, e.g. screen capture, primary selection, virtual
  keyboard, etc. Most of these are plug-and-play with wlroots, but they're
  omitted for brevity.

## Debugging Wayland Compositors

You can run a wayland compositor by switching to a tty and launching it directly. But for debugging 
it is much nicer to run it embedded in your current window manager. We can set up a nice environment 
quite easily that will work regardless of window manager, display server, or video card. This is a way
get wlroots based compositors to play nice with NVIDIA graphics cards.

```
kwin_wayland --xwayland --socket wayland-1 --width 1920 --height 1080
WAYLAND_DISPLAY=wayland-1 ./result/bin/tinywl -s alacritty
```
Now tinywl will be running on `wayland-0`, inside the kwin window. Note that it doesn't matter if you
use KDE Plasma (or litterally anything else), it's just that kwin is a mature compositor with multiple
backends that will let us run tinywl (or any other compositor/window manager) embdedded. The kwin display
will be called `WL-1`, as opposed to something like `HDMI-A-1` if you need to access it (like from a sway
config).

# [TinyWL's readme](https://gitlab.freedesktop.org/wlroots/wlroots/-/tree/master/tinywl)
