cat << 'EOF' > docs/COMMANDS_LOG.md
########### Ubuntu Samba AD DC & File Share - Command Reference################

This document explains the key commands executed during this project and their purpose.


## 1. Prerequisites & Package Installation
**Command:** `sudo apt update && sudo apt install -y samba samba-ad-dc krb5-user winbind bind9-dnsutils`
  - **Description:** Installs Samba, essential Active Directory packages, Kerberos, and DNS utilities.

## 2. Domain Provisioning
- **Command:** `sudo samba-tool domain provision --use-rfc2307 --interactive`
  - **Description:** Configures and provisions the AD domain (`BIDYUT.LOCAL`) in interactive mode.

## 3. Kerberos Configuration
- **Command:** `sudo cp /var/lib/samba/private/krb5.conf /etc/krb5.conf`
  - **Description:** Copies the Kerberos configuration file from the Samba private directory to the system directory for proper authentication.

## 4. Disabling Standalone Services
- **Command:** `sudo systemctl stop smbd nmbd winbind`
  - **Description:** Stops legacy standalone file sharing daemon services since AD DC uses the unified `samba-ad-dc` service.
- **Command:** `sudo systemctl disable smbd nmbd winbind`
  - **Description:** Disables these legacy services on system boot.

## 5. Enabling & Starting Samba AD-DC Service
- **Command:** `sudo systemctl enable samba-ad-dc && sudo systemctl start samba-ad-dc`
  - **Description:** Enables and starts the unified Active Directory domain controller service.

## 6. Checking Domain Status
- **Command:** `sudo samba-tool domain level show`
  - **Description:** Verifies forest and domain functional levels (e.g., Windows 2008 R2).

## 7. Shared Directory Setup
- **Command:** `sudo mkdir -p /srv/samba/shared`
  - **Description:** Creates a new directory/folder for network sharing.
- **Command:** `sudo chown -R root:root /srv/samba/shared`
  - **Description:** Sets base ownership of the shared folder to root (permissions are managed via Samba ACLs).
- **Command:** `sudo chmod -R 0770 /srv/samba/shared`
  - **Description:** Sets strict read/write permissions on the folder (restricted to authorized users/admins).

## 8. Configuration Validation
- **Command:** `sudo testparm`
  - **Description:** Checks the `/etc/samba/smb.conf` file for syntax errors and displays loaded shares.

## 9. Package Cache Update & Broken Dependencies Fix:
    commands: sudo apt --fix-broken install
## 10.Missing Repository/Universe Repositories Enable
   Commands: sudo add-apt-repository universe && sudo apt update
## 11. Samba/Winbind cache conf file clean
   commands: sudo apt purge samba samba-common winbind
## 12 check active share list on Samba Server
   Commands: smbclient -L localhost -U %
## 13 This commands to check shares properly loaded or  not
## 14 This commands using for show content Administrator 
   smbclient //localhost/CompanyShare -U Administrator
   sudo testparm -s
## 14 This commands for check Active SMB Connections
   sudo smbstatus
   


