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

```
krayon@host:/tmp/lfslocal$ loremipsum >lorem3.txt

krayon@host:/tmp/lfslocal$ loremipsum >lorem4.txt

krayon@host:/tmp/lfslocal$ git add lorem[34].txt

krayon@host:/tmp/lfslocal$ git commit -S -m 'Add more Lorem Ipsum texts'
[main f87b7ce] Add more Lorem Ipsum texts
 2 files changed, 10 insertions(+)
 create mode 100644 lorem3.txt
 create mode 100644 lorem4.txt

krayon@host:/tmp/lfslocal$ git push origin
Enumerating objects: 5, done.
Counting objects: 100% (5/5), done.
Delta compression using up to 8 threads
Compressing objects: 100% (4/4), done.
Writing objects: 100% (4/4), 3.31 KiB | 3.31 MiB/s, done.
Total 4 (delta 1), reused 0 (delta 0)
To file:///tmp/lfssource.git
   41d2dc2..f87b7ce  main -> main

krayon@host:/tmp/lfslocal$ git log
commit f87b7ceb3e69034ba18c7606a60da8ef8348f129 (HEAD -> main, origin/main)
Author: Krayon <krayon@github.com>
Date:   2023-10-11 12:51:17 +1100

    Add more Lorem Ipsum texts

commit 41d2dc2c883d708a3aa68c09e6b30eeb3dbe1bf0
Author: Krayon <krayon@github.com>
Date:   2023-10-11 12:50:51 +1100

    Update README

commit 0cf475dbdbecb3d456a2add2bcf1d00beecac0c6
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

### Step 4: Add another branch with a new big file

```
krayon@host:/tmp/lfslocal$ git checkout -b betterbig f87b7ceb3e69034ba18c7606a60da8ef8348f129
Switched to a new branch 'betterbig'

krayon@host:/tmp/lfslocal$ dd if=/dev/urandom of=random.101mb.dat bs=1024 count=$((1024 * 101))
103424+0 records in
103424+0 records out
105906176 bytes (106 MB, 101 MiB) copied, 0.411487 s, 257 MB/s

krayon@host:/tmp/lfslocal$ git add random.101mb.dat

krayon@host:/tmp/lfslocal$ git commit -S -m 'Better big file'
[betterbig 5f6e07f] Better big file
 1 file changed, 0 insertions(+), 0 deletions(-)

krayon@host:/tmp/lfslocal$ git log --graph --all
* commit 5f6e07f0e4bd52cd7bd9ae0bc340deb62968fcb8 (HEAD -> betterbig)
| Author: Krayon <krayon@github.com>
| Date:   2023-10-11 13:09:51 +1100
|
|     Better big file
|
| * commit 4d383707d5a963eef367e6d3b573d2a736f9718e (origin/main, main)
|/  Author: Krayon <krayon@github.com>
|   Date:   2023-10-11 12:56:18 +1100
|
|       Update README
|
* commit f87b7ceb3e69034ba18c7606a60da8ef8348f129
| Author: Krayon <krayon@github.com>
| Date:   2023-10-11 12:51:17 +1100
|
|     Add more Lorem Ipsum texts
|
* commit 41d2dc2c883d708a3aa68c09e6b30eeb3dbe1bf0
| Author: Krayon <krayon@github.com>
| Date:   2023-10-11 12:50:51 +1100
|
|     Update README
|
* commit 0cf475dbdbecb3d456a2add2bcf1d00beecac0c6
| Author: Krayon <krayon@github.com>
| Date:   2023-10-11 12:48:20 +1100
|
|     Add 101mb file
|
* commit ec461a8f6dc47471d3a84c365fde39dcf0fd1bf2
| Author: Krayon <krayon@github.com>
| Date:   2023-10-11 12:48:08 +1100
|
|     Update README
|
* commit 2542e4eed2d478d65cb9993a8807bfdbe95b53e5
| Author: Krayon <krayon@github.com>
| Date:   2023-10-11 12:42:26 +1100
|
|     Add Lorem Ipsum texts
|
* commit 0bb90da7d7568f2b9e1e03c53f146e50d6249b81
  Author: Krayon <krayon@github.com>
  Date:   2023-10-11 12:36:17 +1100

      Add README

krayon@host:/tmp/lfslocal$ git push origin betterbig:betterbig
Enumerating objects: 5, done.
Counting objects: 100% (5/5), done.
Delta compression using up to 8 threads
Compressing objects: 100% (3/3), done.
Writing objects: 100% (3/3), 101.03 MiB | 32.15 MiB/s, done.
Total 3 (delta 1), reused 0 (delta 0)
To file:///tmp/lfssource.git
 * [new branch]      betterbig -> betterbig

krayon@host:/tmp/lfslocal$ git checkout main
```

----
## Migrate to GitHub (no LFS)

Now that we have a repository, lets try to migrate to GitHub:

```
krayon@host:/tmp/lfslocal$ git push github main:main

Enumerating objects: 20, done.
Counting objects: 100% (20/20), done.
Delta compression using up to 8 threads
Compressing objects: 100% (19/19), done.
Writing objects: 100% (20/20), 101.04 MiB | 1.20 MiB/s, done.
Total 20 (delta 4), reused 0 (delta 0)
remote: Resolving deltas: 100% (4/4), done.
remote: error: Trace: e5082655a8b61dcfa1415583b180fb3f8a3d57423f3a18feaebb64232285365d
remote: error: See https://gh.io/lfs for more information.
remote: error: File random.101mb.dat is 101.00 MB; this exceeds GitHub's file size limit of 100.00 MB
remote: error: GH001: Large files detected. You may want to try Git Large File Storage - https://git-lfs.github.com.
To ssh://github.com/krayon/lfsmigrate.git
 ! [remote rejected] main -> main (pre-receive hook declined)
error: failed to push some refs to 'ssh://git@github.com/krayon/lfsmigrate.git'
```

The operation failed, so we must now resort to moving the large file(s) to LFS.

----
## Migrate to GitHub (using LFS)



----
[//]: # ( vim: set ts=4 sw=4 et cindent tw=80 ai si syn=markdown ft=markdown: )
