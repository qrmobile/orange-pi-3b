# How to Clone System Drive to Larger Storage on Single Development Board

## Cloning the System Drive using `dd` command

Yes, you can clone the system drive using the `dd` command. The `dd` command is a powerful command-line tool used for copying and converting files on Unix-based systems, including Linux. It can be used to create a bit-for-bit copy of an entire drive or partition, which is useful for cloning system drives.

Here's how to clone a system drive using the `dd` command:

1. **Identify the source and target drives:**
   - Run the following command to list all connected storage devices: 
```
   sudo fdisk -l
```
   - Identify the device names for the source drive (e.g., /dev/sda) and the target drive (e.g., /dev/sdb).

2. **Clone the source drive to the target drive:**
   - Use the `dd` command to copy the entire source drive to the target drive. Replace 'X' and 'Y' with the appropriate letters for the source and target devices (e.g., sda or mmcblk1 and sdb):
```
   sudo dd if=/dev/sdX of=/dev/sdY bs=4M status=progress
```
or
```
   sudo dd if=/dev/mmcblk1 of=/dev/sdb bs=4M status=progress
```
   - This process may take some time depending on the size of the drive.

Please note that cloning a system drive while it is in use might result in an inconsistent copy due to files being modified during the cloning process. To ensure a consistent copy, it is recommended to boot your system from a live USB and perform the cloning process from there.

Also, keep in mind that the target drive should be of equal or larger size than the source drive. If the target drive is larger, you may need to resize the partition(s) after cloning to utilize the additional space.

## Resizing Partitions after Cloning to Larger Storage

To resize the partition(s) after cloning a 32GB source system drive to a 128GB microSD card, you can use the `fdisk` and `resize2fs` tools. Here's how to resize the root partition:

1. **Identify the device name for the target microSD card (128GB):**
   - Run the following command to list all connected storage devices:
```
   sudo fdisk -l
```
   - Identify the device name for the target microSD card (e.g., /dev/sdb or /dev/sdc).

2. **Start the `fdisk` utility:**
```
   sudo fdisk /dev/sdX
```
   - Replace 'X' with the appropriate letter for the target device (e.g., sdb or sdc).

3. **Delete the existing root partition:**
   - In the `fdisk` utility, press `p` to print the partition table.
   - Identify the root partition number (e.g., 2 for /dev/sdb2).
   - Press `d` to delete the partition, and then enter the partition number.

4. **Create a new root partition:**
   - Press `n` to create a new partition.
   - Choose `p` for a primary partition.
   - Enter the same partition number as the deleted root partition.
   - Specify the same starting sector as the deleted root partition.
   - Accept the default ending sector to use the remaining available space.
   - Press `w` to write the changes and exit `fdisk`.

5. **Reboot the system:**
```  
   sudo reboot
```
   - This step is necessary for the kernel to reload the new partition table.

6. **Resize the root partition's filesystem:**
   - After the system reboots, run the following command to resize the filesystem (replace 'X' and 'Y' with the appropriate letters and numbers for
