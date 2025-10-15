# Create local account via PowerShell

> **Disclaimer**: Techniques to create an administrator local account
> immediately after a fresh install or clean reset of Windows 11 is continuously
> evolving and comprehensively covered on the Internet. This tech tip assumes
> you already have an administrator Windows User Account and wish to create
> additional local accounts via a terminal approach.

This tech tip shows you how to create an administrator or user local account
via PowerShell on Windows 11. This workflow is particularly useful for users on
Windows 11 Home, which has more limitations than other Windows editions to
create a local account.

## Useful Background Knowledge

1. A Windows User Account is the identity you use to sign in to Windows. There
   are two types of Windows User Accounts:

   1. **Local account**: Exists only on the computer.

   1. **Microsoft account**: Linked to Microsoft cloud services.

1. There are two tiers of user privileges:

   1. **Administrator**: Grants full control over the Windows system, should be
      reserved for system management purposes.

   1. **Standard User**: Grants limited control over the Windows system, should
      be reserved for daily use.

1. Mixing the above gives you four configurations of Windows User Accounts.

   1. Administrator Microsoft account

   1. Administrator local account

   1. User Microsoft account

   1. User local account

> [!NOTE]
> A Windows User Profile is a collection of settings and files linked to a
> Windows User Account. Windows 11 allocates one Windows User Profile to a
> Windows User Account.

## Create a local account

Once you are logged into an administrator Microsoft or local account on your
Windows 11 system,

1. Open Terminal (Admin). A Windows PowerShell terminal will appear.

1. Store your new account password as a PowerShell variable with the following
   command.

   ```Powershell
   $Password = Read-Host -AsSecureString
   ```

   A blank line appears immediately below your command waiting for your password
   input. Type your new password and press Enter.

1. Store your account username, user full name, and account description as
   variables for convenience.

   ```Powershell
   $UserName = Read-Host
   $FullName = Read-Host
   $Description = Read-Host
   ```

1. Create a new local account with the following command.

   ```Powershell
   New-LocalUser $UserName -Password $Password -FullName $FullName -Description $Description
   ```

1. (Optional) If you are creating an administrator local account, add the newly
   created local account to the Administrators user group.

   ```Powershell
   Add-LocalGroupMember -Group "Administrators" -Member $UserName
   ```

1. Check if the newly created local account has password expiry enabled.
   Password expiry is enabled when ``PasswordExpires = True`` for the account
   name.

   ```Powershell
   Get-CimInstance -ClassName Win32_UserAccount | Format-Table -Property Name, Disabled, PasswordExpires
   ```

1. If the local account has password expiry enabled, disable password expiry.

   ```Powershell
   Set-LocalUser -Name $UserName -PasswordNeverExpires $true
   ```

## Delete a Microsoft account or local account

1. If you need to delete a Windows User Account (e.g., another Microsoft account
   or local account) on your computer, login to an administrator local account
   and open Terminal (Admin).

1. Take note of the account username of the Windows User Account to be deleted
   in the first column (Name) of the following command.

   ```Powershell
   Get-LocalUser
   ```

   Get the user object of the target account username. Replace ``<user name>``
   with the target account username.

   ```Powershell
   $User = Get-LocalUser -Name "<user name>" -ErrorAction Stop
   ```

1. Remove the associated Windows User Profile (from both filesystem and
   registry).

   ```Powershell
   Get-CimInstance -Class Win32_UserProfile | ? SID -eq $User.SID | Remove-CimInstance
   ```

1. Remove the Windows User Account.

   ```Powershell
   Remove-LocalUser -SID $User.SID
   ```
