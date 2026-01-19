**\========================================**  
**CATEGORY 10: SECURITY & BEST PRACTICES**  
**\========================================**

**10.1 SSH SECURITY:**

**/\* COMMENT: SSH is the backbone of remote server access. Proper SSH configuration**  
   **prevents unauthorized access and is critical for system security. \*/**

**KEY CONCEPTS:**  
**• Public Key Authentication: More secure than passwords**  
**• SSH Agent: Manage private keys**  
**• Port Forwarding: Secure tunneling**  
**• Bastion Hosts: Jump servers for internal access**  
**• SSH Config: Simplify connection management**

**GENERATE SSH KEYS:**  
**\# Generate ED25519 key (recommended)**  
**ssh-keygen \-t ed25519 \-C "your\_email@example.com"**

**\# Generate RSA key (4096 bits)**  
**ssh-keygen \-t rsa \-b 4096 \-C "your\_email@example.com"**

**\# Copy public key to server**  
**ssh-copy-id user@server**

**\# Manual copy**  
**cat \~/.ssh/id\_ed25519.pub | ssh user@server "mkdir \-p \~/.ssh && cat \>\> \~/.ssh/authorized\_keys"**

**SSH CONFIG (/etc/ssh/sshd\_config):**  
**\# Disable root login**  
**PermitRootLogin no**

**\# Disable password authentication**  
**PasswordAuthentication no**  
**PubkeyAuthentication yes**

**\# Change default port**  
**Port 2222**

**\# Limit users**  
**AllowUsers user1 user2**  
**DenyUsers baduser**

**\# Set idle timeout**  
**ClientAliveInterval 300**  
**ClientAliveCountMax 2**

**\# Disable X11 forwarding if not needed**  
**X11Forwarding no**

**CLIENT SSH CONFIG (\~/.ssh/config):**  
**Host myserver**  
    **HostName server.example.com**  
    **User admin**  
    **Port 2222**  
    **IdentityFile \~/.ssh/id\_ed25519**

**Host bastion**  
    **HostName bastion.example.com**  
    **User admin**  
    **ForwardAgent yes**

**Host internal**  
    **HostName 10.0.1.100**  
    **User admin**  
    **ProxyJump bastion**

**SSH TUNNELING:**  
**\# Local port forwarding**  
**ssh \-L 8080:localhost:80 user@server**

**\# Remote port forward**  
**ing**  
**ssh \-R 8080:localhost:80 user@server**

**\# Dynamic port forwarding (SOCKS proxy)**  
**ssh \-D 1080 user@server**

**BEST PRACTICES:**  
**• Use ED25519 keys (faster and more secure)**  
**• Disable password authentication**  
**• Change default SSH port**  
**• Use fail2ban to prevent brute force attacks**  
**• Implement SSH key passphrases**  
**• Use SSH agent forwarding cautiously**  
**• Regular audit of authorized\_keys**

**10.2 FIREWALL (IPTABLES & UFW):**

**/\* COMMENT: Firewalls control network traffic at the host level. UFW provides a**  
   **simple interface to iptables, while iptables offers granular control.**  
   **Understanding both is essential for server security. \*/**

**KEY CONCEPTS:**  
**• Chains: INPUT, OUTPUT, FORWARD**  
**• Tables: filter, nat, mangle**  
**• Policies: ACCEPT, DROP, REJECT**  
**• Stateful: Track connection state**  
**• Rules: Match conditions and actions**

**UFW (UNCOMPLICATED FIREWALL):**  
**\# Enable/disable firewall**  
**sudo ufw enable**  
**sudo ufw disable**  
**sudo ufw status verbose**

**\# Default policies**  
**sudo ufw default deny incoming**  
**sudo ufw default allow outgoing**

**\# Allow specific services**  
**sudo ufw allow ssh**  
**sudo ufw allow 80/tcp**  
**sudo ufw allow 443/tcp**  
**sudo ufw allow 3306/tcp comment 'MySQL'**

**\# Allow from specific IP**  
**sudo ufw allow from 192.168.1.100**  
**sudo ufw allow from 192.168.1.0/24 to any port 22**

**\# Delete rule**  
**sudo ufw delete allow 80/tcp**  
**sudo ufw delete 1  \# By rule number**

**\# Deny/reject**  
**sudo ufw deny 25/tcp**  
**sudo ufw reject out to 192.168.1.50**

**\# Application profiles**  
**sudo ufw app list**  
**sudo ufw allow 'Nginx Full'**

**IPTABLES COMMANDS:**  
**\# List rules**  
**sudo iptables \-L \-n \-v**  
**sudo iptables \-L INPUT \-n \-v**

**\# Allow SSH**  
**sudo iptables \-A INPUT \-p tcp \--dport 22 \-j ACCEPT**

**\# Allow HTTP and HTTPS**  
**sudo iptables \-A INPUT \-p tcp \--dport 80 \-j ACCEPT**  
**sudo iptables \-A INPUT \-p tcp \--dport 443 \-j ACCEPT**

**\# Allow established connections**  
**sudo iptables \-A INPUT \-m state \--state ESTABLISHED,RELATED \-j ACCEPT**

**\# Allow loopback**  
**sudo iptables \-A INPUT \-i lo \-j ACCEPT**

**\# Drop everything else**  
**sudo iptables \-P INPUT DROP**

**\# Delete rule**  
**sudo iptables \-D INPUT 5  \# By line number**  
**sudo iptables \-D INPUT \-p tcp \--dport 80 \-j ACCEPT**

**\# Save rules**  
**sudo iptables-save \> /etc/iptables/rules.v4**  
**sudo netfilter-persistent save**

**BEST PRACTICES:**  
**• Default deny all incoming traffic**  
**• Allow only necessary services**  
**• Use connection state tracking**  
**• Log dropped packets for monitoring**  
**• Regular review of firewall rules**  
**• Test before deploying to production**

**10.3 SSL/TLS CERTIFICATES (LET'S ENCRYPT):**

**/\* COMMENT: SSL/TLS encrypts traffic between clients and servers. Let's Encrypt**  
   **provides free, automated certificates. Certbot simplifies the process**  
   **of obtaining and renewing certificates. \*/**

**KEY CONCEPTS:**  
**• Certificate Authority (CA): Issues certificates**  
**• Certificate Signing Request (CSR): Request for certificate**  
**• Public/Private Key Pair: Encryption keys**  
**• Certificate Chain: Root, intermediate, and leaf certificates**  
**• ACME Protocol: Automated certificate management**

**INSTALL CERTBOT:**  
**\# Ubuntu/Debian**  
**sudo apt update**  
**sudo apt install certbot python3-certbot-nginx**

**\# For Apache**  
**sudo apt install certbot python3-certbot-apache**

**OBTAIN CERTIFICATE:**  
**\# Standalone (port 80 must be available)**  
**sudo certbot certonly \--standalone \-d example.com \-d www.example.com**

**\# Webroot (for running web server)**  
**sudo certbot certonly \--webroot \-w /var/www/html \-d example.com**

**\# Nginx automatic**  
**sudo certbot \--nginx \-d example.com \-d www.example.com**

**\# Apache automatic**  
**sudo certbot \--apache \-d example.com \-d www.example.com**

**RENEW CERTIFICATE:**  
**\# Test renewal**  
**sudo certbot renew \--dry-run**

**\# Renew all certificates**  
**sudo certbot renew**

**\# Auto-renewal (cron)**  
**0 0,12 \* \* \* /usr/bin/certbot renew \--quiet**

**CERTIFICATE MANAGEMENT:**  
**\# List certificates**  
**sudo certbot certificates**

**\# Revoke certificate**  
**sudo certbot revoke \--cert-path /etc/letsencrypt/live/example.com/cert.pem**

**\# Delete certificate**  
**sudo certbot delete \--cert-name example.com**

**NGINX SSL CONFIGURATION:**  
**server {**  
    **listen 443 ssl http2;**  
    **server\_name example.com www.example.com;**  
      
    **ssl\_certificate /etc/letsencrypt/live/example.com/fullchain.pem;**  
    **ssl\_certificate\_key /etc/letsencrypt/live/example.com/privkey.pem;**  
      
    **ssl\_protocols TLSv1.2 TLSv1.3;**  
    **ssl\_prefer\_server\_ciphers on;**  
    **ssl\_ciphers HIGH:\!aNULL:\!MD5;**  
      
    **ssl\_session\_cache shared:SSL:10m;**  
    **ssl\_session\_timeout 10m;**  
      
    **\# HSTS**  
    **add\_header Strict-Transport-Security "max-age=31536000; includeSubDomains" always;**  
**}**

**\# Redirect HTTP to HTTPS**  
**server {**  
    **listen 80;**  
    **server\_name example.com www.example.com;**  
    **return 301 https://$server\_name$request\_uri;**  
**}**

**BEST PRACTICES:**  
**• Use strong TLS protocols (TLSv1.2+)**  
**• Enable HSTS for security**  
**• Automate certificate renewal**  
**• Monitor certificate expiration**  
**• Use wildcard certificates when appropriate**

**10.4 SECURITY HARDENING:**

**/\* COMMENT: Security hardening involves multiple layers of protection to reduce**  
   **attack surface. This includes system updates, minimal services, proper**  
   **permissions, and security tools. \*/**

**KEY CONCEPTS:**  
**• Principle of Least Privilege: Minimal access rights**  
**• Defense in Depth: Multiple security layers**  
**• Attack Surface: Exposed system components**  
**• Security Patches: Regular updates**  
**• Auditing: Monitor and log activities**

**SYSTEM UPDATES:**  
**\# Ubuntu/Debian**  
**sudo apt update && sudo apt upgrade \-y**  
**sudo apt dist-upgrade**  
**sudo apt autoremove**

**\# Enable automatic security updates**  
**sudo apt install unattended-upgrades**  
**sudo dpkg-reconfigure \-plow unattended-upgrades**

**\# CentOS/RHEL**  
**sudo yum update \-y**  
**sudo yum upgrade**

**DISABLE UNNECESSARY SERVICES:**  
**\# List running services**  
**systemctl list-units \--type=service \--state=running**

**\# Disable service**  
**sudo systemctl disable service-name**  
**sudo systemctl stop service-name**

**\# Remove unused packages**  
**sudo apt autoremove \--purge**

**FILE PERMISSIONS:**  
**\# Secure important files**  
**sudo chmod 600 /etc/ssh/sshd\_config**  
**sudo chmod 600 \~/.ssh/authorized\_keys**  
**sudo chmod 700 \~/.ssh**

**\# Find world-writable files**  
**find / \-type f \-perm \-002 2\>/dev/null**

**\# Find SUID/SGID files**  
**find / \-type f \\( \-perm \-4000 \-o \-perm \-2000 \\) 2\>/dev/null**

**SECURITY TOOLS:**  
**\# Fail2Ban (brute force protection)**  
**sudo apt install fail2ban**  
**sudo systemctl enable fail2ban**  
**sudo systemctl start fail2ban**

**\# Check banned IPs**  
**sudo fail2ban-client status sshd**

**\# Lynis (security audit)**  
**sudo apt install lynis**  
**sudo lynis audit system**

**\# RKHunter (rootkit detection)**  
**sudo apt install rkhunter**  
**sudo rkhunter \--update**  
**sudo rkhunter \--check**

**\# ClamAV (antivirus)**  
**sudo apt install clamav clamav-daemon**  
**sudo freshclam**  
**sudo clamscan \-r /home**

**AUDITING & LOGGING:**  
**\# Check authentication logs**  
**sudo tail \-f /var/log/auth.log**  
**sudo grep 'Failed password' /var/log/auth.log**

**\# System logs**  
**sudo journalctl \-xe**  
**sudo journalctl \-u sshd**

**\# Install auditd**  
**sudo apt install auditd**  
**sudo systemctl enable auditd**

**\# Audit rules**  
**sudo auditctl \-w /etc/passwd \-p wa \-k passwd\_changes**  
**sudo auditctl \-w /etc/shadow \-p wa \-k shadow\_changes**

**BEST PRACTICES:**  
**• Keep systems updated and patched**  
**• Disable unnecessary services**  
**• Use strong passwords and 2FA**  
**• Implement proper file permissions**  
**• Enable and monitor security logs**  
**• Regular security audits**  
**• Use security tools (fail2ban, Lynis)**  
**• Backup regularly**
