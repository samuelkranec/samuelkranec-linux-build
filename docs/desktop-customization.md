# Desktop customization

After finishing the basic system setup, I started changing the Ubuntu desktop to make it more comfortable for me.

## Taskbar

First I changed the taskbar settings in Ubuntu Settings.

I moved the taskbar to the bottom of the screen and changed the side panel behavior.

## GNOME Tweaks

Ubuntu Settings does not have every option I wanted, so I installed GNOME Tweaks.

I used the terminal because I also wanted to practice installing packages with APT.

```bash
sudo apt update
sudo apt install gnome-tweaks
```

I can start it with:

```bash
gnome-tweaks
```

## GNOME extensions

I also installed the tools for managing GNOME extensions:

```bash
sudo apt install gnome-shell-extensions gnome-shell-extension-manager
```

I can use Extension Manager to install and manage GNOME extensions.

## MacTahoe GTK theme

For the desktop theme I chose MacTahoe because I like its macOS-style look.

The theme source is:

https://github.com/vinceliuice/MacTahoe-gtk-theme

I cloned the repository with:

```bash
git clone https://github.com/vinceliuice/MacTahoe-gtk-theme.git --depth=1
```

Then I entered the directory:

```bash
cd MacTahoe-gtk-theme
```

Before installing a third-party theme, I can check what the installer does with:

```bash
./install.sh --help
```

I installed the theme with:

```bash
./install.sh
```

The command runs a script from a third-party Git repository, so I should review the script before running it, especially when using scripts from software I do not already trust.

## Applying the theme

After installing the theme, I opened GNOME Tweaks and selected the theme options that I wanted.

I did not need Extension Manager to apply the GTK theme itself. Extension Manager is for GNOME extensions.

After making the desktop changes, I restarted the system:

```bash
sudo reboot
```

## What I changed

- Moved the taskbar to the bottom.
- Installed GNOME Tweaks.
- Installed GNOME Extension Manager.
- Installed the MacTahoe GTK theme.
- Changed the desktop appearance to what I wanted.
