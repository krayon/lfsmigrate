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

```
krayon@host:/tmp/lfslocal$ dd if=/dev/urandom of=random.101mb.dat bs=1024 count=$((1024 * 101))
103424+0 records in
103424+0 records out
105906176 bytes (106 MB, 101 MiB) copied, 0.403264 s, 263 MB/s

krayon@host:/tmp/lfslocal$ ls -lah random.101mb.dat
-rw-rw-r--  1 krayon krayon 101M Oct 11 12:46 random.101mb.dat

krayon@host:/tmp/lfslocal$ git add random.101mb.dat

krayon@host:/tmp/lfslocal$ git commit -S -m 'Add 101mb file'
[main 807e148] Add 101mb file
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 random.101mb.dat

krayon@host:/tmp/lfslocal$ git push origin
Enumerating objects: 4, done.
Counting objects: 100% (4/4), done.
Delta compression using up to 8 threads
Compressing objects: 100% (3/3), done.
Writing objects: 100% (3/3), 101.03 MiB | 31.71 MiB/s, done.
Total 3 (delta 1), reused 0 (delta 0)
To file:///tmp/lfssource.git
   a34c816..807e148  main -> main

krayon@host:/tmp/lfslocal$ git log
commit 0cf475dbdbecb3d456a2add2bcf1d00beecac0c6 (HEAD -> main, origin/main)
Author: Krayon <krayon@github.com>
Date:   2023-10-11 12:48:20 +1100

    Add 101mb file

commit ec461a8f6dc47471d3a84c365fde39dcf0fd1bf2
Author: Krayon <krayon@github.com>
Date:   2023-10-11 12:48:08 +1100

    Update README

commit 2542e4eed2d478d65cb9993a8807bfdbe95b53e5
Author: Krayon <krayon@github.com>
Date:   2023-10-11 12:42:26 +1100

    Add Lorem Ipsum texts

commit 0bb90da7d7568f2b9e1e03c53f146e50d6249b81
Author: Krayon <krayon@github.com>
Date:   2023-10-11 12:36:17 +1100

    Add README
```

### Step 3: Add more basic files



----
## Migrate


----
[//]: # ( vim: set ts=4 sw=4 et cindent tw=80 ai si syn=markdown ft=markdown: )
