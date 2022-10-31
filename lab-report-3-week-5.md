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
The find shows all files (while excluding the directories) when searched on ./technical as an asterisk. It is especially useful when one would want to list only the files to be outputed to run additional commands on those files.

### -size \<N\>

### -exec \<cmd\>
For each of those options, give 3 examples of using it on files and directories from ./technical. Show each example as a code block that shows the command and its output, and write a sentence or two about what it’s doing and why it’s useful.

That makes 9 total examples, three each for three different command-line options. Many commands like these have pretty sophisticated behavior possible – it can take years to be exposed to and learn all of the possible tricks and inner workings.

To find information about the commands, a simple Web search like “find command-line options” will probably give decent results. There is also a built-in command on many systems called man (short for “manual”) that displays information about commands; you can use man grep, for example, to see a long listing of information about how grep works.
