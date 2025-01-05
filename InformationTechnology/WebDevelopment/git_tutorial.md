## Git Tutorial by: boot.dev

## Introduction:

- Git is a distributed version control system(VCS), which maintains your code basically, where you can control
  the flow of the development of your code, when you make any changes that is a commit in the git VCS and you
  pretty manipulate that commit, go back and forth between that and do much more in it.

- Linus torvalds built Git VCS in 2005.

## Workflow:

- Basically you create commits in git vsc and modify or maintain that information according to your needs.
  which contains author, creation time,commit message and other information.

- What you can basically do with commits in git:

  - git provides you the set of command that allow you to `search, modify and manipulate` the commit history.

  - in any commit you can `branch off` and create a new commits.

  - any of the branch can be merged into the main branch.

  - multiple commits can be squashed into on commit and commit messages can be added to it.

  - git commits can be reverted.

## Things that we need to learn:

1. Installing and configuring git
2. porcelain and plumbing commands
3. inspecting git history
4. branching
5. merging
6. rebasing
7. undoing changes
8. remote repos & github

## Installing git:

- on Windows, download the windows executable from git-scm website
- on Linux, based on your distro install the git from your package
  manager.
- same with macOS, you can install the git from `brew`, if you have
  this on your system.

## Porceling and Plumbing:

- In Git, commands are divided into high-level("porcelain") commands
  and low-level("plumbing") commands. The porcelain commands are the ones
  that you will use most often as a developer to interact with your code.

Some porcelain commands are: - `git status` - `git add` - `git commit` - `git push` - `git pull` - `git log`

Some examples of plumbing are: - `git apply` - `git commit-tree` - `git hash-object`

## Quick Config:

- Whenever code changes, Git tracks who make the change. To ensure you
  get proper credit (or more likely, blame) for all the code you write,
  you need to set your name and email.

- Git comes with a configuration both at the global and the repo
  (project) level. Most of the time, you'll just use the global config.

- for checking if your `user.name` and `user.email` are already set:

```
git config --get user.name
```

```
git config --get user.email
```

- if not, then you can add them using:

```
git config --add --global user.name "your_kind_username"
```

```
git config --add --global user.email "your_email_address"
```

- setting up a default branch:

```
git config --global init.defaultBranch master
```

## Config:

- The very first step of any project is to create a repository.

- A Git "repository" (or "repo") represents a single project. You'll
  typically have one repository for each project you work on.

- Here we creating a sample folder named: `webflyx` and then `cd` to
  it and then:

- initialize the git into the webflyx directory:

```
git init
```

> We're using `master` for now because it is Git's default, but later
> we'll change it to `main`, which is Github's default.

## Staging

- The `contents.md` file has beed created, but it's untracked. We need
  to stage it (add it to the "index") with the `git add` command before
  commiting it later.

- Without staging, every file in the repository would be included in
  every commit, but that's often not what you want.

- Here's the command:

```
git add <path-to-file | pattern>
```

## Commit

- After staging a file, we can `commit` it.

- A commit it a snapshot of the repository at a given point in time.
  It's a way to save that state of the repository, and it's how Git keeps
  track of changes to the project. A commit with a message that describes
  the changes made in the commit.

- Here's how to commit all of your staged files:

```
git commit -m "your message here"
```

## Half of Git

- Half of your workflow as a developer will just be 3 simple commands:
  - git status
  - git add
  - git commit

## Git Log

- A Git repo is a (potentially very long) list of commits, where each
  commit represents the full state of the repository at a given point in
  time.

- The `git log` command shows a history of the commits in a repository.
  This is what makes Git a version control system. You can see. - Who made a commit - When the commit was made - What was changed

### A commit hash

- Each commit has a unique identifier called a "commit hash". This is a
  long string of characters that uniquely identifies the commit. Here's
  and example:

```
5ba786fcc93e8092831c01e71444b9baa2228a4f
```

- For convenience, you can refer to any commit or change withing Git by
  using the first `7` characters of its hash. For mine, that's `5ba786f`

## Different Hashes

- Every hash that is ever going to generate in anyones project is
  going to be different, because they are generated automatically.

- `Hash = SHA`, Git uses a cryptographic hash function called SHA-1 to
  generate commit hashes. Sometime they're referred to as "SHAs".

## The Plumbing:

- All the data in a Git repository is storedj directly in the (hidden) `.git`
  directory. That includes all the commits, branches, tags, and other objects
  we'll learn about later.

