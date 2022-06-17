# Super Grub2

1.  First we will need to download the Super Grub2 beta ISO from the official [website](https://www.supergrubdisk.org/super-grub2-disk/).

2.  Next flash the ISO to a flash drive:

    - On Windows:

      Use either [Rufus](https://rufus.ie/en/) or [BalenaEtcher](https://www.balena.io/etcher/).

    - On Linux:

      ```bash
      $ df

      Filesystem      Size  Used Avail Use% Mounted on
      dev              16G     0   16G   0% /dev
      run              16G  2.0M   16G   1% /run
      /dev/nvme1n1p2  921G   86G  789G  10% /
      tmpfs            16G   91M   16G   1% /dev/shm
      tmpfs            16G  3.8M   16G   1% /tmp
      /dev/nvme1n1p1  300M  288K  300M   1% /boot/efi
      tmpfs           3.2G   96K  3.2G   1% /run/user/1000
      /dev/usb_drive       3.8G  3.0G  821M  79% /run/media/.../USBDRIVE


      $ sudo dd if=file.iso of=/dev/usb_drive status=progress
      ```

3.  Reboot into the USB Drive.

    You might need to reoder your boot devices priority found in BIOS/UEFI settings.

    You can press `ESC/DEL/F12` etc to get into your BIOS/UEFI settings.

4.  Once you have booted in SuperGrub2, select show everything and find your Linux bootloader.

5.  Boot into your Linux bootloader.

&nbsp;

# Once you are in your linux machine.

1. Run this command:

   ```bash
   $ sudo grub-install --target=x86_64-efi --efi-directory=/boot/efi --bootloader-id=manjaro --recheck
   ```

   Replace `manjaro` with whatever you would like the boot-entry to be called.

2. Restart the computer and you should boot into GRUB.

3. Do check your UEFI/BIOS for HardDrive boot priority and ensure manjaro (or whatever your boot-entry is called) is top priority.
