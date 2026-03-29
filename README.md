# PowerShell & Command Prompt Commands

> [!IMPORTANT]
> Created and tested with **PowerShell 5.1**

INDEX

1. **GENERAL (PowerShell)**
   - Get-Process
     - [Show processes by name](#show-processes-by-name)
     - [Show file version info for a process](#show-file-version-info-for-a-process)
   - Start-Process
     - [Start a process or executable file](#start-a-process-or-executable-file)
   - Get-WindowsOptionalFeature
     - [Check the status of the built-in Telnet Client feature](#check-the-status-of-the-built-in-telnet-client-feature)
     - [Install and enable the built-in Telnet Client feature](#install-and-enable-the-built-in-telnet-client-feature)
     - [Disable the built-in Telnet Client feature](#disable-the-built-in-telnet-client-feature)
   - Test-NetConnection
     - [Test a port on remote host](#test-a-port-on-remote-host)
     - [Test a port on remote host with advanced details](#test-a-port-on-remote-host-with-advanced-details)
   - Get-SmbSession
     - [Show active SMB sessions](#show-active-smb-sessions)
   - Get-SmbOpenFile
     - [Show SMB files opened by users](#show-smb-files-opened-by-users)
   - Remove-Item
     - [Delete PSReadLine command history file](#delete-psreadline-command-history-file)
   - Get-CimInstance
     - [Retrieving BIOS serial number (output as object)](#retrieving-bios-serial-number-output-as-object)
     - [Retrieving BIOS serial number (output as a simple value)](#retrieving-bios-serial-number-output-as-a-simple-value)

2. **ADDS (PowerShell)**
   - Get-ADUser
     - [Show users of an OU](#show-users-of-an-ou)
     - [Export users of an OU to CSV](#export-users-of-an-ou-to-csv)
     - [Show only enabled users of an OU](#show-only-enabled-users-of-an-ou)
     - [Export only enabled users of an OU to CSV](#export-only-enabled-users-of-an-ou-to-csv)
     - [Show only disabled users of an OU](#show-only-disabled-users-of-an-ou)
     - [Export only disabled users of an OU to CSV](#export-only-disabled-users-of-an-ou-to-csv)
   - Get-ADUser + Set-ADUser
     - [Edit a user's profile attribute](#edit-a-users-profile-attribute)
     - [Update attributes (e.g. initials) via UPN filter](#update-attributes-eg-initials-via-upn-filter)
   - Get-ADGroup
     - [Find groups that contain a specific word in the name](#find-groups-that-contain-a-specific-word-in-the-name)
     - [Show all AD groups with the number of members](#show-all-ad-groups-with-the-number-of-members)
   - Get-ADGroupMember
     - [Show members of an AD group](#show-members-of-an-ad-group)
   - Get-ADComputer
     - [Show details of an AD computer](#show-details-of-an-ad-computer)
     - [Show details for a list of AD computers](#show-details-for-a-list-of-ad-computers)
     - [Export details for a list of AD computers](#export-details-for-a-list-of-ad-computers)
   - Get-ADDomainController
     - [Locate the Primary DC](#locate-the-primary-dc)
     - [Find DC with specific services](#find-dc-with-specific-services)
   - Start-ADSyncSyncCycle
     - [Start Azure AD Connect Sync](#start-azure-ad-connect-sync)

3. **EXCHANGE (Exchange Management Shell)**
   - Get-DistributionGroup
     - [Show distribution group details](#show-distribution-group-details)

4. **OTHER (Command Prompt)**
   - Repadmin
     - [Show AD replica status](#show-ad-replica-status)
     - [General summary of the AD reply](#general-summary-of-the-ad-reply)
   - gpupdate
     - [Force a background update of all Group Policy settings](#force-a-background-update-of-all-group-policy-settings)
   - ipconfig
     - [Displays the contents of the DNS client resolver cache](#displays-the-contents-of-the-dns-client-resolver-cache)
     - [Flushes and resets the contents of the DNS client resolver cache](#flushes-and-resets-the-contents-of-the-dns-client-resolver-cache)
   - netstat
     - [Show active connections and processes](#show-active-connections-and-processes)
     - [Show keyword-filtered active connections and processes](#show-keyword-filtered-active-connections-and-processes)
   - tasklist
     - [Show keyword-filtered active processes](#show-keyword-filtered-active-processes)
   - query
     - [Show users connected to the machine](#show-users-connected-to-the-machine)
   - winget
     - [List applications with an upgrade available](#list-applications-with-an-upgrade-available)

<br><br><br>

## GENERAL (PowerShell)

## Get-Process

#### Show processes by name

```powershell
Get-Process -Name "<PROCESS_NAME[]>"
```

#### Show file version info for a process

```powershell
Get-Process -Name "<PROCESS_NAME[]>" -FileVersionInfo
```

## Start-Process

#### Start a process or executable file

```powershell
Start-Process -FilePath "<PROCESS_NAME/FILE_PATH>"
```

## Get-WindowsOptionalFeature

#### Check the status of the built-in Telnet Client feature

```powershell
Get-WindowsOptionalFeature -Online -FeatureName "TelnetClient"
```

#### Install and enable the built-in Telnet Client feature

```powershell
Enable-WindowsOptionalFeature -Online -FeatureName "TelnetClient"
```

#### Disable the built-in Telnet Client feature

```powershell
Disable-WindowsOptionalFeature -Online -FeatureName "TelnetClient"
```

## Test-NetConnection

#### Test a port on remote host

```powershell
Test-NetConnection -ComputerName "<HOSTNAME/IP>" -Port "<PORT>"
```

#### Test a port on remote host with advanced details

```powershell
Test-NetConnection -ComputerName "<HOSTNAME/IP>" -Port "<PORT>" -InformationLevel "Detailed"
```

## Get-SmbSession

#### Show active SMB sessions

```powershell
Get-SmbSession | Select-Object ClientComputerName, ClientUserName, NumOpens, SessionId
```

## Get-SmbOpenFile

#### Show SMB files opened by users

```powershell
Get-SmbOpenFile | Select-Object ClientComputerName, ClientUserName, Path, SessionId
```

## Remove-Item

#### Delete PSReadLine command history file

```powershell
Remove-Item (Get-PSReadLineOption).HistorySavePath
```

## Get-CimInstance

#### Retrieving BIOS serial number (output as object)

```powershell
Get-CimInstance -ClassName Win32_BIOS -Property SerialNumber | Select-Object -Property SerialNumber
```

#### Retrieving BIOS serial number (output as a simple value)

```powershell
Get-CimInstance -ClassName Win32_BIOS -Property SerialNumber | Select-Object -ExpandProperty SerialNumber
```

```powershell
(Get-CimInstance -ClassName Win32_BIOS -Property SerialNumber).SerialNumber
```

<br><br><br>

## ADDS (PowerShell)

## Get-ADUser

#### Show users of an OU

```powershell
Get-ADUser -Filter * -SearchBase "OU=<OU_NAME>,OU=<OU_NAME>,DC=<SUBDOMAIN>,DC=<SLD>,DC=<TLD>" -Properties Name | Select-Object Name, Enabled, DistinguishedName | Format-Table -AutoSize
```

#### Export users of an OU to CSV

```powershell
Get-ADUser -Filter * -SearchBase "OU=<OU_NAME>,OU=<OU_NAME>,DC=<SUBDOMAIN>,DC=<SLD>,DC=<TLD>" -Properties Name | Select-Object Name, Enabled, DistinguishedName | Export-Csv -Path "C:\Users\<USER_NAME>\Documents\User_List.csv" -NoTypeInformation -Encoding UTF8
```

#### Show only enabled users of an OU

```powershell
Get-ADUser -Filter 'Enabled -eq $true' -SearchBase "OU=<OU_NAME>,OU=<OU_NAME>,DC=<SUBDOMAIN>,DC=<SLD>,DC=<TLD>" -Properties Name | Select-Object Name, Enabled, DistinguishedName | Format-Table -AutoSize
```

#### Export only enabled users of an OU to CSV

```powershell
Get-ADUser -Filter 'Enabled -eq $true' -SearchBase "OU=<OU_NAME>,OU=<OU_NAME>,DC=<SUBDOMAIN>,DC=<SLD>,DC=<TLD>" -Properties Name | Select-Object Name, Enabled, DistinguishedName | Export-Csv -Path "C:\Users\<USER_NAME>\Documents\Enabled_User_List.csv" -NoTypeInformation -Encoding UTF8
```

#### Show only disabled users of an OU

```powershell
Get-ADUser -Filter 'Enabled -eq $false' -SearchBase "OU=<OU_NAME>,OU=<OU_NAME>,DC=<SUBDOMAIN>,DC=<SLD>,DC=<TLD>" -Properties Name | Select-Object Name, Enabled, DistinguishedName | Format-Table -AutoSize
```

#### Export only disabled users of an OU to CSV

```powershell
Get-ADUser -Filter 'Enabled -eq $false' -SearchBase "OU=<OU_NAME>,OU=<OU_NAME>,DC=<SUBDOMAIN>,DC=<SLD>,DC=<TLD>" -Properties Name | Select-Object Name, Enabled, DistinguishedName | Export-Csv -Path "C:\Users\<USER_NAME>\Documents\Disabled_User_List.csv" -NoTypeInformation -Encoding UTF8
```

## Get-ADUser + Set-ADUser

#### Edit a user's profile attribute

```powershell
Get-ADUser -Filter {GivenName -like "<FIRST_NAME>" -and Surname -like "<LAST_NAME>"} | Set-ADUser -title "JOB_TITLE"
```

#### Update attributes (e.g. initials) via UPN filter

```powershell
Get-ADUser -Filter "UserPrincipalName -like '<E-MAIL>'" | Set-ADUser -Replace @{initials="000"}
```

## Get-ADGroup

#### Find groups that contain a specific word in the name

```powershell
Get-ADGroup -Filter 'Name -like "*<KEYWORD>*"' | Select-Object Name, DistinguishedName, GroupScope, GroupCategory
```

#### Show all AD groups with the number of members

```powershell
Get-ADGroup -Filter * | Select-Object Name, GroupScope, GroupCategory, @{Name="MembersCount";Expression={(Get-ADGroupMember $_ | Measure-Object).Count}} | Format-Table -AutoSize
```

## Get-ADGroupMember

#### Show members of an AD group

```powershell
Get-ADGroupMember -Identity "<ADGroup>"
```

## Get-ADComputer

#### Show details of an AD computer

```powershell
Get-ADComputer -Identity "<ADComputer>" -Properties Description | Select-Object Name, DNSHostName, Description | Format-Table -AutoSize
```

#### Show details for a list of AD computers

```powershell
Get-Content "C:\Users\<USER_NAME>\Documents\Server_List.txt" | ForEach-Object {Get-ADComputer -Identity $_ -Properties Description | Select-Object Name, DNSHostName, Description} | Format-Table -AutoSize
```

#### Export details for a list of AD computers

```powershell
Get-Content "C:\Users\<USER_NAME>\Documents\Server_List.txt" | ForEach-Object { Get-ADComputer -Identity $_ -Properties Description | Select-Object Name, DNSHostName, Description } | Export-Csv -Path "C:\Users\<USER_NAME>\Documents\Server_Output.csv" -NoTypeInformation -Encoding UTF8
```

## Get-ADDomainController

#### Locate the Primary DC

```powershell
Get-ADDomainController -Discover -Service "PrimaryDC"
```

#### Find DC with specific services

```powershell
Get-ADDomainController -Discover -Domain "<FQDN>" -Service "PrimaryDC", "TimeService"
```

## Start-ADSyncSyncCycle

#### Start Azure AD Connect Sync

```powershell
Start-ADSyncSyncCycle -PolicyType Delta
```

<br><br><br>

## EXCHANGE (Exchange Management Shell)

## Get-DistributionGroup

#### Show distribution group details

```powershell
Get-DistributionGroup -Identity "<DistributionGroupIdParameter>" | Format-List
```

<br><br><br>

## OTHER (Command Prompt)

## Repadmin

#### Show AD replica status

```bash
repadmin /showrepl
```

#### General summary of the AD reply

```bash
repadmin /replsummary
```

## gpupdate

#### Force a background update of all Group Policy settings

```bash
gpupdate /force
```

## ipconfig

#### Displays the contents of the DNS client resolver cache

```bash
ipconfig /displaydns
```

#### Flushes and resets the contents of the DNS client resolver cache

```bash
ipconfig /flushdns
```

## netstat

#### Show active connections and processes

```bash
netstat -abno
```

#### Show keyword-filtered active connections and processes

```bash
netstat -abno | findstr /I "<KEYWORD>"
```

## tasklist

#### Show keyword-filtered active processes

```bash
tasklist | findstr /I "<KEYWORD>"
```

## query

#### Show users connected to the machine

```bash
query user
```

## winget

#### List applications with an upgrade available

```bash
winget upgrade
```
