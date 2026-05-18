**Platform:** TryHackMe  
**Difficulty:** Easy  
**Category:** Offensive Tools
**Date:** 17 May 2026

---

## Objective
Learn how to use enumeration tool, Gobuster. it can enumerate web directory, subdomain, and virtual hosts.

---

## Key Concepts Learned
- Understanding the basics of enumeration
- How to use Gobuster to enumerate web directories and files
- How to use Gobuster to enumerate subdomains
- How to use Gobuster to enumerate virtual hosts
- How to use a wordlist
- Understand different syntax and flag



---

## Gobuster Enumeration Practiced
```bash
gobuster dir -u "http://www.example.thm" -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -r
```
*What it does: enumerate web directory **dir** targeting www.example.com using flag **-u**, using local wordlist **-w** and **-r** for redirect responses for code 301*

```bash
gobuster dir -u "http://www.example.thm" -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -x .php,.js
```
*What it does: same functions as above command, but **-x**also look for .php and .js extension. *

```bash
gobuster dns -d example.thm -w /usr/share/wordlists/SecLists/Discovery/DNS/subdomains-top1million-5000.txt
```
*What it does: Enumerate subdomain using **dns -d** targeting domain.

```bash
gobuster vhost -u "http://MACHINE_IP" --domain example.thm -w /usr/share/wordlists/SecLists/Discovery/DNS/subdomains-top1million-5000.txt --append-domain --exclude-length 250-320
```
*What it does: Enumerate vhost, must have **-u** and **--domain**, wordlists, `-append-domain` appends the configured domain to each entry in the wordlist. `--exclude-length` filters the responses we get from the sent web requests like "Found: Orion.example.thm Status: 404 [Size: 279]" or  "Found: pm.example.thm Status: 404 [Size: 276]".


---

## Answers & Analysis

### Task 3
**Q: What flag do we use to specify the target URL?**
**A:** -u , -u flag is for enumerate target url

**Q: What command do we use for the subdomain enumeration mode?**  
**A:** dns - dns for subdomain, dir for directory and vhost for virtual host.

### Task 4
**Q: Which flag do we have to add to our command to skip the TLS verification? Enter the long flag notation.**
**A:** --no-tls-validation

**Q: Enumerate the directories of www.offensivetools.thm. Which directory catches your attention?**  
**A:** secret - use dir to enumerate the website.

**Q: Continue enumerating the directory found in question 2. You will find an interesting file there with a .js extension. What is the flag found in this file?**  
**A:** THM{ReconWasASuccess} - continue enumerate the directory /secret/, and manage to get flag.js, open it directly on web browser will show the flag. i didnt know gobuster can enumerate within the folder until i google for solution. learned something new.

### Task 5
**Q: Apart from the dns keyword and the -w flag, which shorthand flag is required for the command to work?**
**A:** -d - a flag must have after **dns**, followed by target domain.

**Q: Use the commands learned in this task, how many subdomains are configured for the offensivetools.thm domain?**
**A:** 4 - gobuster dns -d offensivetools.thm -w /usr/share/wordlists/SecLists/Discovery/DNS/subdomains-top1million-5000.txt 

### Task 6
**Q: Use the commands learned in this task to answer the following question: How many vhosts on the offensivetools.thm domain reply with a status code 200?**
**A:** 4 - gobuster vhost -u "http://MACHINE_IP" --domain example.thm -w /usr/share/wordlists/SecLists/Discovery/DNS/subdomains-top1million-5000.txt --append-domain --exclude-length 250-320

---

## Takeaways
Enumerating web directory, subdomain and vhost is fun. it can list down all the directory, file extension that hide inside the web app, list down all sub domian etc by using wordlists. 

## Gobuster Cheatsheet

| Short Flag | Long Flag    | Description                                                                                                                                                                                                                                                                                                            |
| ---------- | ------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `-t`       | `--threads`  | This flag configures the number of threads to use for the scan. Each of these threads sends out requests with a slight delay. The default number of threads is 10. This number may be slow when using large wordlists. You can increase or decrease the number of threads depending on the available system resources. |
| `-w`       | `--wordlist` | The flag configures a wordlist to use for iterating. Each wordlist entry is attached to the URL you included in the command.                                                                                                                                                                                           |
|            | `--delay`    | This flag defines the amount of time to wait between sending requests. Some web servers include mechanisms to detect enumeration by looking at how many requests are received in a certain period of time. We can increase the delay between subsequent requests to make it look like normal web traffic.              |
|            | `--debug`    | This flag helps us to troubleshoot when our command gives unexpected errors.                                                                                                                                                                                                                                           |
| `-o`       | `--output`   | This flag writes the enumeration results to a file we choose.                                                                                                                                                                                                                                                          |
|            |              |                                                                                                                                                                                                                                                                                                                        |
|            |              |                                                                                                                                                                                                                                                                                                                        |

|      |                            |                                                                                                                                                                                                                               |
| ---- | -------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `-c` | `--cookies`                | This flag configures a cookie to pass along each request, such as a session ID.                                                                                                                                               |
| `-x` | `--extensions`             | This flag specifies which file extensions you want to scan for. E.g., .php, .js                                                                                                                                               |
| `-H` | `--headers`                | This flag configures an entire header to pass along with each request.                                                                                                                                                        |
| `-k` | `--no-tls-validation`      | This flag  skips the process that checks the certificate when https is used. It often happens for CTF events or test rooms like the ones on THM a self-signed certificate is used. This causes an error during the TLS check. |
| `-n` | `--no-status`              | You can set this flag when you don’t want to see status codes of each response received. This helps keep the output on the screen clear.                                                                                      |
| `-P` | `password`                 | You can set this flag together with the --username flag to execute authenticated requests. This is handy when you have obtained credentials from a user.                                                                      |
| `-s` | `--status-codes`           | With this flag, you can configure which status codes of the received responses you want to display, such as 200, or a range like 300-400.                                                                                     |
| `-b` | `--status-codes-blacklist` | This flag allows you to configure which status codes of the received responses you don’t want to display. Configuring this flag overrides the -s flag.                                                                        |
| `-U` | `--username`               | You can set this flag together with the `--password` flag to execute authenticated requests. This is handy when you have obtained credentials from a user.                                                                    |
| `-r` | `--followredirect`         | This flags configures Gobuster to follow the redirect that it received as a response to the sent request. A HTTP redirect status code (e.g., 301 or 302) is used to redirect the client to a different URL.                   |

| Flag | Long Flag      | Description                                                                       |
| ---- | -------------- | --------------------------------------------------------------------------------- |
| `-c` | `--show-cname` | Show CNAME Records (cannot be used with the `-i` flag).                           |
| `-i` | `--show-ips`   | Including this flag shows IP addresses that the domain and subdomains resolve to. |
| `-r` | `--resolver`   | This flag configures a custom DNS server to use for resolving.                    |
| `-d` | `--domain`     | This flag configures the domain you want to enumerate.                            |