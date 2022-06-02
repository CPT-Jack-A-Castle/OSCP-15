# Network Security

## Passive vs Active Reconnaissance 

Before the dawn of computer systems and networks, in the Art of War, Sun Tzu taught, "If you know the enemy and know yourself, your victory will not stand in doubt." If you are playing the role of an attacker, you need to gather information about your target systems. If you are playing the role of a defender, you need to know what your adversary will discover about your systems and networks.

Reconnaissance (recon) can be defined as a preliminary survey to gather information about a target. It is the first step in The Unified Kill Chain to gain an initial foothold on a system. We divide reconnaissance into:

1. Passive Reconnaissance 
2. Active Reconnaissance 

In passive reconnaissance, you rely on publicly available knowledge. It is the knowledge that you can access from publicly available resources without directly engaging with the target. Think of it like you are looking at target territory from afar without stepping foot on that territory. 

Passive reconnaissance activities include many activities, for instance: 

- Lokking up DNS records of a domain from a public DNS server.
- Checking job ads related to the target website.
- Reading news articles about the target compnay 

Active reconnaissance, on the other hand, cannot be achieved so discreetly. It requires direct engagement with the target. Think of it like you check the locks on the doors and windows, among other potential entry points.

Examples of active reconnaissance activities include: 

- Connecting to one of the company server such as HTTP, FTP, SMTP
- Calling the company in an attempt to get information (social engineering)
- Entering company premises pretending to be a repairman 

## Whois 

WHOIS is a request and respose protocol that follows the RFC 3912 specification. A WHOIS server listens on TCP port 43 for incoming requests. The domain registrar is responsible for maintaining the WHOIS records for the domain names it is leasing. The WHOIS server replies with various information related to the domain requested. Of particular interest, we can learn:

- Registrar: Via which registrar was the domain name registered?
- Contact info of registrant: Name, Organization, address, phone, among other things. (Unless made hidden via privacy service) 
- Creation, update and expirartion dates: When was the domain name first registered? When was it last updated? And when does it need to be renewed?
- Name Server: Which server to ask to resolve the domain name?

To get this information, we need to use a ```whois``` client or an online service. Many online services provide ```whois``` information; however, it is generally faster and more convenient to use your local whois client. 

