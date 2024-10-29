This file explains how to create a backup image of the Raspberry pi MicroSD Card. This should be done to quickly rollback to a previously known working state.
There are premade backup images for the Pi inside the Images folder. TMWA requires a 16GB sdcard, TMWB requires a 8GB sdcard.

Backup Instructions linux:
- 1. Plug in sd card.
- 2. Open a terminal.
- 3. Use command sudo: fdisk -l 
- 4. Find name of SDCard (E.g. /dev/sda, /dev/sdb etc.). Be 100% sure that the name is correct and belongs to the SDCard.
- 5. Use following command to create image: sudo dd if=/dev/[SDCARD NAME] of=[BACKUP FILE PATH] status=progress
-    (e.g. sudo dd if=/dev/sdb of=~/TAMARIWBackups/TMWBackup2 status=progress) Tip: Use ~/ for file path in reference to user.

Restore Instrcutions linux:
- 1. Plug in sd card.
- 2. Open a terminal.
- 3. Use command sudo: fdisk -l 
- 4. Find name of SDCard (E.g. /dev/sda, /dev/sdb etc.). Be 100% sure that the name is correct and belongs to the SDCard. Incorrect name could lead to file loss on host machine.
- 5. Use following command to create image: sudo dd of=/dev/[SDCARD NAME] if=[BACKUP FILE PATH] status=progress
-    (e.g. sudo dd of=/dev/sdb if=~/TAMARIWBackups/TMWBackup2 status=progress) Tip: Use ~/ for file path in reference to user.
