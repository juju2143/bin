# bin

This is a collection of little bash scripts I wrote and regularly use that will be useful either as keyboard bindings for your window manager, clickable widgets in your swaybar or just useful commands to have around in your PATH.

Works best with sway, rofi as a dmenu replacement and mako as a notification daemon on Arch Linux, with the contents of this repository first in your PATH.

## _x11-mode

Forces a GTK, QT, SDL or Clutter application to use their X11 backend instead of Wayland. 

### Requirements

These environment variables are set before your Wayland window manager is started:
```sh
export PATH=$HOME/bin:$PATH
export QT_QPA_PLATFORM=wayland-egl
export SDL_VIDEODRIVER=wayland
export CLUTTER_BACKEND=wayland
export XDG_CURRENT_DESKTOP=Unity
```
Your window manager also supports Xwayland.

### Usage

Say you want OBS to use X11 because it doesn't quite work on Wayland, just make a symbolic link of its name in your `bin` directory.
```sh
ln -s _x11-mode $HOME/bin/obs
```
Of course, it only works if that `bin` directory comes before the directory the actual binary is in in the PATH (usually `/usr/bin`).

## calc

Simple calculator. Asks for a question, gives the answer in a notification and the clipboard.

### Requirements

[QuickJS](https://bellard.org/quickjs/), [wl-clipboard](https://github.com/bugaevc/wl-clipboard), and a notification daemon is installed with `notify-send`.

### Usage

Just put this as a binding in your sway or waybar config:
```sh
calc
```

### Notes

A previous version used `bc`, was replaced with a JavaScript engine because `bc` doesn't work well with floating points. You can easily replace `qjsbn` with `node` without problems, QuickJS was chosen because it was faster and you probably don't need everything `node` has to offer if you're only using it for quick calculations. Future versions could implement history, or even an engine such as Alexa.

## colorpicker

Color picker for your screen. Pretty useful if you're working with color.

### Requirements

[slurp](https://wayland.emersion.fr/slurp/), [grim](https://wayland.emersion.fr/grim/), [ImageMagick](https://imagemagick.org/), [wl-clipboard](https://github.com/bugaevc/wl-clipboard), and a notification daemon is installed with `notify-send`.

### Usage

Just put this as a binding in your sway or waybar config:
```sh
colorpicker
```

## dmenu_midi

Frontend to `midiprog` using a dmenu.

### Requirements

See `midiprog`.

### Usage

Just put this as a binding in your sway or waybar config:
```sh
dmenu_midi
```

## file_run

Simple file browser.

## midiprog

Simple instrument changer for MIDI devices.

### Requirements

fluidsynth, OpenBSD's netcat

Fluidsynth is running in the background, here's a command line example you can put in a systemd user unit:
```sh
fluidsynth -a pulseaudio -m alsa_seq -r 48000 -o midi.autoconnect=1 -g 1.0 -l -i -s /usr/share/soundfonts/default.sf2
```
The `-s` is important as it allows commands to be sent to it with netcat.

### Usage

```sh
midiprog <bank> <program>
```

### Notes

`dmenu_midi` and `midiprog` can easily be combined in one program, but I like the convenience of having it available when the WM isn't running.

## swaysaver

Hack to make `swaylock` work with `xscreensaver`. The script watches for screensaver daemon status and calls `swaylock` 5 seconds after `xscreensaver` blanks the screen.

### Requirements

swaylock, xscreensaver

### Usage

Call this script together with the `xscreensaver` daemon in your sway config:
```sh
exec xscreensaver
exec swaysaver
```

### Notes

Based on some example code from `xscreensaver`, its licence might apply instead.

## emojipicker

It's just a simple emoji picker. Select your emoji, paste it with the middle button of your mouse.

### Requirements

unicode-emoji (provides the emoji database), [wl-clipboard](https://github.com/bugaevc/wl-clipboard)

### Usage

Just put this as a binding in your sway or waybar config:
```sh
emojipicker
```

# Licence

All original code licenced under LiLiQ-P 1.1. If you liked this software, [buy me a beer](https://patreon.com/juju2143) :)
