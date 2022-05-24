
# Burp Suite

## What is Burp Suite 

Burp Suite is a framework wirtten in Java that aims to provide a one-stop-shop for web application penetration testing. In many ways, this goal is achieved as Burp is very much the industry standard tool for hands-on web app security assessments. Burp Suite is also very commonly used when assesing mobile application, as the same features which make it so attractive for web app testing translate almost perfectly into testing the APIs (Application Programming Interfaces) powering most mobile apps.

At the simplest level, Burp can capture and manipulate all of the traffic between an attacker and webserver: this is the core of the framework. After capturing requests, we can choose to send them to various other parts of Burp Suite framework

## Features of Burp Community 

Whilst Burp Community has a relatively limited feature-set compared to the Professional edition, it still has many superb tools available. 

- **Proxy**: The most well known aspect of the Burp Suite, the Burp Proxy allows us to intercept and modify request/responses when interacting with web application. 
- **Repeater**: The second most well known Burp feature: **Repeater** allows us to capture, modify, then resend the same request numerous times. This feature can be absolutely invaluable, especially when we need to craft a payload through trial and error (e.g. in an SQLi - Structured Query Language Injection) or when testing the functionality of an endpoint for falws. 
- **Intruder**: Although harshly rate-limited in Burp Community, Intruder allows us to spray an endpoint with requests. This is often used for bruteforce attacks or to fuzz endpoints 
- **Decoder**: Though less-used than the previously mentioned features, Decoder still provides a valuable service when transforming data -- either in terms of decoding captured information, or encoding a payload prior to sending it to the target. Whilst there are other services available to do the same job, doing this direectly within Burp Suite can be very efficient.
- **Comparer**: As the name suggests, Comparer allows us to compare two pieces of data at either word or byte level. Again, this is not something that is unique to Burp Suite, but being able to send (potentially very large) pieces of data directly into a comparison tool with a single keyboard shortcut can speed things up considerably. 
- **Sequencer**: We usually use Sequencer when assessing the randomness of tokens such as session cookie values or other supposedly random generated data. If the algorithm is not generating secure random values, then this could open up some devastating avenues for attack. 

## Burp Suite Getting Started 

