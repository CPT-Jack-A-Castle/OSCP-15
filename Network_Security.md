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

