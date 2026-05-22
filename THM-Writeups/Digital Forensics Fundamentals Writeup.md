**Platform:** TryHackMe  
**Difficulty:** Easy  
**Category:** Defensive Security
**Date:** 22 May 2026

---

## Objective
- Phases of digital forensics
- Types of digital forensics
- Procedure of evidence acquisition
- Windows forensics
- Solving a forensics case

---

## Key Concepts Learned
- How to get metadata from pdf and image file. 
- understand that have to use write blocker to prevent data alter during investigation
- know that Chain of Custody is important to prove that evidence is integrity and reliability.
- understanding digital forensics methodology - collection > examination > analysis > report.
- understand different type of digital forensics. 
![[Pasted image 20260522161023.png|448]]
- know the different between volatile data (memory image) and non-volatile data (disk image).

---

## Digital Forensics Tools Practiced
```shell
exiftool -c "%.6f" letter-image.jpg
```
*What it does: brute force web login page, using id molly and wordlist as password. **F=incorrect** to be change to match the login error on webpage, and **/login** is endpoint/path to login page.*

```shell
exiftool -c "%.6f" letter-image.jpg | grep -i gps
```
*What it does: brute-forcing ssh login using login id molly and password list.*

```shell
pdfinfo ransom-letter.pdf
```
*What it does: brute force web login page, using id molly and wordlist as password. **F=incorrect** to be change to match the login error on webpage, and **/login** is endpoint/path to login page.*

```shell
exiftool letter-image.jpg | grep -i model
```
*What it does: login to ssh after getting password from hydra.*

---

## Answers & Analysis

**Q: Using pdfinfo, find out the author of the attached PDF file, ransom-letter.pdf.?**  
**A:** Ann Gree Shepherd - by using `pdfinfo ransom-letter.pdf` we can see the author name.

**Q: Using exiftool or any similar tool, try to find where the kidnappers took the image they attached to their document. What is the name of the street?**  
**A:** Milk Street - `exiftool -c "%.6f" letter-image.jpg | grep -i gps` thm used manual convert gps location. i search for automation which use `-c` to automatic convert to  decimal Degree that searchable in googlemap. and grep gps info only.

**Q: What is the model name of the camera used to take this photo?**  
**A:** Canon EOS R6 - `exiftool letter-image.jpg | grep -i model`

---
## Tools 
| Tools          | Purpose                         | Type                   | Link                                                                         |
| -------------- | ------------------------------- | ---------------------- | ---------------------------------------------------------------------------- |
| **FTK Imager** | Disk image collection & analyze | Acquisition & Analysis | —                                                                            |
| **Autopsy**    | Disk image analyze              | Analysis               | [autopsy.com](https://www.autopsy.com/)                                      |
| **DumpIt**     | Memory image collection         | Acquisition            | [toolwar.com](https://www.toolwar.com/2014/01/dumpit-memory-dump-tools.html) |
| **Volatility** | Memory image analyze            | Analysis               | [volatilityfoundation.org](https://volatilityfoundation.org/)                |



## Takeaways
Forensics investigation must follow strict procedure, like volatile data(memory) must be collect first otherwise all will be gone. 
and Chain of Custody is very important in court, its not only recording the details of the evidence. if missing some part of information in Chain of Custody, it cant be used as evidence anymore.
metadata contain so much information that i think, its so useful when investigating. we can get location, author and time information, ETC



