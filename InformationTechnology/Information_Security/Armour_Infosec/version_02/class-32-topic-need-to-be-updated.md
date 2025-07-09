# Class 01

## Topic: Shell configuration:

### grc configuration:

- installing in RHEL distros:

```
yum install bash-*
```

- Downloading the grc from the github, extract it and place the
folder into `/opt`.

- using `grc` example:

```
grc ping 8.8.8.8
```

- you can provide grc

- setting default shell in linux

```
chsh -s $(which zsh)
```

### Installing the fish shell:

- Download it from its source, and configure the fish shell
repo.

- Then install it via yum:

```
yum install fish
```

# Class 02

## Topic: Group Policies in ADDS

- centralize wallpaper setting in a OU:
    - create a new public folder name: `data`
        - share this folder to the particular OU, only with read permission

- Now make a policy:
    - Policies
        - for setting up the wallpaper: (provide the network location with IP)
        - then gpupdate /force

- Sharing a data folder from the server:
    - creating a blank folder under c drive and sharing to the particular OU.

- Blocking Devices
    - System --> Removable Storage Access
    - on cmd --> gpupdate /force

- Prevent Access to Drive

- Folder Redirection

### Tools:

- Hiren's BootCD
- Windows Preinstallation Environment
