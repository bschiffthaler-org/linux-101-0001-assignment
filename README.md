# Linux 101 - 01 Filesystem

## Core take aways from this module

* Understand how the file system is organized on a Linux system
* Understand absolute and relative paths
* Understand the difference between file types
* Get to know tools to navigate and manipulate the filesystem

## General layout of the filesystem

The Linux filesystem is organized like a tree. Every directory and every file exists somewhere downstream from the root of the tree, which we'll denote as "`/`".

Take this example filesystem tree. Here, directories are shaded purple, regular files have a white background:

<!-- graph source
graph LR

  / -- usr
  usr -- local
  / -- lib
  / -- lib64
  / -- home
  / -- bin
  / -- sbin
  / -- boot
  home -- bastian
  home -- nicolas
  bastian -- x[[some_data.csv]]
  nicolas -- y[[other_data.csv]]
  
  style x fill:white
  style y fill:white
-->

<img src='https://mermaid.ink/svg/eyJjb2RlIjoiXG5ncmFwaCBMUlxuXG4gIC8gLS0-IHVzclxuICB1c3IgLS0-IGxvY2FsXG4gIC8gLS0-IGxpYlxuICAvIC0tPiBsaWI2NFxuICAvIC0tPiBob21lXG4gIC8gLS0-IGJpblxuICAvIC0tPiBzYmluXG4gIC8gLS0-IGJvb3RcbiAgaG9tZSAtLT4gYmFzdGlhblxuICBob21lIC0tPiBuaWNvbGFzXG4gIGJhc3RpYW4gLS0-IHhbW3NvbWVfZGF0YS5jc3ZdXVxuICBuaWNvbGFzIC0tPiB5W1tvdGhlcl9kYXRhLmNzdl1dXG4gIFxuICBzdHlsZSB4IGZpbGw6d2hpdGVcbiAgc3R5bGUgeSBmaWxsOndoaXRlIiwibWVybWFpZCI6eyJ0aGVtZSI6ImRlZmF1bHQiLCJ0aGVtZVZhcmlhYmxlcyI6eyJiYWNrZ3JvdW5kIjoid2hpdGUiLCJwcmltYXJ5Q29sb3IiOiIjRUNFQ0ZGIiwic2Vjb25kYXJ5Q29sb3IiOiIjZmZmZmRlIiwidGVydGlhcnlDb2xvciI6ImhzbCg4MCwgMTAwJSwgOTYuMjc0NTA5ODAzOSUpIiwicHJpbWFyeUJvcmRlckNvbG9yIjoiaHNsKDI0MCwgNjAlLCA4Ni4yNzQ1MDk4MDM5JSkiLCJzZWNvbmRhcnlCb3JkZXJDb2xvciI6ImhzbCg2MCwgNjAlLCA4My41Mjk0MTE3NjQ3JSkiLCJ0ZXJ0aWFyeUJvcmRlckNvbG9yIjoiaHNsKDgwLCA2MCUsIDg2LjI3NDUwOTgwMzklKSIsInByaW1hcnlUZXh0Q29sb3IiOiIjMTMxMzAwIiwic2Vjb25kYXJ5VGV4dENvbG9yIjoiIzAwMDAyMSIsInRlcnRpYXJ5VGV4dENvbG9yIjoicmdiKDkuNTAwMDAwMDAwMSwgOS41MDAwMDAwMDAxLCA5LjUwMDAwMDAwMDEpIiwibGluZUNvbG9yIjoiIzMzMzMzMyIsInRleHRDb2xvciI6IiMzMzMiLCJtYWluQmtnIjoiI0VDRUNGRiIsInNlY29uZEJrZyI6IiNmZmZmZGUiLCJib3JkZXIxIjoiIzkzNzBEQiIsImJvcmRlcjIiOiIjYWFhYTMzIiwiYXJyb3doZWFkQ29sb3IiOiIjMzMzMzMzIiwiZm9udEZhbWlseSI6IlwidHJlYnVjaGV0IG1zXCIsIHZlcmRhbmEsIGFyaWFsIiwiZm9udFNpemUiOiIxNnB4IiwibGFiZWxCYWNrZ3JvdW5kIjoiI2U4ZThlOCIsIm5vZGVCa2ciOiIjRUNFQ0ZGIiwibm9kZUJvcmRlciI6IiM5MzcwREIiLCJjbHVzdGVyQmtnIjoiI2ZmZmZkZSIsImNsdXN0ZXJCb3JkZXIiOiIjYWFhYTMzIiwiZGVmYXVsdExpbmtDb2xvciI6IiMzMzMzMzMiLCJ0aXRsZUNvbG9yIjoiIzMzMyIsImVkZ2VMYWJlbEJhY2tncm91bmQiOiIjZThlOGU4IiwiYWN0b3JCb3JkZXIiOiJoc2woMjU5LjYyNjE2ODIyNDMsIDU5Ljc3NjUzNjMxMjglLCA4Ny45MDE5NjA3ODQzJSkiLCJhY3RvckJrZyI6IiNFQ0VDRkYiLCJhY3RvclRleHRDb2xvciI6ImJsYWNrIiwiYWN0b3JMaW5lQ29sb3IiOiJncmV5Iiwic2lnbmFsQ29sb3IiOiIjMzMzIiwic2lnbmFsVGV4dENvbG9yIjoiIzMzMyIsImxhYmVsQm94QmtnQ29sb3IiOiIjRUNFQ0ZGIiwibGFiZWxCb3hCb3JkZXJDb2xvciI6ImhzbCgyNTkuNjI2MTY4MjI0MywgNTkuNzc2NTM2MzEyOCUsIDg3LjkwMTk2MDc4NDMlKSIsImxhYmVsVGV4dENvbG9yIjoiYmxhY2siLCJsb29wVGV4dENvbG9yIjoiYmxhY2siLCJub3RlQm9yZGVyQ29sb3IiOiIjYWFhYTMzIiwibm90ZUJrZ0NvbG9yIjoiI2ZmZjVhZCIsIm5vdGVUZXh0Q29sb3IiOiJibGFjayIsImFjdGl2YXRpb25Cb3JkZXJDb2xvciI6IiM2NjYiLCJhY3RpdmF0aW9uQmtnQ29sb3IiOiIjZjRmNGY0Iiwic2VxdWVuY2VOdW1iZXJDb2xvciI6IndoaXRlIiwic2VjdGlvbkJrZ0NvbG9yIjoicmdiYSgxMDIsIDEwMiwgMjU1LCAwLjQ5KSIsImFsdFNlY3Rpb25Ca2dDb2xvciI6IndoaXRlIiwic2VjdGlvbkJrZ0NvbG9yMiI6IiNmZmY0MDAiLCJ0YXNrQm9yZGVyQ29sb3IiOiIjNTM0ZmJjIiwidGFza0JrZ0NvbG9yIjoiIzhhOTBkZCIsInRhc2tUZXh0TGlnaHRDb2xvciI6IndoaXRlIiwidGFza1RleHRDb2xvciI6IndoaXRlIiwidGFza1RleHREYXJrQ29sb3IiOiJibGFjayIsInRhc2tUZXh0T3V0c2lkZUNvbG9yIjoiYmxhY2siLCJ0YXNrVGV4dENsaWNrYWJsZUNvbG9yIjoiIzAwMzE2MyIsImFjdGl2ZVRhc2tCb3JkZXJDb2xvciI6IiM1MzRmYmMiLCJhY3RpdmVUYXNrQmtnQ29sb3IiOiIjYmZjN2ZmIiwiZ3JpZENvbG9yIjoibGlnaHRncmV5IiwiZG9uZVRhc2tCa2dDb2xvciI6ImxpZ2h0Z3JleSIsImRvbmVUYXNrQm9yZGVyQ29sb3IiOiJncmV5IiwiY3JpdEJvcmRlckNvbG9yIjoiI2ZmODg4OCIsImNyaXRCa2dDb2xvciI6InJlZCIsInRvZGF5TGluZUNvbG9yIjoicmVkIiwibGFiZWxDb2xvciI6ImJsYWNrIiwiZXJyb3JCa2dDb2xvciI6IiM1NTIyMjIiLCJlcnJvclRleHRDb2xvciI6IiM1NTIyMjIiLCJjbGFzc1RleHQiOiIjMTMxMzAwIiwiZmlsbFR5cGUwIjoiI0VDRUNGRiIsImZpbGxUeXBlMSI6IiNmZmZmZGUiLCJmaWxsVHlwZTIiOiJoc2woMzA0LCAxMDAlLCA5Ni4yNzQ1MDk4MDM5JSkiLCJmaWxsVHlwZTMiOiJoc2woMTI0LCAxMDAlLCA5My41Mjk0MTE3NjQ3JSkiLCJmaWxsVHlwZTQiOiJoc2woMTc2LCAxMDAlLCA5Ni4yNzQ1MDk4MDM5JSkiLCJmaWxsVHlwZTUiOiJoc2woLTQsIDEwMCUsIDkzLjUyOTQxMTc2NDclKSIsImZpbGxUeXBlNiI6ImhzbCg4LCAxMDAlLCA5Ni4yNzQ1MDk4MDM5JSkiLCJmaWxsVHlwZTciOiJoc2woMTg4LCAxMDAlLCA5My41Mjk0MTE3NjQ3JSkifX0sInVwZGF0ZUVkaXRvciI6ZmFsc2V9'> </img>

