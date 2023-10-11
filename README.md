# LFS Migrate

This repository is going to contain big files that cannot be uploaded to GitHub.
We will then, migrate them to LFS, rewriting history, before finally uploading
to GitHub.



----
## Setup

- Source repository:         `file:///tmp/lfssource.git/`
- Working (local) directory: `/tmp/lfslocal/`
- Destination repository:    `ssh://git@github.com/krayon/lfsmigrate.git`

### Step 1: Readme and basic files

#### Repo cloned

```
krayon@host:/tmp/$ git clone file:///tmp/lfssource.git lfslocal
Cloning into 'lfslocal'...
...


krayon@host:/tmp/$ cd lfslocal

krayon@host:/tmp/$ git remote -v
origin	file:///tmp/lfssource.git/ (fetch)
origin	file:///tmp/lfssource.git/ (push)
```

#### Add README

```
krayon@host:/tmp/lfslocal$ git add README.md

krayon@host:/tmp/lfslocal$ git commit -S -m 'Add README'
[main (root-commit) 0bb90da] Add README
 1 file changed, 16 insertions(+)
 create mode 100644 README.md

krayon@host:/tmp/lfslocal$ git push origin main:main
Enumerating objects: 3, done.
...

krayon@host:/tmp/lfslocal$ git log
commit 0bb90da7d7568f2b9e1e03c53f146e50d6249b81 (HEAD -> main, origin/main)
Author: Krayon <krayon@github.com>
Date:   2023-10-11 12:36:17 +1100

    Add README
```

#### Add more files

```
krayon@host:/tmp/lfslocal$ loremipsum >lorem1.txt

krayon@host:/tmp/lfslocal$ loremipsum >lorem2.txt

krayon@host:/tmp/lfslocal$ git add lorem1.txt lorem2.txt

krayon@host:/tmp/lfslocal$ git commit -S -m 'Add Lorem Ipsum texts'
[main 2542e4e] Add Lorem Ipsum texts
 2 files changed, 10 insertions(+)
 create mode 100644 lorem1.txt
 create mode 100644 lorem2.txt

krayon@host:/tmp/lfslocal$ git push origin main:main
Enumerating objects: 5, done.
Counting objects: 100% (5/5), done.
Delta compression using up to 8 threads
Compressing objects: 100% (4/4), done.
Writing objects: 100% (4/4), 3.40 KiB | 1.70 MiB/s, done.
Total 4 (delta 0), reused 0 (delta 0)
To file:///tmp/lfssource.git
   0bb90da..2542e4e  main -> main

krayon@host:/tmp/lfslocal$ git log
commit 2542e4eed2d478d65cb9993a8807bfdbe95b53e5 (HEAD -> main, origin/main)
Author: Krayon <krayon@github.com>
Date:   2023-10-11 12:42:26 +1100

    Add Lorem Ipsum texts

commit 0bb90da7d7568f2b9e1e03c53f146e50d6249b81
Author: Krayon <krayon@github.com>
Date:   2023-10-11 12:36:17 +1100

    Add README
```

### Step 2: Add big files




----
## Migrate


----
[//]: # ( vim: set ts=4 sw=4 et cindent tw=80 ai si syn=markdown ft=markdown: )
