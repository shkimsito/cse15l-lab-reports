# Researching Commands

## `find`
### -type
Type option specifies whether the path should search for file, directory, symlink or device files.
The type is specified as, f or d or l or c or s, which each signifies file/directory/link/device/socket respectively.

```
**chris@Chriss-MacBook-Air technical % find * -type d**
911report
biomed
government
government/About_LSC
government/Env_Prot_Agen
government/Alcohol_Problems
government/Gen_Account_Office
government/Post_Rate_Comm
government/Media
plos
```
The find shows directories only when searched on `./technical` as an asterisk. This is useful when one is trying to see what types of directories are listed under the path while removing all the noisy outputs with paths with many files such as the `/technical`.

```
chris@Chriss-MacBook-Air technical % find ?????? -type d
biomed
```
On the otherhand if I wanted to search for a specific directory that is n-length long, I could just use the commandline patterns (six question marks in the example) to specify how length I'm looking for and let `find` output all directories of that length.

```
chris@Chriss-MacBook-Air technical % find * -type f
911report/chapter-13.4.txt
911report/chapter-13.5.txt
911report/chapter-13.1.txt
911report/chapter-13.2.txt
911report/chapter-13.3.txt
911report/chapter-3.txt
911report/chapter-2.txt
911report/chapter-1.txt
911report/chapter-5.txt
911report/chapter-6.txt
...
```
The example shows all files (while excluding the directories) when searched on `./technical` as an asterisk. It is especially useful when one would want to list only the files to be outputed to run additional commands on those files.

### -size \<N\>
The size option specifies path size of exactly N, or at least N if appended by plus sign, at most N if appended by minus sign. The default unit is in 512 byte blocks, but unit can be changed with added suffixes as k for kilobytes, M for megabytes and G for gigabytes.

```
```

```
```

```
```

### -exec \<cmd\>
The execute option executes the command on the list of files returned by find.

```
```

```
```

```
```


---
**References**: https://man7.org/linux/man-pages/man1/find.1.html
