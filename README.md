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

### Principle of Security 

CIA traid is an information security model that is used in consideration throughout creating a security policy 

**Confidentiality** 

Protection of data from unauthorized access and misuse. Organization will always have some form of sensitive data stored on their systems. To provide confidentiality is to protect this data from parties that it is not intended for. 

**Integrity** 

Condition where information is kept accurate and consistent unless authorized changes are made. It is possible for the information to change because of careless access and use, errors in the information system, or unauthroized access and use.

**Availability** 

The main concern in the CIA traid is that the information should be available when authroized users need to access it. 

### Principles of Privileges 

The level of access given to individuals are determined on two primary factors:

- The inidividual's role/function within the organization </br>
- The sensitivity of the information being stored on the system </br>

Two key concepts are used to assign and manage the access rights of individuals, two key concepts are used: Privileged Identity Management (PIM) and Privileged Access Management (or PAM) 

### The Bell-La Padula Model 

The Bell-La Padula Model is used to achieve confidentiality. This model has a few assumptions, such as an organization's hierarchical structure it is used in, where everyone's responsibilities/roles are well defined.

The model works by granting access to pieces of data (called objects) on a strictly need to know basis 

Advantages:
- Policies in this model can be replicated to real-life organizations hierarchies (and vice versa) 
- Simple to implement and understand, and has been proven to be successful. 

Disadvantages:
- Even though a user may not have access to an object, they will know about its existence (so it is not confidential in that aspect) 
- The model relies on a large amount of trust within the organization 

![image](https://user-images.githubusercontent.com/79100627/165843855-ebf846d7-9d05-41dd-a885-521d8d918c2d.png)

The Bell LaPadula Model is popular within organizations such as govermental and military. This is because members of the organization are presumed to have already gone through a prcocess called vetting. Vetting is a screening process where applicant's backgrounds are examined to establish the risk they pose to the organziation. Therefore, applicant who are successfully vetted are assumed to be trust worthy - which is where this model fits in.

### Biba Model 

The Biba model is arguably equivalent tof Bell-La Padula model but for the integrity of CIA triad.

This model applies the rule to objects(data) and subjects (users) that can be summarised as "no writeup, no read down". This rule means that subjects can create or write content to objects at or below their level but can only read the contents of objects above the subject's level 

Advantages:
- This model is simple to implement 
- Resolves the limitations of Bell-La Padula model by addressing both confidentiality and data integirty. 

Disadvantages: 
- There will be many levels of access and objects. Things can be easily overlooked when applying security controls. 
- Often results in delays within a business. For example, a doctor would not be able to read the notes made by nurse in a hospital with this model 

![image](https://user-images.githubusercontent.com/79100627/165844848-b3b343f7-658d-4b2e-ac86-bc7eb1b290e5.png)

The Biba model is used in organziation or situation where integrity is more important than confidentiality. For example, in software development, developers may only have access to the code that is necessary for their job. They may not need access to criticial pieces of information such as database

### Threat Modelling & Incident Response

The threat modelling process is very similar to a risk assessment made in workplaces for employees and customers. The principles all return to: 
- Preparation
- Identification
- Mitigations
- Review 

A complex process that needs constant review and discussion with a dedicated team. An effective threat model includes:
- Threat intelligence 
- Asset identification
- Mitigation Capabilities 
- Risk assessment 

### STRIDE (Spoofing Identity, Tampering with data, Repudiation threats, Information disclosure, Denial of Service and Elevation of Privileges)

![image](https://user-images.githubusercontent.com/79100627/165845965-4ebfe464-8f5d-441f-bde0-8277bb7e5d50.png)


### PASTA (Process for Attack Simulation and Threat Analysis)

![image](https://user-images.githubusercontent.com/79100627/165846519-79d95f19-b163-4c2d-ab7e-8b39c2ca8fa3.png)


### CSIRT (Computer Security Incident Response Team)

![image](https://user-images.githubusercontent.com/79100627/165846460-26fe7242-4daa-4919-912b-fad9398a77d6.png)
