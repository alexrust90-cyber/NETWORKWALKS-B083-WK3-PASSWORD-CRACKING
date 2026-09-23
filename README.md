<div align="center">
 
PASSWORD CRACKING REPORT

EXPLOITATION AND CREDENTIAL ATTACKS PHASE

| Field | Information |
|:---:|:---:|
| Cybersecurity Professional | Alexandra Rustamova |
| Program/Batch | B083-Networkwalks |
| Date | 23 September 2026 |
| Modules Completed | W3-PM1: Password cracking with JTR<br>W3-PM2: Password cracking with NW tools<br>W3-Optional1: AI - JTR Password Cracking Lab with Claude & Hexstrike MCP v1 |
| Client/Target | Networkwalks (secured with permission already) |
| Permission secured from client? | Yes |
| Phases covered | Phase 1. Reconnaissance and Footprinting<br>Phase 2. Scanning and Network Discovery<br>Phase 3. Vulnerability Assessment and Analysis<br>Phase 4. Exploitation and Credential Attacks<br>Phase 5. In Progress |

</div>

---

### **1. LIABILITY DISCLAIMER**

I have performed these activities only on the systems & devices where I had secured written permission or the devices/systems that I own myself. All these materials are for education and research purpose only. Do not use anything from here to break the law. The instructor, the authors and Networkwalks are not responsible for what you do with this knowledge. Every action you take is your own responsibility. Misuse can lead to criminal charges, heavy fines, loss of your job and a permanent record. In most countries unauthorised access is a crime even when nothing is damaged.   

### **2. INTRODUCTION**

This report documents my Week 3 work as part of my ongoing cybersecurity internship program at Networkwalks. This week focused on the exploitation and credential-attack stage of the penetration-testing process, with an emphasis on password and hash cracking in an authorized lab environment.

The activities included setting up and using the HexStrike AI MCP server with Claude Desktop, integrating security tools available in the Kali Linux environment, and applying this workflow to a password-cracking exercise. The practical task involved analyzing a protected PDF, obtaining the corresponding password hash, and using John the Ripper (JtR) together with a wordlist to recover the password.

The exercises provided practical experience with password hashes, hash identification, password-cracking techniques, wordlists, and the use of AI-assisted security tooling. The objective was to understand how weak or guessable passwords can potentially be recovered from captured hashes and how these techniques fit into the exploitation stage of a penetration test.

For each activity, I documented the setup and commands or actions performed, the results obtained, screenshots as evidence, and a short explanation of the purpose and security relevance of each step.

### **3. TOOLS USED**

| Tool | Purpose |
|---|---|
| Kali Linux | Operating system used to perform the password-cracking and security-testing activities in the authorized lab environment |
| Kali Linux Terminal | Used to execute commands, navigate files, calculate hashes, prepare password-cracking files and run security tools |
| John the Ripper (JtR) | Used to perform password cracking against a password hash using a wordlist and identify the original password |
| Hash utilities | Used to calculate and verify cryptographic hash values of the protected PDF and other files |
| PDF password/hash extraction tools | Used to extract the password hash from the protected PDF so it could be analyzed and tested with JtR |
| Wordlists | Provided candidate passwords that John the Ripper tested against the extracted hash |
| Hexstrike MCP | Provided an AI-assisted interface for interacting with security tools and automating or coordinating security-testing tasks |
| Claude Desktop | Used as the AI interface for interacting with Hexstrike MCP and requesting security-tool operations |
| Networkwalks Browser Tools | Used as part of the lab workflow to access and work with the provided security-testing environment and tools |
| HexStrike security tools | Used through the HexStrike MCP environment to support security assessment and password-cracking activities |

### **4. ACTIVITIES PERFORMED**

**4.1. Password Cracking with John the Ripper**

As part of the exploitation and credential-attack phase, I performed a password-cracking exercise using **John the Ripper (JtR)** against a password-protected PDF provided for the authorized lab environment. The objective was to understand how a password can be recovered when an attacker has access to the appropriate password hash.

I started by obtaining the password hash associated with the protected PDF using a PDF hash-extraction tool. The extracted value was then saved in a text file (`hash1.txt`) in a format compatible with John the Ripper. I also verified that the hash was correctly formatted before proceeding with the cracking process.

Next, I used **John the Ripper** from the Kali Linux terminal and supplied the hash file using the command `john hash1.txt`. JtR recognized the supplied value as a **PDF password hash** and loaded one hash for processing. The output identified the format as `PDF [MD5 SHA2 RC4/AES 32/64]`.