## Absolute paths

Now that we understand the idea of the filesystem layout, we understand that every file and every directory exists somewhere on this graph. We can note where a file exists as a path on this graph starting from the root. As a convention, borders between directories are indicated with a `/`:

`/home/bastian/some_data.csv`

In the diagram above, you can follow this path and find your way to the file `some_data.csv`. A path that begins from the root of the filesystem is called an **absolute path**.

## Working directory and relative path

When you interact with a computer by text, you usually type code into a terminal. At the other end of this terminal is the shell, which interprets the commands you send and processes them further. We don't need to worry about the shell too much for now, but we need to understand that your shell has a _working directory_. This is the directory that your shell uses when you don't provide an _absolute path_ and instead use a _relative path_. Here's an example:

When you log into a computer, your shell's working directory is your user's home directory:

<!-- graph source
graph LR

  / -- usr
  usr -- local
  / -- lib
  / -- lib64
  / -- home
  / -- bin
  / -- sbin
  / -- boot
  home -- bastian
  home -- nicolas
  subgraph bastian's home
  bastian -- x[[some_data.csv]]
  end
  subgraph nicolas' home
  nicolas -- y[[other_data.csv]]
  end
  
  style x fill:white
  style y fill:white
-->  

<img src='https://mermaid.ink/svg/eyJjb2RlIjoiZ3JhcGggTFJcblxuICAvIC0tPiB1c3JcbiAgdXNyIC0tPiBsb2NhbFxuICAvIC0tPiBsaWJcbiAgLyAtLT4gbGliNjRcbiAgLyAtLT4gaG9tZVxuICAvIC0tPiBiaW5cbiAgLyAtLT4gc2JpblxuICAvIC0tPiBib290XG4gIGhvbWUgLS0-IGJhc3RpYW5cbiAgaG9tZSAtLT4gbmljb2xhc1xuICBzdWJncmFwaCBiYXN0aWFuJ3MgaG9tZVxuICBiYXN0aWFuIC0tPiB4W1tzb21lX2RhdGEuY3N2XV1cbiAgZW5kXG4gIHN1YmdyYXBoIG5pY29sYXMnIGhvbWVcbiAgbmljb2xhcyAtLT4geVtbb3RoZXJfZGF0YS5jc3ZdXVxuICBlbmRcbiAgXG4gIHN0eWxlIHggZmlsbDp3aGl0ZVxuICBzdHlsZSB5IGZpbGw6d2hpdGUiLCJtZXJtYWlkIjp7InRoZW1lIjoiZGVmYXVsdCIsInRoZW1lVmFyaWFibGVzIjp7ImJhY2tncm91bmQiOiJ3aGl0ZSIsInByaW1hcnlDb2xvciI6IiNFQ0VDRkYiLCJzZWNvbmRhcnlDb2xvciI6IiNmZmZmZGUiLCJ0ZXJ0aWFyeUNvbG9yIjoiaHNsKDgwLCAxMDAlLCA5Ni4yNzQ1MDk4MDM5JSkiLCJwcmltYXJ5Qm9yZGVyQ29sb3IiOiJoc2woMjQwLCA2MCUsIDg2LjI3NDUwOTgwMzklKSIsInNlY29uZGFyeUJvcmRlckNvbG9yIjoiaHNsKDYwLCA2MCUsIDgzLjUyOTQxMTc2NDclKSIsInRlcnRpYXJ5Qm9yZGVyQ29sb3IiOiJoc2woODAsIDYwJSwgODYuMjc0NTA5ODAzOSUpIiwicHJpbWFyeVRleHRDb2xvciI6IiMxMzEzMDAiLCJzZWNvbmRhcnlUZXh0Q29sb3IiOiIjMDAwMDIxIiwidGVydGlhcnlUZXh0Q29sb3IiOiJyZ2IoOS41MDAwMDAwMDAxLCA5LjUwMDAwMDAwMDEsIDkuNTAwMDAwMDAwMSkiLCJsaW5lQ29sb3IiOiIjMzMzMzMzIiwidGV4dENvbG9yIjoiIzMzMyIsIm1haW5Ca2ciOiIjRUNFQ0ZGIiwic2Vjb25kQmtnIjoiI2ZmZmZkZSIsImJvcmRlcjEiOiIjOTM3MERCIiwiYm9yZGVyMiI6IiNhYWFhMzMiLCJhcnJvd2hlYWRDb2xvciI6IiMzMzMzMzMiLCJmb250RmFtaWx5IjoiXCJ0cmVidWNoZXQgbXNcIiwgdmVyZGFuYSwgYXJpYWwiLCJmb250U2l6ZSI6IjE2cHgiLCJsYWJlbEJhY2tncm91bmQiOiIjZThlOGU4Iiwibm9kZUJrZyI6IiNFQ0VDRkYiLCJub2RlQm9yZGVyIjoiIzkzNzBEQiIsImNsdXN0ZXJCa2ciOiIjZmZmZmRlIiwiY2x1c3RlckJvcmRlciI6IiNhYWFhMzMiLCJkZWZhdWx0TGlua0NvbG9yIjoiIzMzMzMzMyIsInRpdGxlQ29sb3IiOiIjMzMzIiwiZWRnZUxhYmVsQmFja2dyb3VuZCI6IiNlOGU4ZTgiLCJhY3RvckJvcmRlciI6ImhzbCgyNTkuNjI2MTY4MjI0MywgNTkuNzc2NTM2MzEyOCUsIDg3LjkwMTk2MDc4NDMlKSIsImFjdG9yQmtnIjoiI0VDRUNGRiIsImFjdG9yVGV4dENvbG9yIjoiYmxhY2siLCJhY3RvckxpbmVDb2xvciI6ImdyZXkiLCJzaWduYWxDb2xvciI6IiMzMzMiLCJzaWduYWxUZXh0Q29sb3IiOiIjMzMzIiwibGFiZWxCb3hCa2dDb2xvciI6IiNFQ0VDRkYiLCJsYWJlbEJveEJvcmRlckNvbG9yIjoiaHNsKDI1OS42MjYxNjgyMjQzLCA1OS43NzY1MzYzMTI4JSwgODcuOTAxOTYwNzg0MyUpIiwibGFiZWxUZXh0Q29sb3IiOiJibGFjayIsImxvb3BUZXh0Q29sb3IiOiJibGFjayIsIm5vdGVCb3JkZXJDb2xvciI6IiNhYWFhMzMiLCJub3RlQmtnQ29sb3IiOiIjZmZmNWFkIiwibm90ZVRleHRDb2xvciI6ImJsYWNrIiwiYWN0aXZhdGlvbkJvcmRlckNvbG9yIjoiIzY2NiIsImFjdGl2YXRpb25Ca2dDb2xvciI6IiNmNGY0ZjQiLCJzZXF1ZW5jZU51bWJlckNvbG9yIjoid2hpdGUiLCJzZWN0aW9uQmtnQ29sb3IiOiJyZ2JhKDEwMiwgMTAyLCAyNTUsIDAuNDkpIiwiYWx0U2VjdGlvbkJrZ0NvbG9yIjoid2hpdGUiLCJzZWN0aW9uQmtnQ29sb3IyIjoiI2ZmZjQwMCIsInRhc2tCb3JkZXJDb2xvciI6IiM1MzRmYmMiLCJ0YXNrQmtnQ29sb3IiOiIjOGE5MGRkIiwidGFza1RleHRMaWdodENvbG9yIjoid2hpdGUiLCJ0YXNrVGV4dENvbG9yIjoid2hpdGUiLCJ0YXNrVGV4dERhcmtDb2xvciI6ImJsYWNrIiwidGFza1RleHRPdXRzaWRlQ29sb3IiOiJibGFjayIsInRhc2tUZXh0Q2xpY2thYmxlQ29sb3IiOiIjMDAzMTYzIiwiYWN0aXZlVGFza0JvcmRlckNvbG9yIjoiIzUzNGZiYyIsImFjdGl2ZVRhc2tCa2dDb2xvciI6IiNiZmM3ZmYiLCJncmlkQ29sb3IiOiJsaWdodGdyZXkiLCJkb25lVGFza0JrZ0NvbG9yIjoibGlnaHRncmV5IiwiZG9uZVRhc2tCb3JkZXJDb2xvciI6ImdyZXkiLCJjcml0Qm9yZGVyQ29sb3IiOiIjZmY4ODg4IiwiY3JpdEJrZ0NvbG9yIjoicmVkIiwidG9kYXlMaW5lQ29sb3IiOiJyZWQiLCJsYWJlbENvbG9yIjoiYmxhY2siLCJlcnJvckJrZ0NvbG9yIjoiIzU1MjIyMiIsImVycm9yVGV4dENvbG9yIjoiIzU1MjIyMiIsImNsYXNzVGV4dCI6IiMxMzEzMDAiLCJmaWxsVHlwZTAiOiIjRUNFQ0ZGIiwiZmlsbFR5cGUxIjoiI2ZmZmZkZSIsImZpbGxUeXBlMiI6ImhzbCgzMDQsIDEwMCUsIDk2LjI3NDUwOTgwMzklKSIsImZpbGxUeXBlMyI6ImhzbCgxMjQsIDEwMCUsIDkzLjUyOTQxMTc2NDclKSIsImZpbGxUeXBlNCI6ImhzbCgxNzYsIDEwMCUsIDk2LjI3NDUwOTgwMzklKSIsImZpbGxUeXBlNSI6ImhzbCgtNCwgMTAwJSwgOTMuNTI5NDExNzY0NyUpIiwiZmlsbFR5cGU2IjoiaHNsKDgsIDEwMCUsIDk2LjI3NDUwOTgwMzklKSIsImZpbGxUeXBlNyI6ImhzbCgxODgsIDEwMCUsIDkzLjUyOTQxMTc2NDclKSJ9fSwidXBkYXRlRWRpdG9yIjpmYWxzZX0'></img>

