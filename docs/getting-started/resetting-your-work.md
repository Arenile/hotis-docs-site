---
tags:
  - git
  - reset
  - start over
---

# Resetting Your Work

If your edits have gotten into a broken state and you want to start a file completely fresh, you can reset it to the original version from the starter repository.

---

## The command

Make sure you are in the `hotis-projects-starter` folder, then run:

```
git reset --hard
```

---

!!! warning "This permanently discards all your edits"
    `git reset --hard` is the "start this file over from scratch" button. **Every change you have made to every file in the folder will be erased** and replaced with the original starter versions. There is no undo.

    Only use this when you genuinely want to throw away your work and begin again. If you just want to fix a bug, close the file, re-read the error message, and try editing again.

---

## What it does

The starter code lives in a **git repository** — a system that tracks versions of your files. `git reset --hard` tells git to discard everything since the last saved snapshot and restore the original files.

After running it, your `.c` files will be back to exactly the way they were when you first cloned the repo.

---

## See also

- [Reading error messages](reading-errors.md)
- [Using the terminal](using-the-terminal.md)
