# General NECCDC Roles

hehe - E

hey - K

Hello - N

[NECCDC Palo Alto Academy Resources.zip](General%20NECCDC%20Roles%20409e7fc6444f4139baf1478bec02966e/NECCDC_Palo_Alto_Academy_Resources.zip)

[NECCDC 2020](General%20NECCDC%20Roles%20409e7fc6444f4139baf1478bec02966e/NECCDC%202020%20f4747f03d4104349b56bc83daec52514.md)

[NECCDC 2021](General%20NECCDC%20Roles%20409e7fc6444f4139baf1478bec02966e/NECCDC%202021%2050ca292089ba4554beea9475d5737d31.md)

ASSUME COMPROMISE - When we get these systems, assume [ the Red Team ] they're already in there somehow.

- Windows Admin

    [Win Admin](General%20NECCDC%20Roles%20409e7fc6444f4139baf1478bec02966e/Win%20Admin%2062ec950deee441a3be88794ba1e0e6fd.md)

    Correct user list

    Change user passwords (write these down! might have to submit them)

    Correct group list

    User assignment (proper admin list)

    Proper rights (finance has finance network share)

    Service identification (IIS, DHCP, DNS, ADUC)

    Change default passwords on administrator accounts

    Disable unwanted services

    RDP 

    Network shares enumerated on all devices

    fsmgmt.msc

    Disable administrative shares (NET SHARE C$ /delete)

    Computer Management > Shared Folders as well (check permissions, only certain users)

    [https://patchmypc.com/home-updater](https://patchmypc.com/home-updater)

    Comodo KillSwitch

    Group Policy (a beast)

    Password policies

    Password history (24), min age(90), max age(15), length, complexity, not reversible 

    Account lockout policies

    Duration, threshold, reset time

    Auditing

    Logon events

    Privilege use

    User rights assesment

    Deny access from the network, logon as a batch job, logon as a service, through RDP

    Security Options

    Rename Admin and Guest

    User Account Control > Admin Approval mode

    local use of blank passwords to console only

    Domain Mamber > digitally encrypt or sign secure channel data

    Other misc. best-practice GPOs we can churn through

    Domain Controller has an overall GPO that can update all Windows clients (gpupdate /force) 

    secpol.msc on individual machines

    rsop.msc (Resultant Set of Policy) shows what GPOs are applied and where

    wf.msc for firewall

    Services (SNMP, FTP)

    Windows Update Service enabled

    Simple TCP/IP stopped disabled

- Linux Admin

    [Linux Admin](General%20NECCDC%20Roles%20409e7fc6444f4139baf1478bec02966e/Linux%20Admin%20b3a5f41136de415981eba8f0b77f044a.md)

    Correct user list (hidden users are UID below 1000) 

    Change user passwords (write these down! might have to submit them)

    Minimum password age, maximum password age, lockout policy (passwd or chage)

    Correct group list

    User assignment (proper admin list)

    Proper rights (finance has finance network share)

    /etc/passwd and /etc/shadow should be 0640 admin:admins at least, if not 0600 admin:admins

    /etc/sysctl.conf irregularities? (IPv4 TCP SYN cookies enabled, ICMP errors ignored, Logging martian packets, ignore broadcast ICMP echo request, IPv4 ICMP redirects disabled)

    Service identification (IIS, DHCP, DNS, ADUC)

    Change default passwords on administrator accounts

    Disable unwanted services (FTP, POP3, SMTP)

    Remove too (systemctl | grep <service name>)

    apt remove <package>

    Check apt log or Ubuntu Software Center (like windows Control Panel > uninstall a program)

    Apache2 > /etc/apache2/apache2.conf hardening

    Log monitoring?

    cat /var/log/auth.log -n | grep -e sshd  # -n is cat with line numbers

    ^ For ssh logins failed or otherwise

    Look for bad binaries/back doors

    Could be a trojaned binary, fake binary (ex. copied netcat to something else), SetUID binary, etc
    Check listening ports (ss -plunt) and find / -perm -4000 (SUID/SGID) for Linux

    Cron Jobs

    crontab -l (may need a sudo in there)

- Networking

    [Networking](General%20NECCDC%20Roles%20409e7fc6444f4139baf1478bec02966e/Networking%2016715b5ec5ea4286b2b1b3ad471d8589.md)

    Firewalls!

    Linux

    Uncomplicated Firewall (ufw)

    Look up IPv6 disable for linux (sorry)

    Windows 

    No irregular exceptions

    IPv6 disabled on network adapters

    Border router

    Update it? Firmware? 

    DHCP as a service?

    Change passwords

    Check for users

    disable any unused switchports 

- Vuln Mgmt

    [Vuln Mngt](General%20NECCDC%20Roles%20409e7fc6444f4139baf1478bec02966e/Vuln%20Mngt%204e88d765c1d3403d858c77a86633075c.md)

    Updates (apt or yum, check repository files /etc/[apt/yum]/[sources.list/repo.d])

    apt update && apt full-upgrade

    Check for misconfiguration files (SSH, Apache, Nginx)

    PAM Configuration (Password Complexity)

    /etc/pam.d/common-auth and common-password defaults

    Fail2Ban (SSH Firewall)

    Change Users Passwords

    Fixing groups (Make sure users are in respected groups)

    Lock Root Privilege (sudo -L || or /etc/passwd and change /bin/bash to /sbin/nologin || or /etc/ssh/sshd_config change PermitRootLogin to No and #systemctl restart sshd)

    Try and discover any hacking tools