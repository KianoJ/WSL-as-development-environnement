# WSL as development environnement

## Before starting 

I'm not a pro in WSL or Linux or programmation. I'm just passionate about new technologies and I like to program in my spare time. And English is not my native language so if there are spelling mistakes, excuse me.

## Introduction

I was looking for a solution to be able not to install all frameworks or dependency on my computer to have something cleaner. I've tried different solution that allows me to work easily without the need to install different software in Windows (less messy) while consuming fewer resources:
- using a raspberry
- using a light Linux VM (Fedora server, Ubuntu server)
- using the new WSL 2

## What is WSL ?

WSL stand for `Windows Subsystem for Linux`. It allows to use the Linux terminal inside Windows. 

### What's the point of using that ?

We know that Windows is sometimes less performing than Linux for using some development tool. Using WSL allow to take advantage of a Linux environment without using a virtual machine, server or installing software inside Windows.

As I said earlier, I tried different solutions but :
- using a raspberry dramatically slowed my workflow (speed of SD card and poor performance);
- using a virtual machine include using SSH and all your project are stored in the virtual machine. It also takes more resources (at least one CPU core and 2Go of RAM). Using a less powerful computer will also make slow workflow;
- using WSL use fewer resources than a virtual machine, allow navigating inside of your drive without any configuration and it's easier than other solutions.

## How to use it

#### Requirements

- Windows 10 Pro version 1903 or higher with Build 18362 or higher
- CPU compatible with Virtualization (VT for Intel and AMD-V for AMD)
- WSL2 kernel : https://aka.ms/wsl2kernel

#### Quality of life tool

- Windows package Manager (WinGet-CLI) : https://github.com/microsoft/winget-cli/releases
- Windows new terminal : https://www.microsoft.com/en-us/p/windows-terminal/9n0dx20hk701

Before beginning, I will use `winget` because I hate using the Microsoft Store and the new Windows terminal.

### **1) Install Windows Package Manager**

Download the winget `appxbundle` from GitHub and execute it. It will update the `App Installer` package installed by default. If you can't execute the file, execute this command in powershell **as Admin** to reinstall `App Installer`.

```ps
Get-AppxPackage -allusers Microsoft.DesktopAppInstaller | Foreach {Add-AppxPackage -DisableDevelopmentMode -Register "$($_.InstallLocation)\AppXManifest.xml"}
```

Then you will be able to install the `Windows Package Manager`.

### **2) Install Windows Terminal**

Close all your powershell window and reopen one (no need to open as Admin) and enter this :

```ps
winget install Microsoft.WindowsTerminal -e
```

Once installed you can close Powershell to switch for your new terminal.

### **3) Enable WSL**

Open Terminal as Admin and enter this :

```ps
# Activate WSL
dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart

# Activate Virtual Machine Platform
dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart
```

You will need to reboot your computer. After that reopen Terminal as Admin and enter this :

```ps
# Set WSL 2 default version
wsl --set-default-version 2
```

We almost finish, now you need to install the WSL2 Kernel (Link above) and all done. WSL is set and operational.

### **4) Install your WSL distribution**

I'm using Ubuntu as WSL distribution for multiples reasons :
- first to work with WSL;
- officially supporter by Windows;
- used to this distribution;

You have different method to install Ubuntu. I'll use `winget`. Open Terminal without admin permission and enter :

```ps
winget install ubuntu
```

Once installed, close Terminal and open Ubuntu from the start menu. Wait until it ask you to enter your username (in lowercase) and a password.

### **5) Use Linux inside Windows**

Close Ubuntu windows and open Terminal. Click the drop down button next to the `plus` sign and actual tab then select Ubuntu.

I highly recommend you to update and upgrade packages :

```
sudo apt update && sudo apt upgrade -y
```

By default it will be inside your Windows profile folder. All your drive is int `/mnt` folder. You can change it in Terminal settings by adding `"startingDirectory": "//wsl$/Ubuntu-20.04/home/USERNAME",` in Ubuntu profile.

`Visual Studio Code` will recommend you to install the `Remote - WSL` extension. Activate it, it allow you to start WSL with VSCode.

### **6 - Install Docker Desktop**

Some tools or service is not *yet* available in WLS so we gonna use Docker inside Linux.

Download and install [Docker Desktop](https://desktop.docker.com/win/stable/Docker%20Desktop%20Installer.exe). Let `Install required Windows components for WSL 2` check.

### **7 - Configure Docker**

Once log in, open Docker and skip tutorial.
Open docker's settings. Verify that `Use the WSL 2 based engine` is enabled.
Go to `Resources` -> `WSL integration` and enable Ubuntu then apply.

Now we can use docker inside Ubuntu.

---

## Finish

Congratulation ! You can use and install all your Frameworks inside Linux __***INSIDE***__ Windows.

I'll update how to install some tools or framework.


## More options

WSL instance stay active when you leave the Terminal. You can kill it in Powershell with : 

```bash
# List all running WSL
wsl --list --running
# Terminate a WSL install
wsl -t NAME_OF_THE_DISTRIBUTION

# Or you can kill WSL instance and VMMEN process
wsl --shutdown
```

You can limit the amount of resource WSL use. Create a file called `.wslconfig` inside your user folder and add : 

```
[wsl2]
memory=3GB
processors=2
```

Close all instance and shut WSL

__OR__

Open Powershell __not as admin__ and run :

```powershell
New-Item -ItemType File -Path $env:USERPROFILE -Name .wslconfig
"[wsl2]" | Out-File -FilePath $env:USERPROFILE\.wslconfig
"memory=3GB" | Out-File -FilePath $env:USERPROFILE\.wslconfig -Append
"processors=2" | Out-File -FilePath $env:USERPROFILE\.wslconfig -Append
wsl --shutdown 
```

Change the amount of memory you allow and CPU core to fit your computer available resources.

---
