# Set up WSL on Windows 11

Windows Subsystem for Linux (WSL) allows developers to install Linux on Windows
and allows a side-by-side use of both Windows and Linux terminals. This tech tip
provides a fast and consistent way to install the most updated version of WSL on
your Windows.

## Useful Background Knowledge

1. WSL 2 was introduced in Windows 11 and some versions of Windows 10 to
   supersede the deprecated WSL 1. WSL 2 is the default target version when you
   install Linux distributions in Windows 11.

1. WSL, by default, allocates up to 50% of the RAM available to your Windows
   operating system. You can change this setting by creating the file at
   `%UserProfile%\.wslconfig` with the following content

   ```text
   [wsl2]
   memory=8GB
   ```

1. WSL in Windows 11 uses servicing updates from the Microsoft Store. You can
   get the latest WSL features and patches by running the following command

   ```powershell
   wsl.exe --update
   ```

## Install WSL 2

1. Install WSL 2 (from Microsoft Store) via Windows Terminal.

   1. Open Terminal (Admin). A Windows PowerShell terminal will appear. Use the
      following command to check if WSL is installed.

      ```powershell
      wsl.exe --version
      ```

      If WSL is installed, you should see something similar as follows

      ```text
      WSL version: 2.6.1.0
      Kernel version: 6.6.87.2-1
      WSLg version: 1.0.66
      MSRDC version: 1.2.6353
      Direct3D version: 1.611.1-81528511
      DXCore version: 10.0.26100.1-240331-1435.ge-release
      Windows version: 10.0.26100.6899
      ```

   1. If WSL is not installed, run the following command to install WSL.

      ```powershell
      wsl.exe --install --no-distribution
      ```

   1. Once WSL is installed, run the following to ensure that WSL 2 is the
      default.

      ```powershell
      wsl.exe --set-default-version 2
      wsl.exe --status
      ```

      You should see something similar as follows

      ```text
      Default Version: 2
      WSL1 is not supported with your current machine configuration.
      Please enable the "Windows Subsystem for Linux" optional component to use WSL1.
      ```

1. Update WSL to latest version.

   ```powershell
   wsl.exe --update
   ```

## Install Linux distribution for WSL

1. Install target Linux distribution (from Microsoft Store).

   1. Open a standard Terminal (without Admin). A Windows PowerShell terminal
      will appear.

   1. List available Linux distributions.

      ```powershell
      wsl.exe --list --online
      ```

      The list should look something similar to the following

      ```text
      NAME                            FRIENDLY NAME
      AlmaLinux-8                     AlmaLinux OS 8
      AlmaLinux-9                     AlmaLinux OS 9
      AlmaLinux-Kitten-10             AlmaLinux OS Kitten 10
      AlmaLinux-10                    AlmaLinux OS 10
      Debian                          Debian GNU/Linux
      FedoraLinux-42                  Fedora Linux 42
      SUSE-Linux-Enterprise-15-SP6    SUSE Linux Enterprise 15 SP6
      SUSE-Linux-Enterprise-15-SP7    SUSE Linux Enterprise 15 SP7
      Ubuntu                          Ubuntu
      Ubuntu-24.04                    Ubuntu 24.04 LTS
      archlinux                       Arch Linux
      kali-linux                      Kali Linux Rolling
      openSUSE-Tumbleweed             openSUSE Tumbleweed
      openSUSE-Leap-16.0              openSUSE Leap 16.0
      Ubuntu-20.04                    Ubuntu 20.04 LTS
      Ubuntu-22.04                    Ubuntu 22.04 LTS
      OracleLinux_7_9                 Oracle Linux 7.9
      OracleLinux_8_10                Oracle Linux 8.10
      OracleLinux_9_5                 Oracle Linux 9.5
      openSUSE-Leap-15.6              openSUSE Leap 15.6
      ```

      Let us choose `Ubuntu-22.04` as an example for the rest of the guide.

   1. Install a target Linux distribution and set it as default distribution.

      ```powershell
      wsl.exe --install --distribution Ubuntu-22.04
      wsl.exe --set-default Ubuntu-22.04
      ```

   1. Check to ensure target Linux distribution is installed

      ```powershell
      wsl --list --verbose
      ```

      You should see something similar as follows

      ```text
        NAME            STATE           VERSION
      * Ubuntu-22.04    Stopped         2
      ```

   1. You may want to reboot your Windows machine at this point to ensure the
      Linux installation is complete for the next step.

   1. Open a new tab in Terminal app that has an option similar to
      `Ubuntu 22.04.5 LTS`. You should see something similar to the following

      ```text
      Provisioning the new WSL instance Ubuntu-24.04
      This might take a while...
      Create a default Unix user account:
      ```

      Enter your username and password as the default user to login to your
      Linux distribution.

   1. (Optional) Update Ubuntu 22.04 to the latest packages and patches.

      ```bash
      sudo apt update
      sudo apt upgrade -y
      ```

## Uninstall Linux distribution in WSL

To remove a Linux distribution from WSL, open a standard Terminal (without
Admin) and run the following

```powershell
wsl.exe --shutdown
wsl --unregister Ubuntu-22.04
```

## Password Management of WSL Users

There are two types of users in WSL

1. WSL root user
1. default user for a distribution in WSL

When you are logged in to the Linux distribution in WSL,

1. `sudo passwd` changes the password of the WSL root user.

1. `passwd` changes the password of the current user of a distribution.

1. `passwd <username>` changes the password of user associated with
   `<username>` for a distribution.

1. `sudo` asks for the password of the current user for a distribution.