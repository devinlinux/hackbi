# Basics
## File Hierarchy Standard (FHS)
| Path   | Content                             |
| ------ | ----------------------------------- |
| /bin   | Binaries (User)                     |
| /boot  | Static boot loader files            |
| /etc   | Host specific configs               |
| /lib   | Shared libraries and kernel modules |
| /sbin  | Binaries (System/root)              |
| /var   | Varying files (e.g. Logs)           |
| /usr   | 3rd party software                  |
| /proc  | Pseudo file system                  |
| /sys   | Pseudo file system                  |
| /mnt   | Mountpoint for internal drives      |
| /media | Mountpoint for external drives      |
| /home  | User homes                          |
| /run   | PID files of running processes      |

## Commands
**File System Commands**

| Command | Param            | Description                                       |
| ------- | ---------------- | ------------------------------------------------- |
| `cd`    | `-`              | Navigate to last dir                              |
|         | `~`              | Navigate to home                                  |
|         | `~username`      | Navigate to home of specified user                |
| `pwd`   |                  | Print working dir                                 |
| `ls`    |                  | Print dir content                                 |
|         | `-l`             | Format as list                                    |
|         | `-a`             | Show hidden items (`-A` without `.` and `..`)     |
|         | `-r`             | Invert order                                      |
|         | `-R`             | Recurse                                           |
|         | `-S`             | Sort by size                                      |
|         | `-t`             | Sort by date modified                             |
| `mkdir` | `-p`             | Create dir with parents                           |
| `cp`    | `-r`             | Copy dir                                          |
| `rmdir` | `-p`             | Remove dir and empty parents                      |
| `rm`    | `-rf`            | Remove dir recursively, `-f` without confirmation |
| `mv`    |                  | Move recursively                                  |
| `find`  | `-iname pattern` | Search dir/file case-insensitive                  |
|         | `-mmin n`        | Last modified n minutes ago                       |
|         | `-mtime n`       | Last modified n days ago                          |
|         | `-regex pattern` | Path matches pattern                              |
|         | `-size n[kMG]`   | By file size (`-n` less than; `+n` greater than)  |
|         | `! searchparams` | Invert search                                     |

**File Manipulation**

| Command | Param                                      | Description                                |
| ------- | ------------------------------------------ | ------------------------------------------ |
| `cat`   | `file`                                     | Print content                              |
| `tac`   | `file`                                     | Print content inverted                     |
| `sort`  | `file`                                     | Print sorted                               |
|         | `file -r -u`                               | Print sorted descending without dublicates |
| `wc`    | `file`                                     | Count Lines, Words, Chars (Bytes)          |
| `head`  | `-n10 file | tail -n5`                     | Print lines 5-10                           |
| `tail`  | `-f file`                                  | Print new lines automatically              |
| `cut`   | `-f -4,7-10,12,15- file`                   | Print selected fields (tab delimited)      |
|         | `-c -4,7-10,12,15- file`                   | Print selected characters positions        |
|         | `-f 2,4 -d, --output-delimiter=$'\t' file` | Change delimiter (but use tab for output)  |
| `uniq`  | `file`                                     | Hide consecutive identical lines           |
|         | `file -c`                                  | Show consecutive identical line count      |
|         | `file -u`                                  | Hide consecutive identical lines           |
| `file`  | `file`                                     | Get file type                              |

**Archiving**

| Command          | Param                            | Beschreibung                                             |
| ---------------- | -------------------------------- | -------------------------------------------------------- |
| `tar`            | `cfv archiv.tar file1 file2`     | Archiv erstellen / Inhalt hinzufügen oder überschreiben  |
|                  | `tfv archiv.tar`                 | Inhalt anzeigen                                          |
|                  | `xf archiv.tar [-C ~/extracted]` | Archiv (nach ~/extracted) entpacken (und dekomprimieren) |
|                  | `cfvj archiv.tar.bz2 file`       | bzip2 komprimiertes Archiv erstellen                     |
|                  | `cfvz archiv.tar.gz file`        | gzip komprimiertes Archiv erstellen                      |
|                  | `cfa archiv.tar.[komp] file`     | komprimiertes Archiv erstellen (auto Typ anhand Name)    |
| `bzip2` / `gzip` | `file1 file2`                    | Dateien (einzeln) komprimieren                           |
|                  | `-d file1 file2`                 | Dateien dekomprimieren                                   |

**Other**