- Git is made up of objects that are stored in the `.git/objects` directory.
  A commit is just a type of object.

## The Object File:

- The file followed by this kind of path: `.git/objects/b5/c454d3fabab49a55cd672429abc9602b3b462c`
  contains some unreadable characters inside it.

- The contents have been compressed to raw bytes!

- using `xxd`, then we have this sample hex code:

```
00000000: 7801 958d 4b0a 0231 1005 5de7 14bd 1786  x...K..1..].....
00000010: ceaf 3388 881e a5f3 d380 9940 2603 1edf  ..3........@&...
00000020: 6c3c 80bb 4741 d50b add6 3240 3a77 1a3d  l<..GA....2@:w.=
00000030: 25b0 5ec9 68b2 2436 1e1d 5388 c9b2 5646  %.^.h.$6..S...VF
00000040: c9d5 6562 cbb4 7a24 cc82 8ff1 6a1d 5a4f  ..eb..z$....j.ZO
00000050: 9f52 8f1d aebf 757f 562e ef25 b47a 9b59  .R....u.V..%.z.Y
00000060: 4da8 1459 0d67 b41a c5a4 f36e a4bf 45f1  M..Y.g.....n..E.
00000070: b800 c708 a16d 236d 635f 6a14 5f8a 7b3a  .....m#mc_j._.{:
00000080: 21
```

## Cat File

- Git has a built-in plumbing command, cat-file, that allows us to see the
  contents of a commit without needing to futz around with the object files
  directly.

```
git cat-file -p <hash>
```

- using this cat-file we can view the contents of our last commit.

## Trees and Blobs

- Some useful terms in Git to know:

  - `tree`: git's way of storing a directory
  - `blob`: git's way of storing a file

- Here's is the sample output from `git cat-file -p <git-hash>`:

```
tree 5b21d4f16a4b07a6cde5a3242187f6a5a68b060f
author oreximus <oreximus@gmail.com> 1736022653 +0530
committer oreximus <oreximus@gmail.com> 1736022653 +0530

A: add contents.md
```

- Notice that we can see:

  - The `tree` object
  - The `author`
  - The `committer`
  - The commit message

- However, we cannot see the contents of the `contents.md` file itself! that's
  because the `blob` object stores it.

- for checking the `blob` or file hash we'll use the `tree hash` in the
  place of our commit hash:

```
git cat-file -p <your-tree-hash>
```

- and you'll get some output like this:

```
100644 blob ef7e93fc61a91deecaa551c4707e4c3049af42c9	contents.md
```

- now you can again use the git cat-file command to view this file content
  content by replace its hash in the command.

## Second Commit

- some commands to revise:

  - `git log` (`q` to exit, arrow keys to scroll)
  - `git cat-file -p <hash>`

- Note: `log` is a porcelain command, while `cat-file` is a plumbing command.
  You'll use `log` much more often when working on coding projects, but `cat-file`
  is useful for us to understand Git's internals.

- Now, doing git cat-file on the latest commit hash return one extra line
  in the output, of `parent`:

```
tree 37712fab0aa902b37e2197ebb71e4e1ba4f45f3d
parent b5c454d3fabab49a55cd672429abc9602b3b462c
author oreximus <oreximus@gmail.com> 1736085499 +0530
committer oreximus <oreximus@gmail.com> 1736085499 +0530

B: add title
```

## Storing Data

- Git stores an entire snapshot of files on a per-commit level.

### Optimization:

- While it's true that Git stores entire snapshots, it does have some
  performance optimizations so that your `.git` directory doesn't get too
  unbearably large.

      - Git compresses and packs files to store them more efficiently.
      - Git deduplicates files that are the same across different commits.
      If a file doesn't change between commits, Git will only store it once.

## Git Config

- Git stores author information so that when you're making a commit it can
  track who made the change. Here's how you might update your global Git
  configuration (don't do this yet):

```
git config --add --global user.name "oreximus"
git config --add --global user.email "oreximus@gmail.com"
```

- Let's take the command apart:
  - `git config`: The command to interact with your Git configuration.
  - `--add`: Flag stating you want to add a configuration.
  - `--global`: Flag starting you want this configuration to be stored
    globally in your `~/.gitconfig`. The opposite is "local", which stores
    the configuration in the current repository only.
  - `user`: The section.
  - `name`: The key within the setion.
  - `"oreximus"`: The value want to set for the key.
