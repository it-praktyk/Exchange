# ConvertFrom-O365IPAddressesXMLFile
## SYNOPSIS
Convert the O365IPAddresses.xml file to the custom PowerShell object

## SYNTAX
```powershell
ConvertFrom-O365IPAddressesXMLFile [[-Path] <Object>] [<CommonParameters>]
```

## DESCRIPTION
Function intended for converting to the custom PowerShell object the list of hosts used for Office 365 services published as the O365IPAddresses.xml file.

The list contains addresses (IPv4, IPv6, URL) for what communication can't be proxied on customer/client side.

More information on the Microsoft support page: "Office 365 URLs and IP address ranges", http://bit.ly/1LD8fYv

## PARAMETERS
### -Path &lt;Object&gt;
The xml file containing data like O365IPAddresses.xml downloaded manually.
If the the parameter is ommited the file O365IPAddresses.xml will be downloaded from the Microsoft site and saved with
```
Required?                    false
Position?                    1
Default value                .\O365IPAddresses.xml
Accept pipeline input?       false
Accept wildcard characters?  false
```

## INPUT
The xml file published by Microsoft what contains the list of IP addresses ranges used by Office 365 addresses.

## OUTPUTS
The custom PowerShell object what contains properties: Service,Type,IPAddress,SubNetMaskLength,SubnetMask,Url.

## NOTES
AUTHOR: Wojciech Sciesinski, wojciech[at]sciesinski[dot]net  


KEYWORDS: PowerShell, Exchange, Office 365, O365, XML, proxy

VERSIONS HISTORY
- 0.1.0 - 2016-02-23 - The first working version
- 0.1.1 - 2016-02-24 - The parameter name in the helper function ConvertTo-Mask corrected
- 0.1.2 - 2016-02-24 - The output spelling corrected for SubNetMaskLength, help update, the function reformatted

TODO
- add only summary mode/switch
- add support for downloading the file via proxy with authentication
- add parameter to custom naming downloaded file
- handle errors of a download operation (?)
- add whatif (?)
- check/correct verbose and debug mode

LICENSE

Copyright (c) 2016 Wojciech Sciesinski  
This function is licensed under The MIT License (MIT)  
Full license text: https://opensource.org/licenses/MIT  

## EXAMPLES
### EXAMPLE 1
```powershell
[PS] >ConvertFrom-O365IPAddressesXMLFile

Service          : o365
Type             : IPv6
IPAddress        : 2603:1030:800:5::bfee:a0ad
SubNetMaskLength : 128
SubnetMask       :
Url              :

<Output partially omitted>

Service          : LYO
Type             : IPv4
IPAddress        : 23.103.129.128
SubNetMaskLength : 25
SubnetMask       : 255.255.255.128
Url              :

<Output partially omitted>

Service          : ProPlus
Type             : URL
IPAddress        :
SubNetMaskLength : 0
SubnetMask       :
Url              : go.microsoft.com

<Output partially omitted>

```

### EXAMPLE 2

```powershell
.EXAMPLE

[PS] >ConvertFrom-O365IPAddressesXMLFile -Path .\O365IPAddresses.xml | Get-Member

TypeName: System.Management.Automation.PSCustomObject

Name             MemberType   Definition
----             ----------   ----------
Equals           Method       bool Equals(System.Object obj)
GetHashCode      Method       int GetHashCode()
GetType          Method       type GetType()
ToString         Method       string ToString()
IPAddress        NoteProperty ipaddress IPAddress=2603:1030:800:5::bfee:a0ad
Service          NoteProperty string Service=o365
SubnetMask       NoteProperty string SubnetMask=
SubNetMaskLenght NoteProperty int SubNetMaskLenght=128
Type             NoteProperty string Type=IPv6
Url              NoteProperty string Url=
```
