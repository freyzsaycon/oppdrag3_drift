# oppdrag3_drift


## Powershell commands for Windows Server


## Set new static IP
```
New-NetIPAddress -InterfaceIndex <YourInterfaceIndex> -IPAddress <CorrectIPAddress> -PrefixLength 24 -DefaultGateway <YourGateway>

```

## Install new roles

```
Get-WindowsFeature

Install-WindowsFeature -name ad-domain-services -IncludeAllSubFeature - IncludeManagementTools

Install-WindowsFeature -name DNS -IncludeAllSubFeature - IncludeManagementTools

Install-WindowsFeature -name DHCP -IncludeAllSubFeature - IncludeManagementTools

Install-WindowsFeature -name Web-Webserver -IncludeAllSubFeature - IncludeManagementTools

Install-WindowsFeature -name FS-fileserver -IncludeAllSubFeature - IncludeManagementTools

```

## Make domain 

```
Install-ADDSForest -DomainName "name.local" -InstallDNS -Force

New-ADOrganizationUnit -Name "name" -Path "DC=name,DC=local"


```

