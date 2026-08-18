# Applications

After installing Ubuntu and doing the basic system setup, I started installing the applications that I normally use.

One of the things I wanted was to use Google Docs instead of LibreOffice.

## Google Apps Desktop

I first tried to use Google Docs through the Ubuntu App Center, but the application did not work correctly.

After that I searched for another option and found Google Apps Desktop in the Snap Store.

Google Apps Desktop is a desktop application that gives access to Google apps from one place.

It is important to mention that this is **not an official Google application**.

The Snap Store lists **Nanda Kumar Matha (`n-incognito`)** as the publisher.

The application is available as:

```text
google-apps-desktop
````

The Snap Store also lists the project as MIT licensed and provides the source code:

[https://github.com/NandaKumarMatha/Google-apps](https://github.com/NandaKumarMatha/Google-apps)

## Installing Google Apps Desktop

First I checked if Snap was available on my Ubuntu installation.

If `snap` is not installed, it can be installed with:

```bash
sudo apt update
sudo apt install snapd
```

After installing `snapd`, I can restart the system or log out and back in.

Then I installed Google Apps Desktop:

```bash
sudo snap install google-apps-desktop
```

After installing it, I opened the application and logged into my Google account.

It worked and I could access my Google applications from the desktop.

### Security note

Because this is not an official Google application, I don't want to describe it as if Google made it.

When installing third-party software, I should always check where it comes from and who maintains it before logging into an account through it.

---

# Firefox Nightly

I also wanted to try Firefox Nightly.

Firefox Nightly is a testing version of Firefox where newer features are available before they reach the normal Firefox release.

## Check system architecture

Before downloading Firefox, I checked the architecture of my system:

```bash
uname -m
```

My output was:

```text
x86_64
```

This means that my system uses the 64-bit x86 architecture.

## Download Firefox Nightly

I downloaded Firefox Nightly from the official Mozilla website.

The first version I downloaded was not the correct one for my system, so I removed it and downloaded the correct version.

When removing files with `sudo rm`, I need to be careful with the path because the command permanently removes the file.

Example:

```bash
sudo rm "/home/samuel/Downloads/firefox-old.tar.xz"
```

I should always check the path before using `sudo rm`.

## Extract Firefox Nightly

I went to the Downloads folder:

```bash
cd ~/Downloads
```

Then I extracted the archive:

```bash
tar -xf firefox-*.tar.xz
```

After extracting it, I moved Firefox to `/opt`:

```bash
sudo mv firefox /opt/firefox-nightly
```

I used `/opt` because it can be used for manually installed applications.

## Create application shortcut

To make Firefox Nightly appear in the applications menu, I created a desktop entry:

```bash
sudo nano /usr/share/applications/firefox-nightly.desktop
```

I added:

```ini
[Desktop Entry]
Name=Firefox Nightly
Comment=Firefox Nightly Browser
Exec=/opt/firefox-nightly/firefox %u
Icon=/opt/firefox-nightly/browser/chrome/icons/default/default128.png
Terminal=false
Type=Application
Categories=Network;WebBrowser;
StartupNotify=true
```

After saving the file, I updated the desktop database:

```bash
sudo update-desktop-database
```

Firefox Nightly then appeared in the applications menu.