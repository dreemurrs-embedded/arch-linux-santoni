[postmarketOS]: https://postmarketos.org

# Native Arch Linux on Redmi 4X (santoni)

This project here aims to get Native Arch Linux running on the Xiaomi Redmi 4X (no chroot)
I would recommend to use a USB stick or SD card to boot this, you can install it on the eMMC, but SD card is working for me now.

If you cannot get it to boot, you should try to get console-ramoops in `/sys/fs/pstore`.

## System Specs:
| Part     | Component                                  | 
| -------- |:------------------------------------------:|
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
- Flashing (not tested, but of course it should flash!)
- Display
- Wi-Fi
- USB Ethernet (for local SSH)
- Sound
- Xorg

## Not working (yet)
- Camera (shown as /dev/video32-33, however opening it with freeze and might crash)
- Modem (calling/SMS/mobile data)
- GPS
- Accelerometer
- Light Sensor
- GPU (Freedreno only supports a2xx-a4xx, which this device is a Adreno 505)

## Bugs
- Framebuffer Console doesn't work.
- Sometimes the device will freeze during booting.

## To do:
- Mainline the device (like what postmarketOS guys did)

All the changes and anything I got to work will be upstreamed to [postmarketOS] in order to help development.

For more information in development (but also interested into getting Arch on any devices), join DanctNIX Discord: https://discord.gg/AvtdRJ3
