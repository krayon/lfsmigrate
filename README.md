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

krayon@host:/tmp/lfslocal$ git remote add github ssh://git@github.com/krayon/lfsmigrate.git

krayon@host:/tmp/$ git remote -v
github	ssh://git@github.com/krayon/lfsmigrate.git (fetch)
github	ssh://git@github.com/krayon/lfsmigrate.git (push)
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

### Current state

The current state of our repository, as shown by `git log`, with my own
annotations added:

```
krayon@host:/tmp/lfslocal$ git log --all >before-lfs.txt

krayon@host:/tmp/lfslocal$ git log --all --graph

* commit 3939ea806e7306c921ff9ba4c66bd7942092049a (HEAD -> main, origin/main)
| Author: Krayon <krayon@github.com>
| Date:   2023-10-11 13:21:09 +1100
|
|     README - document betterbig
|
* commit 4d383707d5a963eef367e6d3b573d2a736f9718e
| Author: Krayon <krayon@github.com>
| Date:   2023-10-11 12:56:18 +1100
|
|     Update README
|
| * commit a9982b9ec34bcbb12738c27131179ad07221fb96 (origin/betterbig, betterbig)
| | Author: Krayon <krayon@github.com>
| | Date:   2023-10-11 13:20:18 +1100
| |
| |     Better big README
| |
| * commit 5f6e07f0e4bd52cd7bd9ae0bc340deb62968fcb8 <-- This commit changes the
|/  Author: Krayon <krayon@github.com>                  content of the 101mb
|   Date:   2023-10-11 13:09:51 +1100                   file. This occurs on
|                                                       another branch called
|       Better big file                                 "betterbig"
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
* commit 0cf475dbdbecb3d456a2add2bcf1d00beecac0c6 <-- This commit adds the 101mb
| Author: Krayon <krayon@github.com>                  file to the "main" branch
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
```

### Install LFS

We now install LFS support to the repository:

```
krayon@host:/tmp/lfslocal$ git lfs install
Updated git hooks.
Git LFS initialized.
```

And familiarise ourselves with the LFS migrate help:

```
krayon@host:/tmp/lfslocal$ git lfs migrate --help
git lfs migrate <mode> [options] "--" [branch ...]
...
```

### Deciding what to LFS

We've read that we can use the `info` subcommand to retrieve information.

```
krayon@host:/tmp/lfslocal$ git lfs migrate info --everything --above=100MB
migrate: Sorting commits: ..., done.
migrate: Examining commits: 100% (10/10), done.
*.dat	212 MB	2/2 files(s)	100%
```

This shows us that we have 2 files above 100 megabytes that are in our
repository. These are our `101mb.dat` file in both the `main` and `betterbig`
branches.

We think long and hard and decide that these files are critical to building this
product, and that they indeed belong in the repository. We also know that in
future, we may need to add other binary files that will have the extension
`dat`. We therefore decide to have LFS automatically manage any files, ending in
`.dat`.

### Store in LFS, rewriting history

```
krayon@host:/tmp/lfslocal$ git lfs migrate import --everything --include="*.dat"
git lfs migrate import --everything --include="*.dat"
migrate: override changes in your working copy? [Y/n] y
migrate: changes in your working copy will be overridden ...
migrate: Sorting commits: ..., done.
migrate: Rewriting commits: 100% (10/10), done.
  betterbig	a9982b9ec34bcbb12738c27131179ad07221fb96 -> 62caadd960f36782513d155819d86abec66033b2
  main     	3939ea806e7306c921ff9ba4c66bd7942092049a -> b271363dcae6c8c8fb6063083db03322537e839b
migrate: Updating refs: ..., done.
migrate: checkout: ..., done.
```

### Confirm

