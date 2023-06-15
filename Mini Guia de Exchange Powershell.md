# Mini Guia de Exchange Powershell

# Sanity Check
`Get-Host`

`$PSVersionTable`

# Import module

`Import-Module ExchangeOnlineManagement`
# Connect

`Connect-ExchangeOnline -UserPrincipalName adm_COABE@clarkemodet.com -InlineCredential`
# Remove member from groups
`Remove-DistributionGroupMember -Identity 083f89b8-af57-458c-814c-834c5ffabeae -Member bcc26e71-4823-4c28-94f3-ed41ae63a852`

# Liz Saunders can modify Rick He's mailbox:
`Add-MailboxPermission -Identity bcc26e71-4823-4c28-94f3-ed41ae63a852 -User f1e6c766-1bdd-44c5-8ec3-2dfae8ed66e2 -AccessRights FullAccess -InheritanceType All`
# Rick He is a shared mailbox now
`Set-Mailbox -Identity bcc26e71-4823-4c28-94f3-ed41ae63a852 -Type Shared`


# Get members in group

```
$groups = Get-Group -Identity "Es Team"
$groups.Members
```


El Identity puede ser también el ID (que sacamos de Graph API)

# Quitar usuario de un grupo

```
 Remove-DistributionGroupMember -Identity 083f89b8-af57-458c-814c-834c5ffabeae -Member bcc26e71-4823-4c28-94f3-ed41ae63a852
```
-Identity del grupo (vale el nombre, o el ID, el ID lo podemos sacar fácilmente de Graph API)
-Member vale el ID del miembro (Graph API, lo mejor) o el nombre interno (más difícil de ver)


# Docs

NOTA: Hay que instalar Powershell 7 en las maquinas

https://learn.microsoft.com/en-us/powershell/exchange/app-only-auth-powershell-v2?view=exchange-ps
https://learn.microsoft.com/en-us/powershell/exchange/connect-to-exchange-online-powershell?view=exchange-ps
https://learn.microsoft.com/en-us/powershell/exchange/exchange-online-powershell-v2?view=exchange-ps
https://learn.microsoft.com/en-us/powershell/exchange/exchange-online-powershell-v2?view=exchange-ps#install-and-maintain-the-exchange-online-powershell-module


https://learn.microsoft.com/en-us/exchange/recipients-in-exchange-online/manage-permissions-for-recipients#use-the-eac-to-assign-permissions-to-individual-mailboxes
https://learn.microsoft.com/en-us/powershell/module/exchange/remove-distributiongroupmember?view=exchange-ps