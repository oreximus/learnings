# Notes

- create a blank folder in the C drive.

  - then share it the group for which you want the access to it.

- then set the Group Policy of `folder redirection` from:
  - User Configuration --> Administrative Template --> System --> Folder Redirection

> Group Policy Management (use this for editing GPO)
> Apply `gpupdate /force`, after applying or making any changes in the GPO

- while applying setting for each folder in folder redirection choose this option:
  - `create a folder for each user under the root path`