![image](https://user-images.githubusercontent.com/79100627/170852179-904b22b8-d619-4133-bc48-d14cede065ff.png)

We can see plenty of information; we will inspect them in the order displayed. First, we notice that we were redirected to ```whois.namecheap.com``` to get our information. In this case and at the time being, ```namecheap.com``` is maintaining the WHOIS record for this domain name. Furthermore, we can see the creation date along with the last update date and expiration date.

Next, we obtain information about registrar and registrant. We can find the registrant's name and contact information unless they are using some privacy service. Although not displayed above, we get the admin and tech contracts for this domain. Finally, we see the domain name servers that we should query if we have any DNS records to look up.

The information collected can be insepcted to find new attack surfaces, such as social engineering or technical attacks. For instance, depending on the scope of the penetration test, you might consider an attack against the email server of the admin user or the DNS servers, assuming they are owned by your client and fall within the scope of penetration test.

It is important to note that due to automated tools abusing WHOIS queries to harvest email addresses, many WHOIS services take measures against this. They might redact email addresses, for instance. Moreover, many registrants subscribe to privacy services to avoid their email addresses being harvested by spammers and keep their information private.

## NSLOOKUP and Dig 

In the previous task, we used WHOIS protocol to get various information about the domain name we were looking up. In particular, we were able to get the DNS servers from the registrar. 

Find the IP address of a domain name using ```nslookup```, which stands for Name Server Look Up. You need to issue the command ```nslookup DOMAIN_NAME```, for example, ```nslookup tryhackme.com```. Or, more generally, you can use ```nslookup OPTIONS DOMAIN_NAME SERVER```. The three main parameters are:

- OPTIONS contains the query type as shown in the table below. For instance, you can use ```A``` for IPv4 addresses and ```AAAA``` for IPv6 addresses. 
- DOMAIN_NAME is the domain name you are looking up. 
- SERVER is the DNS server that you want to query. You can choose any local or public DNS server to query. Cloudflare offers ```1.1.1.1``` and ```1.0.0.1```, Google offers ```8.8.8.8``` and ```8.8.4.4```, and Quad9 offers ```9.9.9.9``` and ```149.112.112.112```. There are many more public DNS servers that you can choose from if you want alternatives to your ISP's DNS servers. 

![image](https://user-images.githubusercontent.com/79100627/170885371-450769f6-2015-41a6-ab87-ac11c53a2474.png)

For instance, ```nslookup -type=A tryhackme.com 1.1.1.1``` (or ```nslookup -type=a tryhackme.com 1.1.1.1``` as it is case-insensitive) can be used to return all the IPv4 addresses used by tryhackme.come 

![image](https://user-images.githubusercontent.com/79100627/170885458-763f342c-2cca-489a-b752-2088d879d73b.png)

The A and AAAA records are used to return IPv4 and IPv6 addresses, respectively. This lookup is helpful to know from a penetration testing perspective. In the example above, we started with one domain name, and we obtained three IPv4 addresses. Each of these IP addresses can further checked for insecurities, assuming they lie when the scope of the penetration testing.

Let's say you want to learn about the email servers and configuration for a particular domain. You can issue ```nslookup -type=MX tryhackme.com```. Here is an example:

![image](https://user-images.githubusercontent.com/79100627/170885799-da2c80ba-9864-4583-898a-3cb51cd31fc2.png)

We can see that tryhackme.com's current email configuration uses Google. Since MX is looking up the MailExchange servers, we notice that when a mail server tries to deliver email ```@tryhackme.com```, it will try to connect to the ```aspmx.l.google.com```, which has order 1. If it is busy or unavailable, the mail server will attempt to connect to the next in order mail exchange servers, ```alt1.aspmx.l.googke.com``` or ```alt2.aspmx.l.google.com```. Google provides the listed mail servers; therefore, we should not expect the mail servers to be running a vulnerable server version. However, in other cases, we might find mail servers that are not adequately secured or patched. 

Such pieces of information might prove valuable as you continue the passive reconnaissance of your target. You can repeat similar queries fro other domain names and try different types, such as ```-type=txt```. Who knows what kind of information you might discover along your way 

For more advanced DNS queries and additional functionality, you can use ```dig```, the acronym for "Domain Information Groper". we can use ```dig DOMAIN_NAME```, but to specify the record type, we would use ```dig DOMAIN_NAME TYPE```. Optionally, we can select the server we want to query using ```dig@SERVER DOMAIN_NAME TYPE```.

- SERVER is the DNS server that you want to query 
- DOMAIN_NAME is the domain name you are looking up 
- TYPE contains the DNS record type, as shown in the table provided earlier

![image](https://user-images.githubusercontent.com/79100627/170886338-328dd966-846d-4dd3-be65-940b1023415c.png)

A quick comparison between the output of ```nslookup``` and ```dig``` shows that ```dig``` returned more information, such as the TTL (Time to Live) by default. If you want query a ```1.1.1.1``` DNS server, you can execute ```dig @1.1.1.1 tryhackme.com MX```.

## DNSDumpster

DNS lookup tools, such as nslookup and dig, cannot find subdomains on their own. The domain you are inspecting might include a different subdomain that can reveal much information about the target. For instance, if tryhackme.com has the subdomains wiki.tryhackme.com and webmail.tryhackme.com, you want to learn more about these two as they can hold a trove of information about your target. There is a possibility that one of these subdomains has been set up and is not updated regularly. Lack of proper regular updates usually leads to vulnerable services. But how can we know that such subdomain exists?

We can consider using multiple search engines to compile a list of publicly known subdomains. One search engine won't be enough; moreover, we should expect to go through at least tens of results to find interesting data. After all, you are looking for subdomains that are not explicitly advertised, and hence it is not necessary to make it to first page of search results. Another approach to discover such subdomains would be rely on brute-forcing queries to find which subdomains have DNS records. 

To avoid such a time-consuming search, one can use an online service that offers detailed answer to DNS queries, such as DNSDumpster. If we search DNSDumpster for ```tryhackme.com```, we will discover the subdomain ```blog.tryhackme.com```, which a typical DNS query cannot provide. In addition, DNSDumpster will return the collected DNS information in easy to read tables and graph. DNSDumpster will also provide any collected information about listening servers.

We will search for ```tryhackme.com``` on DNSDumpster to give you a glimpse of the expected output. Among the results, we got a list of DNS servers for the domain we are looking up. DNSDumpster also resolved the domain names to IP addresses and even tried to geolocate them. We can also see the MX records; DNSDumpster resolved all five mail exchange servers to their respective IP addresses and provided more information about the owner and location. 

![image](https://user-images.githubusercontent.com/79100627/170887007-7e569d90-faa5-415a-8422-f013874c3373.png)

DNSDumpster will also represent the collected information graphicaly. DNSDumpster displayed the data from the table earlier as a graph. You can see the DNS and MX branching to their respective server and also showing the IP addresses. 

## Shodan.io 

When you are tasked to run a penetration test against specific targets, as part of the passive reconnaissance phase, a service like Shodan.io can be helpful to learn various pieces of information about client's network, without actively connecting to it. Furthermore, on the defensive side, you can use different services from Shodan.io to learn about connected and exposed devices belonging to your organization.

Shodan.io tries to connect every device reachable online to build a search engine of connected "things" in contrast with a search engine for web pages. Once it gets a response, it collects all the information releated to the service and saves it in the database to make it searchable. Consider the saved record of one of tryhackme.com's servers. 

![image](https://user-images.githubusercontent.com/79100627/170887283-06757b0d-723f-45ab-8685-23fd1171f2e6.png)

This record shows a web server; however, as mentioned already, Shodan.io collects information related to any device it can find connected online. Searching for ```tryhackme.com``` on Shodan.io will display at least the record shown in the screenshot above. Via this Shodan.io search result, we can learn several things related to our search such as:

- IP address
- Hosting company
- Geographic location
- Server type and version 

You may also try searching for the IP addresses you have obtained from DNS lookups. There are, of course, more subject to change. On their help page, you can learn about all the search options available at Shodan.io, and you are encouraged to join TryHackMe's Shodan.io.

![image](https://user-images.githubusercontent.com/79100627/170887472-45688313-849a-4a5d-b511-c81b2da5efe1.png)

## Active Reconnaissance 

We learn to use a web browser to collect more information about our target. Moreover, we discuss using simple tools such as ```ping```, ```traceroute```, ```telnet```, and ```nc``` to gather information about the network, system, and services. 

Active reconnaissance requires you to make some kind of contact with your target. This contact can be a phone call or a visit to the target company under some pretence to gather more information, usually as part of social engineering. Alternatively, it can be direct connection to the target system, whether visiting their website or checking if their firewall has SSH port open. Think of it like you are closely inspecting windows and door locks. Hence, it is essential to remember not to engage in active reconnaissance work before getting signed legal authorization from the client. 

We focus on active reconnaissance. Active reconnaissance begins with direct connections made to the target machine. Any such connection might leave information in the logs showing the client IP address, time of the connection, and duration of the connection among other things. However, not all connections are suspicious. It is possible to let your active reconnaissance appear as regular client activity. Consider web browsing; no one would suspect a browser connected to a target web server among hundreds of other legitimate users. You can use such techniques to your advantage when working as part of the red team (attacker) and don't want to alarm the blue team (defenders).

## Web Browser 

The web browser can be a convenient tool, especially that it is readily available on all systems. There are several ways where you can use a web browser to gather information about a target. 

On the transport level, the browser connects to:
- TCP port 80 by default when website is accessed over HTTP
- TCP port 443 by default when the website is accessed over HTTPS

Since 80 and 443 are default ports for HTTP and HTTPS, the web browser does not show them in the address bar. However, it is possible to use custom ports to access a service. For instance, http://127.0.0.1:8834/ will connect to 127.0.0.1 (localhost) at port 8834 via HTTPS protocol. If there is an HTTPS server listening on that port, we will receive a web page.

While browsing a web page, you can press ```CTRL+SHIFT+I``` on a PC or ```Option + Command + I``` to open Developer Tools on Firefox. Similar shortcuts will also get you started with Google Chrome or Chromium. Developer Tools lets you inspect many things that your browser has received and exchanged with the remote server. For instance, you can view and even modify the JavaScript (JS) files, inspect the cookies set on your system and discover the folder structure of the site content. 

There are also plenty of add-ons for Firefox and Chrome that can help in penetration testing. Here are few examples:
- FoxyProxy: lets you quickly change the proxy server you are using to access the target website. This browser extension is convenient when you are using a tool such as Burp Suite or if you need to switch proxy servers regularly. 
- User-Agent Switcher and Manager: gives you the ability to pretend to be accessing the webpage from a different operating system or different web browser. In other words, you can pretend to be browsing a site using an iPhone when in fact, you are accessing it from Mozila Firefox. You can download User-Agent Switcher and Manager for Firefox here. 
- Wappalyzer: provides insights about the technologies used on the visited websites. Such extension is handy, primarily when you collect all this information while browsing the website like any other user. A screenshot of Wappalyzer is shown below

![image](https://user-images.githubusercontent.com/79100627/170897573-ef20fa39-79ff-465f-bd29-5aac07d73ef6.png)

## Ping 

In simple terms, the ping command sends a packet to a remote system, and the remote system replies. This way, you can conclude that the remote system is online and that the network is working between the two systems. If you prefer a pickier definition, the ping is a command that sends an ICMP Echo packet to a remote system. If the remote system is online, and the ping packet was correctly routed and not blocked by any firewall, the remote system should send back an ICMP Echo Reply. Similarly, the ping reply should reach the first system if appropriately routed and not blocked by any firewall. 

The objective of such a command is to ensure that the target system is online before we spend time carrying out more detailed scans to discover the running operating system and services. 

![image](https://user-images.githubusercontent.com/79100627/170897801-3d2560a8-8039-4031-84b0-621903145a3a.png)

In the example above, we saw clearly that the target system is responding. The ping output is an indicator that it is online and reachable. We have transmitted five packets, and we received five replies. We notice that, on average, it took 0.475 ms (millisecond) for the reply to reach our system, with the maximum being 0.636 ms. 

From a penetration testing point of view, we will try to discover more about this target. We will try to learn as much as possible, for example, which ports are open and which services are running.

Let's consider the following case: we shut down the target virtual machine and then tried to ping . As you would expect in the following example, we don;t recieve any reply.

![image](https://user-images.githubusercontent.com/79100627/170897948-1e968066-a515-4350-9f78-8d2e351bc47e.png)

In this case, we already know that we have shut down the target computer. For each ping, the system we are using, is responding with "Destination Host Unreachable". We can see that we have transmitted five packets, but none was received, resulting in a %100 packet loss. 

Generally speaking, when we don't get a ping reply back, there are a few explanations that would explain why we didn't get a ping reply, for example:

- The destination computer is not responsibe; possibly still booting up or turned off, or the OS has crahsed
- It is unplugged from the network, or there is a faulty network device accross the path.
- A firewall is configuredto block such packets. The firewall might be a piece of software running on the system itself or a separate network appliance. MS Windows firewall blocks ping by default.
- Your system is unplugged from the network. 

## Traceroute 

As the name suggests, the traceroute command traces the route taken packets from your system to another host. The purpose of a traceroute is to find the IP addresses of the routers or hops that a packet traverses as it goes from your system to a target host. This command also reveals the number of routers between the two systems. It is helpful as it indicates the number of hops (routers) between your system and the target host. However, note that the route taken by the packets might change as many routers use dynamic routing protocol that adapt to network changes. 

On Linux and macOS, the command to use is ```traceroute MACHINE_IP```, and MS Windows, it is tracert MACHINE_IP```. ```traceroute``` tries to discover router across the path from your system to the target system.

There is no direct way to discover the path from your system to a target system. We rely on ICMP to "trick" the routers into revealing their IP addresses. We can accomplish this by using a small Time To Live (TTL) in the IP header field. Although the T in TTL stands for time, TTL indicates the maximum number of routers/hops that packet can pass through before being dropped; TTL is not a maximum number of time units. When a router receives a packet, it decrements the TTL by one before passing it to the next router. The following figure shows that each time the IP packet passes through a router, its TTL value is decremented by 1. Initially, it leaves the system with a TTL value of 64; it reaches the target system with a TTL value of 60 after passing through 4 routers.

![image](https://user-images.githubusercontent.com/79100627/171254308-1a757212-04bd-40b3-ae52-488891134b16.png)

![image](https://user-images.githubusercontent.com/79100627/171254356-7c592c46-49f5-4a02-95a6-d3a6652c8b6f.png)

However, if the TTL reaches 0, it will droppped, and an ICMP Time-To-Live exceeded would be sent to the original sender. In the following figure, the system set TTL to 1 before sending it to the router. The first router on the path decrements the TTL by 1, resulting in a TTL of 0. consequently, this router will discard the packet and send an ICMP time exceeded in-transit error message. Note that some routers are configured not to send such ICMP messages when discarding a packet. 

![image](https://user-images.githubusercontent.com/79100627/171254967-e2e6182b-f1d3-4c2d-a8bb-7c232a08bca6.png)
![image](https://user-images.githubusercontent.com/79100627/171255008-16ceb2d9-d873-4217-a3e1-ecc88bc41546.png)

On Linux, ```traceroute``` will start by sending UDP datagrams within IP packets of TTL being 1. Thus, it causes the first router to you. Then it will send another packet with TTL=2; this packet will be dropped at the second router. And so on. Let's try this on live systems

In the following examples, we run the same command, ```traceroute tryhackme.com``` from TryHackMe's AttackBox. We notice that different runs might lead to different routes taken by the packets. 

Traceroute A

![image](https://user-images.githubusercontent.com/79100627/171255486-62c6cc5d-ee7e-4733-a114-d1c6c6864e8b.png)

In the traceroute output above, we have 14 numbered lines; each line represents one router/hop. Our system sends three packets with TTL set to 1, then three packets with TTL set to 2, and so forth. Depending on the network topology, we might get replies from up to 3 different routers, depending on the route taken by the packet. Consider line number 12, the twelfth router with the listed IP address has dropped the packet three times and sent an ICMP time exceeded in transit message. The line ```12, 99.83.69.207 (99.83.69.207) 17.603ms 15.827 ms 17.351 ms``` shows the time in millieseconds for each reply to reach our system. 

On the other hand, we can see that we recieved only a single reply on the third line. The two starts in the output ```3 * 100.66.16.176 (100.66.16.176) 8.006 ms * ``` indicate that our system didn't receive two expected ICMP time exceeded in transit messages.

Finally, in the first line of the output, we can see that the packets leaving the AttackBox take different rotues. We can see two routers that responded to TTL 

TraceRoute B

![image](https://user-images.githubusercontent.com/79100627/171257112-bbc15825-8047-4062-a8eb-3e6e64f2fac8.png)

In the second run of the traceroute program, we noticed that the packets took a longer route this time, passing through 26 routers. If you are running a traceroute to a system within your network, the route will be unlikely to chagne. However, we can not expect the route to remain fixed when the packets need to go via other routers outside our network.

To Summarize, we can notice the following:
- THe number of hops/routers between your system and the target system depends on the time you are running tracerroute. There is no guarantee that your packets will always follow the same route, even if you are on the same network or you repeat the traceroute command within a short time.
- Some routers return a public ip address. You might examine a few of these routers based on the scope of the intended penetration testing.
- Some routers don't return a reply.

## Telnet 

The TELNET (Teletype Network) protocol was developed in 1969 to communicate with a remote system via a command-line interface (CLI). Hence, the command ```telnet``` uses the TELNET protocol for remote administration. The default port used by telnet is 23. From a security perspective, ```telnet``` sends all the data, including usernames and passwords, in cleartext. Sending in cleartext makes it easy for anyone, who has access to the communication channel, to steal the login credentials. The secure alternative SSH (Secure SHell) protocol.

However, the telnet client, with its simplicity, can be used for other purposes. Knowing that telnet client relies on the TCP protocol, you can use Telnet to connect to any service and grab its banner. Using ```telnet MACHINE_IP Port```, you can connect to any service running on TCP and even exchange a few messages unless it uses encryption.

Let's say we want to discover more information about a web server, listening on port 80. We connect to the server at port 80, and then we communicate using the HTTP protocol. You don't need to dive into the HTTP protocol; you just need to issue ```GET/HTTP/1.1```. To specify something other that we want to use HTTP version 1.1 for communication. To get a valid response, insted of an error, you need to input some value for the host ```host: example``` and hit enter twice. Executing these steps will provide the requested index page. 

![image](https://user-images.githubusercontent.com/79100627/171259330-fbfa2d6b-5670-41fe-939d-e33120142699.png)

Of particular intrest for us is discovering the type and version of the installed web server, ```Server: nginx/1.6.2```. In this example, we communicated with a web server, so we used basic HTTP commands. If we connect to a mail server, we need to use proper commands based on the protocol, such as SMTP and POP3.

## Netcat 

Netcat or simply nc has different applications that can be great value to a pentester. Netcat supports both TCP and UDP protocols. It can function as client that connects to a listening port; alternatively, it can act as a server that listens on a port of your choice. Hence, it is a convenient tool that you can use as a simple client or server over TCP or UDP.

First, you can connect to a server,as you did with Telnet, to collect its banner using ```nc 10.10.154.156 PORT```, which is quite similar to our previous ```telnet 10.10.154.156 PORT```

![image](https://user-images.githubusercontent.com/79100627/171264014-474e8c97-00cd-45ca-b70b-9a4e28080750.png)

In the terminal shown above, we used netcat to connect to 10.10.154.156 port 80 using ```nc 10.10.154.156 80```. Next, we issued a get for the default page using ```GET / HTTP/1.1```; we are specifying to the target server that our client supports HTTP version 1.1. Finally, we need to give a name to our host, so we added on a new line, ```host: netcat```; you can name your host anything as this has no impact on this exercise.

Based on the output ```Server: nginx/1.6.2``` we received, we can tell that on port 80, we have Nginx version 1.6.2 listening for incoming connections. 

You can use netcat to listen on a TCP port and connect to a listening port on another system. 

On the server system, where you want to open a port and listen on it, you can issue ```nc -lp 1234``` or better yet, ```nc -vnlp 1234```, which is equivalent to ```nc -v -l -n -p 1234```, as you would remember from the Linux room, The exact order of the letters does not matter as long as the port number is preceded directly by ```-p```.

![image](https://user-images.githubusercontent.com/79100627/171265381-fb8db003-a442-4dfb-8e69-fa5a3fbae950.png)

Notes: 
- The option ```-p``` should appear just before the port number you want to listen on.
- The option ```-n``` will avoid DNS lookups and warnings. 
- port numbers less 1024 require root privileges to listen on. 

On the client-side, you would issue ```nc 10.10.154.156 PORT```. Here is an example of using ```nc``` to echo. After you successfully establish a connection to the server, whatever you type on the client-side will be echoed on the server-side and vice versa.

Consider the following example. On the server side, we will listen on port 1234. We can achieve this with the command ```nc -vnlp 1234``` (same as ```nc -lvnp 1234```). In our case, the listening server has the IP address ```10.10.154.156```, so we can connect to it from the client-side by executing ```nc 10.10.154.156 1234```. This setup would echo whatever you type on the other side of the TCP tunnel. You can find a recording of the process below.

## Putting All together 

![image](https://user-images.githubusercontent.com/79100627/171268464-cee3d800-d91a-470d-8dce-92c9cd285417.png)

## Nmap Live Host Discovery 

When we want to target a network, we want to find an efficient tool to help us handle repetitive tasks and answer the following questions:

1. Which systems are up?
2. What services are running on these systems?

The tool that we will reply on is Nmap. The first question about finding live computers is answered in this room. This room is the first in a series of four rooms dedicated to Nmap. The second question about discovering running services is answered in the next Nmap rooms that focus on port-scanning. 

We present the different approaches that Nmap uses to discover live hosts. In particular we cover:

1. ARP scan: This scan uses ARP requests to discover live hosts
2. ICMP scan: This scan ICMP requests to identify live hosts 
3. TCP/UDP ping scan: This scan sends packet to TCP ports and UDP ports to determine live hosts 

## Subnetworks 

Let's review a couple of terms before we move on the main tasks. A network segment is a group of computers connected using a shared medium. For instance, the medium can be the Ethernet switch of WiFi access point. In an IP network, a subnetwork is usually the equivalent of one or more network segments connected together and configured to use the same router. The network segment refers to a physical connection, while a subnetwork refers to a logical connection. 

In following network diagram, we have four network segments or subnetworks. Generally speaking, your system would be connected to one of these network segments/subnetworks. A subnetwork, or simply a subnet, has its own IP address range and is connected to a more extensive network via a router. There might be a firewall enforcing security policies depending on each network. 

![image](https://user-images.githubusercontent.com/79100627/171719993-e972d496-e71f-4bfe-a4a9-c90bd04d31d5.png)

The figure above shows two types of subnets:

- subnet with ```/16```, which means that subnet mask is ```255.255.0.0```. This subnet can have around 2^16 hosts 
- subnet with ```/24```, which indicates subnet mask is ```255.255.255.0``` This subnet can have around 2^8 hosts (-2 for 0.0.0.0 (network ID) 255.255.255.255 (broadcasting)

As part of active reconnaissance, we want to discover more information about a group of hosts or about a subnet. If you are connected to the same subnet, you would expect your scanner to rely on ARP (Address Resolution Protocol) queries to discover live hosts. An ARP query aims to get the hardware address (MAC address) so that communication over the link-layer becomes possible; however, we can use this to infer that the host is online. 

If you are in Network A, you can use ARP only to discover the devices within that subnet (10.1.100.0/24). Suppose you are connected to a subnet different from the subnet of the target system. In that case, all packets generated by your scanner will be routed via the default gateway to reach the systems on another subnet; however the ARP queries won't be routed and hence cannot cross the subnet router. ARP is a link-layer protocol, and ARP packets are bound to their subnet. 

## Enumerating Targets 

We mentioned the different techniques we can use for scanning in Task 1. Before we explain each in detail and put it into use against a live target, we need to specify the targets we want to scan. Generally speaking, you can provide a list, a range or a subnet. Examples of target specification are:

- List: ```MACHINE IP scanme.nmap.org example.com``` will scan 3 IP addresses. 
- range: ```10.11.12.15-20``` will scan 6 IP addresses: ```10.11.12.15```, ```10.11.12.13.16```,...and ```10.11.12.13.20```. 
- subnet: ```MACHINE_IP/30``` will scan 4 IP addresses

You can also provide a file as input for your list of targets, ```nmap -iL list_of_host.txt```.

If you want to check the list of hosts that Nmap will scan, you can use ```nmap -sL TARGETS```. This option will give you a detailed list of the hosts that Nmap will scan without scanning them; however, Nmap will attempt a reverse-DNS resolution on all the targets to obtain their names. Names might reveal various information to the pentester. (if you don't want Nmap to DNS server, you can add ```-n```)

![image](https://user-images.githubusercontent.com/79100627/171724732-3eb87172-498d-47be-b297-342a392a6039.png)

## Discovering Live Hosts

Let's revisit the TCP/IP layer shown in the figure next. We will leverage the protocols to discover the live hosts. Starting from bottom to top we can use 

- ARP from Link Layer
- ICMP from network layer
- TCP from Transport Layer
- UDP from Transport Layer

![image](https://user-images.githubusercontent.com/79100627/171725192-9738d706-1bb5-4f94-953d-0ff3ecad90f5.png)

Before we discuss how scanners can use each in deatil, we will brefly review these four protocols. ARP has one purpose: sending a frame to braodcast address on the network segment and asking the computer with a specific IP address to respond by providing its MAC (hardware) address. 

ICMP has many types. ICMP ping uses Type 8 (Echo) and Type 0 (Echo Reply) 

If you want to ping a system on the same subnet, an ARP request should precede the ICMP Echo. 

Although TCP and UDP are transport layers, for network scanning purposes, a scanner can send a specially-crafted packet to common TCP or UDP ports to check whether the target will respond. This method is efficient, especially when ICMP Echo is blocked. 

## Nmap Host Discovery Using ARP 

How would you know which hosts are up and running? It is essential to avoid wasting our time port-scanning an offline or an IP address not in use. There are various ways to discover online hosts. When no host discovery options are provided, Nmap follows the following approaches to discover live hosts:

1. When a prvileged user tires scan targets on a local network (Ethernet), Namp uses ARP requests. A privileged user is ```root``` or a user who belongs to ```sudoers``` and can run ```sudo```.
2. When a privileged user tries to scan target outside the local network, Nmap uses ICMP echo requests, TCP ACK to port 80, TCP SYN to port 443, and ICMP timestamp request. 
3. When an unprivileged user treis to scan targets outside the local network, Nmap resorts to a TCP 3-way handshake by sending SYN packets to port 80 and 443. 

Nmap, by defaultm uses a ping scan to find live hosts, then proceeds to scan live hosts only. If you want to use Nmap to discover online hosts without port-scanning the live system, you can issue ```nmap -sn TARGETS```. 

ARP scan is possible only if you are on the same subnet as the target systems. On a Ethernet (802.3) and WiFi(802.11), you need to know the MAC address of any system before you can communicate with it. The MAC address is necessary for the link-layer header; the haeader contains the source MAC address and destination MAC address among other fields. To get the MAC address, the OS sends an ARP query. A host that replies ARP quieres is up. The ARP queries only owkrs if the target is on the same subnet as yourself. You should expect to see many ARP queries generated during a Nmap scan of a local network. if you want Nmap only to perfrom an ARP scan without port-scanning, you can use ```nmap -PR -sn TARGETS```, where ```-PR``` indicates that you only want an ARP scan. The following example shows Nmap using 
