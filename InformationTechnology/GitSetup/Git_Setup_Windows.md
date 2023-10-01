# Windows Git Setup

## Installing Softwares with Chocolatey:

- **Command to be run in Windows powershell**

```
Set-ExecutionPolicy Bypass -Scope Process -Force; [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://community.chocolatey.org/install.ps1'))
```

#### Setting Up Access Token in Github:

- Settings --> Developer Option --> Access Token (Classic)

#### Git Basic Commands:

- For Cloning Repository:

```
git clone <repo link>
```

- For Checking Status:

```
git status
```

- Adding Files in Git

```
git add .
```

- Before Pushing any changes to the Remote Repository, setup your IDs:

- **for username**

```
git config --global user.name "oreximus"
```

- **for email**

```
git config --global user.name "oreximus"
```

- Now you can finally Push:

```
git push
```

### Contributing in The Project:

- Fork the Repo

- Clone the Repo

- Create a separate branch and Work with it!

- Creating a Branch:

```
git branch <branch name>
```

- listing branches:

```
git branch
```

- Changing the branch

```
git checkout <branch name>
```


