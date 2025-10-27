# Set up WSL on Windows 11

Windows Subsystem for Linux (WSL) allows developers to install Linux on Windows
and allows a side-by-side use of both Windows and Linux terminals. This tech tip
provides a consistent way to install the most updated version of WSL on your
Windows.

## Useful Background Knowledge

1. WSL 2 was introduced in Windows 11 and some versions of Windows 10 to
   supersede the deprecated WSL 1. WSL 2 is the default target version when you
   install Linux distributions in Windows 11.

1. You can install more than one Linux distribution in WSL for your computer.

1. WSL in Windows 11, by default, uses servicing updates from the Microsoft
   Store. You can get the latest WSL features and patches from the Microsoft
   Store by running the following command

   ```powershell
   wsl.exe --update
   ```

1. There are two types of users in WSL

   1. WSL root user
   1. default user for a distribution in WSL

   When you are logged in to the Linux distribution in WSL,

   1. `sudo passwd` changes the password of the WSL root user.

   1. `passwd` changes the password of the current user of a distribution.

   1. `passwd <username>` changes the password of user associated with
      `<username>` for a distribution.

   1. `sudo` asks for the password of the current user for a distribution.

## Install WSL 2

1. Install WSL 2 (from Microsoft Store) via Windows Terminal.

   Open **Terminal (Admin)**. A Windows PowerShell terminal will appear. Use
   the following command to check if WSL is installed.

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

   Otherwise, if WSL is not installed, you may see the following and press
   any key to install WSL.

   ```text
   The Windows Subsystem for Linux is not installed. You can install by running 'wsl.exe --install'.
   For more information please visit https://aka.ms/wslinstall

   Press any key to install Windows Subsystem for Linux.
   Press CTRL-C or close this window to cancel.
   This prompt will time out in 60 seconds.

   Press any key to continue
   ```

   Once the installation is complete, you should see something similar as
   follows

   ```text
   Downloading: Windows Subsystem for Linux 2.6.1
   Installing: Windows Subsystem for Linux 2.6.1
   Windows Subsystem for Linux 2.6.1 has been installed.
   The operation completed successfully.
   WSL version: 2.6.1.0
   Kernel version: 6.6.87.2-1
   WSLg version: 1.0.66
   MSRDC version: 1.2.6353
   Direct3D version: 1.611.1-81528511
   DXCore version: 10.0.26100.1-240331-1435.ge-release
   Windows version: 10.0.26200.6899
   ```

1. (Optional) If the above step did not trigger the installation process, you
   may run the following command to invoke installation WSL.

   ```powershell
   wsl.exe --install --no-distribution
   ```

1. Once WSL is installed, ensure that WSL 2 is the default.

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

1. Ensure WSL is installed with the latest version.

   ```powershell
   wsl.exe --update
   ```

## Install Linux distribution for WSL

1. Install target Linux distribution via Terminal.

   1. Open a PowerShell Terminal.

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

      Let us choose `Ubuntu-24.04` as an example for the rest of the guide.

   1. Install a target Linux distribution.

      ```powershell
      wsl.exe --install --distribution Ubuntu-24.04
      ```

      Once the installation is done, WSL will prompt for you to create a default
      user account for the target Linux distribution. Enter your preferred
      username and password, and you will be logged in to the Linux
      distribution. You should see an output as follows

      ```text
      Downloading: Ubuntu 24.04 LTS
      Installing: Ubuntu 24.04 LTS
      Distribution successfully installed. It can be launched via 'wsl.exe -d Ubuntu-24.04'
      Launching Ubuntu-24.04...
      Provisioning the new WSL instance Ubuntu-24.04
      This might take a while...
      Create a default Unix user account:
      Create a default Unix user account: my_user
      New password:
      Retype new password:
      passwd: password updated successfully
      To run a command as administrator (user "root"), use "sudo <command>".
      See "man sudo_root" for details.
      my_user@my_computer:/mnt/c/Users/MyUser$
      ```

      Press `Ctrl + D` to logout of the Linux distribution back to PowerShell
      terminal.

   1. Check to ensure target Linux distribution is installed

      ```powershell
      wsl --list --verbose
      ```

      You should see something similar as follows

      ```text
        NAME            STATE           VERSION
      * Ubuntu-22.04    Stopped         2
      ```

   1. (Optional) If you do not see a `*` beside `Ubuntu-24.04`, it means that
      `Ubuntu-24.04` is not set as the default distribution. Run the following
      command to set `Ubuntu-24.04` as the default distribution.

      ```powershell
      wsl.exe --set-default Ubuntu-24.04
      ```

   1. (Optional) WSL allocates a maximum of 50% of the RAM available to your
      Windows operating system for your Linux distribution. If you desire a
      bigger amount of RAM for your Linux distribution, you can change this
      memory setting creating the file `%UserProfile%\.wslconfig` with the
      following configuration

      ```text
      [wsl2]
      memory=8GB
      ```

      Reboot your Windows machine before proceeding to the next step.

   1. Open a new tab in Terminal that has an option similar to
      `Ubuntu 22.04.5 LTS`. You can do this by clicking the "Pull Down v" icon
      beside the  "Add new tab +" icon in Terminal, and select
      `Ubuntu-24.04.05 LTS` to log in. You should see a new Linux terminal as
      follows

      ```bash
      my_user@my_computer:~$
      ```

   1. Update Ubuntu 22.04 to the latest packages and patches.

      ```bash
      sudo apt update
      sudo apt upgrade -y
      ```

      You may need to logout and login again for the patches to come into
      effect in your Linux terminal environment.

> [!TIP]
> It is a good cybersecurity practice to perform daily activities in user
> privileges rather than administrator privileges. If you see your Linux
> terminal ending with a `#` instead of a `$`, it means that you are
> running in superuser `su` account.

## Uninstall a Linux distribution in WSL

To remove a Linux distribution from WSL, open a PowerShell Terminal and run the
following command

```powershell
wsl.exe --shutdown
wsl --unregister Ubuntu-24.04
```
