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