![image](https://user-images.githubusercontent.com/79100627/169669779-0caf68dd-88b3-432d-8935-7cd42e77ecfc.png)

![image](https://user-images.githubusercontent.com/79100627/169669806-f4df4734-2d8b-4025-9587-da8bc5fb8217.png)

![image](https://user-images.githubusercontent.com/79100627/169669824-866b05ba-159a-4383-82d1-908842cf4630.png)

1. The Tasks menu allows us to define background tasks that Burp Suite will run whilst we use the application. The Pro version allow us to create on-demand scans. The default "Live Passive Crawl" (which automatically logs the pages we visit) will be more than suitable for our uses 
2. The Event log tells us what Burp Suite is doing (e.g. Starting the Proxy), as well as information about any connections that we are making through Burp.
3. The Issue Activity section is exclusive to Burp Pro. It won't give us anything using Burp community 
4. The Advisory section gives more information about the vulnerabiliities found, as well as references and suggested remediations. These could then be exported into a report 

## Navigation

Navigating around the Burp Suite GUI by default is done entirely using the top menu bars:

![image](https://user-images.githubusercontent.com/79100627/169669915-234a8233-7475-4303-ad5b-57c712235e73.png)

These allow you to switch between modules (along the top row of the attached image). If the selected module has more than one sub-tab, then these can be selected using a second menu bar which appears directly below the original bar (the bottom row of the image above). It is common for module-specific settings to be provided in these sub-tabs (as is the case with the Proxy Options above). 

Tabs can also be popped out into separate windows should you prefer to view multiple tabs separately. This can be done by clicking "Window" in the application menu at the top of the screen, then choosing "Detach" tabs

![image](https://user-images.githubusercontent.com/79100627/169670132-0a2d8356-a432-464b-b9de-090d1db03fc9.png)

### Shortcuts 

![image](https://user-images.githubusercontent.com/79100627/169670151-2dc28dd6-607f-4665-8bc8-d3dc3b7f8c63.png)

## Options 

- Global settings can be found in the User options tab along the top menu bar. 
- Project - Specific settings can be found in the Project options tab

The options provided in the User options tab will apply every time we open Burp Suite. In contrast, the Project options will only apply to the current project. Given that we can't save projects in Burp Community, this means that our project options will reset every time we close Burp 

![image](https://user-images.githubusercontent.com/79100627/169670202-33b0891a-078a-41c3-9832-1ac767e66157.png)

The settings here apply globally (i.e. they control the Burp Suite application -- not just the project). That said, many of them can be overwritten in the project settings. 

There are four main sub-sections of the User options tab: 

- The options in the Connections sub-tab allow us to control how Burp makes connections to targets. For example, we can set a proxy for Burp Suite to connect through; this is very useful if we want to use Burp Suite through a network pivot.
- The TLS sub-tab allows us to enable and disable various TLS (Transport Layer Security) options, as well as giving us a place to upload client certificates should a web app require us to use one for connections.
- An essential set of options: Display allows us to change how Burp Suite looks. The options here include things like changing the font and scale, as well as setting the theme for the framework (e.g. dark mode) and configuaring various options to do with the rendering engine in Repeater.
- The Misc sub-tab contains a wide variety of settings, including the keybinding table (HotKeys), which allowing us to view and alter the keyboard shortcuts used by Burp Suite. 

There are five sub-tabs:

- Connections holds many of the same options as the equivalent section of the User options tab: these can be used to override the application-wide settings. For example, it is possible to set a proxy for just the project, overriding any proxy settings that you set in the User options tab. There are few differences between this sub-tab and that of the User options, however. For example "Hostname Resolution" option (allowing you to map domains to IPs directly with Burp Suite) can be very handy -- as can the "Out-of-Scope Requests" settings, which enable us to determine whether Burp will send requests to anything you aren't explicitly targeting (more on this later!). 
- The HTTP sub-tab defines how Burp handles various aspects of the HTTP protocol: for example, whether it follows redirects or how to handle unusal reponse codes.
- TLS allows us to override application-wide TLS options, as well as showing us a list of public server certificates for sites that we have visited.
- The Sessions tab provides us with options for handling sessions. It allows us to define how Burp obtains, saves, and uses session cookies that it receives from target sites. it also allows us to define macros which we can use to automate things such as logging into web applications (giving us an instant authenticated session, assuming we have valid credentials).
- There are fewer options in the Misc sub-tab than in equivalent tab for the "user options" section.

## Intoduction to the Burp Proxy 

The Burp Proxy is the most fundamental of tools available in Burp Suite. It allows us to capture requests and responses between ourselves and our target. These can be manipulated or sent to other tools for further processing before being allowed to continue to their destination 

For example, if we make a request to ```https://tryhackme.com``` through the Burp Proxy, our request will be captured and won't be allowed to continue to the TryHackMe servers until we explicitly allow it through. We can choose to do same with the reponse from the server, although this isn't active by default. This ability to intercept requests ultimately means that we can take complete control over our web traffic --an invaluable ability when it comes to testing web applications

There are few configurations we need to make before we can use the proxy, but let's start by looking at the interface.

When we first open Proxy tab, Burp gives us bunch of useful information and background reading. This information is well worth reading through; however, the real magic happens after we capture a request: 


![image](https://user-images.githubusercontent.com/79100627/169670957-cc76943d-bf9b-47c9-a59a-9a5880e1dc50.png)

With the proxy active, a request was made to the TryHackMe website. At this point, the browser making the request will hang, and the request will appear in the proxy tab giving us the view shown in the screenshot above. We can then choose to forward or drop the request (potentially after editing it). We can also do various other things here, such as sedning the request to one of the other Burp Modules, copying it as a cURL command, saving it to a file, and many others. 

Burp Suite will still (by default) be logging requests made through the proxy when the intercept is off. This can be very useful for going back and analysing prior requestsm even if we didn't specifically capture them when they were made.

Burp will also capture and log WebSocket communication, which, again, can be exceedingly helpful when analysing a web app. 

The logs can be viewed by going to the "HTTP history" and "WebSockets history: sub-tabs: 

![image](https://user-images.githubusercontent.com/79100627/169671128-35304484-583c-4685-b6be-50ae6fb01ecb.png)

It is worth nothing that any requests captured here can be sent to other tools in the framework by right-lciking them and choosing "Send to...". For exmaple, we could take a previous HTTP request that has already been proxied to the target and send it to Repeater. 

These options give us a lot of control over how the proxy operates, so it is an excellent idea to familiarise yourself with these. 

For example, the proxy will not intercept server responses by deafult unless we explicitly ask it to on a per-request basis. We can override the default setting by selecting the "Intercept responses based on the following rules" checkbox and picking one or more rules. The "OR Requst Was Intercepted" rule is good for catching responses to all requests that were intercepted by the proxy:

![image](https://user-images.githubusercontent.com/79100627/169671227-106b2168-7097-4cf5-8269-5bca8d8f9811.png)

The "And URL Is in Target Scope" is another very good default rule; we will look at scoping later in this room. 

You can make your own rules for most of Proxy options, so this is one section where looking around and experimenting will serve you very well indeed 

## Connecting through the Proxy 

There are two ways to proxy our traffic through Burp Suite.

1. We could use the embedded browser 
2. We can configure our local web browser to proxy our traffic through Burp; This is more common and so will be focus of this task

The Burp Profxy works by opening a web interface on ```127.0.0.1:8080``` (by default). As implied by the fact that this is a "proxy", we need to redirect all of our borwswer traffic through this port before we can start intercepting it with Burp. We can do this by altering our browswer settings or, more commonly, by using a Firefox browser extension called FoxyProxy. FoxyProxy allows us to save proxy profiles, meaning we can quickly and easily switch to our "Burp Suite" profile in a matter of clicks, then disable the proxy just as easily. 

There are two versions of FoxyProxy: Basic and Standard. Both versions allow you to change your proxy settings on the fly; however, FoxyProxy Standard gives you a lot more control over what traffic gets sent through the proxy. For example, it will allow you to set pattern matching rules to determine whether a request should be proxied or not: this is more complicated than the simple proxy offered by FoxyProxy basic.

The basic edition is more than adequate for our usage. It is pre-installed and configured in the Firefox browser of the AttackBox, so if you are using the AttackBox, please feel free to skip ahead to the last section of this task. 

## Proxying HTTPS

Great, so we can intercept HTTP traffic -- what is next?

Unfortunately, there is a problem. What happens if we navigate to a site with TLS enabled? For example, https://google.com/

![image](https://user-images.githubusercontent.com/79100627/169672746-f9aaf872-b92e-4209-ad12-ac8e8c2a409e.png)

we get an error. Specifically, Firefox is telling us that the Portswigger Certificate Authority (CA) isn't authorised to secure the connection/

Fortunately, Burp offers us an easy way around this. We need to get Firefox to trust connections secure by Portswigger certs, so we will manually add the CA certificate to our list of trusted certificate authorities. 

First, with proxy activated head to ```http://burp/cert```; this will download a file called ```cacert.der``` -- save it somewhere 

Next, type ```about:preferences``` into your firefox search bar and press enter; this takes us to the FireFox setting page. Search the page for "certificates" and we find the option to "View Certificates"

![image](https://user-images.githubusercontent.com/79100627/169672878-0524d196-15e9-4035-a259-8c90847a7c02.png)

## The Burp Suite Browser

In addition to giving us the option to modify our regular web browser to work with the proxy, Burp Suite also includes a built in Chromium browser that is pre-configured to use the proxy without any of the modification we just had to do.

Whilst this may seem ideal, it is not as commonly used as the process detailed in the previous few tasks. People tend to stick with their own borwser as it gives them a lot more customisability; however, both are perfectly valid choices. 

## Scoping and Targeting

It can get extremely tedious having Burp capturing all of our traffic. When it logs everything (including traffic to sites we aren't targeting), it muddies up logs we may later wish to send to clinets. In short, allowing Burp to capture everything can quickly become a massive pain. 

What's the solution? Scoping

Setting a scope for the project allows us to define what gets proxied and logged. We can restrict Burp Suite to only target the web application(s) that we want to test. The easiest way to do this is by switching over to the "Target" tab, right-clicking our target from our list on the left then choosing "Add To Scope". Burp will then ask us whether we want to stop logging anything which isn't in scope 

![image](https://user-images.githubusercontent.com/79100627/169673302-e778ccf7-740d-481c-929c-ddda24df98f2.png)

We can now check our scope by switching to the "Scope" sub-tab

The scope sub-tab allows us to control what we are targeting by either Including or Excluding domains / IPs. This is very powerful section, so it's well worth taking the time to get accustomed to using it.

We just chose to disable logging for out of scope traffic, but proxy will still be intercepting everything. To turn this off, we need to go into Proxy options sub-tab and select "And URL Is in target scope" from the Intercept Client Requests Section: 

## Site Map and Issue Definitions

Control of the scope may be most useful aspect of the Target tab, but it's by no means the only use for this section of Burp.

There are three sub tabs under target:

- Site map: allows us to map out the apps we are targeting in a tree structure. Every page that we visit will show up here, allowing us to automatically generate a site map for the target simply by browsing around the web app. Burp Pro would also allow us to spider the targets automatically (i.e. look through every page for links and use them to map out as much of the site as-is publicly accessible using the links between pages); however, with Burp community, we can still use this to accumulate data whilst we perform our initial enumeration steps. The Site map can be especially useful if we want to map out an API, as whenever we vist a page, any API endpoints that the page retrieves data from whilst loading will show up here. 
- Scope: We have already seen the Scope sub-tab -- it allows us to control Burp's target scope for the project.
- Issue Definitions: Whilst we don't have access to the Burp Suite vulnerability scanner in Burp Community, we do still have access to a list of all the vulnerabilities it looks for. The Issue Definitions section gives us a huge list of web vulnerabilities (complete with description and references) which we can draw from should we need ciations for a report help describing a vulnerability  

## Example Attack 

![image](https://user-images.githubusercontent.com/79100627/169673739-21175bf0-0e00-41cd-976a-df5f50d4de71.png)

In real world web app pentest, we would test this for a variety of things: one of which would be Cross-Site Scripting (or XSS). If you have not yet encountered XSS, it can be though of as injecting a client-side script (usually in Javascript) into a webpage in such as way that it executes. There are various kinds of XSS -- the type that we are using here is referred to as "Reflected" XSS as it only affects the person making the web request. 

![image](https://user-images.githubusercontent.com/79100627/169673814-c2838994-6e81-4163-a0b6-b360d58e04ab.png)

![image](https://user-images.githubusercontent.com/79100627/169673829-e27001e9-073c-491d-b65d-21b2bd8cc911.png)

With the request captured in the proxy, we can now change the email field to be our very simple payload from above: ```<script>alter("Succ3ssful XSS")</script>```. After pasting payload, we need to select it, then URL encode it with the ```Ctrl+U``` Shortcut to make it safe to send.

![image](https://user-images.githubusercontent.com/79100627/169673875-c97bd0a8-29e9-4f60-b59c-23fa173ce0a6.png)

![image](https://user-images.githubusercontent.com/79100627/169673896-50aad28f-e66b-41c9-b4a1-1bc7f6d1693a.png)

## Burp Suite Repeater 

Burp Suite Reapeater allows us to craft and/or relay intercepted requests to a target at will. In layman's terms, it means we can take a request captured in the Proxy, edit it, and send the same requeset repeatedly as many times as we wish. Alternatively, we could craft requests by hand, much as we would from the CLI (Command Line Interface), using tool such as cURL to build and send requests.

The ability to edit and resent the same request multiple times makes Repeater ideal for any kind of manual poking around at an endpoint, providing us with a nice Graphical User Interface (GUI) for writing the request payload and numerous views (including a rendering engine for a graphical view) of the response so that we can see the results of our handiwork in action.

The Repeater interface can be split into six main sections --an annotated diagram can be found below the following bullet points:

1. At the very top left of the tab, we have a list of Repeater requests. We can have many different requests going through Repeater: each time we send a new request to Repeater, it will appear up here.
2. Directly underneath the request list, we have the controls for the current request. These allow us to send a request, cancel a hanging request, and go forwards/backwards in the request history.
3. Still on the left-hand side of the tab, but taking up most of the window, we have the request and response view. We edit the request in the Request view then press send. The response will show up in the Response view. 
4. Above the request/response section, on the right-hand side, is a set of options allowing us to change the layout for the request and response views. By default, this is usualy side-by-side (horizontal layout, as in the screenshot); however, we can also choose to put them above/below each other (vertical layout) or in separate tabs (combined view).
5. At the right-hand side of the window, we have the inspector, which allows us to break requests apart to analyse and edit them in a slightly more intuitive way than with the raw editor. We will cover this in a later task.
6. Finally, above the Inspector we have our target. Quite simply, this is the IP address or domain to which we are sending requests. When we send requests to Repeater from other parts of Burp Suite, this will be filled in automatically. 

![image](https://user-images.githubusercontent.com/79100627/169707384-fe6b028a-a88c-42e9-966a-c170b96e2464.png)

## Basic usage of Repeater 

Whilst we can craft requests by hand, it would be much more common to simply capture a request in the Proxy, then send that through to Repeater for editing/resending 

With a request captured in the proxy, we can send to repeater either by right-clicking on the request and choosing "Send to Repeater" or by pressing ```Ctrl + R```.

Switching back to the Repeater, we can see that our request is now available:

![image](https://user-images.githubusercontent.com/79100627/169707510-efd2f06a-b89d-4a9d-b028-a40a9a0a3016.png)

The target and Inspector elements are now also showing information; however, we do not yet have a response. When we click "Send", the Response section quickly populates 

![image](https://user-images.githubusercontent.com/79100627/169707572-70b96e8f-ea55-4045-9de0-33994910c45e.png)

If we want to change anything about the request, we can simply type in the Request window and press "Send" again; this will update the Response on the right. For example, changing the "Connection header to ```open``` rather than ```close``` results in a response "Connection" header with a value of ```keep-alive```:

![image](https://user-images.githubusercontent.com/79100627/169707726-d6214759-daa1-4220-aded-01194e950745.png)

## Repeater Views 

Repeater offers us various ways to present the responses to our requests -- these range from hex output all the way up a fully rendered version of the page. We can see the available options by looking above the response box: 

![image](https://user-images.githubusercontent.com/79100627/169707788-91e30551-b54f-411e-bb21-ecd23247aaf6.png)

We have four display options here:

1. Pretty: This is the default option. It takes the raw response and attempts to beautify it slightly, making it easier to read.
2. Raw: The pure, un-beautified response from the server
3. Hex: This view takes the raw response and gives us a byte view of it -- especially useful if the reponse is a binary file 
4. Render: The render view renders the page as it would appear in your browser. Whilst not hugely useful given that we would usually be interested in the source code when using Repeater, this is still a neat trick 

## Repeater Inspector 

In many ways, Inspector is entirely supplementary to the request and response fields of the Repeater window. If you understand how to read and edit HTTP requesets, then you may find that you rarely use Inspector at all.

That said, it is a superb way to get prettified breakdown of the requests and responses, as well as for experimenting to see how changes made using the higher-level Inspector affect the equivalent raw versions.

Inspector can be used in Proxy as well as Repeater. In both cases, it appears over at the very right hand side of the window and gives us a list of the components in the request and response: 

![image](https://user-images.githubusercontent.com/79100627/169708474-464b9413-f687-46c9-8c2e-7b1594d22c2b.png)

Of these, the request sections can nearly always be altered, allowing us to add, edit and delete items. For example, in the Request Attributes section, we can edit the parts of the request that deal with location, method and protocol; e.g. changing the resource we are looking to retrieve, altering the request from GET to another HTTP method, or switching protocol from HTTP/1 to HTTP/2:

![image](https://user-images.githubusercontent.com/79100627/169708525-b2a4f553-ec1e-4155-8eb7-66f7ed36f9d0.png)

The other sections available for viewing and/or editing are:

- Query parameters, which refers to dat abeing sent to the server in the URL. For example, in a GET request to ```https://admin.tryhackme.com/?redirect=false```, there is a query parameter called "redirect" with a value of "false" 
- Body Parameters, which do the same thing as Query Parameters, but for POST requests. Anything that we send as data in a POST request will show up in this section, once again allowing us to modify the parameters before re-sending.
- Request Cookies contain, as you may expect, a modifiable list of the cookies which are being sent with each requeset. 
- Request Headers allow us to view, access, and modify (including outright adding or removing) any of the headers being sent with our requests. Editing these can be very useful when attempting to see how a webserver will respond to unexpected headers.
- Request Headers show us the header that the server sent back in response to our requeset. These cannot be edited (as we can't control what headers the server returns to us!). Note that this section will only show up after we have sent the request and received a response. 

These components can all be found as text within the request and response sections; however, it can be nice to see them in the tabular format offered by Inspector. It is well worth adding, removing and editing headers in Inspector to get a feel for how the raw version changes as you do so. 


## Example 

Repeater is best suited for the kind of task where we need to send the same request numerous times, usually with small changes in between requests. For example, we may wish to manually test for SQL Injection vulnerability, attempt to bypass a web application firewall filter or simply add or change parameters in a form submission

![image](https://user-images.githubusercontent.com/79100627/169708930-c6d8d643-444d-4606-95b7-fb8194ad3ad5.png)

## SQLi with Repeater 

This task contains an extra mile challenge, which means that it is a slightly harder, real-world aplication for Burp Repeater. 

The breif will follows:

- There is a Union SQL Injection vulnerability in the ID parameter of the ```/about/ID``` endpoint. Find this vulnerability and execute an attack to retrieve the notes about the CEO stored in the database

Let's start by capturing request to /about/2 in the Burp Proxy

![image](https://user-images.githubusercontent.com/79100627/169709783-c17d9fe8-18b4-4ca7-bb15-e685b2315238.png)

![image](https://user-images.githubusercontent.com/79100627/169709821-e84fa3b8-158f-4142-879b-329b082c1d9f.png)

Now that we have requested primed, let's confirm that a vulnerability exist. Adding a single apostrophe ```'``` is usually enough to cause the server to error when a simple SQLi is present, so, either using Insepctor or by editing the request path manually, add apostrophe after the "2" at the end of the path and send the request 

![image](https://user-images.githubusercontent.com/79100627/169709881-697d6c00-9c4a-4eb4-8a2b-44aad712d5c5.png)

![image](https://user-images.githubusercontent.com/79100627/169709941-138f5842-bb7d-46a1-89ec-09b453141e1c.png)

You should see that the server responds with a "500 Internal Server Error" indicating that we successfully broke the query 

If we look through the body of the server response, we see something very intresting at around line 40 that the server is telling us the query we tried to execute.

![image](https://user-images.githubusercontent.com/79100627/169710066-95f6faca-946e-4ab0-8382-4ca73efb11f6.png)

This is an extremely useful error message which the server should absolutely not be sending us, but fact that we have it makes our job significantly more straightfoward. 

The message tell us couple things that will be invaluable when exploiting this vulnerability:
- The database table we are selecting from is called people. 
- The query is selecting five columns from the table: ```firstName```, ```lastName```, ```pfpLink```, ```role```, and ```bio```. We can guess where these fit into the page, which will be helpful for when we choose where to place our responses

Although we have managed to cut out a lot of the enumeration required here, we still need to find the name of our target column.

As we know the table name and the number of rows, we can use union query to select the column names for the people table from the columns tables in the ```information_schema``` default database. 

A simple query for this is as follows:

```/about/0 UNION ALL SELECT column_name,null,null,null,null FROM information_schema.columns WHERE table_name="people"```

This creates a union query and selects our target then four null columns (to avoid the query error out). Notice that we also changed the ID that we are selecting from 2 to 0. By setting the ID to an invalid number, we ensure that we don't retrieve anything with the original (legitimate) query; this means that the first row returned from the database will be our desired response from the injected query. 

Looking thorugh the returned response, we can see that the first column name ```id``` has been inserted into the page title:

![image](https://user-images.githubusercontent.com/79100627/169710337-f5f18c49-d886-476a-8c78-14f62f81ef18.png)

We have successfully pulled the first column name out of the database, but we now have a problem. The page is only displaying the first matching item -- we need to see all of the matching items 

Fortunately, we can use our SQLi to group the results. We can still only retrieve one result at a time, but by using ```group_concat()``` function, we can amalgamate all of the column names into a single output: 

```/about/0 UNION ALL SELECT group_concat(column_name),null,null,null,null FROM information_schema.columns WHERE table_name="people"```

![image](https://user-images.githubusercontent.com/79100627/169710479-e1e0d036-0b13-40ca-a425-a41882f93027.png)

We have successfully identified eight columns in this table: ```id```,```firstName```,```lastName```,```pfpLink```,```role```,```shortRole```,```bio```, and ```notes```. 

Considering our task, it seems a safe bet that our target column is ```notes```.

Finally, we are ready to take the flag from this database -- we have all of the information that we need:

- The name of the table: people.
- The name of the target column: notes.
- The ID of CEO is 1; this can be found simply by clicking on Jameson Wolfe's profile on the ```/about/``` page and checking the ID in URL 

Query should be 
```0 UNION All SELECT notes,null,null,null,null FROM people WHERE id=1```

![image](https://user-images.githubusercontent.com/79100627/169710622-aeef12b2-b3a2-4fd1-9d19-aef821e0c0fe.png)

## Burp Suite Intruder 

Intruder allows us to automate requests, which is very useful when fuzzing or bruteforcing. 

## What is Intruder?

Intruder is Burp Suite's in-built fuzzing tool. It allows us to take a request (usually captured in the Proxy before being passed into Intruder) and use it as template to send many more requests with slightly altered values automatically. For example, by capturing a request containing a login attempt, we could then configure Intruder to swap out the username and password fields for values from a wordlist, effectively allowing us to brutefoce the login form. Similarly, we could pass in a fuzzing wordlist and use Intruder to fuzz for subdirectories, endpoints, or virtual hosts. This functionality is very similar to that provided by command-line tools such as Wfuzz or Ffuf.

In short, as a method for automating reuqests,Intruder is extremly powerful -- there is just one problem: to access the full speed of Intruder, we need Burp Professional. We can still use Intruder with Burp Community, but it is heavily rate-limited. The speed restriction means that many hackers choose to use other tools for fuzzing and bruteforcing.

![image](https://user-images.githubusercontent.com/79100627/169912164-3787e277-233f-4887-9359-282ebf6c7507.png)

The first view we get is a relatively sparse interface that allows us to choose our target. Assuming that we sent a request in from Proxy (by using ```Ctrl + I``` or right-clicking and selecting "Send to Intruder"), this should already be populated for us. 

There are four other Intruder sub-tabs:
- Positions allows us to select Attack Type, as well as configure where in the request template we wish to insert our payloads.
- Payloads allows us to select values to insert into each of the positions we defined in the previous sub-tab. For example, we may choose to load items in from wordlist to serve as payloads. How these get inserted into the template depends on the attack type we chose in the Position tab. There are many payload types to choose from (anything from a simple wordlist to regexes based on responses from the server). The Payloads sub-tab also allows us to alter Intruder's behaviour with regards to payloads; for example, we can define pre-processing rules to apply to each payload (e.g. add a prefix or suffix, match and replace, or skip if the payload matches a defined regex) 
- Resource Pool is not particularly useful to us in Burp Community. It allows us to divide our resources between tasks. Burp Pro would allow us to run various types of automated tasks in the background, which is where we may wish to manually allocate our available memory and processing power between these automated tasks and Intruder. Without access to these automated tasks, there is little point in using this, so we wont devote much time to it.
- As with most of other Burp tools, Intruder allows us to configure attack behaviour in Options sub-tab. The settings here apply primarily to how Burp handles results and how Burp handles the attack itself. For example, we can choose to flag requests that contain specified pieces of text or define how Burp responds to redirect (3xx) reponses. 

Fuzzing is when we take a set of data and apply it to a parameter to test functionality or to see if something exists. For example, we may choose to "fuzz for endpoints" in a web application; this would involve taking each word in a wordlist and adding it to the end of a request to see how the webserver is responds 
```http://10.10.245.17/WORD_GOES_HERE```

## Intruder Positions 

When we are looking to perform an attack with Intruder, the first thing we need to do is look at positions. Positions tell Intruder where to insert payloads 

![image](https://user-images.githubusercontent.com/79100627/169913488-82218b42-5b62-4122-bf65-0efce0cc6bac.png)

Notice that Burp will attempt to determine the most likely places we may wish to insert a payload automatically --these are highlighted in greed and surronded by silcrows.

On the right-hand side of the interface, we have the buttons labelled "Add", "Clear", and "Auto"
- Add let us define new positions by highlighting them in the editor and clicking the button.
- Clear removes all defined positions, leaving us with a blank canvas to define our own.
- Auto attempts to select most likely positions automatically; this is useful if we cleared the default positions and want them back. 

## Attack Types 
- Sniper 
- Battering ram
- Pitchfork
- Cluster bomb

## Sniper 

Sniper is the first and most common attack type.

When conducting a sniper attack, we provide one set of payloads. For example, this could be a single file containing a wordlist or a range of numbers. From here on out, we will refer to a list of items to be slotted into requests using the Burp Suite terminology of a "Payload Set". Intruder will take each payload in a payload set and put it into each defined position in turn 

![image](https://user-images.githubusercontent.com/79100627/169913953-968d22a0-74aa-4765-8092-25957060f411.png)

There are two positions defined here, targeting the ```username``` and ```password``` body parameters. 

In a sniper attack, Intruder will take each position and subsitute each payload into it in turn.

For example, let's assume we have a wordlist with three words in it: ```burp```, ```suite```, and ```intruder```. 

With the two positions that we have above, Intruder would use these words to make Six requests 

![image](https://user-images.githubusercontent.com/79100627/169914148-13004b73-6732-4cf8-9c06-17c317d186d8.png)

Notice how Intruder starts with the first position (```username```) and tries each our payloads, then moves to the second position and tries the same payloads again. We can calculate the number of requests that Intruder Sniper will make as ```requests = numberOfwords * numberOfPositions```.

This quality makes sniper very good for single-position attacks (e.g. password bruteforce if we know the username or fuzzing for API endpoints).

## Battering Ram

Like Sniper, Battering ram takes one set of payloads (e.g. wordlist). Unlike Sniper, the Battering ram puts the same payload in every position rather than in each position in turn. 

![image](https://user-images.githubusercontent.com/79100627/170092149-225ec2d2-4ac7-40e7-87af-54c1248aa677.png)

If we use Battering ram to attack this, Intruder will take each payload and subsitute it into every position at once. 

With the two positions that we have above, Intruder would use the three words from before (```burp```, ```suite```, and ```intruder```) to make three requests:

![image](https://user-images.githubusercontent.com/79100627/170092368-0d7beb7a-58ca-4b98-a5e7-ee9955cd0cae.png)

As can be seen in hte table, each item in our list of payloads gets put into every position for each requests. True to the name, Battering ram just throws payloads at the target to see what sticks.

