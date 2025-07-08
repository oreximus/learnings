# Class 01

## Topic: Environment Variables:

- printing variables:

**for example printing the executables paths in the system:**
```
echo $PATH
```

- printing current logged-in user:

```
echo $USER
```

- printing the current home directory value:

```
echo $HOME
```

- printing the present working directory:

```
echo $PWD
```

- defining custom variables:

```
var1="My variable value"
```

- printing the variable value:

```
ech $var1
```

- exporting variables in the shell environment, (make this available to subprocesses):

```
export target=192.168.1.1
```

- testing (i.e. exporting IP of the target and pinging it):

```
ping target
```

- printing whats in our `env`:

```
env
```

- permanent environment variables declaration:

**save this in your `.bashrc` file**:

```
export MY_VAR="my-persistent-value"
```

- reloading the changes in the .bashrc file:

```
source ~/.bashrc
```

### Shells

- used to interact with the operating system

- common shells in linux:
    - `sh`: Bourne Shells, classic shell.
    - `bash`: Bourne Again Shell, most commonly used shell in linux.
    - `ksh`: Korn Shell
    - `zsh`: Z shell
        - highly customizable shell.
    - `fish`: Friendly interactive shell.

- listing all of the availables shells in linux:

```
cat /etc/shells
```

- checking the current shell:

```
echo $SHELL
```

# Class 02

## Topic: Group Policies Application on users in ADDS OU.

- you need a OU named HR and Group name HR.

- and hr1, hr2, hr3, users.

- same for sales, OU, a group and users.

- you need a OU named: Manager, group MGR and somewhat three users.

> In the actual environment, the local admin is blocked.

- applying the group policies from the server:
    - open the group policy management:
        - select the forest --> domain --> select OU --> group policy object
            - create your own new policy
                - name it (i.e. HR)
                    - edit (right click)
                        - user configuration --> Policies --> Admin. Template
                            - (i.e. applying Personalization Policies)
                            - You can cross check this via looking at HR Policy settings
                            (**restart the client systems after application of policies**)

> Try to create a linked group policy

> Try to block the control panel for the OU users.

**command to update the group policies**:

```
gpupdate /force
```

## Homework

- Storage
- USB Block
- Registry Block