John the Ripper subsequently completed the password-cracking process and reported that there were no password hashes left to crack. The recovered password was then used to open the original protected PDF, confirming that the password had been successfully recovered.

This activity demonstrated how password-cracking techniques can be used as part of a credential attack during a penetration test. It also showed the importance of strong and unpredictable passwords, as a password that can be recovered from an obtained hash may allow an attacker to gain access to protected resources.

By completing this exercise, I gained practical experience with password hashes, hash extraction, John the Ripper, and the relationship between password strength and resistance to credential attacks.

**4.2. Password Cracking with Networkwalk Tools**

As part of the exploitation and credential-attack phase, I performed a second password-cracking exercise using the **Networkwalks Hash Calculator and Password Cracker** tools in a web browser. The objective was to demonstrate an alternative password-cracking workflow without requiring locally installed cracking software.

I started by obtaining the password-protected PDF provided for the authorized lab exercise and uploading it to the **Networkwalks Hash Calculator**. The tool processed the protected document and extracted a password-cracking hash beginning with `$pdf$`. I copied the complete hash value for use in the next stage of the exercise.

Next, I opened the **Networkwalks Password Cracker** and submitted the extracted PDF hash. The tool attempted different password candidates against the supplied hash until it identified a matching password.

After the cracking process was completed, I used the recovered password to open the original protected PDF. This successfully confirmed that the recovered credential matched the password protecting the document.

This activity demonstrated a browser-based approach to password cracking and reinforced the relationship between protected files, password hashes, and password recovery. It also showed that password-cracking activities do not necessarily require a locally installed tool, as web-based security tools can provide similar functionality.

By completing this exercise alongside the John the Ripper activity, I was able to compare two different approaches to password cracking: a locally executed security tool in Kali Linux and a browser-based workflow using Networkwalks tools. Both exercises demonstrated the importance of using strong, unique passwords to reduce the risk of successful credential attacks.

**4.3. AI - JTR Password Cracking Lab with Claude & Hexstrike MCP v1**

As part of the exploitation and credential-attack phase, I performed an AI-assisted password-cracking exercise using **John the Ripper (JtR)** through the **HexStrike-AI MCP server and Claude Desktop** in a Kali Linux virtual machine. The objective was to demonstrate how an AI interface can interact with locally available security tools and assist with an authorized password-cracking task.

I started by launching the **HexStrike server** on the Kali Linux system. The server was configured to listen on the local port **8888**. I then opened a second terminal, activated the HexStrike Python virtual environment, and started the **HexStrike MCP connection**, connecting it to the local server at `http://localhost:8888`. Both processes were kept running while Claude Desktop was used to interact with the environment.

Before beginning the password-cracking activity, I verified that the HexStrike server was listening on the expected port. This confirmed that the local server and MCP components were running correctly and were ready to receive requests from Claude Desktop.

Next, I copied the target password-protected PDF, **`My-Locked-PDF3.pdf`**, to the Kali Linux desktop. I then used **Claude Desktop** to interact with the HexStrike MCP environment through natural-language prompts. First, I asked Claude to check whether **John the Ripper** was available through HexStrike and to display its installed version. I then requested that the hash value of `My-Locked-PDF3.pdf` be calculated.

After obtaining the PDF hash, I instructed Claude to use the **John the Ripper tool available through HexStrike** to perform the password-cracking operation against the extracted hash, using the **RockYou wordlist** as the password dictionary.

The password was successfully recovered. The recovered password was then verified against the original `My-Locked-PDF3.pdf` file, confirming that the credential identified during the cracking process was valid and could be used to access the protected document.

This activity demonstrated an AI-assisted workflow for a traditional password-cracking task. Rather than manually executing every command, I used natural-language prompts through Claude Desktop to request operations from the HexStrike MCP environment.

The exercise also demonstrated the different roles of the components involved: **Claude Desktop provided the AI-based user interface, HexStrike MCP provided the connection and orchestration layer for the security tools, and John the Ripper performed the actual password-cracking operation**.

By completing this exercise, I gained practical experience with **AI-assisted security testing, MCP communication, John the Ripper, PDF password hashes, wordlists, and security-tool orchestration**. It also reinforced the importance of understanding the underlying security tools even when an AI interface is used to assist with their operation.

### **5. RISK ANALYSIS/IMPACT**

Based on the password-cracking and AI-assisted security activities performed during Week 3, I identified the following potential security risks and observations.