You can use the `pwd` command in a shell to print your current working directory. Let's try it out:

```
>pwd
/home/bs
```

My current working directory is `/home/bs`. Therefore, when I provide programs with relative paths to the filesystem, they will be interpreted relative to that directory (`/home/bs`). Let's introduce two more programs:

* `cd` - to change my working directory
* `ls` - to list files and directory

We can change our working directory, depending on where we need to do work. Before we change, here's a tip: if you ever want to reset your working directory and go back to your home, just run `cd` without any arguments. So let's try:

```
>cd /
>pwd
/
```
So now our working directory is the root of the file tree. We can now use the `ls` command to list the contents of our working directory:

```
>ls
bin  boot  dev  etc  home  lib  lib64  lost+found  media  mnt  opt  proc  root  run  sbin  srv  sys  tmp  usr  var
```

So there are a bunch of file-like objects in `/`. We can get more detailed output by changing the nature of the `ls` command. We do this by providing options, which is usually done with a minus (`-`) and the short - single character - name of the option, or two minuses (`--`) and the long name. For now, let's keep it simple with a single option:

```
>ls -l
total 64
lrwxrwxrwx.   1 root root    7 Jan 28  2020 bin -> usr/bin
dr-xr-xr-x.   2 root root 4096 Jan 28  2020 boot
drwxr-xr-x.   5 root root  360 Nov  2 20:12 dev
drwxr-xr-x.   1 root root 4096 Nov  2 20:12 etc
drwxr-xr-x.   1 root root 4096 Nov  2 20:12 home
lrwxrwxrwx.   1 root root    7 Jan 28  2020 lib -> usr/lib
lrwxrwxrwx.   1 root root    9 Jan 28  2020 lib64 -> usr/lib64
drwx------.   2 root root 4096 Oct  8 06:48 lost+found
drwxr-xr-x.   2 root root 4096 Jan 28  2020 media
drwxr-xr-x.   2 root root 4096 Jan 28  2020 mnt
drwxr-xr-x.   2 root root 4096 Jan 28  2020 opt
dr-xr-xr-x. 525 root root    0 Nov  2 20:12 proc
dr-xr-x---.   2 root root 4096 Oct  8 06:49 root
drwxr-xr-x.  13 root root 4096 Oct  8 06:49 run
lrwxrwxrwx.   1 root root    8 Jan 28  2020 sbin -> usr/sbin
drwxr-xr-x.   2 root root 4096 Jan 28  2020 srv
dr-xr-xr-x.  13 root root    0 Oct 15 08:00 sys
drwxrwxrwt.   2 root root 4096 Oct  8 06:49 tmp
drwxr-xr-x.  12 root root 4096 Oct  8 06:48 usr
drwxr-xr-x.   1 root root 4096 Oct  8 06:48 var
```

You can tell that the minimal output from before has changed into a detailed list. Here's what they mean using the first file as an example:
`lrwxrwxrwx.   1 root root    7 Jan 28  2020 bin -> usr/bin`

* `lrwxrwxrwx.`   : The first field indicates the file type and permissions. We'll talk about both of those in a minute
* `1`             : This is the number of times the file is referenced on the computer. Rarely useful to most people
* `root`          : This is the user who owns the file
* `root`          : And the group who owns the file
* `7`             : This is the file size in bytes
* `Jan 28  2020`  : This is the date the file was last modified
* `bin -> usr/bin`: And this is the file itself

## File types

There are a large number of file types present in a typical linux system, but there are only three that are usually relevant to the average user:

* Regular files: `-`
* Directories: `d`
* Links: `l`

When you run the `ls` command in Linux, you have the option to print

## File permissions

## Interacting with the filesystem

### Essential commands

* `pwd` - Print the working directory
* `cd` - Change the working directory
* `ls` - List files
* `mv` - Move (rename) files
* `cp` - Copy files
* `ln` - Create links to files
* `rm` - Remove files
* `less` - Read text files
* `touch` - Create new/empty files or update mtime
* `chmod` - Change file permissions
* `chown` - Change file owner
* `chgrp` - Change file group
