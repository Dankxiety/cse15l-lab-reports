# Lab Report 1 - 11 Jan 2024
## `cd`
1. No arguments: `cd`
```
[user@sahara ~/lecture1]$ cd
[user@sahara ~]$
```
- Working Directory: `~/lecture1`
- No output was printed, but the working directory changed from `~/lecture1` to `~`. This is because running `cd` with no arguments returns the terminal to the home directory.
- The output is not an error.
<br />

2. Directory as an argument: `cd messages`
```
[user@sahara ~/lecture1]$ cd messages
[user@sahara ~/lecture1/messages]$
```
- Working Directory: `~/lecture1`
- Again, no output was printed, but the working directory changed from `~/lecture1` to `~/lecture1/messages`. Running `cd messages` moved the terminal from the `lecture` directory to the `messages` folder contained inside `lecture`.
- The output is not an error.
<br />

3. File as an argument: `cd Hello.java`
```
[user@sahara ~/lecture1]$ cd Hello.java
bash: cd: Hello.java: Not a directory
[user@sahara ~/lecture1]$ 
```
- Working Directory: `~/lecture1`
- The terminal printed an error message telling me that `Hello.java` is not a directory and stayed in the `~/lecture1` directory because it could not change the working directory to a file.
- This output is an error. The `cd` command is supposed to change the working directory, but since I inputted a file and not a directory, it could not change the working directory to the argument I inputted.
