# Powershell commands for Windows Server 🖥️

## Install new roles for Windows Server Manager

```powershell
# Finds all downloadable features for server
Get-WindowsFeature 

# Install all required features below
Install-WindowsFeature -name ad-domain-services -IncludeAllSubFeature - IncludeManagementTools

Install-WindowsFeature -name DNS -IncludeAllSubFeature - IncludeManagementTools

Install-WindowsFeature -name DHCP -IncludeAllSubFeature - IncludeManagementTools

Install-WindowsFeature -name Web-Webserver -IncludeAllSubFeature - IncludeManagementTools

Install-WindowsFeature -name FS-fileserver -IncludeAllSubFeature - IncludeManagementTools

```

Restart PC after installation

## Set new static IP
```powershell
New-NetIPAddress -InterfaceIndex <YourInterfaceIndex> -IPAddress <CorrectIPAddress> -PrefixLength 24 -DefaultGateway <YourGateway>
```

## Add/Configure domain

```powershell
Install-ADDSForest -DomainName "name.local" -InstallDNS -Force

New-ADOrganizationUnit -Name "name" -Path "DC=name,DC=local"

Get-ADOrganizationalUnit -Filter*|Select Name, DistinguishedName

```
Replace all "xxx" and "name", "name.local" with your own values.

## Add/Configure DHCP

```powershell
Add-DhcpServerInDC -Dnsname "name.local" -IPAddress xxx.xxx.xxx.xxx

restart-service DHCPServer

add-dhcpserverv4scope -name "name" -StartRange xxx.xxx.xxx.xxx -EndRange xxx.xxx.xxx.xxx -Subnetmask 255.255.255.0 -state Active

Get-DhcpServerv4Scope

```

## Make test account in AD

```powershell
Redircmp "OU=name, DC=name,DC=name"

Rediusr "OU=name,DC=name,DC=name"

New-ADUser -Name "Test User" -SamAccountName "test.user" -UserPrincipalName "test.user@name.name" -AccountPassword (ConvertTo-SecureString "P@ssw0rd!" -AsPlainText -Force) -Enabled $true

Get-ADUser -Identity "test.user"|Select DistinguishedName

```

## CSV file to create users 

```powershell
$csvPath = "C:\Users\Administrator\Documents\xxx.csv"
 

$users = Import-Csv -Path $csvPath
foreach ($user in $users) {
    $firstName = $user.FirstName
    $lastName = $user.LastName
    $userName = $user.UserName
    $password = $user.Password
    $ou = $user.OU


    New-ADUser -GivenName $firstName 
               -Surname $lastName 
               -Name "$firstName $lastName" 
               -SamAccountName $userName 
               -UserPrincipalname "$userName@example.com" 
               -AccountPassword (ConvertTo-SecureString $password -AsPlainText -Force) 
               -Path $ou 
               -Enabled $true 
               -PassThru
```


