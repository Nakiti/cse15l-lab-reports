# Lab Report 1 - Remote Access and File System
## `cd`
**No Arguments**
```
[user@sahara ~/lecture1]$ cd
[user@sahara ~]$
```
- Prior to running the `cd` command, the working directory was `/lecture`
- When the `cd` command was run with no arguments, the working directory went to the `/home` directory. This occurred because `cd` changes the directory to `/home` by default when it is provided with no arguments.
- The output of this command was not an error.


**Path to a Directory as the Argument**
  
  ```
  [user@sahara ~/lecture1]$ cd messages
  [user@sahara ~/lecture1/messages]$
  ```
- Prior to running the `cd` command, the working directory was `/lecture`
- When the `cd` command was run with the directory path `/messages` as the argument, the working directory went to the `/lecture1/messages` directory. This occured because the `cd` command changes the directory to that which matches the argument provided. In this instance, since the working directory was already `/lecture1` as opposed so the `/home` directory, the cd command only looked for matches within the `/lecture1` directory.
- The output of this command was not an error.

**Path to a File as the Argument**
```
[user@sahara ~/lecture1/messages]$ cd en-us.txt
bash: cd: en-us.txt: Not a directory
[user@sahara ~/lecture1/messages]$
```
- Prior to running the `cd` command, the working directory was `/lecture1/messages`
- When the `cd` command was run with the `en-us.txt` as the argument, the program returned `bash: cd: en-us.txt: Not a directory` and stayed in the current working directory. This occured because `cd` is built to change between directories and as the argument provided was a text file, it was unable to do so.
- The output of this command was an error because the `cd` command is not meant to handle files.
  
  
