cat << 'EOF' > README.md
# Ubuntu Samba Active Directory Domain Controller & File Server

Professional guide and deployment documentation for setting up an enterprise-grade Active Directory Domain Controller (DC) and secure File Sharing Server on Ubuntu Linux.

##  Project Overview
- **Operating System:** Ubuntu ( IT-Admin01L )
- **Domain Name (Realm):** BIDYUT.LOCAL
- **NetBIOS Domain:** BIDYUT
- **Services Provided:** Active Directory DC, DNS, Kerberos Authentication, and secure SMB File Sharing (`CompanyShare`).

************ Repository Structure *******************



## 🛠️Quick Deployment Steps
1. Install required Samba AD-DC packages.
2. Run interactive domain provisioning via "samba-tool".
3. Configure Kerberos (`krb5.conf`).
4. Stop legacy standalone SMB/Winbind services and enable "samba-ad-dc".
5. Create shared directories and apply fine-grained ACL permissions.

## 💻 Accessing the File Share (Windows Clients)
- Open **Run** (`Win + R`) on any domain-joined or network client.
- Enter: `\\<Server_IP>\CompanyShare`
- Authenticate using domain credentials (e.g., `BIDYUT\Administrator`).