| # | Risk/Finding | Evidence/Observation | Potential impact | Risk Level |
|---|---|---|---|---|
| 1 | Password successfully recovered from protected PDF hash | John the Ripper successfully recovered the password associated with `My-Locked-PDF3.pdf` | Demonstrates that an attacker with access to the relevant password-cracking data may be able to recover a weak or predictable password | 🟠 Medium  |
| 2 | Password hash can be used for offline password attacks | The PDF password hash was extracted and supplied to JtR for cracking | If password hashes are obtained by an unauthorized party, they may be subjected to offline cracking without interacting directly with the protected application or file | 🟠 Medium  |
| 3 | Password strength affects resistance to cracking | The password was successfully recovered using a password-cracking process and the RockYou wordlist | Common, predictable, or reused passwords may be more susceptible to dictionary-based attacks | 🟠 Medium  |
| 4 | Password-protected files depend on the strength of the password | The recovered credential successfully opened the protected PDF | A weak password can reduce the effective protection provided by an otherwise password-protected document | 🟠 Medium  |
| 5 | Browser-based password-cracking capability demonstrated | The Networkwalks Hash Calculator extracted the PDF hash and the Networkwalks Password Cracker successfully recovered the password | Demonstrates that password-cracking functionality can be accessible without locally installing specialized cracking software | 🟠 Medium  |
| 6 | AI-assisted security-tool operation demonstrated | Claude Desktop was used with HexStrike MCP to interact with John the Ripper and perform the cracking workflow | AI-assisted interfaces can simplify interaction with security tools, potentially lowering the technical barrier to performing authorized or unauthorized security operations | 🟠 Medium  |
| 7 | Security-tool availability depends on environment configuration | HexStrike detected a subset of the security tools available in the Kali environment | Missing or incorrectly configured tools can limit the effectiveness and scope of an assessment | 🟢 Low |
| 8 | Password-cracking activity performed against an authorized laboratory target | The exercises used the provided `My-Locked-PDF3.pdf` laboratory file | The activity itself does not represent a confirmed vulnerability in a production system; it demonstrates a credential-attack technique in a controlled environment | 🟢 Low |

Risk Level Key:

🔴 Critical
🟠 Medium
🟢 Low

The risks and observations above are based on activities performed against provided laboratory files and an authorized testing environment. The successful recovery of the PDF password demonstrates the effectiveness of the password-cracking technique, but it should not be interpreted as evidence that a production system or organization has the same weakness.

The main security lesson from these activities is that password strength and password-hash protection are important factors in resisting credential attacks. If an attacker obtains a usable password hash and the underlying password is weak, common, or predictable, offline password-cracking techniques may potentially recover the original credential.

The AI-assisted exercise also demonstrated that tools such as Claude Desktop and HexStrike MCP can simplify interaction with existing security tools. However, the underlying password-cracking operation was still performed by John the Ripper; the AI interface assisted with tool interaction and workflow orchestration rather than replacing the underlying security mechanism.

### **6. RECOMMENDATIONS**

Based on the activities performed during Week 3, the following recommendations can help reduce the risk of successful credential and password-cracking attacks:

1. **Use strong and unique passwords**
   Passwords should be sufficiently long, complex, and difficult to predict. Common words, simple patterns, and reused passwords should be avoided because they can increase the likelihood of successful dictionary or brute-force attacks.

2. **Avoid password reuse across systems and applications**
   Each account or protected resource should use a unique password. If one password is compromised, reuse across multiple systems could allow an attacker to gain access to additional resources.

3. **Protect password hashes and credential data**
   Password hashes and other authentication-related data should be properly protected from unauthorized access. If an attacker obtains suitable password-cracking data, offline attacks can be performed without interacting directly with the original application or system.

4. **Use appropriate password protection for sensitive files**
   Sensitive documents should be protected using strong passwords and appropriate encryption mechanisms. Password protection should not be considered sufficient when weak or predictable passwords are used.

5. **Implement multi-factor authentication (MFA)**
   Where supported, MFA should be enabled for user accounts and administrative access. This provides an additional authentication factor so that knowledge of a password alone is not sufficient to access the protected resource.

6. **Perform periodic password-security assessments**
   Organizations can conduct authorized password audits to identify weak or easily recoverable credentials. These assessments should be performed in a controlled environment and with appropriate authorization.

7. **Secure AI-assisted security tooling**
   AI-assisted tools such as Claude Desktop and MCP-based security environments should be configured carefully. Access to security tools, local files, credentials, and system commands should be restricted to authorized users and controlled environments.

