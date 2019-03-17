---
title: "eGPU Build Log - RTX2070 on 2016 Macbook Pro 15"
published: true
---

> Originally posted on egpu.io

# System Specs
15" Macbook Pro (Late 2016)
CPU: Intel i7-6820HQ
dGPU: Radeon Pro 460
OS: Windows 10 1809

# eGPU Hardware
Aorus Gaming Box RTX2070

# Hardware Pictures

![](https://i.imgur.com/f9dfQbp.png)

![](https://i.imgur.com/d3hW51a.png)


# Installation Steps

0. Install Windows and Bootcamp drivers.

1. Use DDU to remove AMD driver.

> Internal display could still work under Microsoft Basic Display Driver.

2. Install Thunderbolt Driver from Intel: [v17.4.77.400 (Latest as of writing)](https://downloadcenter.intel.com/download/28616/Thunderbolt-Bus-Driver-for-Intel-NUC-Kit-NUC6i7KYK?v=t)
> If this driver is not installed, gaming box will be shown as "Base System Device" in Device Manager.

3. Disable the following in Device Manager to solve error 12:
- FaceTime HD Camera
- PCIe Controller (x4) - 1909 (Right side usb-c/tb3 ports)

> USB 3.0 do not work on right side ports afterwards. USB 2.0 still work.

4. Press option key on boot to hold the system on bootloader. Plug in eGPU cable to left bottom port and boot to windows.

> If eGPU is hotplugged after booting it will not be recognized at all. Only thunderbolt controller will be shown.

> Gaming Box is activated (denoted by RGB light) after windows spinner screen and before login screen.

> Internal display may be frozen at windoes spinner screen after eGPU is on. To fix this use Win-P to select Extend Displays then back to Main Display Only. Internal display will then stay blank. (Or just use extend if wished)

5. Windows should be able to detect nvidia card and auto-install an older driver. Download the latest one from nvidia website for best performance.

# Benchmarks
All benchmarks below is done with external display, stock speed and H2D firmware.

## GPU-Z
![](https://i.imgur.com/m5xg1dF.png)

## CUDA-Z
![](https://i.imgur.com/LiOKHPS.png)

## 3DMark Time Spy
[Link to result page](https://www.3dmark.com/3dm/34564439?)

![](https://i.imgur.com/mXIjZxU.png)

Graphics score ~5% dropoff from [desktop score of 8405](https://www.guru3d.com/articles-pages/msi-geforce-rtx-2070-armor-8g-review,27.html)

## Unigine Superposition
![](https://i.imgur.com/3N8wQRb.png)

~4 frame difference from [desktop FPS of 41](https://www.guru3d.com/articles_pages/msi_geforce_rtx_2070_armor_8g_review,25.html)

# Overclocking
Using MSI Afterburner's OC Scanner feature, my card was able to achieve +255Mhz core clock with stock voltage

![](https://i.imgur.com/urRXgDO.png)


# Comments
- Some coil whine can be heard during high loads. Fans are quite noisy even when idle.
- Either my keyboard's usb hub or Logitech mouse receiver did not play well with the box's usb ports. Plugging in my HHKB / G Pro Wireless receiver combo caused immediate system crash and infinite boot loop. External SSD works fine tho.
