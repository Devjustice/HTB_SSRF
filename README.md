# HTB_SSRF

Today's 27-05-2025 God's speaking
 bye beep beep slumin reverse engineer whiner WooHoo potentially delightful LOL if anything can go wrong on occassion boss I didn't see that air head car liberal endure lulz umm what now manufacturing holy grail crash and burn you're nuts God Angel zoot African Give me praise I had a crazy dream daunting once upon a time in theory


Server-side attacks are one of the most popular vulnerabilities.
Congregate with Server-Side Request Forgery, Server-Side Template Injection, Server-Side Includes, And eXtensible Stylesheet Language Transformations. SSRF is one of OWASPs Top 10 vulnerabilities.

We probably use file:// URL scheme and gopher:// protocol. One can see that gopher://was developed for a specific reason for file transfer (FTP) in 1991 by McCahill at the University of Minnesota when the time developed HTTP. I guess that old companies still can use it 
regardless of HTTP, or HTTP because of misconfigurations. The gopher protocol can be used by attackers while the protocol uses HTTP POST requests on SMTP servers or databases. 

While I speculate this SSRF attack, I have learned that while clients send POST requests to the target server If an SSRF attack is exploitable, the POST request can also send POST request to the client's server (netcat server, client's Apache server, tomcat server, flask server whatever) then client's server receives POST request occurs in Web browser or curl and hold it until server closed by Control C user interrupt or closed server then I can check it from original target web server with specific error code.

We should closely look at this bottom line HTTP header code the 'dataserver=http://'.  The target website uses a data-related function to book a motel. As a result, &date=2024-01-01 comes at the end of the request URL. This was initially linked with http://dataserver.htb.
We can manipulate to our Netcat server or our local server where we turned on at our IP number (which can represent the HTB VPN server if not our public IP perhaps we can use a proxy chain for the real deal). At this time, I was confused a bit and spent time investigating more. 
I found dataserver=http://127.0.0.1:80 port led me to index.php and
this means that dataserver worked on the target server's local area 127.0.0.1:80 and exploitable. Now we successfully recon that SSRF vuln. For the next step, HTB suggested me to the FUZZ port number through 

seq 1 10000 > ports.txt 

ffuf -w ./ports.txt -u http://172.17.0.2/index.php -X POST -H "Content-Type: application/x-www-form-urlencoded" -d "dateserver=http://127.0.0.1:FUZZ/&date=2024-01-01" -fr "Failed to connect to"


The port is usually 80, 8080, or not far from that number you can try.

seq 80 8080 > ports.txt

Remember the concept is not difficult. We can simply do this in order to find the right port number with FUZZ that port and simply find through burpsuite repeater. 

dataserver=http://127.0.0.1:PORTHERE/&date=2024-01-01









