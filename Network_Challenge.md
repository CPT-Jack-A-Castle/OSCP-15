# Network Challenge Write Up

HealthGongDoll

## What is the highest port number being open less than 10,000?

For this question, you can just do normal nmap Searching with various methods 

![1](https://user-images.githubusercontent.com/79100627/173692240-54125efd-c67f-4a53-bc41-54e406dbb63e.jpg)

## There is an open port outside the common 1000 ports; it is above 10,000 what is it?

For this question, the port above 10,000 couldn't detected with the normal option, So i used the All port scan to scan the open port. 

![1](https://user-images.githubusercontent.com/79100627/173692240-54125efd-c67f-4a53-bc41-54e406dbb63e.jpg)

```nmap -p- -T4 IP_ADDRESS```

Where ```-p-``` scans all the ports ```-T4``` does the scanning faster 

## What is the flag hidden in the HTTP server header?

In order to see the HTTP server header used the telnet 

![2](https://user-images.githubusercontent.com/79100627/173692775-82f7521a-a094-4c9e-83f6-2dba5d754af6.jpg)

## What is the flag hidden in the SSH server header?

Same as previous question, in order to see SSH server I used telnet and SSH port ```-22```

![3](https://user-images.githubusercontent.com/79100627/173692950-a418fe05-49e9-4963-8108-5772278bae51.jpg)

## We learned two usernames using social engineering: eddie and quinn. What is the flag hidden in one of those two account?

In order to get flag file, we need to login as eddie or quinn. However, we do not know the password yet. Therefore we use ```Hydra``` tool to find out the ftp server password for eddie and quinn

![4](https://user-images.githubusercontent.com/79100627/173693157-faf4c841-6d00-43df-b781-0cfcd015f946.jpg)

After find the password, use ```ftp IP address``` to connect to the FTP server and ```ls``` and ```get``` file. 

