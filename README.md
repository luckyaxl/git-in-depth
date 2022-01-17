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

You can use this command if you want to look at **`.git/objects`** directory

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
Print the type
```
$ git cat-file -t 5b3c
commit
```
Print the contents
```
$ git cat-file -p 5b3c
tree f93e3a1a1525fb5b91020da86e44810c87a2d7bc
author Luckyaxl <luckyaxl3@gmail.com> 1642432249 +0700
committer Luckyaxl <luckyaxl3@gmail.com> 1642432249 +0700

initial commit
```

# Git Areas and Stashing
The **`working area`** is like your scratch space, it's where you can add new content, or modify and delete. and you don't need to worry about losing your work. The file in your working area that are also not in the staging are not handled by git. Also untracked files

The **`staging area`** is how git knows what will change between the currentt commit and the next commmit, consider the baseline staging area as being an exact copy of the latest commit.

```
$ git ls-files -s
100644 e69de29bb2d1d6434b8b29ae775ad8c2e48c5391 0	README.md
```

**`Git Stash`** is a way to save uncomitted work, the stash is safe from destructive operations, can be deleted, change or overwrite like git reset or git checkout

## Git stash basic use
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

# References, Commits, Branches
Three types of Git References

- Tags & Annotated Tags
- Branches
- HEAD

**`Branch`** is a pointer to a particular commit. The pointer to the current branch is going to change as new commits are made.

**`HEAD`** is how git knows what branch you’re currently on, and what the next parent will be.
```
$ git checkout master
```
```
$ cat .git/HEAD
ref: refs/heads/master
```
```
$ git checkout feature
Switched to branch 'feature'
```
```
$ cat .git/HEAD
ref: refs/heads/feature
```
# Merging and Rebasing
Merge commits are just commit, but they happen to be commits that have more than one parent. It maintains all the same commits that you had created on a future branch.

**Merge Conflicts**
- Attempt to merge, but files have diverged
- Git stops until the conflicts are resolved

```
$ git merge feature
CONFLICT (add/add): Merge conflict in feature
```

# History and Diffs
**`git log`** is the basic command that shows the history of your repository.

```
$ git log
commit fba0d50cc3216a0770fa2764d4780b3974516f00 (HEAD -> master)
Author: Luckyaxl <luckyaxl3@gmail.com>
Date:   Mon Jan 17 23:51:31 2022 +0700

    git refs

commit 83ef6c0d3859d6f8f527f328eb63248102374dc6
Author: Luckyaxl <luckyaxl3@gmail.com>
Date:   Mon Jan 17 23:35:29 2022 +0700

    learn git

commit 5b3c332d9a80d9afd578293e58081d210e79413e (origin/master)
Author: Luckyaxl <luckyaxl3@gmail.com>
Date:   Mon Jan 17 22:10:49 2022 +0700

    initial commit
```

**`git show`** is the basic command to look at commits and their content

**`git diff`** shows you changes: 
- Between commits
- Between the staging area and repository
- What’s in the working area

Unstaged changes
```
$ git diff
```

Staged changes
```
$ git diff --staged
```


# Fixing Mistakes

There’s a few tools for Fixing mistakes in git.
> checkout, reset, revert, clean

`Git checkout` is a command that restore working tree files or switch branches

`Git reset` is another comment that performs different actions depending on the arguments.

`Git revert` creates a new commit that introduces the opposite changes from the specified commit and the original commit stays in the repository.

`Git clean` will clear your working area by deleting untracked files.  Use —dry-run flag to see what would be deleted

# Rebase and Amend
# Forks & Remote Repos
# Danger Zone
# Github
# Advanced Github
