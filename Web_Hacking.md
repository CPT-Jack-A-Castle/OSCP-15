# Web Hacking

Browser Tools 

- **View Source** - Use your browser to view the human-readable source code of a website.
- **Inspector** - Learn how to inspect page elements and make changes to view usually blocked content 
- **Debugger** - Inspect and control the flow of a page's JavaScript 
- **Network** - See all the network requests a page makes 

### Developer Tools (Insepctor)

![image](https://user-images.githubusercontent.com/79100627/165856751-68abf0ed-54ad-4a56-8680-e1c3a3fc73e1.png)

DIV element with the class premium-customer-blocker - you can see the display as **block** </br>
However, you can write the the value of your own choice. Try type **none** </br> 
It will show the original text 

![image](https://user-images.githubusercontent.com/79100627/165856908-68c60f78-6c13-4fa3-9c55-375ee2179e29.png)

### Developer Tools (Debugger) 

Debugger is intended to debugging javascript </br>
As a penetration testers, it gives us the option of digging deep into the JavaScript code 

JavaScript files formats are removed due to the file utilization 

![image](https://user-images.githubusercontent.com/79100627/165858912-87721477-9bc8-4f32-86ea-65f1640c5604.png)

By clicking this, it will format the JS file

![image](https://user-images.githubusercontent.com/79100627/165858974-b94c978b-b0fd-4951-8846-eadf0b75092a.png)

Set the pointer and refresh for the debugging

### Developer Tools (Network)

The network tab on the developer tools can be used to keep track of every external request a webpage makes. If you click on the Network tab and then refresh the page, you will see all the files the page is requesting 

![image](https://user-images.githubusercontent.com/79100627/165859452-04062387-a6f8-4c7d-a7b6-f556bbf507e3.png)

There is a event happening for contact-msg which is the form being submitted in the background using a method called AJAX. AJAX is a method of sending and receiving network data in a web application background without interfering by changing the current web page. 


### What is Content Discovery 

Content can be many things, a file, video, picture, backup, a website feature. When we talk about content discovery, we're not talking about the obvious things we can see on a website; it's the thing that aren't immeidately presented to us and that weren't always intended for public access. 

There are three ways of discovering content on a website called **Manually, Automated and OSINT (Open Source Intelligence)**

![image](https://user-images.githubusercontent.com/79100627/165861123-6eb3c5ce-21e3-4132-b1cc-86edf1c9db13.png)

The file contains search engines which pages they are and aren't allowed to show their search engine result or ban specific search engines from crawling the website. 

### Manual Discovery (Favicon)

The favicon is a small icon displayed in the browswer's address bar or tab used for branding a website 

![image](https://user-images.githubusercontent.com/79100627/165861294-fe7a77e9-e0e3-45ff-8316-59f205cbded0.png)

Sometimes when frameworks are used to build a website, a favicon that is part of the installation gets leftover, and if the website developer does not replace with a custom one, this can give us a clue on what framework is in use. OWASP host a database of common framework icons 

To find the vulnerability of a website 

![image](https://user-images.githubusercontent.com/79100627/165861574-91734266-1b65-4fe1-960a-969e34afb3b4.png)

Here is the icon and if you download favicon and get md5 hash by using curl command and compare with the https://wiki.owasp.org/index.php/OWASP_favicon_database

![image](https://user-images.githubusercontent.com/79100627/165861793-c9fb8b96-1508-4589-9bcd-3ab64f059967.png)


### Maunal Discovery (Sitemap.xml) 

unlike the txt file above, which restricts what search engine crawlers can look at, the sitemap.xml file gives a list of every file the website owner wishes to be listed on a search engine. These can contain areas of the website that are bit mroe difficult to navigate to or even list some old webpages that the current site no loger uses but are still working behind the scenes. 

### Manual Discovery (Headers) 

When we make a requests to the web server, the server returns various HTTP headers. These headers can sometimes contain useful information such as the webserver software and possibly the programming/scripting language in use. 

By using the curl command we can see the version of the website and using this information, we could find vulnerable versions of software being used. Try running the below crul command (-v)

![image](https://user-images.githubusercontent.com/79100627/165862848-f8775fb8-19ec-4813-a3f6-65bc2a7e8b82.png)

### Manual Discovery (Framework Stack) 

Once you've established the framework of website, either from the above favicon example or by looking for clues in the page source such as comments, copyright notices or credits, you can then locate the framework website. 






