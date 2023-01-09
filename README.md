# mounting-drive-plex-rpi
A short explanation how to mount the drive for you Raspberry-Pi-Plex-Server correctly

### Find the right drive

With the command
```bash
lsblk
```
we get the list of all drives

Output:
```bash
pi@plex:/mnt/exSSD $ lsblk
NAME        MAJ:MIN RM   SIZE RO TYPE MOUNTPOINT
sdb           8:16   0 223.6G  0 disk 
`-sdb1        8:17   0 223.6G  0 part 
mmcblk0     179:0    0  14.5G  0 disk 
|-mmcblk0p1 179:1    0   256M  0 part /boot
`-mmcblk0p2 179:2    0  14.3G  0 part /
```

In my case the SSD ```sdb1``` is the correct one.

### Mount it

First we create a folder to mount the drive to

```bash
sudo mkdir /mnt/exSSD
```

then we mount the drive to it
```bash
sudo mount /dev/sdb1 /mnt/exSSD
```


### Set the permission for the current user (normally pi user) 
This is the step most of the people miss and get some troubles when they try to store the data or download some new stuff.
```bash
sudo chmod ugo+wx /mnt/exSSD/
```

### mount on startup
```bash
sudo blkid
```

Output: 
```bash
/dev/mmcblk0p1: LABEL_FATBOOT="boot" LABEL="boot" UUID="0F92-BECC" BLOCK_SIZE="512" TYPE="vfat" PARTUUID="dd7d86c0-01"
/dev/mmcblk0p2: LABEL="rootfs" UUID="41c98998-6a08-4389-bf74-79c9efcf0739" BLOCK_SIZE="4096" TYPE="ext4" PARTUUID="dd7d86c0-02"
/dev/sdb1: LABEL="Media" UUID="63B1-F995" BLOCK_SIZE="512" TYPE="exfat" PARTUUID="2fb3af64-01"
```

```bash
sudo nano /etc/fstab
```

UUID=D632-BE5F /mnt/exdisk fstype defaults,auto,users,rw,nofail 0 0

```bash
```
