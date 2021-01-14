# Win Admin

### Migrate from Local AD to Azure

- Links

    [https://www.codetwo.com/admins-blog/how-to-sync-on-premises-active-directory-to-azure-active-directory-with-azure-ad-connect/](https://www.codetwo.com/admins-blog/how-to-sync-on-premises-active-directory-to-azure-active-directory-with-azure-ad-connect/) - Commands included

    [https://practical365.com/identity/migrating-azure-ad-connect-new-server/](https://practical365.com/identity/migrating-azure-ad-connect-new-server/) - Commands included

    [https://www.assistanz.com/steps-to-migrate-users-from-on-premises-active-directory-to-azure/](https://www.assistanz.com/steps-to-migrate-users-from-on-premises-active-directory-to-azure/)

    [https://www.simplicit365.com/2020/01/how-to-migrate-on-premises-distribution-lists-in-active-directory-to-azure-ad-using-powershell/](https://www.simplicit365.com/2020/01/how-to-migrate-on-premises-distribution-lists-in-active-directory-to-azure-ad-using-powershell/) - Script included

### Commands to Know

**Sign in to Azure:** Connect-AzAccount

If using a regional cloud, use this command: Connect-AzAccount -Environment (name of regional cloud)

**Find Commands**

- List of Find Commands

    Verb-Noun - The verb describes the action (examples include New, Get, Set, Remove) and the noun describes the resource type. 

    EX: find all VM-related commands that use the Get verb : Get-Command -Verb Get -Noun AzVM* -Module Az.Compute

**Azure Resource Types:** 

- Resource group

    Azure PowerShell module: Az.Resources

    Noun prefix: AzResourceGroup

- Virtual machines

    Azure PowerShell module: Az.Compute

    Noun prefix: AzVM

- Storage accounts

    Azure PowerShell module: Az.Storage

    Noun prefix: AzStorageAccount

- Key Vault

    Azure PowerShell module: Az.KeyVault

    Noun prefix: AzKeyVault

- Web applications

    Azure PowerShell module: Az.Websites

    Noun prefix: AzWebApp

- SQL Databases:

    Azure PowerShell module: Az.Sql

    Nound prefix: AzSqlDatabase

### **Prevent Hash Stealing On Kerebos**

[https://stealthbits.com/blog/how-to-detect-pass-the-ticket-attacks/](https://stealthbits.com/blog/how-to-detect-pass-the-ticket-attacks/)

**Kerebos Pass The Ticket Attacks** 

- resembles a PtH attack in its execution
steps
- requires the attacker to obtain local administrative access to capture the stored Ticket Granting
Tickets (TGTs) before they can reused with the Kerberos protocol
- [https://resources.infosecinstitute.com/topic/pass-hash-pass-ticket-no-pain/](https://resources.infosecinstitute.com/topic/pass-hash-pass-ticket-no-pain/)
- [https://media.blackhat.com/bh-us-12/Briefings/Duckwall/BH_US_12_Duckwall_Campbell_Still_Passing_WP.pdf](https://media.blackhat.com/bh-us-12/Briefings/Duckwall/BH_US_12_Duckwall_Campbell_Still_Passing_WP.pdf) (Look at pages 7-9)

**Kerobasting**

- [https://www.lepide.com/blog/how-to-prevent-kerberoasting-attacks/](https://www.lepide.com/blog/how-to-prevent-kerberoasting-attacks/) - Prevention
- [https://adsecurity.org/?p=3458](https://adsecurity.org/?p=3458) - prevention
- [https://sra.io/blog/selective-kerberoast-prevention-using-dacls/](https://sra.io/blog/selective-kerberoast-prevention-using-dacls/) -prevention
- [https://medium.com/swlh/kerberoasting-in-a-nutshell-dfac1163949c](https://medium.com/swlh/kerberoasting-in-a-nutshell-dfac1163949c) - detect and prevent