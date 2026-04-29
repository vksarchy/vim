
LUKS ENCRYPTED PENDRIVE — README
=================================

WHAT IS LUKS?
-------------
LUKS is a Linux encryption standard. Your pendrive's data is scrambled
and unreadable without your passphrase. If someone steals it, they see
garbage — not your files.

The chain works like this:
  /dev/sda1  →  /dev/mapper/luks-...  →  /mnt/luks/luks-.../
  (pendrive)    (unlocked virtual        (where you access
  encrypted     device after             your files)
  garbage)      passphrase entry)


HOW TO MOUNT (UNLOCK)
----------------------
Using the script:
  sudo ~/.config/scripts/manage_encrypted_drives open

Manually (on any Linux machine without the script):
  sudo cryptsetup luksOpen /dev/sda1 pendrive
  sudo mount /dev/mapper/pendrive /mnt/


HOW TO UNMOUNT (LOCK)
----------------------
Using the script:
  sudo ~/.config/scripts/manage_encrypted_drives close

Manually:
  sudo umount /mnt/
  sudo cryptsetup luksClose pendrive


CHECK STATUS
-------------
  sudo ~/.config/scripts/manage_encrypted_drives status
  sudo ~/.config/scripts/manage_encrypted_drives list


COPY FILES
-----------
  cp ~/somefile.txt /mnt/luks/pendrive/
  cp -r ~/somefolder/ /mnt/luks/pendrive/


ON WINDOWS
-----------
Windows does not understand LUKS. It will say "disk needs formatting".
DO NOT FORMAT. Use LibreCrypt (free) to open it on Windows:
  https://github.com/t-d-k/LibreCrypt


ON ANOTHER LINUX (no script, no desktop)
-----------------------------------------
  sudo cryptsetup luksOpen /dev/sda1 pendrive   # unlock
  sudo mount /dev/mapper/pendrive /mnt/          # mount
  sudo umount /mnt/                              # unmount
  sudo cryptsetup luksClose pendrive             # lock


ON LINUX DESKTOP (GNOME/KDE)
------------------------------
Plug in the pendrive → a popup will ask for passphrase → type it → done.
No terminal needed.


IMPORTANT WARNINGS
-------------------
- If you forget your passphrase, data is GONE FOREVER. No recovery possible.
- Always lock (close) before unplugging.
- Never click "Format" when Windows asks — that wipes your encrypted data.
