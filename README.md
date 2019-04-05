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

If you cannot get it to boot, you should try to get ~~console-ramoops in `/sys/fs/pstore`~~ **TO-DO: GET PSTORE/RAMOOPS TO WORK**.

## System Specs:
| Part     | Component                                  | 
| -------- | ------------------------------------------ |
| CPU      | Qualcomm Snapdragon 435 - 8 Cores, 1.4 GHz |
| RAM      | 2/3 GB                                     |
| GPU      | Adreno 505                                 |
| Storage  | 16/32 GB eMMC                              |
| Ext Storage | microSD - up to 128 GB                  |
| OS       | Android 6.0 (launch)                       |
| Other    | Wi-Fi, Bluetooth 4.2, GPS                  |

Full system specs: https://www.gsmarena.com/xiaomi_redmi_4_(4x)-8608.php#redmi-4x

## What's working
- Booting
- Flashing (boot.img only tested)
- Display
- Wi-Fi + Hotspot
- USB Ethernet (for local SSH)
- Sound (drop msm8920-sku7-snd-card folder from this repo to /usr/share/alsa/ucm)
- Xorg
- USB OTG
- Vibrator (/sys/class/timed_output/vibrator)
- DPMS for Xorg (screen going to sleep just fine)

## Not working (yet)
- Camera (shown as /dev/video32-33, however opening it will freeze/crash the kernel)
- Modem (for calls/SMS/mobile data)
- GPS
- Accelerometer
- Light Sensor
- GPU (Freedreno only supports a2xx-a4xx, which this device is a Adreno 505)
- Wayland (works in [postmarketOS])

## Bugs
- Framebuffer Console doesn't work.
~~- Sometimes the device will freeze during booting.~~ Seems to be fixed with msm-3.18 upstream kernel.
- Power management doesn't work this moment, due to Qualcomm's so-called "Crypto Engine" for SDHCI interrupting the device from going to sleep.
- Framebuffer colors are messed up.
- WCNSS driver might not have enough time to be loaded on first bootup, this might be able to work around by adding a delay after the Wi-Fi service started.
 
## Device Source:
- Kernel Source: https://github.com/Danct12/msm-3.18
- Device tree: https://github.com/LineageOS/android_device_xiaomi_santoni

## To do:
- ~~Mainline the device (like what postmarketOS guys did)~~ There's always a risk of getting the magic smoke out of the device, so this isn't going to happen anytime soon (if you're someone with a brave **SOUL** and determination, feel free to help out!)
- Get pstore/ramoops to work for further debugging (when kernel crashes or when I do a reboot sometimes?)
- Chainload distro's initramfs (so no need to run mkbootimg again with the new initramfs). Not sure if that's possible?

All the changes and anything I got to work will be upstreamed to [postmarketOS] in order to help development.

For more information in development (but also interested into getting Arch on any devices), join DanctNIX Discord: https://discord.gg/AvtdRJ3
