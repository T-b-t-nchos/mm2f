# 🔧 mm2f
##### \[M\]ulti package \[M\]anager packages \[To\] a \[F\]ile

## ✨️ Description
This is a simple script to install packages with multiple package managers (winget, choco, scoop, apt) to a file.  
You can customize the priority of package managers, the commands to install packages, and so on.   
It's designed for use in dotfiles.

> [!WARNING]
> This script is not a package manager.
> It's just a simple script to install packages with multiple package managers.
> So, you need to install the package managers before using this script manually.  

> [!CAUTION]
> Do not run this script with untrusted `packages.yml`.  
> Always review the file or run in a sandbox/container.  

## 🎉 Features
- Manage packages with multiple package managers with a single file.
- Customize the priority of package managers.
- Customize the commands to install packages.
- Supports Windows and Linux.

## 📦 Requirements
### 🪟 Windows
- powershell 7 (For running the script)

### 🐧 Linux
- bash (For running the script)
- sudo (For running as root)
- wget (For installing yq)

## 📦 Package managers
### 🪟 Windows
- winget
- scoop
- choco

### 🐧 Linux
- apt
- scoop
- pacman

> [!NOTE]
> If you want to install the scoop package only on Linux, you can use `linuxscoop` instead of `scoop`.
> Windows users can use `winscoop` instead of `scoop`.
> Also, you can use `scoop` if you want to install the scoop package on both Windows and Linux.

## 📦 Usage
1. Install the package managers you want to use.
2. Copy mm2f.sh, mm2f.ps1, or both files to the directory where you want to use it.
3. Edit the `packages.yml` file. (You can use the `packages.example.yml` as an example.)
4. Run the script.
5. Enjoy!

## 🔧 Configuration
```yaml
# packages.yml

# options is optional.
options:
  windows:
    # Priority of package managers to install packages.
    priority: [winget, choco, winscoop, scoop]

    # Commands to install packages.
    # You can use {id} as a placeholder for the package ID.
    commands:
      winget: winget install --id {id} -e --accept-package-agreements --accept-source-agreements
      choco: choco install {id} -y
      scoop: scoop install {id}

  # Same as above, but for Linux.
  linux:
    priority: [apt, linuxscoop, scoop, pacman]
    commands:
      apt: sudo apt install -y {id}
      scoop: scoop install {id}
      pacman: sudo pacman -S --noconfirm {id}    

packages:
  - name: Package name
    winget: Winget package ID (Optional)
    choco: Chocolatey package name (Optional)
    scoop: Scoop package name (Optional)
    winscoop: Scoop package name (Only for Windows) (Optional)
    apt: Apt package name (Optional)
    pacman: Pacman package name (Only for Linux) (Optional)
    linuxscoop: Scoop package name (Only for Linux) (Optional)
```

## 🧩 Options
- You can set the package.yml file path with the first argument. (e.g. `mm2f.sh /path/to/packages.yml`)  
  Default: `./packages.yml`
