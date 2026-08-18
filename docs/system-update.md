# System Update

After connecting to the internet, I updated the Ubuntu package database.

## Update package lists

```bash
sudo apt update
```

The command completed successfully.

The following day I noticed that 329 packages were available for upgrade.

To see the available upgrades:

```bash
apt list --upgradable
```

This only lists packages that can be updated.

## Upgrade installed packages

To install all available updates:

```bash
sudo apt upgrade
```

After upgrading all packages, I also ran a full system upgrade:

```bash
sudo apt full-upgrade
```

This can add or remove packages when needed to satisfy dependencies.

## Remove unused packages

```bash
sudo apt autoremove
```

This removes packages that are no longer needed.

## Reboot

To finish the update process:

```bash
sudo reboot
```
