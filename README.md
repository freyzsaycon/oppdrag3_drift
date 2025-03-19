# oppdrag3_drift


## Powershell commands for Windows Server


## Install new roles

```
Get-WindowsFeature

Install-WindowsFeature -name ad-domain-services -IncludeAllSubFeature - IncludeManagementTools

Install-WindowsFeature -name DNS -IncludeAllSubFeature - IncludeManagementTools

Install-WindowsFeature -name DHCP -IncludeAllSubFeature - IncludeManagementTools

Install-WindowsFeature -name Web-Webserver -IncludeAllSubFeature - IncludeManagementTools

Install-WindowsFeature -name FS-fileserver -IncludeAllSubFeature - IncludeManagementTools

```

Restart PC

## Set new static IP
```
New-NetIPAddress -InterfaceIndex <YourInterfaceIndex> -IPAddress <CorrectIPAddress> -PrefixLength 24 -DefaultGateway <YourGateway>

```


## Configure domain

```
Install-ADDSForest -DomainName "name.local" -InstallDNS -Force

New-ADOrganizationUnit -Name "name" -Path "DC=name,DC=local"

Get-ADOrganizationalUnit -Filter*|Select Name, DistinguishedName

```

## Configure DHCP

```
Add-DhcpServerInDC -Dnsname "name.local" -IPAddress xxx.xxx.xxx.xxx

restart-service DHCPServer

add-dhcpserverv4scope -name "name" -StartRange xxx.xxx.xxx.xxx -EndRange xxx.xxx.xxx.xxx -Subnetmask 255.255.255.0 -state Active

Get-DhcpServerv4Scope

```

## Make test account in AD

```
Redircmp "OU=name, DC=name,DC=name"

Rediusr "OU=name,DC=name,DC=name"

New-ADUser -Name "Test User" -SamAccountName "test.user" -UserPrincipalName "test.user@name.name" -AccountPassword (ConvertTo-SecureString "P@ssw0rd!" -AsPlainText -Force) -Enabled $true

Get-ADUser -Identity "test.user"|Select DistinguishedName

```


