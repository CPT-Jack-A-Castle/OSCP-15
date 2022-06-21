# OSCP Textbook Exercise 

## 2.4.3.4 Exercise 

### Use the man to look at the man page of one of your preferred commands 

![image](https://user-images.githubusercontent.com/79100627/174873008-f4c53fa6-d8b1-47c6-a09f-84a358af3ad6.png)
man 

### Use the man to look for a keyword related to file compression 

Option -K refers to Keyword

![image](https://user-images.githubusercontent.com/79100627/174873416-a64575f9-828f-4268-b258-809014d9528d.png)

### Use which to locate the pwd command on your Kali virtual machine 

![image](https://user-images.githubusercontent.com/79100627/174873885-ee4612ff-a104-41d9-9d85-8a8a68d13e65.png)

### Use locate to locate wce32.exe on your Kali virtual machine

Locate command is the quickest way to find the locations of files and directories in Kali. Locate searches a built-in database named locate.db rather than the entire hard disk itself. 

locate searches a built-in database named locate.db rather than the entire hard disk itself. This database is automatically updated on a regular basis by the cron scheduler. To manually update the locate.db database, you can use the updatedb command.

```
sudo updatedb

locate sbd.exe
```

![image](https://user-images.githubusercontent.com/79100627/174874442-832d9954-4aac-47b4-88aa-cf9c4d9bb0fb.png)


### Use the find to identify any file (not directory) modified in the last day, Not owned by the root user and execute ls -l on them.

use the command:

```
find [dir-name] -type -f -mtime -1 
```

Change the ```mtime -1``` to ```mtime -2``` to search last 48 hours, or change it to ```mmin -120``` to search the last 2 hours.

Searches the ```dir-to-search``` (or current dir if not provided) recursively for entries of type f (file) which were modified less than (1*24) hours ago.




