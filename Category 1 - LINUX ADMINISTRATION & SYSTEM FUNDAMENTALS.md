**════════════════════════════════════════════════════════════════════**  
**CATEGORY 1: LINUX ADMINISTRATION & SYSTEM FUNDAMENTALS**  
**════════════════════════════════════════════════════════════════════**

**Covering: 16 articles on user management, boot process, LVM, NFS, filesystems, kernel tuning, swap, rsync, sudo, SSH, and essential commands**

**/\* COMMENT: This section consolidates fundamental Linux system administration skills**  
   **that every DevOps engineer and sysadmin must master. These are the building blocks**  
   **for managing production Linux servers effectively. \*/**

**━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━**

**1.1 USER ADMINISTRATION**

**/\* COMMENT: User management is critical for security, access control, and compliance.**  
   **Understanding the user database files (/etc/passwd, /etc/shadow, /etc/group) is**  
   **essential for troubleshooting authentication issues and managing permissions. \*/**

**KEY CONCEPTS:**

**● User Types in Linux:**  
  **\- Root (UID 0): Superuser with unlimited privileges**  
  **\- System Users (UID 1-999): For services/daemons, typically no login shell**  
  **\- Regular Users (UID 1000+): Human users with home directories**

**● Critical Files:**  
  **/etc/passwd     \- User account database (7 fields)**  
  **/etc/shadow     \- Encrypted passwords & aging policies (9 fields, root-only)**  
  **/etc/group      \- Group membership database**  
  **/etc/gshadow    \- Secure group data**  
  **/etc/login.defs \- Default settings for user creation**  
  **/etc/default/useradd \- useradd defaults**

**● User Creation Process:**  
  **When 'useradd john' executes:**  
  **1\. Assigns unique UID/GID**  
  **2\. Creates /home/john with 700 permissions**  
  **3\. Copies files from /etc/skel/**  
  **4\. Adds entries to passwd, shadow, group**  
  **5\. Creates private group (john:john)**

**ESSENTIAL COMMANDS:**

**\# User Management**  
**useradd \-m \-s /bin/bash \-c "Full Name" \-G wheel,developers username**  
**usermod \-aG groupname username     \# Add to secondary group (append)**  
**usermod \-g primarygroup username   \# Change primary group**  
**usermod \-L username                \# Lock account**  
**usermod \-U username                \# Unlock account**  
**userdel \-r username                \# Delete user \+ home directory**

**\# Password Management**    
**passwd username                    \# Set/change password**  
**passwd \-l username                 \# Lock password**  
**passwd \-u username                 \# Unlock password**  
**passwd \-e username                 \# Expire password (force change)**  
**chage \-d 0 username                \# Force password change on next login**  
**chage \-l username                  \# View password aging info**  
**chage \-M 90 username               \# Set max password age to 90 days**

**\# Group Management**  
**groupadd developers**  
**groupadd \-g 2000 admins           \# Specific GID**  
**groupdel groupname**  
**gpasswd \-a username groupname      \# Add user to group**  
**gpasswd \-d username groupname      \# Remove user from group**

**\# Information Commands**  
**id username                        \# Show UID, GID, groups**  
**groups username                    \# Show group memberships**  
**who                               \# Currently logged in users**  
**w                                 \# Who is doing what**  
**last                              \# Login history**  
**lastlog                           \# Last login for all users**

**BEST PRACTICES:**

**✓ Never use root for daily operations \- use sudo instead**  
**✓ Implement strong password policies (complexity, expiration)**  
**✓ Use /sbin/nologin shell for service accounts**  
**✓ Regularly audit /etc/passwd and /etc/group**  
**✓ Use groups for permission management instead of individual users**  
**✓ Document user creation procedures for consistency**  
**✓ Enable password aging to enforce regular changes**  
**✓ Lock/disable unused accounts rather than deleting immediately**

**/\* COMMENT: In production environments, consider integrating with centralized**  
   **authentication systems like LDAP, Active Directory, or modern solutions like**  
   **FreeIPA/Keycloak for enterprise-scale user management. \*/**

**━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━**

**1.2 BOOT PROCESS & GRUB**

**/\* COMMENT: Understanding the Linux boot process is crucial for troubleshooting**  
   **boot failures, implementing kernel parameters, and recovering broken systems.**  
   **GRUB (Grand Unified Bootloader) is the most common bootloader. \*/**

**BOOT SEQUENCE:**

**1\. BIOS/UEFI POST (Power-On Self-Test)**  
**2\. Boot loader (GRUB2) loads from MBR/GPT**  
**3\. GRUB loads kernel and initramfs**  
**4\. Kernel initializes hardware and mounts root filesystem**  
**5\. Systemd/init starts as PID 1**  
**6\. System services start according to targets/runlevels**

**GRUB CONFIGURATION:**

**Key Files:**  
**/boot/grub2/grub.cfg           \# Main config (auto-generated, don't edit)**  
**/etc/default/grub              \# User settings (edit this)**  
**/etc/grub.d/                   \# Scripts generating grub.cfg**

