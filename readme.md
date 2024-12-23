# move files across bind mounts

this is a missing feature in `coreutils-9.5`



## feature request

```
subject: mv: move files across bind mounts using the rename syscall
from: Milan Hauth <milahu@gmail.com>
to: coreutils@gnu.org
date: 2024-12-06 13:07 +01:00

currently mv fails to detect an identical filesystem
of source and destination file across bind mounts

instead of using the rename syscall
mv copies the file (to the same filesystem)
and then deletes the source file

obviously, this is not ideal:

- slow
- waste of disk space
- change of inode number
- unnecessary disk write operations (destructive)

> currently mv fails to detect an identical filesystem
> of source and destination file across bind mounts

this is possible using /proc/self/mountinfo
proof of concept:
https://github.com/milahu/move-files-across-bind-mounts

related:
https://serverfault.com/questions/327447
https://unix.stackexchange.com/questions/406351
https://unix.stackexchange.com/questions/380025
```



## related

- [mount --bind and moving 2 files between mounts](https://serverfault.com/questions/327447/mount-bind-and-moving-2-files-between-mounts)
- [Mount --bind in the same filesystem move files as in the same filesystem](https://unix.stackexchange.com/questions/406351/mount-bind-in-the-same-filesystem-move-files-as-in-the-same-filesystem)
- [Why can't I create a `hardlink` to a file from a "mount --bind" directory on the same filesystem?](https://unix.stackexchange.com/questions/380025/why-cant-i-create-a-hardlink-to-a-file-from-a-mount-bind-directory-on-the)
