Function New-MarketingUser {
    [CmdletBinding()]
    Param (
    [Parameter(Mandatory=$true)][String]$Firstname,
    [Parameter(Mandatory=$true)][String]$Lastname
    )
    
    New-ADUser `
    -Path "OU=Marketing,DC=Adatum,DC=com" `
    -SamAccountName "$Firstname $Lastname" `
    -UserPrincipalName "$Firstname$Lastname@adatum.com" `
    -Name "$Firstname $Lastname" `
    -GivenName $Firstname `
    -Surname $Lastname `
    -Enabled $True `
    -Displayname "$Lastname, $Firstname" `
    -ChangePasswordAtLogon $true `
    -AccountPassword (ConvertTo-SecureString "Pa55.wrd" -AsPlainText -force) `
    
    
    Add-ADGroupMember -Identity Marketing -members "$Firstname $Lastname"
    }
    
    
    New-marketinguser -Firstname Balrog -Lastname Jefferson
