# Storage

## Adding a new disk

I installed a new secondary disk and wanted to use it for storage.

## 1. Identify the disk

First, I checked the connected storage devices:

```bash
lsblk
```

The secondary disk appeared as:

```text
sda    476.9G    disk
```

So the disk was:

```text
/dev/sda
```

> **Important:** `/dev/sda` identifies the whole disk, while `/dev/sda1` identifies its first partition. Always check the disk before modifying it because partitioning and formatting can permanently delete data.

## 2. Create a GPT partition table

I created a new GPT partition table:

```bash
sudo parted /dev/sda --script mklabel gpt
```

This prepares the disk for partitioning.

## 3. Create a partition

I created one partition using the whole disk:

```bash
sudo parted /dev/sda --script mkpart primary ext4 0% 100%
```

The new partition is:

```text
/dev/sda1
```

## 4. Check the partition before formatting

Before formatting, I checked the disk:

```bash
lsblk -o NAME,SIZE,FSTYPE,MOUNTPOINTS
```

I also checked whether `/dev/sda1` was mounted:

```bash
findmnt /dev/sda1
```

The system showed that `/dev/sda1` was mounted and used the `vfat` filesystem.

## 5. Unmount the partition

Because the partition was mounted, Linux would not let me format it.

The error was:

```text
/dev/sda1 is mounted; will not make a filesystem here!
```

This prevents formatting a filesystem that is currently in use.

I unmounted the partition:

```bash
sudo umount /dev/sda1
```

Then I checked it again:

```bash
lsblk -o NAME,SIZE,FSTYPE,MOUNTPOINTS
findmnt /dev/sda1
```

The partition was no longer mounted.

## 6. Format the partition

I formatted the partition with ext4:

```bash
sudo mkfs.ext4 /dev/sda1
```

This creates a new empty ext4 filesystem.

> **Warning:** Formatting permanently removes the existing filesystem data on the partition.

## 7. Create a storage directory

I created the directory where I wanted to mount the disk:

```bash
sudo mkdir -p /mnt/storage
```

## 8. Mount the disk

I mounted the new filesystem:

```bash
sudo mount /dev/sda1 /mnt/storage
```

The disk is now accessible through:

```text
/mnt/storage
```

## 9. Verify the storage

I checked the available space:

```bash
df -h /mnt/storage
```

This confirmed that the new disk was mounted and available.

## Result

The new disk was:

1. identified
2. partitioned using GPT
3. formatted as ext4
4. mounted at `/mnt/storage`

### Current storage path

```text
/dev/sda1 -> /mnt/storage
```
