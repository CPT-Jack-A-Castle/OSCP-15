# OSCP
OSCP certification study

## Penetration Testing Fundamentals 

A Penetration test or pentest is an ethically-driven attempt to test and analyse the security defences to protect these assets and pieces of information.</br>
A Penetration test involves using the same tools, techniques, and methodologies that someone with malicious intent would use and siilar to an audit

Penetration test is an authroized audit of a computer system's security and defences as agreed by the owners of the systems. The legality of penetration is pretty clear cut in this sense;

Before the penetration test starts, a formal discussion occurs between the penetration tester and the system owner. Various tools, techniques, and systems to be tested are agreed on. The discussion forms the scope of the penetration testing agreement. 

### Rule of Engagement (ROE)

ROE is a document that is created at the initial stages of a penetration testing engagement. This document consists of three main section:

- Permission: This section of the document gives explicit permission for the engagement to be carried out. This permission is essential to legally protect individuals and organizations for the activies they carry out.
- Test Scope: This section of document will annotate specific targets to which the engagement should apply. For example, the penetration test may only apply to certain servers or application but not entire network.
- Rules: The rules section will define exactly the techniques that are permitted during the engagement. For example, the rules may specifically state that techniques such as phishing attacks are prohibited, but MITM(Man in the Middle) attacks are okay. 

### Penetration Testing Methodologies 

Penetration tests can have a wide variety of objectives and targets within scope. Because of this, no penetration test is the same, and there are no one-case fits all as to how a penetration tester should approach it. 

The steps a penetration tester takes during an engagement is known as the methodology. 

There are 5 stategs:

```
===============================================================================================
Stage                |                     Description                                        |
===============================================================================================
Information gathering| This stage invovles collecting as much publically accessible informatio|
                     | n about a target/ organization as possible, for ex) OSINT and research |
                     | This step does not require scanning any systems.                       |
===============================================================================================
Enumeration/ Scanning| This stage involves discovering applications and services running on th|
                     | e systems. For ex) finding a web server that may be potentially vulnera|
                     | ble.                                                                   |
===============================================================================================
Exploitation         | This stage invovles leveraging vulnerabilities discovered on system    |
                     | This stage can invovle the use of public exploits or exploiting applica|
                     | tion logic                                                             |
===============================================================================================
Privilege Escalation | Once you have successfully exploited a system or application (known as |
                     | a foothold), this stage is the attempt to expand your access to a syste|
                     | m. You can escalate horizontally and vertically, where horizontally is |
                     | accessing another account of the same permission group, whereas vertica|
                     | lly, where horizontally is accessing another account of the same permi |
                     | ssion group (i.e. another user), whereas vertically is that of another |
                     | permission group (i.e. an administrator)                               |
===============================================================================================
Post-Exploitation    | This stage invovles a few sub statges: 1. What other host can be target|
                     | 2. What additional information can we gather from the host now that we |
                     | are a privileged user 3. Covering your tracks 4. Reporting             |
===============================================================================================
```

### OSSTMM 

The Open Source Security Testing Methodology Manual provides a detailed framework of testing strategies for systems, software, applications, communications and the human aspect of cybersecurity. 

The methodology focuses primarily on how these systems, application communicate, so it includes a methodology for:
- Telecommunication (phones, VoIP, etc.) 
- Wired Networks 
- Wireless communications 

![image](https://user-images.githubusercontent.com/79100627/165620744-e16c3745-33ad-4e9e-960b-a5a534171a1c.png)

### OWASP 

The Open Web Application Security Project framework is a community-driven and frequently updated framework used solely to test the security of web applications and services 

The foundation regularly writes reports the top ten security vulnerabilities a web application may have, the testing appraoch and remediation. 

![image](https://user-images.githubusercontent.com/79100627/165621044-785142ac-8f41-4fd4-989d-3b678649a09e.png)

### NIST Cybersecurity Framework 1.1 

The NIST Cyber security Framework is popular framework used to improve an organization cyber security standards and manage the risk of cyber threats. 
![image](https://user-images.githubusercontent.com/79100627/165621195-d5458c9b-e0a3-4c67-ad6a-11c4879ed75a.png)


### Black Box Testing 

This testing process is a high level process where the tester is not given any information about the inner workings of the application or service. 

The tester acts as a regular user testing the functionality and interaction of the application or piece of software. This testing can invovle interacting with the interface, i.e. buttons, and testing to see whether the intended result is returned. No knowledge of programming or understanding of the programme is necessary for this type of testing 

Black box testing significantly increases the amount of time spent during the information gathering and enumeration phase to understand the attack surface of the target. 

### Grey Box Testing 

This testing process is the most popular for things such as penetration testing. It is a combination of both black-box and white-box testing. The tester will have some limited knowledge of the internal components of the application or piece of software. Still, it will be interacting with the application as if it were a black-box scenario and then using knowledge of the application to try and resolve issues as they find them. 

### White Box Testing 

This testing process is a low-level process usually done by a software developer who knows programming and application logic. The tester will be testing the internal compnents of the application or piece of software and, for example, ensuring that specific functions work correctly and whithin a reasonable amount of time 
