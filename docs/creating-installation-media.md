# Creating a bootable Ubuntu 26.04 LTS installation USB

These are my notes on how I created an Ubuntu 26.04 LTS installation USB using Rufus on Windows.

I used:

| Component | Version / requirement |
| --- | --- |
| Ubuntu Desktop ISO | 26.04 LTS |
| Rufus | 4.15 (`rufus-4.15.exe`) |
| USB flash drive | At least 8 GB |
| Computer | Windows |

> **Warning**
>
> Rufus will erase the selected USB drive. Check the selected drive before starting and move any important files somewhere else first.

## 1. Download Ubuntu

I downloaded the Ubuntu Desktop 26.04 LTS ISO from:

https://ubuntu.com/download/desktop

The ISO is the installation image that will be written to the USB drive.

## 2. Download Rufus

I downloaded Rufus from its official website:

https://rufus.ie/

For this installation I used version 4.15.

## 3. Connect the USB drive

I connected the USB drive to the Windows computer.

Before opening Rufus, I checked that:

- the USB drive was the correct one,
- there was no important data on it,
- it had enough space for the Ubuntu ISO.

## 4. Create the bootable USB

I opened Rufus and selected the USB drive.

Then I:

1. Clicked **SELECT**.
2. Selected the Ubuntu 26.04 LTS ISO.
3. Checked the partition scheme and target system shown by Rufus.
4. Clicked **START**.
5. Confirmed the warnings shown by Rufus.

For a modern PC using UEFI, GPT is normally the correct partition scheme. Older systems may use Legacy BIOS and MBR instead. I checked the firmware mode of the computer rather than changing these settings randomly.

Rufus then formatted the USB and copied the Ubuntu installation files.

## 5. Check the result

When Rufus finished, it showed **READY**.

I could then use the USB to boot the computer and start the Ubuntu installation.