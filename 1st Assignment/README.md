Goal: To see what parts of my network are publicly visible to the internet — the same way a hacker would.

Methodology

Step 1: Find Public IP 
I visited whatismyipaddress.com to find my public IP address. ( I’ve masked it here:  103.105.227.98)

Step 2: Scan with Shodan
Next, I searched this IP on Shodan.io, a search engine that indexes internet-connected devices.
I carefully reviewed the exposed ports, services, and software banners.

 Findings
Port	Service	                     Info	                                                      Risk Level
22	SSH	                        OpenSSH 7.4 –    running on sophoscukc.christuniversity.in	    High
80	HTTP	                       Apache 2.4.29 running	                                         Medium
443	HTTPS	                     TLS active (encrypted)	                                        Low 
7547	TR-069	                   ISP remote management open – risky	                            High

 Screenshot:
 
 <img width="827" height="664" alt="image" src="https://github.com/user-attachments/assets/28e72430-1a58-4935-9f96-4ff9b1885fbb" />
  
Security Concerns:

Port 22 (SSH) is open to the public. This makes it a common target for brute-force attacks.
Port 7547 (TR-069) is often used by ISPs for remote router management. This port has been exploited by botnets like Mirai.
Apache 2.4.29 is visible, and if not updated, attackers could exploit known vulnerabilities.No signs of a firewall – which means there’s nothing filtering incoming traffic.

Recommendations:

Close Unused Ports,
Use your router settings or a firewall like UFW to block risky ports like 22 and 7547 if not needed.
Secure SSH Access,
If SSH is required, disable password logins and use SSH keys instead.
Disable WAN Management,
Go to your router settings (192.168.1.1) > Advanced > Remote Management > Turn it OFF.
Update Regularly,
Keep your router firmware and software (like Apache) up to date.
Set Up a Firewall.

Conclusion:

This audit revealed that my network has multiple services exposed to the internet ,some of which pose high security risks. Using Shodan helped me understand how visible and vulnerable my system could be to attackers.By taking preventive actions like updating software, configuring a firewall, and disabling unnecessary ports, I can reduce my attack surface and significantly improve the security of my network.



