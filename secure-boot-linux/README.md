# Installing shim-signed:

- Arch-based distro:

  You can install `shim-signed` as an `AUR` package through your package manager.

&nbsp;

# Setting up boot entries:

1. Rename current bootloader to `grubx64.efi`

   In my case, my bootloader can be found at `/boot/efi/EFI/boot/bootx64.efi`

   ```bash
   $ mv /boot/efi/EFI/boot/bootx64.efi /boot/efi/EFI/boot/grubx64.efi
   ```

2. Copy `shim` and `MokManager` to the bootloader directory.

   When copying `shim` over, rename it to `bootx64.efi` or whatever the old bootloader was called.

   In my case, my bootloader directory is at `/boot/efi/EFI/boot/`.\
   Shim-signed files can be found at `'/usr/share/shim-signed/`.

   ```bash
   $ cp /usr/share/shim-signed/shimx64.efi /boot/efi/EFI/boot/bootx64.efi
   $ cp /usr/share/shim-signed/mmx64.efi /boot/efi/EFI/boot/
   ```

3. Find where your `EFI` partition is mounted at.

   ```bash
   $ fdisk -l

   Disk /dev/nvme1n1: 953.87 GiB, 1024209543168 bytes, 2000409264 sectors
   Disk model: INTEL SSDPEKNW010T9
   Units: sectors of 1 \* 512 = 512 bytes
   Sector size (logical/physical): 512 bytes / 512 bytes
   I/O size (minimum/optimal): 512 bytes / 512 bytes
   Disklabel type: gpt
   Disk identifier: 650C2806-7AC5-6740-9E0E-4F4FCE46FD6

   Device Start End Sectors Size Type
   /dev/nvme1n1p1 4096 618495 614400 300M EFI System
   /dev/nvme1n1p2 618496 1964329543 1963711048 936.4G Linux filesystem
   /dev/nvme1n1p3 1964329544 2000397734 36068191 17.2G Linux swap

   Disk /dev/nvme0n1: 953.87 GiB, 1024209543168 bytes, 2000409264 sectors
   Disk model: INTEL SSDPEKNW010T9
   Units: sectors of 1 \* 512 = 512 bytes
   Sector size (logical/physical): 512 bytes / 512 bytes
   I/O size (minimum/optimal): 512 bytes / 512 bytes
   Disklabel type: gpt
   Disk identifier: 0E176B91-CC31-4E7E-9AC5-9DB9A8AC0E23

   Device Start End Sectors Size Type
   /dev/nvme0n1p1 2048 206847 204800 100M EFI System
   /dev/nvme0n1p2 206848 239615 32768 16M Microsoft reserved
   /dev/nvme0n1p3 239616 1999049356 1998809741 953.1G Microsoft basic data
   /dev/nvme0n1p4 1999050752 2000402431 1351680 660M Windows recovery environment

   Disk /dev/sda: 298.09 GiB, 320072933376 bytes, 625142448 sectors
   Disk model: SAMSUNG HM320JI
   Units: sectors of 1 \* 512 = 512 bytes
   Sector size (logical/physical): 512 bytes / 512 bytes
   I/O size (minimum/optimal): 512 bytes / 512 bytes
   Disklabel type: dos
   Disk identifier: 0xb9fc5ecc
   ```

   In my case my EFI parititon is mounted at `/dev/nvme1n1p1`.

4. Create a new NVRAM entry:

   ```bash
   $ efibootmgr --verbose --disk /dev/sdX --part Y --create --label "Shim" --loader /boot/efi/EFI/boot/bootx64.efi

   Replace /dev/sd`X` and --part `Y` with the information from step (3).
   ```

5. Enable Secure-Boot in BIOS.

   This step is dependent on your motherboard.

   Do google how to do it for your motherboard.

   If possible disable CSM support too.

6. Enroll the keys with MOK Manager.

   When you first boot, it should display a "Verification failed: Access is denied" message of sorts.

   Press "OK" followed by any key to begin enrolling keys.

   6.1. Choose `Enroll hash from disk` > ... > `EFI` > `BOOT` > `grubx64.efi` > Continue > Yes

   6.2. Choose `Enroll hash from disk` > ... > `EFI` > `BOOT` > `bootx64.efi` > Continue > Yes

   6.3. `Continue boot`

7. If all went well, you should now be able to dual=boot with secure-boot enabled.

## References:

- [Arch wiki](ttps://wiki.archlinux.org/title/Unified_Extensible_Firmware_Interface/Secure_Boot#shim)
- [Steps in video form](https://www.youtube.com/watch?v=RVkCIc8CzR8)
- [Enrolling keys with MOK Manager](https://www.youtube.com/watch?v=Ljbagg4iXq4&t=0s)
