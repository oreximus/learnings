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
