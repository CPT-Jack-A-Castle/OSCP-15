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

## Piping and Redirection 

Piping -> ```|```
Redirection -> ```>```, ```<``` 

## Redirection 

![image](https://user-images.githubusercontent.com/79100627/175192918-452bbfbb-6b1c-45d2-b5da-ee52f5cef923.png)

## Redirection to Existing File

![image](https://user-images.githubusercontent.com/79100627/175193013-8df4fbc1-3037-4a40-9814-89464a045c1b.png)

Redirection to the other way ```<``` below the picture ```wc``` command STDIN with data originating directly from the file we generated previous section. ```wc -m``` which counts characters in the file 

![image](https://user-images.githubusercontent.com/79100627/175193216-74041081-1e23-422a-a1d2-5e1d91ee332f.png)

## Redirecting the Error 

According tot he POSIX for the STDIN,STOUT, SSTDERR are defined as 0, 1, 2 

![image](https://user-images.githubusercontent.com/79100627/175193457-130c5c9b-6947-4261-8ff1-ec71096f5d12.png)

See the difference between ```ls ./test 2> error.txt``` with the ```ls ./test > error.txt```

## Piping 

![image](https://user-images.githubusercontent.com/79100627/175193614-eccd2777-76bc-4cc5-a28b-57a46e5f0738.png)

## Excercise 

### Use the cat command in conjection with sort to reorder the content of the /etc/passwd

![image](https://user-images.githubusercontent.com/79100627/175193891-518758a6-b746-418f-bedd-38dd2d3089fd.png)

### Redirect output the previous exercise to file of your choice in your home directory 

![image](https://user-images.githubusercontent.com/79100627/175193918-094f7a84-1571-496e-9f4e-8680932bfd71.png)

## Grep 

search text files for occurence of a given regular expression and outputs any line containing a match to the standard output, which is usually the terminal screen. 

![image](https://user-images.githubusercontent.com/79100627/175194260-4fa3af8b-3d33-4345-a042-8d4412b26165.png)

## sed 

sed is a powerful stream deitor. sed performs text editing on a stream of text, either a set of specific files or standard output. 

we created echo command and then piped it to sed in order to replace the word "hard" with "harder" 

![image](https://user-images.githubusercontent.com/79100627/175194534-6b418ea5-4b04-4be3-8325-e2ffb0091214.png)

## Cut

cut used to extract a section of text from a line and output it to the standard output. Some of the most commonly-used switches include -f for the field number we are cutting and ```-d``` for the field delimiter 

![image](https://user-images.githubusercontent.com/79100627/175195156-2dab57ba-d9ed-4584-9b4c-e113d40a310f.png)

![image](https://user-images.githubusercontent.com/79100627/175195252-b4dc2229-1cee-4d26-a554-5efd3bb21913.png)

## AWK 

awk is programming language designed for text processing and data extraction and reporting tool. 

```-F``` field separator , ```print``` result text 

![image](https://user-images.githubusercontent.com/79100627/175195531-6aaf3ec1-17b6-48c3-af11-62d6b42f62c0.png)

## Practical Example 

Apache HTTP server log is given (http://www.ofensive-security.com/pwk-files/access_log.txt.gz) that contains the evidence of attack. Our task is to use Bash comamnd to inspect the file and discover various pieces of information who the attacker and what happened

First we use ```head``` and ```wc``` command to take a quick peek at the log file to understand the stucture. The head command display the first 10 line in a file and wc command along with ```-l``` option displays the total number of lines of the file

![image](https://user-images.githubusercontent.com/79100627/175196268-1ac77fd0-3f24-4caa-99c7-66530da58fca.png)

Notice that log file is text based and contains different field (IP address, time stamp , HTTP request, etc). This is perfectly grep friendly file  we do this by piping output ```cat``` + ```cut``` +```sort```. 

![image](https://user-images.githubusercontent.com/79100627/175196458-2254a393-8b5a-4c7d-9fd2-ff3a8746388a.png)

We see the less than ten IP address, still not telling about the attacker. Next we use ```uniq``` and ```sort``` to show unique lines, further refine our output and sort the data by number of times each IP address accessed the server. the ```-c``` option of uniq will prefix the output line with number of occurrences 

![image](https://user-images.githubusercontent.com/79100627/175196711-a7447d9a-5215-4415-ab54-41ad05c333ec.png)

A few IP address stand out but we will focus on the address of the highest access of frequency. To filter the IP address we do:

![image](https://user-images.githubusercontent.com/79100627/175197005-cb34b50d-0361-44ab-960e-5bce67c2f4e7.png)

From this output it seems that IP address was accessing the /admin. Inspect further: 

![image](https://user-images.githubusercontent.com/79100627/175197563-cc1b3a5e-a94e-4d15-9378-e2892875f914.png)

Apparently IP address has been involved in an HTTP bruteforce attempt against this webserver  it seems like the brute force is succedded that "HTTP 200" message 

## Exercise 

### Using the /etc/passwd extract the user and home directory field for all user on your kali machine 









