# Enable Windows DNS client to use DNS-over-HTTPS

Windows 11 comes pre-registered with a list of popular public Domain Name
System (DNS) servers that Windows can connect to resolve network addresses.
However, the default settings does not automatically use the more secure DNS
protocol known as DNS-over-HTTPS (DoH) for these public DNS servers.

This tech tip shows you how to do a one time configuration to enable the Windows
client to automatically enable DoH for public DNS servers provided by Google and
Cloudflare.

## Useful Background Knowledge

1. PowerShell Cmdlet Official Documentation

   1. [Get-DnsClientDohServerAddress](https://learn.microsoft.com/en-us/powershell/module/dnsclient/get-dnsclientdohserveraddress)

   1. [Set-DnsClientDohServerAddress](https://learn.microsoft.com/en-us/powershell/module/dnsclient/set-dnsclientdohserveraddress)

   1. [Add-DnsClientDohServerAddress](https://learn.microsoft.com/en-us/powershell/module/dnsclient/add-dnsclientdohserveraddress)

1. Official Documentation to [setup Cloudflare public DNS](https://developers.cloudflare.com/1.1.1.1/setup/)

## Enable DoH for Google and Cloudflare public DNS using PowerShell Terminal

1. Open **Terminal (Admin)**. A Windows PowerShell terminal will appear.

1. Copy and paste the following command to enable DoH for Google public DNS.

   ```PowerShell
   Set-DnsClientDohServerAddress -ServerAddress '8.8.8.8' -AutoUpgrade $True;
   Set-DnsClientDohServerAddress -ServerAddress '2001:4860:4860::8888' -AutoUpgrade $True;
   Set-DnsClientDohServerAddress -ServerAddress 8.8.4.4 -AutoUpgrade $True;
   Set-DnsClientDohServerAddress -ServerAddress '2001:4860:4860::8844' -AutoUpgrade $True
   ```

1. Copy and paste the following command to enable DoH for Cloudflare public DNS.

   ```PowerShell
   Set-DnsClientDohServerAddress -ServerAddress '1.1.1.1' -AutoUpgrade $True;
   Set-DnsClientDohServerAddress -ServerAddress '2606:4700:4700::1111' -AutoUpgrade $True;
   Set-DnsClientDohServerAddress -ServerAddress 1.0.0.1 -AutoUpgrade $True;
   Set-DnsClientDohServerAddress -ServerAddress '2606:4700:4700::1001' -AutoUpgrade $True
   ```

1. Verify that the Windows entries for the Google and Cloudflare public DNS
   servers have the `AutoUpgrade` column set to `True`.

   ```PowerShell
   Get-DnsClientDohServerAddress
   ```

   You should see an output similar to that below.

   ```Text
   ServerAddress        AllowFallbackToUdp AutoUpgrade DohTemplate
   -------------        ------------------ ----------- -----------
   149.112.112.112      False              False       https://dns.quad9.net/dns-query
   9.9.9.9              False              False       https://dns.quad9.net/dns-query
   8.8.8.8              False              True        https://dns.google/dns-query
   8.8.4.4              False              True        https://dns.google/dns-query
   1.1.1.1              False              True        https://cloudflare-dns.com/dns-query
   1.0.0.1              False              True        https://cloudflare-dns.com/dns-query
   2001:4860:4860::8844 False              True        https://dns.google/dns-query
   2001:4860:4860::8888 False              True        https://dns.google/dns-query
   2606:4700:4700::1001 False              True        https://cloudflare-dns.com/dns-query
   2606:4700:4700::1111 False              True        https://cloudflare-dns.com/dns-query
   2620:fe::9           False              False       https://dns.quad9.net/dns-query
   2620:fe::fe          False              False       https://dns.quad9.net/dns-query
   ```

## Adding Cloudflare for Families DoH entries

If you plan to use Cloudflare 1.1.1.1 for Families DoH, you can follow the steps
below to do this.

> [!CAUTION]
> These public DNS filter domain names and may cause degradation in your network
> performance. Use them if you assessed that the pros of the additional security
> features outweigh the cons of possible lower performance.

1. Add "block malware" series of Cloudflare for Families public DNS.

   ```PowerShell
   Add-DnsClientDohServerAddress 1.1.1.2 https://security.cloudflare-dns.com/dns-query -AutoUpgrade $True;
   Add-DnsClientDohServerAddress 1.0.0.2 https://security.cloudflare-dns.com/dns-query -AutoUpgrade $True;
   Add-DnsClientDohServerAddress 2606:4700:4700::1112 https://security.cloudflare-dns.com/dns-query -AutoUpgrade $True;
   Add-DnsClientDohServerAddress 2606:4700:4700::1002 https://security.cloudflare-dns.com/dns-query -AutoUpgrade $True
   ```

1. Add "block malware & adult content" series of Cloudflare for Families public
   DNS.

   ```PowerShell
   Add-DnsClientDohServerAddress 1.1.1.3 https://family.cloudflare-dns.com/dns-query -AutoUpgrade $True;
   Add-DnsClientDohServerAddress 1.0.0.3 https://family.cloudflare-dns.com/dns-query -AutoUpgrade $True;
   Add-DnsClientDohServerAddress 2606:4700:4700::1113 https://family.cloudflare-dns.com/dns-query -AutoUpgrade $True;
   Add-DnsClientDohServerAddress 2606:4700:4700::1003 https://family.cloudflare-dns.com/dns-query -AutoUpgrade $True
   ```

## Back to Main Page

> [!NOTE]
> This tech tip is part of [0xNixxy Tech Tips](../README.md) series.
