# Starship terminal

## Install scoop

```bash
Set-ExecutionPolicy RemoteSigned -scope CurrentUser
iwr -useb get.scoop.sh | iex
```

## Install starship

```
scoop install starship
```

## Load through Powershell

$PROFILE
-> path is: c:\Users\{username}\Documents\WindowsPowerShell\
-> create file: Microsoft.PowerShell_profile.ps1


```powershell
Invoke-Expression (&starship init powershell)
```