| Command     | Param           | Beschreibung                               |
| ----------- | --------------- | ------------------------------------------ |
| `<command>` | `--help`        | Help of current command (not standardized) |
|             | `-h`            |                                            |
|             | `-?`            |                                            |
| `man`       | `<command>`     | Manual page of command                     |
|             | `-k keyword`    | Search command by keyword (oder `apropos`) |
| `alias`     |                 | Show aliases                               |
|             | `name='befehl'` | Create alias                               |

## Globs (Wildcards)
The dot `.` in front of hidden items is ignored by glob patterns!

| Character | Description             |
| --------- | ----------------------- |
| `?`       | Any single character    |
| `*`       | Any characters          |
| `[ac-e]`  | 1 character in enum     |
| `[!ac-e]` | 1 character not in enum |

## Regex
Bash itself does not know regex. Use programs like `grep`, `sed`, `awk`.

**Steuerzeichen**

| Character      | Description             |
| -------------- | ----------------------- |
| `.`            | Any single character    |
| `[ac-e]`       | 1 character in enum     |
| `[^ac-e]`      | 1 character not in enum |
| `^`            | Start of string         |
| `$`            | End of string           |
| `\d`           | Digit                   |
| `\D`           | Not a digit             |
| `\s`           | Whitespace              |
| `\S`           | Not a Whitespace        |
| `\<`           | Start of word           |
| `\>`           | End of word             |
| `pattern?`     | Quantifier 0 or 1       |
| `pattern*`     | Quantifier 0..n         |
| `pattern+`     | Quantifier 1..n         |
| `pattern{x}`   | Quantifier exactly x    |
| `pattern{x,}`  | Quantifier x..n         |
| `pattern{x,y}` | Quantifier x..y         |
| `pattern{,y}`  | Quantifier 0..y         |

**Grep**

| Command | Param             | Description    |
| ------- | ----------------- | -------------- |
| `grep`  | `pattern file`    | Extended Regex |
|         | `-E pattern file` | Extended Regex |
|         | `-v pattern file` | Invert match   |
|         | `-w pattern file` | Word match     |
|         | `-i pattern file` | Ignore case    |


## Stream redirection
- `>` overwrite
- `>>` append

| Character             | Description                     |
| --------------------- | ------------------------------- |
| `> file` or `1> file` | STDOUT to file                  |
| `< file`              | Datei to STDIN                  |
| `2> file`             | STDERR to file                  |
| `2>&1`                | STDERR to same target as STDOUT |
| `> file 2>&1`         | STDOUT and STDERR to file       |

# Disk and File System Management

## General Disk Manipulation (non-LVM)
Creating physical partitions is **not required**! You can create PVs directly!

| Command                                     | Description                          |
| ------------------------------------------- | ------------------------------------ |
| `fdisk -l`                                  | List physical disks and partitions   |
| `fdisk /dev/sdb`<br>`n`                     | Create new partition                 |
| `fdisk /dev/sdb`<br>`t`<br>`8e`             | Change partition type to *Linux LVM* |
| `mkfs.xfs /dev/myVG/myVol`                  | Format LV with XFS                   |
| `mkfs.ext4 -f /dev/myVG/myVol`              | Format LV with EXT4 (overwrite)      |
| `blkid /dev/myVG/myVol`                     | Show UUID and formatting of volume   |
| `mount`                                     | Show what is mounted where           |
| `mount -t ext4 /dev/myVG/myVol /mountpoint` | Mount LV to /mountpoint              |
| `umount /dev/myVG/myVol`                    | Unmount LV from /mountpoint          |
| `umount /mountpoint`                        | Unmount LV from /mountpoint          |
| `mount -a`                                  | Mount as configured in /etc/fstab    |
| `df`                                        | Show disk usage                      |
| `xfs_growfs /dev/myVG/myVol`                | Resize xfs filesystem                |
| `resize2fs /dev/myVG/myVol`                 | Resize ext3/4 filesystem             |

# Automatic mounting (/etc/fstab)
Example:

| file system                               | mount point | type | option                           | dump | pass |
| ----------------------------------------- | ----------- | ---- | -------------------------------- | ---- | ---- |
| /dev/sdb1                                 | /myDir1     | ext4 | defaults                         | 0    | 0    |
| /dev/mapper/myVG-myVol                    | /myDir2     | xfs  | defaults                         | 0    | 0    |
| UUID=a924e3de-0414-4228-86bf-b65a4c8ff8ab | /myDir3     | xfs  | defaults                         | 0    | 0    |
| /dev/mapper/myVG-swap                     | swap        | swap | defaults                         | 0    | 0    |
| 192.168.1.1:/shared                       | /targetdir  | nfs  | async                            | 0    | 0    |
| //server/share                            | /targetdir  | cifs | credentials=/root/cifs/.username | 0    | 0    |

