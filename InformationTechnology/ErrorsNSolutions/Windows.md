# Windows Common Errors and Their Expected Solutions:

## Enabling script execution on Windows 11:

[👉**Source of the information**👈](https://www.makeuseof.com/enable-script-execution-policy-windows-powershell/#:~:text=Open%20the%20Privacy%20%26%20Security%20tab,Require%20signing%20for%20remote%20scripts.)

- On Powershell with Admin Privilege:
```
Set-ExecutionPolicy RemoteSigned
```

- To set the **RemoteSigned** execution policy for **CurrentUser**, use the following command:

```
Set-ExecutionPolicy RemoteSigned -Scope CurrentUser
```
