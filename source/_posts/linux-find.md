---
title: linux-find
date: 2018-04-19 12:52:33
categories:
  - linux
tags:
  - linux
  - shell
  - command
---

The Linux **Find Command** is one of the most important and much used command in Linux sytems. Find command used to search and locate list of files and directories based on conditions you specify for files that match the arguments. Find can be used in variety of conditions like you can find files by **permissions**, **users**, **groups**, **file type**, **date**, **size** and other possible criteria.

Through this article we are sharing our day-to-day Linux find command experience and its usage in the form of examples. In this article we will show you the most used **35 Find Commands** examples in Linux. We have divided the section into **Five** parts from basic to advance usage of find command.

1. **Part I**: Basic Find Commands for Finding Files with Names
2. **Part II**: Find Files Based on their Permissions
3. **Part III**: Search Files Based On Owners and Groups
4. **Part IV**: Find Files and Directories Based on Date and Time
5. **Part V**: Find Files and Directories Based on Size
6. **Part VI**: [Find Multiple Filenames in Linux](https://www.tecmint.com/linux-find-command-to-search-multiple-filenames-extensions/)

**Part I – Basic Find Commands for Finding Files with Names**

#### 1. Find Files Using Name in Current Directory

Find all the files whose name is **tecmint.txt** in a current working directory.

```
# find . -name tecmint.txt
./tecmint.txt
```

#### 2. Find Files Under Home Directory

Find all the files under **/home** directory with name **tecmint.txt**.

```
# find /home -name tecmint.txt
/home/tecmint.txt
```

#### 3. Find Files Using Name and Ignoring Case

Find all the files whose name is **tecmint.txt** and contains both capital and small letters in **/home** directory.

```
# find /home -iname tecmint.txt
./tecmint.txt
./Tecmint.txt
```

#### 4. Find Directories Using Name

Find all directories whose name is **Tecmint** in **/** directory.

```
# find / -type d -name Tecmint
/Tecmint
```

#### 5. Find PHP Files Using Name

Find all **php** files whose name is **tecmint.php** in a current working directory.

```
# find . -type f -name tecmint.php
./tecmint.php
```

#### 6. Find all PHP Files in Directory

Find all **php** files in a directory.

```
# find . -type f -name "*.php"
./tecmint.php
./login.php
./index.php
```

**Part II – Find Files Based on their Permissions**

#### 7. Find Files With 777 Permissions

Find all the files whose permissions are **777**.

```
# find . -type f -perm 0777 -print
```

#### 8. Find Files Without 777 Permissions

Find all the files without permission **777**.

```
# find / -type f ! -perm 777
```

#### 9. Find SGID Files with 644 Permissions

Find all the **SGID bit** files whose permissions set to **644**.

```
# find / -perm 2644
```

#### 10. Find Sticky Bit Files with 551 Permissions

Find all the **Sticky Bit** set files whose permission are **551**.

```
# find / -perm 1551
```

#### 11. Find SUID Files

Find all **SUID** set files.

```
# find / -perm /u=s
```

#### 12. Find SGID Files

Find all **SGID** set files.

```
# find / -perm /g=s
```

#### 13. Find Read Only Files

Find all **Read Only** files.

```
# find / -perm /u=r
```

#### 14. Find Executable Files

Find all **Executable** files.

```
# find / -perm /a=x
```

#### 15. Find Files with 777 Permissions and Chmod to 644

Find all **777** permission files and use **chmod** command to set permissions to **644**.

```
# find / -type f -perm 0777 -print -exec chmod 644 {} \;
```

#### 16. Find Directories with 777 Permissions and Chmod to 755

Find all **777** permission directories and use **chmod** command to set permissions to **755**.

```
# find / -type d -perm 777 -print -exec chmod 755 {} \;
```

#### 17. Find and remove single File

To find a single file called **tecmint.txt** and remove it.

```
# find . -type f -name "tecmint.txt" -exec rm -f {} \;
```

#### 18. Find and remove Multiple File

To find and remove multiple files such as **.mp3** or **.txt**, then use.

```
# find . -type f -name "*.txt" -exec rm -f {} \;
OR
# find . -type f -name "*.mp3" -exec rm -f {} \;
```

#### 19. Find all Empty Files

To find all empty files under certain path.

```
# find /tmp -type f -empty
```

#### 20. Find all Empty Directories

To file all empty directories under certain path.

```
# find /tmp -type d -empty
```

#### 21. File all Hidden Files

To find all hidden files, use below command.

```
# find /tmp -type f -name ".*"
```

**Part III – Search Files Based On Owners and Groups**

#### 22. Find Single File Based on User

To find all or single file called **tecmint.txt** under **/** root directory of owner root.

```
# find / -user root -name tecmint.txt
```

#### 23. Find all Files Based on User

To find all files that belongs to user **Tecmint** under **/home** directory.

```
# find /home -user tecmint
```

#### 24. Find all Files Based on Group

To find all files that belongs to group **Developer** under **/home** directory.

```
# find /home -group developer
```

#### 25. Find Particular Files of User

To find all **.txt** files of user **Tecmint** under **/home** directory.

```
# find /home -user tecmint -iname "*.txt"
```

**Part IV – Find Files and Directories Based on Date and Time**

#### 26. Find Last 50 Days Modified Files

To find all the files which are modified **50** days back.

```
# find / -mtime 50
```

#### 27. Find Last 50 Days Accessed Files

To find all the files which are accessed **50** days back.

```
# find / -atime 50
```

#### 28. Find Last 50-100 Days Modified Files

To find all the files which are modified more than **50** days back and less than **100** days.

```
# find / -mtime +50 –mtime -100
```

#### 29. Find Changed Files in Last 1 Hour

To find all the files which are changed in last **1 hour**.

```
# find / -cmin -60
```

#### 30. Find Modified Files in Last 1 Hour

To find all the files which are modified in last **1 hour**.

```
# find / -mmin -60
```

#### 31. Find Accessed Files in Last 1 Hour

To find all the files which are accessed in last **1 hour**.

```
# find / -amin -60
```

**Part V – Find Files and Directories Based on Size**

#### 32. Find 50MB Files

To find all **50MB** files, use.

```
# find / -size 50M
```

#### 33. Find Size between 50MB – 100MB

To find all the files which are greater than **50MB** and less than **100MB**.

```
# find / -size +50M -size -100M
```

#### 34. Find and Delete 100MB Files

To find all **100MB** files and delete them using one single command.

```
# find / -size +100M -exec rm -rf {} \;
```

#### 35. Find Specific Files and Delete

Find all **.mp3** files with more than **10MB** and delete them using one single command.

```
# find / -type f -name *.mp3 -size +10M -exec rm {} \;
```

That’s it, We are ending this post here, In our next article we will discuss more about other Linux commands in depth with practical examples. Let us know your opinions on this article using our comment section.



Many times, we are locked in a situation where we have to search for multiple files with different extensions, this has probably happened to several Linux users especially from within the terminal.

There are several Linux utilities that we can use to locate or find files on the file system, but finding multiple filenames or files with different extensions can sometimes prove tricky and requires specific commands.

![Find Multiple File Names in Linux](https://www.tecmint.com/wp-content/uploads/2016/07/Find-Multiple-File-Names-in-Linux.png)

Find Multiple File Names in Linux

One of the many utilities for locating files on a Linux file system is the `find` utility and in this how-to guide, we shall walk through a few examples of using **find** to help us locate multiple filenames at once.

Before we dive into the actual commands, let us look at a brief introduction to the Linux `find` utility.

The simplest and general syntax of the find utility is as follows:

```
# find directory options [ expression ]
```

Let us proceed to look at some examples of **find** command in Linux.

**1.** Assuming that you want to find all files in the current directory with `.sh` and `.txt` file extensions, you can do this by running the command below:

```
# find . -type f \( -name "*.sh" -o -name "*.txt" \)
```

![Find .sh and .txt Extension Files in Linux](https://www.tecmint.com/wp-content/uploads/2016/07/Find-Multiple-Extension-Files-in-Linux.png)

Find .sh and .txt Extension Files in Linux

Interpretation of the command above:

1. `.` means the current directory
2. `-type` option is used to specify file type and here, we are searching for regular files as represented by `f`
3. `-name` option is used to specify a search pattern in this case, the file extensions
4. `-o` means “OR”

It is recommended that you enclose the file extensions in a bracket, and also use the `\` ( **back slash**) escape character as in the command.

**2.** To find three filenames with `.sh`, `.txt` and `.c` extensions, issues the command below:

```
# find . -type f \( -name "*.sh" -o -name "*.txt" -o -name "*.c" \)
```

![Find Multiple File Extensions in Linux](https://www.tecmint.com/wp-content/uploads/2016/07/Find-Multiple-File-Extensions-in-Linux.png)

Find Multiple File Extensions in Linux

**3.** Here is another example where we search for files with `.png`, `.jpg`, `.deb` and `.pdf` extensions:

```
# find /home/aaronkilik/Documents/ -type f \( -name "*.png" -o -name "*.jpg" -o -name "*.deb" -o -name ".pdf" \)
```

![Find More than 3 File Extensions in Linux](https://www.tecmint.com/wp-content/uploads/2016/07/Find-Multiple-Image-File-Extensions.png)

Find More than 3 File Extensions in Linux

When you critically observe all the commands above, the little trick is using the `-o` option in the **find** command, it enables you to add more filenames to the search array, and also knowing the filenames or file extensions you are searching for.