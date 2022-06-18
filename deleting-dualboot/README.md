#### Note: This document is assuming that you would like to delete Linux from your dual boot setup.

&nbsp;

# Boot into Windows

1. Open up a `Terminal` as administrator:

   ```
   $ bcdedit
   ```

   This will display a list of the boot entries that your machine has.

2. Save a backup of your current boot entries (optional):

   ```
   $ bcdedit /export D:some\path\bcdedit_backup.exe
   ```

   Note: If something goes wrong later you can run this command to restore from the backup file.

   ```
   $ bcdedit /import D:path\to\bcdedit_backup.exe
   ```

3. Find the boot entry of the Linux system:

   `WARNING: Make sure you confirm that it is the correct boot entry!`
   Take note of the identifier.

   Run this command, replacing `$IDENTIFIER` with the one you copied.

   ```
   $ bcdedit /delete $IDENTIFIER
   ```

4. Open up Drive Management.

   Delete all partitions related to the Linux operating system.

   You may choose to extend the current partitions to reclaim back the unallocated space.

5. Restart your machine.

   You should boot into Windows directly now.

   (Assuming you don't have any other Linux installations on your machine)