```
krayon@host:/tmp/lfslocal$ git lfs ls-files --all
8474373dab - random.101mb.dat
90b0ab23c4 - random.101mb.dat

krayon@host:/tmp/lfslocal$ git log --all --not --remotes=\* >after-lfs.txt

krayon@host:/tmp/lfslocal$ diff before-lfs.txt after-lfs.txt
1c1
< commit 3939ea806e7306c921ff9ba4c66bd7942092049a
---
> commit b271363dcae6c8c8fb6063083db03322537e839b
7c7
< commit a9982b9ec34bcbb12738c27131179ad07221fb96
---
> commit 62caadd960f36782513d155819d86abec66033b2
13c13
< commit 5f6e07f0e4bd52cd7bd9ae0bc340deb62968fcb8
---
> commit a7837e0c6919d77855b940c2ec8ff356ae9eda61
19c19
< commit 4d383707d5a963eef367e6d3b573d2a736f9718e
---
> commit 96e1907328203ed3f98f663806990004b250133f
25c25
< commit f87b7ceb3e69034ba18c7606a60da8ef8348f129
---
> commit ff9eb2bf053010f9b5ac11e7cef3e28b91a1172e
31c31
< commit 41d2dc2c883d708a3aa68c09e6b30eeb3dbe1bf0
---
> commit 8b83f2efea583afa169c3fc29b7469a0ecf21cd2
37c37
< commit 0cf475dbdbecb3d456a2add2bcf1d00beecac0c6
---
> commit 9a0673826c8cfe362ded6e3a009d31491dcf4edc
43c43
< commit ec461a8f6dc47471d3a84c365fde39dcf0fd1bf2
---
> commit 34ee3b0086301e023ee71cb49a2364ccdccc1d91
49c49
< commit 2542e4eed2d478d65cb9993a8807bfdbe95b53e5
---
> commit 5e934355aa957ed5c70ed5ad750fbda45ae42bad
55c55
< commit 0bb90da7d7568f2b9e1e03c53f146e50d6249b81
---
> commit dec81990fcba805ecf66a5ff22cd4d8eac2ec54f
```

We can see many commits were changed. In fact, it was ALL commits, as the LFS
attributes file was created at the very root of the repository. You can see this
using `git log`'s `--name-status` argument, against the first commit (
`dec81990fcba805ecf66a5ff22cd4d8eac2ec54f` here ):

```
git log --name-status $(git rev-list --max-parents=0 HEAD)
commit dec81990fcba805ecf66a5ff22cd4d8eac2ec54f
Author: Krayon <krayon@github.com>
Date:   2023-10-11 12:36:17 +1100

    Add README

A       .gitattributes
A       README.md
```



### Force update our origin for each branch

```
krayon@host:/tmp/lfslocal$ git push --force origin main:main
Uploading LFS objects: 100% (1/1), 0 B | 0 B/s, done.
Enumerating objects: 27, done.
Counting objects: 100% (27/27), done.
Delta compression using up to 8 threads
Compressing objects: 100% (26/26), done.
Writing objects: 100% (27/27), 14.06 KiB | 7.03 MiB/s, done.
Total 27 (delta 11), reused 0 (delta 0)
To file:///tmp/lfssource.git
 + 3939ea8...b271363 main -> main (forced update)

krayon@host:/tmp/lfslocal$ git push --force origin betterbig:betterbig
Uploading LFS objects: 100% (1/1), 0 B | 0 B/s, done.
warning: not sending a push certificate since the receiving end does not support --signed push
Enumerating objects: 9, done.
Counting objects: 100% (9/9), done.
Delta compression using up to 8 threads
Compressing objects: 100% (6/6), done.
Writing objects: 100% (6/6), 1.97 KiB | 1.97 MiB/s, done.
Total 6 (delta 3), reused 0 (delta 0)
To file:///tmp/lfssource.git
 + a9982b9...62caadd betterbig -> betterbig (forced update)
```

### Push each branch to GitHub

```
krayon@host:/tmp/lfslocal$ git push github main:main
Uploading LFS objects: 100% (1/1), 106 MB | 2.5 MB/s, done.
warning: not sending a push certificate since the receiving end does not support --signed push
Enumerating objects: 27, done.
Counting objects: 100% (27/27), done.
Delta compression using up to 8 threads
Compressing objects: 100% (26/26), done.
Writing objects: 100% (27/27), 14.06 KiB | 7.03 MiB/s, done.
Total 27 (delta 11), reused 0 (delta 0)
remote: Resolving deltas: 100% (11/11), done.
To ssh://github.com/krayon/lfsmigrate.git
 * [new branch]      main -> main

krayon@host:/tmp/lfslocal$ git push github betterbig:betterbig
...
```

----
[//]: # ( vim: set ts=4 sw=4 et cindent tw=80 ai si syn=markdown ft=markdown: )
