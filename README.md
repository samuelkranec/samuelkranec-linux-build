# Linux Build Project

This was a personal project where I wanted to learn Linux by actually installing, configuring, and using it myself.

Instead of only installing Ubuntu and using it normally, I wanted to understand what was happening in the system. I documented the commands I used, the configuration changes I made, things I tested, and problems I ran into.

## What I worked on

### Installing Ubuntu

I started by creating an Ubuntu installation USB and installing Ubuntu on my system.

* [Creating installation media](docs/creating-installation-media.md)
* [Installing Ubuntu](docs/installing-ubuntu.md)
* [First boot](docs/first-boot.md)

The installation documentation is not fully finished because I stopped the project before completing every part.

### System setup

After installing Ubuntu, I started setting up the system and learning the basic administration commands.

* [System updates](docs/system-update.md)
* [Applications](docs/applications.md)
* [Essential packages](docs/essential-packages.md)
* [Terminal and shell](docs/terminal-and-shell.md)

I also used this project to learn more about packages, services, users, permissions, storage, and general Linux system administration.

### Networking

I worked on basic Linux networking and troubleshooting.

* [Networking](docs/networking.md)

I documented a network problem I had during the installation and how I found the actual cause.

### Linux security

Security became one of the bigger parts of the project.

I wanted to understand what was already running on the system before changing anything and then learn how different security tools work.

* [Security hardening](docs/security.md)

The security work included:

* System security baseline
* Open ports and running services
* UFW firewall
* SSH
* AppArmor
* Automatic updates
* Fail2ban
* Audit logging

The security documentation is unfinished. I stopped the project before completing all of the planned hardening and testing.

### Desktop customization

I also changed the Ubuntu desktop to make it more comfortable for everyday use.

* [Desktop customization](docs/desktop-customization.md)

This includes GNOME settings, extensions, and the MacTahoe theme.

### Development environment

I used the system as a development environment while learning Linux.

* [Development environment](docs/development-environment.md)

I also experimented with development tools and a small Tauri application during the project. Those parts are no longer included in the current repository, but they were part of the original learning process.

### Storage

I experimented with adding and configuring additional storage.

* [Storage](docs/storage.md)

This was also one of the areas where I learned that disk operations need to be checked carefully before changing partitions or filesystems.

### Troubleshooting and learning notes

A large part of this project was figuring out why things did not work.

* [Learning notes](docs/learning-notes.md)
* [Troubleshooting](docs/troubleshooting.md)

I kept these notes so I could remember what went wrong and what I learned from it.

## How I approached the project

My basic approach was:

1. Install something.
2. Check how it works.
3. Learn what the commands and settings do.
4. Change the configuration.
5. Test it.
6. Document what happened.

I did not want to only copy commands from guides. I wanted to understand what the commands actually did and why I was using them.

## Documentation

Most of the documentation in this repository comes from things I actually tried on my own system.

Some documents are complete, while others are unfinished because the project was stopped before I could finish everything.

The external documentation and guides I used while learning are listed in the [bibliography](docs/bibliography.md).

## Project status

### Cancelled

This project was cancelled because I had to relocate my setup.

After relocating the setup, I decided that it would be more useful to work on a homelab project instead of continuing with the Linux OS project.

A lot of what I learned here is still useful for the homelab, especially Linux administration, networking, security, SSH, firewalls, and troubleshooting.

I hope that one day I will make a similar project again and go further with it.

My long-term goal is to eventually create my own operating system from scratch and understand how the system works at a much lower level.

For now, this repository stays here as a record of what I learned and worked on.
