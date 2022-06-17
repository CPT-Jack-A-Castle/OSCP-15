# Metasploit 

## Main Components of Metasploit 

While using the Metasploit Framework, you will primarily interact with the Metasploit console. You can launch it from the AttackBox terminal using the msfconsole command. The console will your main interface to interact with the different modules of the Metasploit Framework. Modules are small components within the Metasploit framework that are built to perform a specific task, such as exploiting a vulnerability, scanning a target, or performing  a brute-force attack.

- Exploit: A peice of code that uses a vulnerability present on the target system.
- Vulnerability: A design, coding, or logic flaw affecting the target system. The exploitation of a vulnerability can result in disclosing confidential information or allowing the attacker to execute code on the target system.
- Payload: An exploit will take advantage of a vulnerability. However, if we want to exploit to have the result we want (gaining access to the target system, read condifential information, etc.), we need to use a payload. Payloads are the code that will run on the target system. 

Modules and categories under each one are listed below. These are given for reference purposes, but you will interact with them through the Metasploit console (msfconsole).

![image](https://user-images.githubusercontent.com/79100627/174391662-2380863e-a5e3-4431-8382-beab1eb2936c.png)

Auxiliary: Any supporting module, such as scanners, crawlers and fuzzers, can be found here. 

![image](https://user-images.githubusercontent.com/79100627/174392091-98b920bf-4b8c-4718-ba25-b84eb52f36e4.png)

Encoders: Encoders will allow you to encode the exploit and payload in the hope that a signature-based antivirus solution may miss them. 

Signature based anitvirus and security solutions have a database of known threats. They detect threats by comparing suspicious files to this database and raise an alert if there is a match. Thus encoder can have a limited success rate as antivirus solutions can perform additional checks.

![image](https://user-images.githubusercontent.com/79100627/174392337-da3ded22-ca35-4373-948a-0744a965b26a.png)

Evaision: While encoders will encode the paylaod, they should not be considered a direct attempt to evade antivirus software. 

On the other hand, "evasion" modules will try that, with more or less success.

![image](https://user-images.githubusercontent.com/79100627/174392459-e5d0ff56-df36-4eb9-b622-246940b98524.png)

Exploits: Exploits, neatly organized by target system. 

![image](https://user-images.githubusercontent.com/79100627/174392553-2a445aa4-cd22-4c12-91b1-f9468e2913e6.png)

NOPs: NOPs (No OPeration) do nothing, literally.

They are represented in the Intel x86 CPU family they are represented with 0x90, following whihch the CPU will do nothing for one cycle. They are often used as a buffer to achieve consistent payload sizes.

Payloads: Payloads are codes that will run on the target system. 

Exploits will leverage a vulnerability on the target system, but to achieve the desired result, we will need a payload. Examples could be; getting a shell, loading a malware or backdoor to the target system, running a command, or launching calc.exe as a proof of concept to add to the penetration test report. Starting the calculator on the target system remotely by launching the cal.exe application is a begign way to show that we can run commands on the target system. 

Running command on the target system is already an important step but having an interactive connection that allows you to type commands that will be executed on the target system is better. Such an interactive command line is called "shell". Metasploit offers the ability to send different payload that can open shells on the target system.

![image](https://user-images.githubusercontent.com/79100627/174394538-570093ae-218e-45dc-987e-c5ef68563f5b.png)


You will see three different directories under payloads: singles, stagers, and stages.

- Singles: self-contained payloads (add user, launch notepad.exe, etc). That do not need to download an additional component to run.
- Stagers: Responsible for setting up a connection channel between Metasploit and the target system. Useful when working with staged payloads. "Staged payloads" will first upload a stager on the target system then downalod the rest of payload (stage). This provides some advantages as the initial size of the payload will be relatively small compared to the full payload sent at once.
- Stages: Downloaded by the stager. This will allow you to use larger sized paylaods. 

##
