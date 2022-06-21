# OSCP Textbook

This note is for OSCP Textbook Study Purposes 

## SSH Service 

SSH service run on port 22.

can use the ```systemctl``` with ```start``` option

![image](https://user-images.githubusercontent.com/79100627/174880396-53afdcdd-38e8-463c-ae05-f3e03091b83f.png)

After this it does not return any output, we need to verify that the SSH service is running and listening on TCP port 22 by using the ```ss``` command and pining the output into ```grep``` to search the output for ```sshd```

![image](https://user-images.githubusercontent.com/79100627/174880582-cfe922ac-dd55-4e5c-b7a9-3a93c8deee60.png)

If we want to start SSH service at boot time we enable the systemctl command 

![image](https://user-images.githubusercontent.com/79100627/174880842-8f2f6dd2-b8c3-4967-a174-63170208799f.png)

## HTTP service 

HTTP is TCP based using Apache port 80 is default.

![image](https://user-images.githubusercontent.com/79100627/174881032-51757bb2-be29-4897-a763-58bb839c3f48.png)

After this we can verify with ```ss``` and ```grep```

![image](https://user-images.githubusercontent.com/79100627/174881185-a0b32cfc-1487-4e05-b732-4713c16acc47.png)

To start the HTTP service at boot time same command ```sudo systemctl enable apache2```

## To see all the service in Kali 

```systemctl``` with the ```list-unit-file``` option 

![image](https://user-images.githubusercontent.com/79100627/174881720-6cdddf2d-7db5-4c82-8482-ed90ad72a8ff.png)

## APT

Searching, Installing and Removing Tools - apt (Advanced Package Tool) (Only Debian based system) 

## APT-Cache search 

```apt-cache search``` command displays much of the information stored in the internal cached package database. Let's say if you want to install it but you have to check if it is already installed

```apt-cache search FILE```
![image](https://user-images.githubusercontent.com/79100627/174882523-8de308d6-c0a3-46bc-84b6-ee266e3fd2ca.png)

but if you do apt-cache search you can't see the pure-ftpd keyword. The reason is that apt-cache search looks for the requested keyword in the package's description rather than packacge name it self. 

so do the ```apt show``` 

![image](https://user-images.githubusercontent.com/79100627/174882793-0e1491c0-7ee7-47a5-bc98-ac40301a670d.png)

## APT install 

install the system followed by the packacge name 

```apt install FILE```

![image](https://user-images.githubusercontent.com/79100627/174882991-81dd88f6-0795-4484-b3e7-fa418626adba.png)

## APT remove --purge 

It completely removes the packacage from Kali. It is important to note that removing a package with apt remove removes all package data but leaves small user configuration files behind. 

![image](https://user-images.githubusercontent.com/79100627/174883250-35f23403-5cff-4587-b748-b8e828fbe476.png)

## dpkg 

dpkg is the core tool used to install a package, either directly or indirectly through APT. It is also the preferred tool to use when operating offline, since it does not require an interent connection. 

dpkg will not install any dependencies that the package might require. To install a package with dpkg, provide the -i or --install option and the path to the .deb package file. (This assume that the .deb file installed previously or downloaded)


## The Bash Environment 

echo command followed by "$" character and an environment variable name 

![image](https://user-images.githubusercontent.com/79100627/174892512-3c25383c-422b-4cf7-a953-070a770b21dc.png)

also you can use the environment variables such as USER, PWD and HOME

![image](https://user-images.githubusercontent.com/79100627/174892850-1c673f30-efd9-4e33-9f82-67ec8fcc6e0a.png)

An environment variable can be defined with the export command. For example. if we are scanning a target and don't want to type int he system's IP address repeatedly, we can quickly assign it an environment variable and use that instead. 

![image](https://user-images.githubusercontent.com/79100627/174893495-c6a22348-1925-4f57-b59d-f1baacfc2c96.png)

The export command makes the variable accessible to any subprocesses we might spawn from our current Bash instance. If we set an environment variable without export it will only be available in the current shell. 

$$  variable to display the process ID of the current shell instance to make sure that we are indeed issuing commands in two different shells: 

![image](https://user-images.githubusercontent.com/79100627/174893747-276e4765-862d-4455-9786-89a15ae015c5.png)

There are many other env variable can view via ```env``` command

![image](https://user-images.githubusercontent.com/79100627/174893941-9de59fb6-bde0-4b02-877e-067a64e01966.png)

## Tab Completion 

The Bash Shell auto complete function allows us to complete filenames and directory paths with the tab key. 

![image](https://user-images.githubusercontent.com/79100627/174894501-4b313ee5-dd25-4264-a599-ebef16bbe6b9.png)

## Bash History Tricks 

Bash maintains a history of commands that have been entered, which can be displayed with the history command 


