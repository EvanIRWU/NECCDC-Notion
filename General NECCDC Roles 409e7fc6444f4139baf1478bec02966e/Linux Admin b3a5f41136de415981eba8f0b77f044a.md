# Linux Admin

- chmod/chown

    ls -lah /etc/shadow # - r w - r *- -* - - - 1 kali:wheel lkdsjfngb;askdjghf

    shadow 600 linus:peanuts

    passwd 640 linus:peanuts

    File Owner : linus

    Group: peanuts

    Permissions: Owner R W -; Group - - -; Others - - -

    - Files

        /etc/passwd - 640

        /etc/shadow - 600 

        /etc/gshadow - 600

        /etc/group - 640

        /etc/sudoers - 600

        /var/spool/cron - 600

        /etc/fstab - 600

    ```bash
    sudo chmod 600 /etc/passwd
    sudo chown linus:peanuts /etc/passwd
    ```

    - 0: (000) No permission.
    - 1: (001) Execute permission.
    - 2: (010) Write permissio
    - 3: (011) Write and execute permissions.
    - 4: (100) Read permission.
    - 5: (101) Read and execute permissions.
    - 6: (110) Read and write permissions.
    - 7: (111) Read, write, and execute permissions.

    [https://www.howtogeek.com/437958/how-to-use-the-chmod-command-on-linux/](https://www.howtogeek.com/437958/how-to-use-the-chmod-command-on-linux/)

- User Accounts

    ```bash
    cat /etc/shadow | grep "/bin"
    ```

    Locate /bin/bash shells check if service should have it - [google](http://google.com)

    If unknown user that is not on google and should not have /bin/bash

    ```bash
    sudo userdel -r <username>
    ```

    “Hidden” users are typically those with UIDs (User IDs) of under 1000

- Passwords

    Change user passwords (write these down! might have to submit them)

    ```bash
    sudo passwd <user>
    ```

    Require user to make new password on next login:

    ```bash
    sudo passwd -e <user>
    ```

    Edit /etc/login.defs:

    ```bash
    sudo nano /etc/login.defs #change PASS_MAX_DAYS, and PASS_MIN_DAYS
    ```

    - Per user

        Min pass age:

        ```bash
        sudo passwd -n <days> <user>
        or
        sudo chage -m <days> <user>
        ```

        Max pass age:

        ```bash
        sudo passwd -x <days> <user>
        or
        sudo chage -M <days> <user>
        ```

- Groups

    Correct User Assignment (proper admin list)

    view groups and users in groups

    ```bash
    cat /etc/group
    ```

    Add User to Group

    ```bash
    usermod -aG <group> <user>
    ```

    Remove User From Group

    ```bash
    gpasswd -d <user> <group>

    On Ubuntu:
    deluser <user> <group>
    ```

- Sudo Access & Root Account

    ```bash
    sudo nano /etc/sudoers #View

    sudo visudo /etc/sudoers #Edit
    ```

    Sudoers syntax:

    ```bash
    <user>  ALL=(ALL:ALL) ALL
    ```

    Disable authentication as root:

    ```bash
    sudo usermod --expiredate 1 root
    ```

    Lock Root Account Password:

    ```bash
    sudo passwd -l root
    ```

    Unlock Root Account Password:

    ```bash
    sudo passwd -u root
    ```

    Disable Shell For Root

    ```bash
    sudo nano /etc/passwd #On root user, change /bin/bash to /usr/sbin/nologin
    ```

    or

    ```bash
    sudo chsh root #When prompted enter /usr/sbin/nologin
    ```

- SSH

    ```bash
    sudo apt install openssh-client
    ```

    ```bash
    sudo nano /etc/ssh/sshd_config
    ```

    Change 

    PermitRootLogin no 

    PermitEmptyPasswords no

    PubkeyAuthentication no

    MaxAuthTries 4

    Protocol 2

    LogLevel VERBOSE

    LoginGraceTime 60

    X11Forwarding no

    AllowTcpForwarding no

    StrictModes yes

- Firewall (UFW)

    [https://www.digitalocean.com/community/tutorials/how-to-setup-a-firewall-with-ufw-on-an-ubuntu-and-debian-cloud-server](https://www.digitalocean.com/community/tutorials/how-to-setup-a-firewall-with-ufw-on-an-ubuntu-and-debian-cloud-server)

    Setup

    sudo apt-get install ufw

    sudo ufw status

    IPv6

    sudo vi /etc/default/ufw

    IPV6=yes

    sudo ufw disable (restart the firewall)

    sudo ufw enable

    Defaults

    sudo ufw default deny incoming (denies all incoming traffic)

    udo ufw default allow outgoing (allows all outgoing traffic)

    Allowing connections

    SSH

    sudo ufw allow ssh

    OR

    sudo ufw allow 22/tcp

    OR

    sudo ufw allow 2222/tcp (if ssh is on 2222)

    HTTP

    sudo ufw allow www 

    or

    sudo ufw allow 80/tcp 

    FTP

    sudo ufw allow ftp 

    or 

    sudo ufw allow 21/tcp

    Random ports

    sudo ufw allow 1000:2000/tcp

    sudo ufw allow 1000:2000/udp

    Random IP addresses

    sudo ufw allow from 192.168.255.255

    Deleting Rules

    sudo ufw delete allow 80/tcp

    sudo ufw delete allow 1000:2000/tcp

    Show list of rules

    sudo ufw status numbered 

    sudo ufw delete [number]

    Remember to enable the firewall after changes!

    sudo ufw enable

    sudo ufw status verbose

    To reset everything

    sudo ufw reset