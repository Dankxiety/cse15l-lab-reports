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
<br />

---

## `ls`

1. No arguments: `ls`
```
[user@sahara ~/lecture1]$ ls
Hello.class  Hello.java  messages  README
[user@sahara ~/lecture1]$
```
- Working Directory: `~/lecture1`
- The files `Hello.class`, `Hello.java`, and `README` and the directory **`messages`** were all printed to the terminal. These are all the files and directories within the `lecture1` directory. They were printed because the `ls` command with no arguments prints all the files and directories in the working directory.
- This output is not an error.
<br />

2. Directory as an argument: `ls messages`
```
[user@sahara ~/lecture1]$ ls messages
en-us.txt  es-mx.txt  is.txt  zh-cn.txt
[user@sahara ~/lecture1]$ 
```
- Working Directory: `~/lecture1`
- The files `en-us.txt`, `es-mx.txt`, `is.txt`, and `zh-cn.txt` were all printed to the terminal because these are the files in the `messages` directory. When `ls` is run with a directory as an argument, it prints all the files and directories within that directory.
- This output is not an error.
<br />

3. File as an argument: `ls Hello.class`
```
[user@sahara ~/lecture1]$ ls Hello.class
Hello.class
[user@sahara ~/lecture1]$ 
```
- Working Directory: `~/lecture1`
- Only the file `Hello.class` was printed because I used a file as an argument. If the `ls` command is run with a file as the argument, it will simply print that file.
- This output is not an error.
---
## `cat`
1. No arguments: `cat`
```
[user@sahara ~/lecture1]$ cat

```
- Working Directory: `~/lecture1`
- Nothing was printed, and the prompt did not appear again for me to continue using commands. If the `cat` command is used without arguments, it will print out anything inputted to the terminal. For example, this is what happens if I type `Hello world` into the terminal:
```
[user@sahara ~/lecture1]$ cat
Hello world
Hello world

```
- This output is not an error.
<br />

2. Directory as an argument: `cat messages`
```
[user@sahara ~/lecture1]$ cat messages
cat: messages: Is a directory
[user@sahara ~/lecture1]$ 
```
- Working Directory: `~/lecture1`
- The terminal printed an error message telling me that `messages` is a directory. This is because the `cat` command cannot print the contents of a directory.
- This output is an error. The `cat` command prints the contents of one or more files, but it could not perform its intended purpose because I used a directory as an argument instead of a file.
<br />

3. File as an argument: `cat README`
```
[user@sahara ~/lecture1]$ cat README
To use this program:

javac Hello.java
java Hello messages/en-us.txt
[user@sahara ~/lecture1]$
```
- Working Directory: `~/lecture1`
- The terminal printed the contents of the `README` file, which is in the `lecture1` directory. The `cat` command prints the contents of any files that are given as arguments.
- This output is not an error.