Column **dump** configures file system for backup with *dump* (program).

Column **pass** configures order of file system check during boot. `0` means no check.

# Text Readers & Editors
## Less
| Command             | Description                     |
| ------------------- | ------------------------------- |
| `q`                 | Quit                            |
| `R`                 | Refresh content                 |
| `F`                 | Auto scroll                     |
| `g number`          | Go to line                      |
| `m lowercaseLetter` | Mark line                       |
| `' lowercaseLetter` | Go to mark                      |
| `/pattern`          | Search forward                  |
| `?pattern`          | Search backward                 |
| `n`                 | Next search result              |
| `N`                 | Last search result              |
| `ESC u`             | Remove highlighting from search |

## VI
**Editing**

To leave editing mode press `ESC`.

| Command   | Description           |
| --------- | --------------------- |
| `i`       | insert before cursor  |
| `a`       | insert after cursor   |
| `A`       | insert at end of line |
| `o`       | new line below        |
| `O`       | new line above        |
| `u`       | undo                  |
| `.`       | repeat last command   |
| `yy`      | copy line             |
| `5yy`     | copy 5 lines          |
| `p`       | paste below           |
| `P`       | paste above           |
| `x`       | delete character      |
| `5x`      | delete 5 characters   |
| `dd`      | delete line           |
| `5dd`     | delete 5 lines        |
| `:10,20d` | delete lines 10-20    |
| `d0`      | delete to line begin  |
| `d$`      | delete to line end    |

**Navigation**

Navigate as usual with `arrow keys`, `home`, `end`, `pg up`, `pg dn`.

| Command | Description            |
| ------- | ---------------------- |
| `5G`    | go to line 5           |
| `H`     | go to top of screen    |
| `M`     | go to middle of screen |
| `L`     | go to end of screen    |
| `5w`    | move over 7 words      |
| `5b`    | move back 5 words      |

**Other**

| Command     | Description                  |
| ----------- | ---------------------------- |
| `/foo`      | search forward               |
| `?foo`      | search backwards             |
| `n`         | repeat search                |
| `:w`        | save                         |
| `:q`        | close                        |
| `:wq`       | save and close               |
| `:q!`       | close without saving         |
| `:!command` | run bash command             |
| `:r foo`    | read file foo into this file |


# User and Group Management
**UID**

| UID   | Type           |
| ----- | -------------- |
| <1000 | system account |
| >1000 | user account   |

**User Database**

User info without passwords is stored in `/etc/passwd`.

| username | PW  | UID  | GID  | Kommentar | HOME        | SHELL     |
| -------- | --- | ---- | ---- | --------- | ----------- | --------- |
| hfict    | x   | 1000 | 1000 |           | /home/hfict | /bin/bash |

**Group Database**

Group info with secondary group members are stored in `/etc/group`.
Primary group members are identified by GID in user database.

| groupname | PW  | GID | Users       |
| --------- | --- | --- | ----------- |
| wheel     | x   | 10  | hfict,user2 |

**Password Database**

Hashed user passwords are stored in `/etc/shadow`.
Password encryption is configured in `/etc/login.defs`.

| username | PW     | Last PW change | Minimum | Maximum | Warn | Inactive | Expire |
| -------- | ------ | -------------- | ------- | ------- | ---- | -------- | ------ |
| hfict    | [hash] | 17803          | 0       | 99999   | 7    |          |        |

PW:
- `[hash]` Verschlüsseltest Passwort
- `![hash]` Account Gesperrt
- `!!` oder `*` Account gesperrt, kein Passwort gesetzt

**Commands**

| Command    | Param                                          | Beschreibung                                             |
| ---------- | ---------------------------------------------- | -------------------------------------------------------- |
| `id`       | `username`                                     | ID und Gruppen eines Benutzers anzeigen                  |
| `who`      |                                                | Angemeldete Benutzer anzeigen                            |
| `last`     |                                                | Letzte Logins anzeigen                                   |
| `lastb`    |                                                | Letzte fehlgeschlagene Logins anzeigen                   |
| `sudo`     | `-u user command`                              | Befehl mit Rechten von user ausführen (Default ist root) |
|            | `-i` oder `su -`                               | Shell mit root Rechten                                   |
| `su`       |                                                | Shell als root (non-login shell)                         |
|            | `-`                                            | Shell als root (login shell)                             |
|            | `- user`                                       | Shell als user                                           |
| `useradd`  | ` -u 2101 -g primarygroup -c comment username` | Benutzer anlegen (ohne `-g` wird neue Gruppe erstellt)   |
| `usermod`  | `-G group1,group2`                             | Sekundärgruppen definieren (überschreiben)               |
|            | `-aG group,group2`                             | Sekundärgruppen hinzufügen                               |
|            | `-l username`                                  | Benutzernamen ändern                                     |
|            | `-L`                                           | Lock Account                                             |
|            | `-U`                                           | Unlock Account                                           |
|            | `-s shellpath`                                 | Shell ändern                                             |
| `userdel`  | `-r username`                                  | Benutzer inkl. Home und Mail-Spool löschen               |
| `passwd`   | `username`                                     | Passwort ändern (interaktiv)                             |
| `groupadd` | `groupname`                                    | Gruppe anlegen (Optional mit `-g` GID setzen)            |
| `groupdel` | `groupname`                                    | Gruppe löschen                                           |

