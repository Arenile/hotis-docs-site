---
tags:
  - terminal
  - command line
  - cd
  - ls
  - navigate
---

# Using the Terminal

The terminal is how you talk directly to the computer. Instead of clicking icons, you type commands. This page covers everything you need to navigate around the file system.

## Opening the terminal

Look for a grey icon with a white `>_` symbol in the top-left corner of the desktop. Click it and a terminal window opens.

You will see a prompt that looks something like this:

```
pi@raspberrypi:~ $
```

That `$` is where you type. Everything before it tells you who you are logged in as (`pi`), the machine name, and your current directory (`~` means your home folder).

---

## Navigating the file system

Think of the file system as a tree of folders. You are always standing in one folder at a time (your **current directory**). These commands let you move around.

### `ls -al` — list all files

```
ls -al
```

Shows every file and folder in the current directory, including hidden ones (names starting with `.`). The `-a` flag means "all" and `-l` means "long format" (shows sizes, dates, and permissions).

### `cd <directory>` — move into a folder

```
cd hotis-projects-starter
```

Changes your current directory to the one named `hotis-projects-starter`. You can only move into folders that exist in your current location — use `ls -al` to see what is available.

### `cd ..` — move up one level

```
cd ..
```

The two dots (`..`) always mean "the folder above this one." This takes you up one level in the tree.

!!! tip "Check where you are"
    If you are ever unsure which folder you are in, look at the part of the prompt between `:` and `$`. Or type `pwd` and press Enter — it prints the full path of your current directory.

---

## Common sequence for the motor labs

Every time you start a lab session, you will do something like this:

```
cd hotis-projects-starter
ls -al
```

First you move into the project folder, then list its contents to confirm you are in the right place.

---

## See also

- [Exploring your system](exploring-your-system.md)
- [Opening & editing code](editing-code.md)
- [Building & running](build-and-run.md)
