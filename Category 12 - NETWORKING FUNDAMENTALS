**\========================================**  
**CATEGORY 12: NETWORKING FUNDAMENTALS**  
**\========================================**

**12.1 NETWORK TROUBLESHOOTING:**

**/\* COMMENT: Network troubleshooting skills are essential for diagnosing connectivity**  
   **issues, performance problems, and security concerns. Understanding these tools**  
   **helps quickly identify and resolve network-related problems. \*/**

**KEY CONCEPTS:**  
**• OSI Model: 7 layers of network communication**  
**• TCP/IP: Protocol suite for internet**  
**• DNS Resolution: Domain name to IP address**  
**• Routing: Path packets take across networks**  
**• Ports: Application-specific endpoints**

**BASIC COMMANDS:**  
**\# Ping \- test connectivity**  
**ping google.com**  
**ping \-c 4 8.8.8.8  \# Send 4 packets**

**\# Traceroute \- show packet path**  
**traceroute google.com**  
**tracepath google.com  \# Alternative**

**\# DNS lookup**  
**nslookup google.com**  
**dig google.com**  
**dig \+short google.com**  
**dig @8.8.8.8 google.com  \# Specific DNS server**

**\# Show routing table**  
**route \-n**  
**ip route show**  
**netstat \-rn**

**\# Show network interfaces**  
**ifconfig**  
**ip addr show**  
**ip link show**

**\# Network statistics**  
**netstat \-tuln  \# Show listening ports**  
**netstat \-antp  \# Show all connections**  
**ss \-tuln       \# Modern alternative to netstat**

**\# ARP table**  
**arp \-a**  
**ip neigh show**

**ADVANCED DIAGNOSTICS:**  
**\# MTR \- combination of ping and traceroute**  
**mtr google.com**  
**mtr \-r \-c 10 google.com  \# Report mode**

**\# Netcat \- network swiss army knife**  
**nc \-zv hostname 80  \# Test port connectivity**  
**nc \-l 8080          \# Listen on port**  
**echo "test" | nc hostname 80  \# Send data**

**\# TCPDump \- packet capture**  
**sudo tcpdump \-i eth0**  
**sudo tcpdump \-i any port 80**  
**sudo tcpdump \-i eth0 \-w capture.pcap**  
**sudo tcpdump \-r capture.pcap**

**\# Nmap \- network scanner**  
**nmap \-sT scanme.nmap.org      \# TCP scan**  
**nmap \-sU 192.168.1.1          \# UDP scan**  
**nmap \-p 80,443 192.168.1.0/24 \# Specific ports**  
**nmap \-A scanme.nmap.org       \# OS detection**

**\# Check open ports locally**  
**sudo lsof \-i \-P \-n**  
**sudo lsof \-i :80**

**CONNECTIVITY TESTING:**  
**\# Test HTTP connectivity**  
**curl \-I https://google.com**  
**wget \--spider https://google.com**

**\# Test specific port**  
**telnet hostname 80**  
**nc \-zv hostname 22**

**\# Check if port is listening**  
**sudo netstat \-tulnp | grep :80**  
**sudo ss \-tulnp | grep :80**

**PERFORMANCE TESTING:**  
**\# Bandwidth test**  
**iperf3 \-s  \# Server**  
**iperf3 \-c server\_ip  \# Client**

**\# Network speed test**  
**speedtest-cli**

**BEST PRACTICES:**  
**• Start with ping to verify basic connectivity**  
**• Use traceroute to identify routing issues**  
**• Check DNS resolution with dig/nslookup**  
**• Verify firewall rules if ports are blocked**  
**• Use tcpdump for detailed packet analysis**  
**• Document findings for future reference**

**12.2 DNS MANAGEMENT:**

**/\* COMMENT: DNS translates domain names to IP addresses. Understanding DNS records**  
   **and management is crucial for web services, email, and network infrastructure. \*/**

**KEY CONCEPTS:**  
**• A Record: Maps domain to IPv4 address**  
**• AAAA Record: Maps domain to IPv6 address**  
**• CNAME: Alias for another domain**  
**• MX Record: Mail server records**  
**• TXT Record: Text information (SPF, DKIM)**

**COMMON DNS RECORDS:**  
**A Record:**  
**example.com.    IN  A  192.0.2.1**

**AAAA Record:**  
**example.com.    IN  AAAA  2001:0db8::1**

**CNAME Record:**  
**www.example.com.  IN  CNAME  example.com.**

**MX Record:**  
**example.com.  IN  MX  10  mail.example.com.**  
**example.com.  IN  MX  20  mail2.example.com.**

**TXT Record:**  
**example.com.  IN  TXT  "v=spf1 mx \-all"**

**NS Record:**  
**example.com.  IN  NS  ns1.example.com.**  
**example.com.  IN  NS  ns2.example.com.**

**DNS QUERIES:**  
**\# Check A record**  
**dig example.com A**  
**host example.com**

**\# Check MX records**  
**dig example.com MX**  
**nslookup \-query=mx example.com**

**\# Check TXT records**  
**dig example.com TXT**

**\# Reverse DNS lookup**  
**dig \-x 8.8.8.8**  
**host 8.8.8.8**

**\# Check all records**  
**dig example.com ANY**

**\# Trace DNS resolution**  
**dig \+trace example.com**

**DNS CONFIGURATION:**  
**\# /etc/hosts \- local DNS**  
**127.0.0.1   localhost**  
**192.168.1.100   server.local**

**\# /etc/resolv.conf \- DNS servers**  
**nameserver 8.8.8.8**  
**nameserver 8.8.4.4**  
**options timeout:2**

**\# Test DNS server**  
**dig @8.8.8.8 example.com**

**CACHE MANAGEMENT:**  
**\# Flush DNS cache (Ubuntu)**  
**sudo systemd-resolve \--flush-caches**  
**sudo systemctl restart systemd-resolved**

**\# Check DNS cache status**  
**sudo systemd-resolve \--statistics**

**BEST PRACTICES:**  
**• Use multiple DNS servers for redundancy**  
**• Implement proper TTL values**  
**• Use CNAME sparingly (adds lookup overhead)**  
**• Implement SPF, DKIM, DMARC for email**  
**• Regular DNS record audits**  
**• Use DNS monitoring tools**
