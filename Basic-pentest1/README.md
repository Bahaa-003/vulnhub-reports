# VulnHub - Basic Pentesting 1

This is a write-up for the **Basic Pentesting 1** machine from VulnHub.

---

##  Machine Information

- **IP Address**: `10.0.2.8`

---

##  Nmap Scan Result

```
Nmap scan report for 10.0.2.8
Host is up (0.0013s latency).
Not shown: 997 closed tcp ports (reset)
PORT   STATE SERVICE VERSION
21/tcp open  ftp     ProFTPD 1.3.3c
22/tcp open  ssh     OpenSSH 7.2p2 Ubuntu 4ubuntu2.2 (Ubuntu Linux; protocol 2.0)
80/tcp open  http    Apache httpd 2.4.18 ((Ubuntu))

MAC Address: 08:00:27:D2:04:C0 (Oracle VirtualBox virtual NIC)
Device type: general purpose
Running: Linux 3.X|4.X
OS CPE: cpe:/o:linux:linux_kernel:3 cpe:/o:linux:linux_kernel:4
OS details: Linux 3.2 - 4.9
Network Distance: 1 hop
Service Info: OSs: Unix, Linux; CPE: cpe:/o:linux:linux_kernel




-------

Notable Service
Port 21/tcp running ProFTPD 1.3.3c, which is known to be vulnerable.

-------


Exploitation
Using Metasploit with the following payload:
		cmd/unix/reverse


I successfully gained root access on the machine



-------

Credentials and Hashes
Discovered Hash for User marlinspike:
		marlinspike:$6$wQb5nV3T$xB2WO/jOkbn4t1RUILrckw69LR/0EMtUbFFCYpM3MUHVmtyYW9.ov/
aszTpWhLaC2x6Fvy5tpUUxQbUhCKbl4/:17484:0:99999:7:::

------


Cracked using john:
Username: marlinspike

Password: marlinspike

The same password works for root as well.


-----

Directory Enumeration
Using gobuster, the following endpoint was discovered:

	http://10.0.2.8/secret/

Also, a possible internal DNS server was observed:

	http://vtcsec


------
Conclusion
Gained root access via ProFTPD vulnerability.

Cracked user hash using john.

Found additional interesting resources via gobuster.















