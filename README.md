# Linux MiniBook X

This project is dedicated to documenting, collaborating and coordinating efforts over excellent out-of-the-box Linux support for the laptop known as

* Chuwi MiniBook X 2023
* Chuwi Minibook X N100
* Chuwi Minibook X 2024

Contributions welcome.

## General info

* https://www.xda-developers.com/chuwi-minibook-x-n100-laptop-review/
* https://www.lerattus.blog/review-for-chuwi-minibook-x-2023/
* https://liliputing.com/chuwi-minibook-x-mini-laptop-gets-an-alder-lake-n-upgrade/

## Hardware Support

As of Linux 6.8 (2023-03-02)

| Feature              | Support | Info |
|----------------------|---------|------|
| Display              | ❌*     | Fixes available see below |
| Audio                | ✅      | Including speakers and combo jack     |
| GPU                  | ✅      |      |
| Accelerometer        | ❌      |      |
| Lid Switch           | ✅      |      |
| Tablet Switch        | ❌      |      |
| Performance profiles | ✅      |      |
| Screen brightness    | ✅      |      |
| Media keys           | ✅      |      |
| USB-C ports          | ✅      | Full featured incl Display Port     |
| Touch screen         | ✅      | Multi-Touch     |
| Keyboard             | ✅      |      |
| Touchpad             | ✅      | Multi-Touch |
| Keyboard backlight   | ✅      | |
| Night Light          | ❌      |
| Bluetooth            | ✅      | |
| Ambient light sensor | ?       | |

## Features

### Broken output

Since Linux 6.6.15 the display output is broken. It looks like a hardware issue where only half of the panel is used and presents glitches.

A kernel patch is available at https://gitlab.freedesktop.org/drm/intel/-/issues/10334

### Orientation

The "physicial" screen orientation is incorrect. You can fix it in` the display settings by changing the orientation to "Portrait Right" but that will only work once post boot.

A better solution is to set the following kernel parameter `video=DSI-1:panel_orientation=right_side_up`.

* https://www.kernel.org/doc/Documentation/fb/modedb.txt
* https://patchwork.kernel.org/project/dri-devel/patch/20191110154101.26486-10-hdegoede@redhat.com/

TODO: submit a patch to https://github.com/torvalds/linux/blob/master/drivers/gpu/drm/drm_panel_orientation_quirks.c

### Refresh rate

Out of the box, the display supports 50hz.

I've succesfully managed to use 60hz and even 90hz on Windows but wasn't able to do so on Linux yet.

⚠️ It's unclear what effects increasing the refresh rate can have. It may degrade the hardware.

* https://forum.chuwi.com/t/minibook-x-2023-50hz-choppy-ghosting/41613/3

### Resolution

The resolution is 1920x1200 (16:10).

You'll need fractonal scaling, on GNOME if it's not enabled you can do so with

`gsettings set org.gnome.mutter experimental-features "['scale-monitor-framebuffer']"`

150% is recommended, specially for touch but it's usable at 125%.

### Brightness

* Software controlled
* 21 levels
* Brightness keyboard keys functional

### Tablet switch

There is a physical switch to trigger the tablet mode in order to lock the keyboard and touchpad.
However it's not currently working. On Windows it appears to use `PNP0C60` / `INT33D3`.

It's not working on Linux but there is some support for it.

* https://www.spinics.net/lists/platform-driver-x86/msg21741.html 1/2
* https://patchwork.kernel.org/project/linux-input/patch/20200620123412.40465-3-hdegoede@redhat.com/ 2/2


Possibly helpful

* https://gitlab.gnome.org/GNOME/mutter/-/issues/1760#note_1102837
* https://patchwork.kernel.org/project/linux-acpi/patch/1472628817-3145-1-git-send-email-wnhuang@google.com/
* https://bbs.archlinux.org/viewtopic.php?id=222950
* https://reviews.freebsd.org/D21612?id=61959
* 4 parts series
  * https://pressers.name/2022/11/07/fixing-linux-unsupported-devices-on-the-lenovo-300e-gen-2/
  * https://pressers.name/2022/11/16/lenovo-300e-gen-2-part-2-lshw-lspci-dmesg-and-some-initial-investigation/
  * https://pressers.name/2022/11/20/lenovo-300e-gen-2-part-3-digging-in-to-the-laptop/slate-switch-and-acpi/
  * https://pressers.name/2023/01/05/lenovo-300e-gen-2-part-4-laptop/slate-driver-investigation/

### Accelerometer 

There is a MEMSIC MXC6655 accelerometer in the device for detecting screen orientation.
It does not appear to be supported at the moment.

* https://cdn.sparkfun.com/assets/3/c/2/0/5/MXC6655XA_datasheet.pdf

## License

CC BY-SA 4.0 

https://creativecommons.org/licenses/by-sa/4.0/