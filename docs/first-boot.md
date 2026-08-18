# First Boot

After the installation finished, Ubuntu asked whether I wanted to contribute system information to help improve Ubuntu. I chose not to send any diagnostic or usage data.

Next, I selected the default UI color theme and completed the initial setup.

## Network Connection

I connected the PC to the network using an Ethernet cable. The Ethernet port showed an orange link light, but there was no internet connection.

Testing with:

```bash
ping 1.1.1.1
```

returned that the destination was unreachable.

The issue was later resolved. More information can be found in `networking.md`.

## Power Settings

To prevent the computer from going to sleep while working, I changed the default power settings.

Path:

```
Settings → Power → Power Saving
```

Configuration:

- Automatic Screen Blank: Off
- Automatic Suspend: On (2 hours)

Continuing with in `system-update.md`

Continuing with in `development-enviroment.md`