**Common Parameters in /etc/default/grub:**  
**GRUB\_TIMEOUT=5                 \# Menu timeout in seconds**  
**GRUB\_DEFAULT=0                 \# Default boot entry**  
**GRUB\_CMDLINE\_LINUX="..."       \# Kernel parameters**

**Useful Kernel Parameters:**  
**quiet                          \# Reduce boot messages**  
**rhgb                           \# Red Hat graphical boot**  
**rd.break                       \# Break at initramfs for emergency**  
**init=/bin/bash                 \# Boot directly to bash (recovery)**  
**selinux=0                      \# Disable SELinux**  
**systemd.unit=rescue.target     \# Boot to rescue mode**  
**systemd.unit=multi-user.target \# Boot to CLI (no GUI)**

**GRUB Commands:**  
**grub2-mkconfig \-o /boot/grub2/grub.cfg  \# Regenerate config**  
**grub2-install /dev/sda                  \# Reinstall GRUB**  
**grub2-editenv list                      \# Show saved environment**

**/\* COMMENT: For emergency recovery, you can edit GRUB menu at boot time by pressing**  
   **'e' on the boot entry. Add 'rd.break' or 'init=/bin/bash' to kernel line, then**  
   **press Ctrl+X to boot. This is essential for password recovery scenarios. \*/**

**━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━**

**1.3 LVM (LOGICAL VOLUME MANAGEMENT)**

**/\* COMMENT: LVM provides flexibility in disk management that traditional partitioning**  
   **can't match. It allows resizing filesystems, creating snapshots, and migrating data**  
   **between disks without downtime. Essential for production servers. \*/**

**LVM ARCHITECTURE:**

**Physical Volumes (PV) → Volume Groups (VG) → Logical Volumes (LV) → Filesystems**

**Example: /dev/sda1 \+ /dev/sdb1 → vg\_data → lv\_mysql → /var/lib/mysql**

**KEY LVM COMMANDS:**

**\# Physical Volume Management**  
**pvcreate /dev/sdb1                    \# Initialize PV**  
**pvdisplay                             \# Show PV details**  
**pvs                                   \# Quick PV summary**  
**pvremove /dev/sdb1                    \# Remove PV**

**\# Volume Group Management**  
**vgcreate vg\_data /dev/sdb1 /dev/sdc1  \# Create VG from multiple PVs**  
**vgdisplay                             \# Show VG details**  
**vgs                                   \# Quick VG summary**  
**vgextend vg\_data /dev/sdd1            \# Add disk to VG**  
**vgreduce vg\_data /dev/sdd1            \# Remove disk from VG**

**\# Logical Volume Management**  
**lvcreate \-L 10G \-n lv\_mysql vg\_data   \# Create 10GB LV**  
**lvcreate \-l 100%FREE \-n lv\_app vg\_data  \# Use all free space**  
**lvdisplay                             \# Show LV details**  
**lvs                                   \# Quick LV summary**  
**lvextend \-L \+5G /dev/vg\_data/lv\_mysql \# Add 5GB**  
**lvextend \-l \+100%FREE /dev/vg\_data/lv\_mysql  \# Use all free space**  
**lvreduce \-L \-2G /dev/vg\_data/lv\_mysql \# Reduce (DANGEROUS\!)**  
**lvremove /dev/vg\_data/lv\_mysql        \# Delete LV**

**\# Resize Filesystem After LV Extension**  
**resize2fs /dev/vg\_data/lv\_mysql       \# For ext4**  
**xfs\_growfs /mount/point               \# For XFS**

**\# LVM Snapshots (for backups)**  
**lvcreate \-L 5G \-s \-n lv\_mysql\_snap /dev/vg\_data/lv\_mysql**  
**\# Mount snapshot, backup, then remove**  
**lvremove /dev/vg\_data/lv\_mysql\_snap**

**COMMON SCENARIOS:**

**1\. Extending root filesystem:**  
   **lvextend \-L \+10G /dev/mapper/rhel-root**  
   **xfs\_growfs /  \# or resize2fs /dev/mapper/rhel-root**

**2\. Moving data between disks:**  
   **pvmove /dev/sdb1 /dev/sdc1**  
   **vgreduce vg\_data /dev/sdb1**

**/\* COMMENT: Always extend filesystems AFTER extending LVs. For reduction, shrink**  
   **filesystem BEFORE reducing LV. XFS cannot be shrunk, only grown. Practice in**  
   **test environments before production changes. \*/**

**━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━**

**1.4 NFS (NETWORK FILE SYSTEM)**

**/\* COMMENT: NFS enables file sharing across Linux/Unix systems. Common in enterprise**  
   **environments for shared storage, home directories, and application data. Understanding**  
   **NFS is essential for storage administration and troubleshooting mount issues. \*/**

**NFS SERVER SETUP:**

**\# Install NFS server**  
**yum install nfs-utils          \# RHEL/CentOS**  
**apt install nfs-kernel-server  \# Debian/Ubuntu**

**\# Configure exports (/etc/exports)**  
**/data  192.168.1.0/24(rw,sync,no\_root\_squash)**  
**/home  \*(ro,sync)  \# Read-only to all**

