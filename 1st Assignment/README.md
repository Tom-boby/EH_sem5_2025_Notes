Goal: To see what parts of my network are publicly visible to the internet — the same way a hacker would.

 Methodology
Step 1: Find My Public IP
I visited whatismyipaddress.com to find my public IP address. (For privacy, I’ve masked it here: XXX.XXX.XX.XX)

Step 2: Scan with Shodan
Next, I searched this IP on Shodan.io, a search engine that indexes internet-connected devices.
I carefully reviewed the exposed ports, services, and software banners.

 Findings
Port	Service	Info	Risk Level
22	SSH	OpenSSH 7.4 – exposed to internet	 High
80	HTTP	Apache 2.4.29 running	 Medium
443	HTTPS	TLS active (encrypted)	 Low
7547	TR-069	ISP remote management interface	 High

 Screenshot:
(Insert Shodan screenshot here – make sure to blur or crop your IP)

 Security Concerns
Port 22 (SSH) is open to the public. This makes it a common target for brute-force attacks.

Port 7547 (TR-069) is often used by ISPs for remote router management. This port has been exploited by botnets like Mirai.

Apache 2.4.29 is visible, and if not updated, attackers could exploit known vulnerabilities.

No signs of a firewall – which means there’s nothing filtering incoming traffic.

🛠️ Recommendations
Close Unused Ports

Use your router settings or a firewall like UFW to block risky ports like 22 and 7547 if not needed.

Secure SSH Access

If SSH is required, disable password logins and use SSH keys instead.

Disable WAN Management

Go to your router settings (192.168.1.1) > Advanced > Remote Management > Turn it OFF.

Update Regularly

Keep your router firmware and software (like Apache) up to date.

Set Up a Firewall

Example commands using UFW on Linux:

bash
Copy
Edit
sudo ufw deny 7547
sudo ufw allow 443
sudo ufw enable
 Conclusion
This self-audit showed that several services on my network are exposed to the internet — and some are high risk. Tools like Shodan help reveal what attackers can already see.
By acting on this information, I can reduce my attack surface and make my system more secure.

