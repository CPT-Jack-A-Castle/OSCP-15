
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