**\# Export options explained:**  
**rw          \# Read-write access**  
**ro          \# Read-only access**    
**sync        \# Synchronous writes (safer)**  
**async       \# Asynchronous writes (faster)**  
**no\_subtree\_check  \# Don't check parent directories**  
**root\_squash       \# Map root to nobody (security)**  
**no\_root\_squash    \# Don't map root (use carefully)**

**\# Apply exports and start service**  
**exportfs \-arv                  \# Apply all exports verbosely**  
**systemctl enable \--now nfs-server**  
**systemctl start rpcbind nfs-server**

**\# Firewall (if needed)**  
**firewall-cmd \--permanent \--add-service=nfs**  
**firewall-cmd \--permanent \--add-service=mountd**  
**firewall-cmd \--permanent \--add-service=rpc-bind**  
**firewall-cmd \--reload**

**NFS CLIENT SETUP:**

**\# Install NFS client**  
**yum install nfs-utils**

**\# Manual mount**  
**mount \-t nfs 192.168.1.100:/data /mnt/nfs\_data**

**\# Persistent mount (/etc/fstab)**  
**192.168.1.100:/data  /mnt/nfs\_data  nfs  defaults,\_netdev  0 0**

**\# Mount options for /etc/fstab:**  
**\_netdev      \# Wait for network before mounting**  
**hard         \# Keep trying on failure (default)**  
**soft         \# Timeout and return error**  
**intr         \# Allow interrupting hung operations**  
**timeo=600    \# Timeout value**  
**retrans=2    \# Number of retries**

**TROUBLESHOOTING:**

**\# Check what's exported**  
**showmount \-e 192.168.1.100**  
**exportfs \-v**

**\# Check NFS mounts**  
**mount | grep nfs**  
**df \-h | grep nfs**

**\# Test NFS connectivity**  
**rpcinfo \-p 192.168.1.100**  
**telnet 192.168.1.100 2049**

**\# Common issues:**  
**\- "mount.nfs: access denied" \= Check /etc/exports and IP ranges**  
**\- "mount.nfs: No such file" \= Check path exists on server**  
**\- Stale file handle \= Server restarted, unmount and remount**

**/\* COMMENT: For production environments, consider NFSv4 with Kerberos authentication**  
   **for enhanced security. Also consider alternatives like GlusterFS or Ceph for**  
   **distributed storage with better performance and redundancy. \*/**

**━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━**

**1.5 LINUX FILESYSTEMS**

**/\* COMMENT: Understanding filesystem types and their characteristics helps you choose**  
   **the right filesystem for different use cases (performance, reliability, features). \*/**

**FILESYSTEM COMPARISON:**

**EXT4 (Fourth Extended Filesystem):**  
**● Most widely used Linux filesystem**  
**● Max file size: 16 TB**  
**● Max filesystem size: 1 EB**  
**● Journaling for crash recovery**  
**● Backward compatible with ext3/ext2**  
**● Can be shrunk**  
**● Use case: General purpose, root filesystems**

**XFS:**  
**● High-performance 64-bit filesystem**  
**● Max file size: 8 EB**  
**● Max filesystem size: 8 EB**  
**● Excellent for large files**  
**● Cannot be shrunk (only grown)**  
**● Parallel I/O operations**  
**● Default in RHEL 7+**  
**● Use case: Large files, databases, media storage**

**BTRFS (B-tree Filesystem):**  
**● Modern copy-on-write filesystem**  
**● Built-in snapshots**  
**● Compression support**  
**● RAID support**  
**● Still maturing (use with caution in production)**  
**● Use case: Desktop, experimental environments**

**ZFS:**  
**● Enterprise-grade filesystem**  
**● Built-in RAID, compression, deduplication**  
**● Snapshots and clones**  
**● Checksums for data integrity**  
**● High RAM requirements**  
**● Use case: Storage servers, NAS devices**

**FILESYSTEM OPERATIONS:**

**\# Create filesystems**  
**mkfs.ext4 /dev/sdb1**  
**mkfs.xfs /dev/sdb1**  
**mkfs.btrfs /dev/sdb1**

**\# Filesystem checks**  
**fsck /dev/sdb1          \# Generic**  
**e2fsck \-f /dev/sdb1     \# ext4**  
**xfs\_repair /dev/sdb1    \# XFS**

**\# Mount filesystems**  
**mount /dev/sdb1 /mnt/data**  
**mount \-o remount,ro /mnt/data  \# Remount read-only**

**\# Get filesystem info**  
**df \-hT                  \# Disk usage with types**  
**du \-sh /var/log         \# Directory size**  
**lsblk \-f                \# Block devices with filesystems**  
**blkid                   \# UUIDs and types**

**\# Tune filesystem**  
**tune2fs \-l /dev/sdb1           \# Show ext4 parameters**  
**tune2fs \-m 1 /dev/sdb1         \# Set reserved blocks to 1%**  
**tune2fs \-c 30 /dev/sdb1        \# Check every 30 mounts**

**━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━**

**1.6 SWAP MANAGEMENT**

**/\* COMMENT: Swap extends physical RAM by using disk space. While slower than RAM,**  
   **it prevents out-of-memory kills and allows system to handle memory spikes. \*/**

**CREATE SWAP FILE (Modern Method):**

**\# Create 2GB swap file**  
**dd if=/dev/zero of=/swapfile bs=1M count=2048**  
**chmod 600 /swapfile**  
**mkswap /swapfile**  
**swapon /swapfile**

**\# Make permanent (/etc/fstab)**  
**/swapfile  none  swap  sw  0  0**

