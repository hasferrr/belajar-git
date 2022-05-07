# Catatan tambahan dari git-scm.com

## Ignoring Files

Find "gitignore" using **ctrl+f** :

[2.2 Git Basics - Recording Changes to the Repository](https://git-scm.com/book/en/v2/Git-Basics-Recording-Changes-to-the-Repository)

```bash
# ignore all .a files
*.a

# but do track lib.a, even though you're ignoring .a files above
!lib.a

# only ignore the TODO file in the current directory, not subdir/TODO
/TODO

# ignore all files in any directory named build
build/

# ignore doc/notes.txt, but not doc/server/arch.txt
doc/*.txt

# ignore all .pdf files in the doc/ directory and any of its subdirectories
doc/**/*.pdf
```

## Undoing Things

One of the common undos takes place when you commit too early and possibly forget to add some files, or you mess up your commit message, more :

[2.4 Git Basics - Undoing Things](https://git-scm.com/book/en/v2/Git-Basics-Undoing-Things)

```bash
git commit --amend
```