# File System Permissions
Permissions can be set on:
- User (owner)
- Group (owner)
- Others

Only root can change *User*. *User* can change *Group*.

Basic permissions (Add binary flags to combine):

| Char | Binary Flag | Permission |
| ---- | ----------- | ---------- |
| r    | 4           | read       |
| w    | 2           | write      |
| x    | 1           | execute    |

Advanced permissions (place in front of basic permissions: `chmod 1777 shared`).:

| Char  | Binary Flag | Name       | Description                                                                |
| ----- | ----------- | ---------- | -------------------------------------------------------------------------- |
| t / T | 1           | Sticky Bit | *Others* can't delete content (only applicable for directories)            |
| s / S | 2           | SGID-Bit   | File: run with permissions of *Group*<br>Dir: New elements inherit *Group* |
| s / S | 4           | SUID-Bit   | File is run with permissions of *User* (only applicable for files)         |

Advanced permissions replace the **x** when using `ls -l`. Lower case if **x** is set, upper case if **x** is not set.

*Read* permission on a directory only allows to see the directory itself but not it's contents. Use *execute* permission to show contents.

**Commands**

| Command   | Param                    | Beschreibung                                      |
| --------- | ------------------------ | ------------------------------------------------- |
| `chmod`   | `-R [uog] dirname`       | Set permissions recursively using binary flags    |
|           | `+[suog] filename`       | Add permissions using binary flags                |
|           | `-[suog] filename`       | Remove permissions using binary flags             |
|           | `u+x filename`           | Add *execute* permission for *User*               |
|           | `g+wx filename`          | Add *write* and *execute* permissions for *Group* |
|           | `o-r filename`           | Remove *read* permission for *Others*             |
| `chown`   | `-R user:group filename` | Change owner (*User* & *Group*) recursively       |
|           | `user filename`          | Change owner (*User*)                             |
|           | `:group filename`        | Change owner (*Group*)                            |
| `chgroup` | `group filename`         | Change owner (*Group*)                            |

# SSH
Configuration is done in `/etc/ssh/sshd_config`.

Reload SSH service with `systemctl reload sshd` to apply changes!

DenyUsers, AllowUsers, DenyGroups, AllowGroups override each other and are applied in the order listed above.

| Config            | Option             | Description                                   |
| ----------------- | ------------------ | --------------------------------------------- |
| `PermitRootLogin` | `no`               | Deny root to login via SSH                    |
|                   | `yes`              | Allow root to login via SSH                   |
|                   | `without-password` | Allow only with private/public key auth       |
| `AllowUsers`      | `user1 user2`      | Allow only user1 and user2                    |
| `DenyUsers`       | `user1 user2`      | Allow all users but user1 and user2           |
| `AllowGroups`     | `group1 group2`    | Allow only users from specified groups        |
| `DenyGroups`      | `group1 group2`    | Allow all users but those in specified groups |

# IPv6 (disable)
Change the *grub* config `/etc/default/grub` to disalbe IPv6.
1. Add `ipv6.disable=1` to the `GRUB_CMDLINE_LINUX` property.
   e.g. `GRUB_CMDLINE_LINUX="ipv6.disalbe=1 crashkernel=auto rd.lvm.lv=centos/root rd.lvm.lv=centos/swap biosdevname=0 net.ifnames=0 rhgb quiet"`
2. Recreate grub config with `grub2-mkconfig -o /boot/grub2/grub.cfg`
3. Reboot the system with `init 6` or `shutdown -r now`

# Package Management
## Pacman
| Command                  | Description                         |
|--------------------------| ----------------------------------- |
| `pacman -S packagename`  | Install package                     |
| `pacman -R packagename`  | Uninstall package                   |
| `pacman -Qi packagename` | Check if package is installed       |
| `pacman -Q packagename`  | List all installed packages         |