**CREATE SWAP PARTITION:**

**fdisk /dev/sdb**  
**\# Create partition type 82 (Linux swap)**  
**mkswap /dev/sdb1**  
**swapon /dev/sdb1**

**\# Add to /etc/fstab**  
**/dev/sdb1  none  swap  sw  0  0**

**SWAP MANAGEMENT:**

**swapon \-s               \# Show active swap**  
**free \-h                 \# Memory and swap usage**  
**swapon \-a               \# Activate all swap in fstab**  
**swapoff \-a              \# Deactivate all swap**  
**swapoff /swapfile       \# Deactivate specific swap**

**SWAPPINESS TUNING:**

**\# Check current swappiness (default 60\)**  
**cat /proc/sys/vm/swappiness**

**\# Set swappiness (0-100, lower \= less swapping)**  
**sysctl vm.swappiness=10**

**\# Make permanent (/etc/sysctl.conf)**  
**vm.swappiness \= 10**

**RECOMMENDATIONS:**  
**✓ Desktop: swappiness 10-30**  
**✓ Server: swappiness 1-10**    
**✓ Database server: swappiness 1 (minimal swapping)**  
**✓ Swap size: 1-2x RAM for systems with \<8GB RAM**  
**✓ Swap size: Equal to RAM for systems with 8-64GB RAM**  
**✓ Swap size: 0.5x RAM or less for systems with \>64GB RAM**

**━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━**

**1.7 ESSENTIAL LINUX COMMANDS CHEAT SHEET**

**/\* COMMENT: These are the most frequently used commands every IT professional should**  
   **memorize. This consolidates knowledge from multiple articles into one quick reference. \*/**

**SYSTEM INFORMATION:**  
**hos**  
**tname \-a               \# System information**  
**uname \-r               \# Kernel version**  
**hostnamectl            \# Set hostname (systemd)**  
**uptime                 \# System uptime**  
**cat /etc/os-release    \# OS version details**  
**lscpu                  \# CPU information**  
**free \-h                \# Memory usage**  
**df \-h                  \# Disk usage**  
**lsblk                  \# Block devices**

**FILE OPERATIONS:**  
**ls \-lah                \# Detailed list with hidden files**  
**cp \-r source dest      \# Copy recursively**  
**mv old new             \# Move/rename**  
**rm \-rf directory       \# Remove recursively (DANGEROUS\!)**  
**find /path \-name "\*.log"  \# Find files**  
**grep \-r "pattern" /path   \# Search in files**  
**tar \-czf backup.tar.gz /data  \# Create compressed archive**  
**tar \-xzf backup.tar.gz        \# Extract archive**

**PROCESS MANAGEMENT:**  
**ps aux                 \# All processes**  
**top / htop             \# Real-time process monitor**  
**kill \-9 PID            \# Force kill process**  
**killall processname    \# Kill by name**  
**pkill \-f pattern       \# Kill matching pattern**  
**nohup command &        \# Run in background**  
**screen / tmux          \# Terminal multiplexer**

**NETWORKING:**  
**ip addr show           \# Network interfaces**  
**ip route show          \# Routing table**  
**netstat \-tulpn         \# Listening ports**  
**ss \-tulpn              \# Socket statistics**  
**ping host              \# Test connectivity**  
**traceroute host        \# Trace route**  
**curl \-I url            \# HTTP headers**  
**wget url               \# Download file**  
**scp file user@host:/path  \# Secure copy**
