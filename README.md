[postmarketOS]: https://postmarketos.org

# Native Arch Linux on Redmi 4X (santoni)

```
/*
 * Your warranty is now void.
 *
 * I am not responsible for bricked devices, dead SD cards,
 * thermonuclear war, or you getting fired because the alarm app failed. Please
 * do some research if you have any concerns about features and tampering with
 * the system before flashing it! YOU are choosing to make these modifications,
 * and if you point the finger at me for messing up your device, 
 * I will laugh at you.
 */
```

This project here aims to get Native Arch Linux running on the Xiaomi Redmi 4X (no chroot)
I would recommend to use a USB stick or SD card to boot this, you can install it on the eMMC, but I prefer SD card more since you don't have to tamper with the eMMC.

If you cannot get it to boot, you should try to get `/proc/last_kmsg`.

## Why are we doing this?
We're doing this because:
- We want to expand the device's lifespan.
- Android is running on a Linux kernel, so why this isn't possible?
- We really enjoy the challenge.

## System Specs:
| Part     | Component                                  | 
| -------- | ------------------------------------------ |
| CPU      | Qualcomm Snapdragon 435 - 8 Cores, 1.4 GHz |
| RAM      | 2/3 GB                                     |
| GPU      | Adreno 505                                 |
| Storage  | 16/32 GB eMMC                              |
| Ext Storage | microSD - up to 128 GB                  |
| OS       | Android 6.0 (launch) - Android 7.1                       |
| Other    | Wi-Fi, Bluetooth 4.2, GPS                  |

Full system specs: https://www.gsmarena.com/xiaomi_redmi_4_(4x)-8608.php#redmi-4x

## What's working
- Booting
- Flashing (boot.img only tested)
- Display
- Wi-Fi + Hotspot
- USB Ethernet (local SSH, but also SSH via USB works)
- Sound
- Xorg
- DPMS for Xorg (screen going to sleep just fine)
- USB OTG
- Vibrator (/sys/class/timed_output/vibrator)

## Not working (yet)
- Camera (broken in kernel? accessing /dev/video32 and 33 will crash the kernel)
- Modem
- GPS
- Accelerometer
- Light Sensor
- GPU (Freedreno, through if that doesn't work, we probably might stuck with libhybris until device's mainline kernel)
- Wayland DPMS (backlight stays on)

## Bugs
- Framebuffer Console doesn't work.
- Power management doesn't work this moment, due to Qualcomm's so-called "Crypto Engine" for SDHCI interrupting the device from going to sleep.
- Framebuffer colors are messed up.
- /proc/last_kmsg is corrupted, through still readable.
 
## Device Source:
- Kernel Source: https://github.com/Danct12/msm-3.18 <rel/msm-3.18-archlinux>
- Device tree: https://github.com/LineageOS/android_device_xiaomi_santoni

## To do:
- Mainline the device (like what postmarketOS guys did)
**WARNING: There's always a risk of getting the magic smoke out of the device (by set the regulator settings wrong, we already have a case of fried device with the xiaomi-tissot), so this isn't going to happen anytime soon (if you're someone with a brave **SOUL** and determination, feel free to help out!)**

All the changes and anything I got to work will be upstreamed to [postmarketOS] in order to help development.

Stay determined, $USER!

For more information in development (but also interested into getting Arch on other devices), join DanctNIX Discord: https://discord.gg/AvtdRJ3
