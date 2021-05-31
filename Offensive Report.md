#  Red Team: Summary of Operations

 ## Table of Contents

  ### * Exposed Services
  ### * Critical Vulnerabilities
  ### * Exploitation
  
### 1. Exposed Services
Nmap scan results for target 1 machine reveal the below services and OS details:

$ nmap -sV 192.168.1.110/24

![image](https://user-images.githubusercontent.com/72705930/120231089-a223e180-c21e-11eb-8ccb-3dac4f28e74f.png)


 
This scan identifies the services below as potential points of entry:

 ●	Port 22/tcp ssh
 ●	80/tcp http
 ●	111 rpcbind
 ●	139 netbios-ssn
 ●	445 netbios-ssn
 

## 2. The following vulnerabilities were identified on target:1

### Rpcbind version 2-4 - CVE-2017-8779. 
Vulnerability type is Denial of Service. It doesn’t have confidentiality and integrity impact, and does not require authentication to exploit vulnerability. According to the CVSS Scores it scored 7.8, making it’s severity high. 

 ![image](https://user-images.githubusercontent.com/72705930/120231346-34c48080-c21f-11eb-858c-45609cedcb93.png)


### CVE-2017-7494 
Samba Netbios does not restrict the file path when using Windows named pipes, which allows remote authenticated users to upload a shared library to a writable shared folder.

 ![image](https://user-images.githubusercontent.com/72705930/120231908-60943600-c220-11eb-9c66-d586e5e9bbc9.png)
 
 

 ![image](https://user-images.githubusercontent.com/72705930/120231952-7bff4100-c220-11eb-8e89-5fb4da14c759.png)


### CVE-2016-1908 
The client in OpenSSH before 7.2 mishandles failed cookie generation for untrusted X11 forwarding and relies on the local X11 server for access-control decisions, which allows remote X11 clients to trigger a fallback and obtain trusted X11 forwarding privileges by leveraging configuration issues on this X11 server, as demonstrated by lack of the SECURITY extension on this X11 server. NVD severity high. 

### CVE-2017-15710 Apache httpd 2.4.10. 
Severity is high according to CVE 7.5 In Apache httpd 2.0.23 to 2.0.65, 2.2.0 to 2.2.34, and 2.4.0 to 2.4.29, mod_authnz_ldap, if configured with AuthLDAPCharsetConfig, uses the Accept-Language header value to lookup the right charset encoding when verifying the user's credentials. If the header value is not present in the charset conversion table, a fallback mechanism is used to truncate it to a two characters value to allow a quick retry (for example, 'en-US' is truncated to 'en'). A header value of less than two characters forces an out of bound write of one NUL byte to a memory location that is not part of the string. In the worst case, quite unlikely, the process would crash which could be used as a Denial of Service attack. In the more likely case, this memory is already reserved for future use and the issue has no effect at all.

## 3. Exploitation
The Red Team was able to penetrate Target 1 and retrieve the following confidential data:

After discovering the users as Michael and Steven. I used SSH to remote login into Michael’s account and used the Command used - find / -name "flag*.txt" to retrieve the 1st flag. 

 ![image](https://user-images.githubusercontent.com/72705930/120231907-60943600-c220-11eb-80fa-09bf9c6ef46b.png)


The second flag was found within the the /var/www directory and was viewed with the cat command

 ![image](https://user-images.githubusercontent.com/72705930/120231968-891c3000-c220-11eb-86b2-2894e6b058d8.png)