8. **Keep security tools and their environments properly configured and updated**
   Security-testing tools and their supporting environments should be maintained and configured correctly. This helps ensure that authorized security assessments can be performed reliably while reducing unnecessary exposure of security tools or services.

9. **Use password-cracking tools only within authorized environments**
   Tools such as John the Ripper can be valuable for security assessments, but password-cracking activities should only be performed against systems, files, and credentials for which explicit authorization has been provided.

Overall, the exercises performed during Week 3 demonstrated that password strength, credential protection, and secure configuration are important factors in reducing the risk of successful credential attacks. The use of AI-assisted interfaces can simplify interaction with security tools, but appropriate authorization, technical understanding, and security controls remain essential.

### **7. CONCLUSION**

During Week 3 of my Cybersecurity & Ethical Hacking internship with Networkwalks, I focused on **Exploitation and Credential Attacks**, with particular emphasis on password cracking and the security of password-protected files.

I completed three password-cracking exercises using different approaches. The first involved **John the Ripper (JtR)** running directly in Kali Linux. The second used the **Networkwalks Hash Calculator and Password Cracker** through a web-based environment. The third combined **John the Ripper with HexStrike-AI MCP and Claude Desktop**, demonstrating how an AI-assisted interface can interact with security tools and support an authorized password-cracking workflow.

These activities helped me understand the relationship between protected files, password-cracking data, wordlists, and password recovery. I also gained practical experience extracting password-cracking data from a protected PDF, preparing it for JtR, using the RockYou wordlist, and verifying the recovered password against the original document.

An important part of this week's learning was understanding the different roles of the tools used in the AI-assisted exercise. **Claude Desktop** provided the natural-language interface, **HexStrike MCP** provided the connection and orchestration layer, and **John the Ripper** performed the actual password-cracking operation. This demonstrated how traditional cybersecurity tools can be combined with AI-assisted workflows without replacing the underlying security concepts or tools.

Overall, Week 3 strengthened my practical understanding of **credential attacks, password security, password cracking, wordlists, PDF protection, and AI-assisted security testing**. The exercises also reinforced the importance of using strong and unique passwords and protecting credential-related data from unauthorized access.

All activities were performed within the authorized training environment provided for the internship. The results obtained during these exercises demonstrate the techniques and risks associated with password attacks, but they should not be interpreted as confirmed vulnerabilities in a production environment.

### **8. EVIDENCES COLLECTED**

***PM1***

<img width="1919" height="900" alt="hash extractor" src="https://github.com/user-attachments/assets/33dcedd7-5c58-4696-87c5-fc2514aef2a7" />
<img width="1919" height="900" alt="jtr command" src="https://github.com/user-attachments/assets/b8baa7f1-cbc6-448f-9aa9-d0633fa75303" />
<img width="1919" height="900" alt="opened pdf" src="https://github.com/user-attachments/assets/3fe36f3f-c882-4f5f-a54b-944e5a26c02e" />

***PM2***

<img width="1919" height="900" alt="W3-PM2-Hash Calculator" src="https://github.com/user-attachments/assets/fa4e1f1d-0537-41a6-abb1-cf51a3a6d491" />
<img width="1919" height="900" alt="W3-PM2-Password Cracking1" src="https://github.com/user-attachments/assets/5ba7d903-afc9-48fe-abdb-4ac3375332b2" />
<img width="1919" height="900" alt="W3-PM2-Pass-Cracking2" src="https://github.com/user-attachments/assets/1a0c2029-ab1c-40a9-a534-43640347ba92" />
<img width="1919" height="900" alt="Final" src="https://github.com/user-attachments/assets/17c7b996-3775-439d-a16e-cb5b9444b6ac" />

***Optional1***

<img width="1919" height="900" alt="Screenshot_2026-09-22_18-48-44" src="https://github.com/user-attachments/assets/aca1ea76-5bb7-408e-b03e-e10aac82d598" />
<img width="1919" height="900" alt="Screenshot_2026-09-22_21-01-42" src="https://github.com/user-attachments/assets/ebe8fed8-6438-4abb-9267-138f2dddb641" />
<img width="1919" height="900" alt="Screenshot_2026-09-22_21-09-23" src="https://github.com/user-attachments/assets/858adc3f-ba60-4ae3-8baa-44467522208c" />

---

Author: 
Alexandra Rustamova
Cybersecurity professional B083
LinkedIn: https://www.linkedin.com/in/alexandra-rustamova-631a1439a/

---

Project Information
Program Name: Cybersecurity program at Networkwalks | Week: 03 | Repository: GitHub
