# Linux

Objective: get people familiar with the basics of Linux

* Navigation on command line (cd, ls)
* File manipulation (touch, cp, mv, rm)
* File display and search (head, tail, grep)
* Permissions (chmod, chown, sudo)
* Profiles (.bash_profile, .bashrc, .profile)
* SSH (ssh_keygen, ~/.ssh, & scp, connecting to remote server)
* Environment variables (env, and how they are set in profiles)
* Piping & redirecting (> stdout, 2> stderr out, 1&2> combine both to single out)


## Command Line Navigation

Getting around via the command line takes some time to get used to, but with a little practice you can get quite comfortable and do many activities more quickly than with point and click tools.

### Create Folder

Use the `mkdir` command to create a new folder/directory. After the command, supply the name of the folder to be created.

```bash
mkdir home
```

### Folder Contents

List contents of current folder

```bash
ls
```

The output will show both files and folders.

```bash
README.md     home
```

To change the current folder location you'll use the `cd` command. Change directory to `home` folder. 

```bash
cd home
```

### Creating New Files

Create an empty file with the `touch` command, passing in the name you want for the file.

```bash
touch file1
```

Prove that you've created the `file1` folder, with the `ls` command.

### Detailed Directory Information

The `ls` command has a flag `-l` that will display detailed information about the contents of current folder. 

```bash
ls -l
```

Ouput:
```bash
total 0
-rw-r--r--  1 greg  staff  0 Jan 29 22:19 file1
```

What does that mean!!

* `-rw-r--r--` are the rights associated with `file1`. We'll see more about this later
* `1` ?????
* `greg` is the owner of the file
* `staff` ?????
* `0` is the size of the file
* `Jan 29 22:19` is the last time the file was modified
* `file1` is the name of the file

### Navigating to Parent Folder

We'll also want to move back 'up' to parent directories. This is done with `..`

```bash
cd ..
```

List the files in the child directory

```bash
ls home
```

Output:
```bash
file1
```

Get back into the `home` directory and list the files in the parent directory (`linux`). Notice how we use `..` to signal we want a parent directory.

```bash
cd home
ls ..
```

Thats the basics of navigation.

## File Manipulation

Learning a couple more commands will allow you to quickly move, copy and delete files.

Lets start by adding a new folder to work with

```bash
mkdir subfolder
```

First lets move `file1` into the `subfolder` using the `mv` or 'move' command. `mv` takes two parameters: `source` and `target`. `source` is the file were going to move, and `target` is the place were going to move it.

```bash
mv file1 subfolder
```

Now display the contents of the current `home` folder

```bash
ls
```

Notice `file1` is not in the folder anymore. Output:

```bash
subfolder
```

### Copy Files

We can also use the `cp` command to `copy` a file from one location to another. It has the same two parameters as `mv`: `source` and `target`.

We have two ways we could make a copy of the `subfolder/file1` file back into the `home` folder. We could change directory(`cd`) to `subfolder` then copy from there back into the parent directory. 

But instead, we'll stay in the `home` directory and make the source `subfolder/file1` and target `.`. `.` means the current folder.

```bash
cp subfolder/file1 .
```

Now list the files in the current directory and the `subfolder` directory. You should see these outputs

```bash
# home
file1		subfolder
# subfolder
file1
```

### Deleting Files and Folders

To delete files and folders we use `rm` or the 'remove' command.

Lets use it to remove the `subfolder` and its contents.

```bash
rm subfolder
```

Oh no! An error occured. The system won't let us remove the folder because... its a folder.

```bash
rm: subfolder: is a directory
```

Lets remove `file1` first:

```bash
rm subfolder/file1
```

Prove to yourself that the file has been removed.

Now we still want to delete `subfolder`, and to do this we need to use whats called a 'flag'. Flags are additional information provided to a command and they use `-` to signify they are a flag. In this case we'll use the `-r` flag, which is the 'recursive' flag.

```bash
rm -r subfolder
```

Prove to yourself that `subfolder` has been removed.

Lastly lets remove `file1`.

You should now have a totally empty `home` directory.

## Displaying and Finding File Contents

You'll also want to be able to see the contents of files, search files, and combine them, so lets go through a couple commands that illustrate that.

The following commands are used on files that are more than a couple lines. So instead of creating a file, we'll just point the commands at the `README.md` file you are currently reading.

### Head/Tail

Lets use the `head` command to view the first 10 lines of the `README.md` file.

```bash
head ../README.md
```

If we want to view more than 10 lines, we can use the `-n` flag.

```bash
head -n 30 ../README.md
```

You can also use the `tail` command to do the same thing as `head`, but it will show the **last** 10 lines of the file. Try it!

```bash
tail ../README.md
```

### Grep

Tools to find text in files can be very helpful, and thats what `grep` is for.

From the docs:

> grep searches for PATTERNS in each FILE.  PATTERNS is one or patterns
> separated by newline characters, and grep prints each line that
> matches a pattern.

Lets search the `README.md` file for patterns. In this case we'll just search for words. `grep` is parameterized by the pattern were searching on and the name of the file.

```bash
grep head ../README.md
```

You should see several lines output that contain 'head' in them

```bash
  * File manipulation (cd, ls, cat, cp, mv, rm, head, tail, grep )
Lets use the `head` command to view the first 10 lines of the `README.md` file.
head ../README.md
head -n 30 ../README.md
You can also use the `tail` command to do the same thing as `head`, but it will show the **last** 10 lines of the file. Try it!
```

