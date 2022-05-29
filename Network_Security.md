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



