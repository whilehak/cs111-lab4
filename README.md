# Hey! I'm Filing Here

In this lab, I successfully implemented ext2 file system. 
It has two directories (root, lost+found), 1 regular file (hello-world), and 1 symbolic link (hello->hello-world).

There are 128 inodes and 1024 blocks of size 1024 bytes. More details in Results section.

## Building
To build, run
```bash
make
./ext2-create # builds cs111-base.img
```

## Running
Run
```bash
dumpe2fs cs111-base.img # dumps filesystem information
fsck.ext2 cs111-base.img # checks filesystem consistency using fsck
```
It can also be mounted using the following commands:
```bash
mkdir mnt
sudo mount -o loop cs111-base.img mnt
cd mnt
```

## Results
Output from dumpe2fs: 
```
$ dumpe2fs cs111-base.img 
dumpe2fs 1.47.0 (5-Feb-2023)
Filesystem volume name:   cs111-base
Last mounted on:          <not available>
Filesystem UUID:          5a1eab1e-1337-1337-1337-c0ffeec0ffee
Filesystem magic number:  0xEF53
Filesystem revision #:    0 (original)
Filesystem features:      (none)
Default mount options:    (none)
Filesystem state:         clean
Errors behavior:          Continue
Filesystem OS type:       Linux
Inode count:              128
Block count:              1024
Reserved block count:     0
Free blocks:              1000
Free inodes:              115
First block:              1
Block size:               1024
Fragment size:            1024
Blocks per group:         8192
Fragments per group:      8192
Inodes per group:         128
Inode blocks per group:   16
Last mount time:          n/a
Last write time:          Wed Mar 18 18:54:18 2026
Mount count:              0
Maximum mount count:      -1
Last checked:             Wed Mar 18 18:54:18 2026
Check interval:           1 (0:00:01)
Next check after:         Wed Mar 18 18:54:19 2026
Reserved blocks uid:      0 (user root)
Reserved blocks gid:      0 (group root)


Group 0: (Blocks 1-1023)
  Primary superblock at 1, Group descriptors at 2-2
  Block bitmap at 3 (+2)
  Inode bitmap at 4 (+3)
  Inode table at 5-20 (+4)
  1000 free blocks, 115 free inodes, 2 directories
  Free blocks: 24-1023
  Free inodes: 14-128
```

Output from fsck:
```
$ fsck.ext2 -f cs111-base.img 
e2fsck 1.47.0 (5-Feb-2023)
Pass 1: Checking inodes, blocks, and sizes
Pass 2: Checking directory structure
Pass 3: Checking directory connectivity
Pass 4: Checking reference counts
Pass 5: Checking group summary information
cs111-base: 13/128 files (0.0% non-contiguous), 24/1024 blocks
```

## Cleaning up
To unmount and delete mnt, run
```bash
sudo umount mnt
rmdir mnt
```
Then, run 
```bash
make clean
```