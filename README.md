# WlxOverlay-S

A lightweight OpenXR/OpenVR overlay for Wayland and X11 desktops, inspired by XSOverlay.

WlxOverlay-S allows you to access your desktop screens while in VR.

In comparison to similar overlays, WlxOverlay-S aims to run alongside VR games and experiences while having as little performance impact as possible. The UI appearance and rendering techniques are kept as simple and efficient as possible, while still allowing a high degree of customizability.

This is the coming-together of two of my previous projects:
- [WlxOverlay](https://github.com/galister/WlxOverlay) (SteamVR overlay written in C#)
- [WlxOverlay-X](https://github.com/galister/wlx-overlay-x) (OpenXR overlay using StereoKit, written in Rust)

![Screenshot of WlxOverlay-S in Action](https://github.com/galister/wlx-overlay-s/blob/guide/wlx-s.png?raw=true)

# Join the Linux VR Community

We are available on either:
- Discord: https://discord.gg/gHwJ2vwSWV
- Matrix Space: `#linux-vr-adventures:matrix.org`

Questions/issues specific to WlxOverlay-S will be handled in the `wlxoverlay` chat room.

# Setup

1. Grab the latest AppImage from [Releases](https://github.com/galister/wlx-overlay-s/releases).
1. `chmod +x WlxOverlay-S-*.AppImage`
1. Start Monado, WiVRn or SteamVR.
1. Run the overlay

AUR package is [wlx-overlay-s-git](https://aur.archlinux.org/packages/wlx-overlay-s-git).

You may also want to [build from source](https://github.com/galister/wlx-overlay-s/wiki/Building-from-Source).

# First Start

**If you get a screen share pop-up, check the terminal and select the screens in the order it tells you to.**

If you selected the screens in the wrong order:
  - `rm ~/.config/wlxoverlay/conf.d/pw_tokens.yaml` then restart

SteamVR users: WlxOverlay-S will register itself for auto-start, so you will not need to start it every time.

**Please continue reading the guide below.**

# Getting Started

### Working Set

Your working set consists of your currently selected overlays; screens, mirrors, keyboard, etc.

The working set appears in front of you when shown, and can be re-centered by hiding and showing again.

Show and hide your working set using:
- Non-vive controller: double-tap B or Y on your left controller.
- Vive controller: double-tap the menu button on your left controller (OpenXR, for SteamVR, you might need to bind `showhide` yourself.)

### Pointer Modes AKA Laser Colors

Much of the functionality in WlxOverlay-S depends on what color of laser you are using to interact with a UI element. \
Using the default settings, there are 3 modes:
- Regular Mode: Blue laser
- Right-click Mode: Orange laser
- Middle-click Mode: Purple laser

Please see the bindings section below on how to activate these modes.

The guide here uses the colors for ease of getting started.

### The Watch

Check your left wrist for the watch. The watch is your primary tool for controlling the app.

![Watch usage guide](https://github.com/galister/wlx-overlay-s/blob/guide/wlx-watch.png)

### The Screens

Hovering a pointer over a screen will move the mouse. If there are more than one pointers hovering a screen, the pointer that was last used to click will take precedence.

The click depends on the laser color:
- Blue laser: Left click
- Orange laser: Right click
- Purple laser: Middle click
- Stick up/down: Scroll wheel

To **curve a screen**, grab it with one hand. Then, using your other hand, hover the laser over the screen and use the scroll action.

See the [bindings](#default-bindings) section on how to grab, move and resize screens.

### The keyboard

The keyboard is fully customizable via the [keyboard.yaml](https://raw.githubusercontent.com/galister/wlx-overlay-s/main/src/res/keyboard.yaml) file. \
Download it into your `~/.config/wlxoverlay/` folder and edit it to your liking.

Typing
- Use the BLUE laser when typing regularly.
- While using ORANGE laser, all keystrokes will have SHIFT applied.
- Purple laser has no effect as of now.

**Modifier Keys** are sticky. They will remain pressed until you press a non-modifier key, or toggle them off.

### Default Bindings

![Index Controller Bindings](https://github.com/galister/wlx-overlay-s/blob/guide/wlx-index.png)

![Touch Controller Bindings](https://github.com/galister/wlx-overlay-s/blob/guide/wlx-oculus.png)

If your bindings are not supported, please reach out. \
We would like to work with you and include additional bindings.

# Troubleshooting

Check [here](https://github.com/galister/wlx-overlay-s/wiki/Troubleshooting) for tips.

# Known Issues

## Mouse is not where it should be
Hyprland users: Hyprland v0.41.0 changed their absolute input implementation to one that does not respect existing absolute input standards. Make your voice heard: [Hyprland#6023](https://github.com/hyprwm/Hyprland/issues/6023)・[Hyprland#6889](https://github.com/hyprwm/Hyprland/issues/6889)

Niri users: use on Niri 0.1.7 or later.

Other desktops: You may have selected the screens in the wrong order, see [First Start](#first-start).

## Space-drag crashes SteamVR

This has been idenfitied as an issue with SteamVR versions 2.5.5 and above (latest tested 2.7.2). One way to avoid the crash is by switching to the `temp-v1.27.5` branch of SteamVR (via beta selection) and selecting [Steam-Play-None](https://github.com/Scrumplex/Steam-Play-None) under the compatibility tab.

## Modifiers get stuck in weird ways

This is a rare issue that can make your desktop not react to click or keys due to a modifier being stuck somewhere. Restarting the overlay fixes this.

## X11 limitations
- X11 capture can generally seem slow. This is because zero-copy GPU capture is not supported on the general X11 desktop. Consider trying Wayland or Picom.
- DPI scaling is not supported and may cause the mouse to not follow the laser properly.
- Upright screens are not supported and can cause the mouse to act weirdly.
- Screen changes (connecting / disconnecting a display, resolution changes, etc) are not handled at runtime. Restart the overlay for these to take effect.
