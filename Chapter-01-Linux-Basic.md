# Linux Basic

## Kernel

### Processor Rings and Privilege

* Intel x86 processor rings
    * 0-3
    * The smaller, the more privileged
* Linux kernel runs at ring 1
* Linux user programs run at ring 3

### Options to add feature to kernel

1. YES - compiled to kernel
1. NO - not compiled to kernel
1. MODULE - compiled to module, loaded to kernel if needed

### Ways to enter kernek mode

1. Using system call
1. Using soft interrupt

## Devices

### Device Types

#### Block Device

* read unit: block, e.g. 512kbytes
* often used together with cache
* example: hard disk

#### Character Device

* read unit: character
* example: console, keyboard, magnetic tape

### Partition of Storage Device

*Required by Intel-based computers*

* at most four primary partitions
* one primary partition can be extended
* unlimited partitions can exist on an extended partition
    * on linux, the limit is 59

### Master Boot Record (MBR)

should be set up properly in order to boot

Tools:

* Windows: fdisk /mbr
    * using chain loading
* Linux: lilo, grub
    * using a configuration file
    * also supports chain loading

## File and File System

File system can have different meaning in different contexts:

* a sub-module of Linux
* some specific collection of file and certain attributes, such as ext2, ntfs
* a medium of physical device storing logical files
 
### File Systems in Linux:

* VFS: virtual file system (switch), all directories are contained in one, virtual unified "file system" (with mount)
* Supported file systems: ext*, FAT, NTFS...

### File types in linux:

* Regular file: no internal structure
* Directory: a table of contents
* Character special file
* Block special file: represent hardware or logical devices
* FIFO: named pipe, but is created by kernel and accessed as part of the file system, handled by kernel, no actual content 
* Socket: special file used for inter-process communication
* Symbolic link: stores file name

### Directories in Linux:

* /bin: basic binary files
* /boot: boot files
* /dev: hardware devices
* /etc: configurations
* /mnt: mount points
* /proc: mirror of the process
* /root: home directory of root account
* /sbin: executables for administrative tasks, also /usr/sbin and /usr/local/sbin
* /tmp: temporary files
* /usr: unix system resource, often very large
* /var: variable files
* /lost+found: recovered files after a power shutdown

### Useful File Commands

* od: octal display
* strings: view strings of a binary file
* file: determine file type
* lpd: linear printing daemon
* wc: word count
