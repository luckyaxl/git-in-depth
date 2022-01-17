# Git Foundations

## What’s Git?
- Git is distributed version control system

## How does git store information?
- Git use key value to store data in storage, and you can use the key to retrieve the content

## Git Blob and trees
- Git stores the compressed data in a blob. When you run git init on directory, GIT will tell you that it initialized an empty GIT repository. So the data is store in .git directory.
- The blob is stored in objects directory inside of .git directory, the directory starts with the first two characters of the hash
- The projects directory structure and filenames is stored in a tree. The tree contains pointers to blobs, to other tree, and metadata

## Git Commits
The commits is a code snapshot from user with a log messages for describing the change from previous code. there's three types of object will create when we do git commit.
- tree
- commit
- blob

You can use this command if you want to look at `.git/objects` directory

>git cat-file -t (type) or -p (print the contents)

```
$ tree .git/objects

.git/objects
├── 5b
│   └── 3c332d9a80d9afd578293e58081d210e79413e
├── e6
│   └── 9de29bb2d1d6434b8b29ae775ad8c2e48c5391
├── f9
│   └── 3e3a1a1525fb5b91020da86e44810c87a2d7bc
├── info
└── pack

5 directories, 3 files
```
See the type
```
$ git cat-file -t 5b3c
commit
```
See the contents
```
$ git cat-file -p 5b3c
tree f93e3a1a1525fb5b91020da86e44810c87a2d7bc
author Luckyaxl <luckyaxl3@gmail.com> 1642432249 +0700
committer Luckyaxl <luckyaxl3@gmail.com> 1642432249 +0700

initial commit
```

## Git Areas and Stashing
The `working area` is like your scratch space, it's where you can add new content, or modify and delete. and you don't need to worry about losing your work. The file in your working area that are also not in the staging are not handled by git. Also untracked files

The `staging area` is how git knows what will change between the currentt commit and the next commmit, consider the baseline staging area as being an exact copy of the latest commit.

```
$ git ls-files -s
100644 e69de29bb2d1d6434b8b29ae775ad8c2e48c5391 0	README.md
```

`Git Stash` is a way to save uncomitted work, the stash is safe from destructive operations, can be deleted, change or overwrite like git reset or git checkout

Git stash basic use
### Stash changes
```
$ git stash
```
### List changes 
```
$ git stash list
```
### Show the contents
```
$ git stash show stash@{0}
```
### Apply the last stash
```
$ git stash apply
```
### Apply a specific stash
```
$ git stash apply stash@{0}
```

### Name stashes
```
$ git stash save "WIP: making progress on foo"
```

### Start a new branch from a stash
```
$ git stash branch <optional stash name>
```

### Grab a single file from a stash
```
$ git checkout <stash name> -- <filename>
```

