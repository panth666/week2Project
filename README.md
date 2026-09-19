# Week2Project at Networkwalks
# FootPrinting And Network Scanning Phases
# Penetration Testing Engagement Information
|Category|Details|
|--------|--------|
|Project Name |Penetration Testing Report|
|Pentester Name	Bibek Panth|
|Role|	Cybersecurity Student |
|Program / Batch|	B083'E' – Networkwalks|
|Assessment Date| 19 Septemer 2026|
|Assessment Type|	Authorized Penetration Testing & Security Assessment|
|Target|	Networkwalks — Written Authorization Secured|
|Additional Target|	Tester-Owned Local LAN Network|
|Authorization Status\	Authorized — Written Permission Secured|
|Testing Environment|	Controlled Cybersecurity Laboratory / Authorized Network|

# 1. Liability Disclaimer
The work documented here was only performed on machines I own, or on systems I have written permission to perform such tests. This repository is for education, research, and authorized security testing purposes only.

Unauthorized or malicious use of any method described here may be a violation of local, state, or federal laws and may result in criminal or professional action. I am not responsible for any such use.

# 2. Introduction
This penetration-testing report includes two activities that I achieved in Week 2 of my cybersecurity internship program at Networkwalks. The first activity is related to footprinting & reconnaissance of the domain networkwalks.com by using several Kali Linux tools, in W2-PM1 (Multiple Kali Tools). The second activity is related to the network scanning & host discovery of my personal local network, using Zenmap, in W2-PM5 (Zenmap Scanning).

These two modules can be seen as key elements of a process-based penetration-testing methodology. The footprinting task illustrates how publicly accessible information can be gathered and processed during the reconnaissance phase, and the Zenmap task illustrates how a tester who has been given the go-ahead can discover live hosts and begin to chart the attack surface in the scanning phase. The combination of these two exercises shows how a security assessment can go from reconnaissance to scanning.

The footprinting activities were performed using Kali Linux, except for the local-network scanning activity that was authorized on a Windows PC running Zenmap. The testing activities were limited only to systems and networks where it was authorized to do so.

To further enhance the trustworthiness and repetition of this report, the following section on each exercise contains the commands that were issued, what the outcome was, screenshot evidence, and a short security evaluation on how that specific finding can relate to a penetration-test. It can be thought of as showing the readers what was done, as well as why and how.

# 3. Used Tools
The table below lists each tool used in this report and its purpose.

|#|	Tool / Operating System	|Purpose / Function|
|1|	Kali Linux & Windows	|Operating systems used for reconnaissance activities|
|2|	WHOIS	|Identifies domain registration details, including owner information, registration/expiration dates, and name servers|
|3|	WhatWeb|	Fingerprints web technologies in use, such as server type, CMS, plugins, and IP address|
|4|	nslookup|	Resolves the target domain name to its corresponding IP address via DNS|
|5|	curl -I|	Retrieves and displays the HTTP response headers of the target website|
|6|	Wafw00f	|Detects the presence of a Web Application Firewall (WAF) protecting the site|
|7|	DNSRecon|	Enumerates DNS records, including NS, MX, SPF, and TXT entries|
|8|	Zenmap (Nmap GUI)|	Scans the local subnet to identify live hosts, their IP addresses, and MAC addresses|
|9|	Windows CMD	| Used for local IP address and MAC address identification|

# 4. Preformed Activities
# 4.1 FootPrinting And Reconnaissance
During my reconnaissance phase, I performed an authorized reconnaissance/footprinting assessment on the networkwalks.com domain using the Kali Linux toolkit consisting of six Linux tools - WHOIS, What Web, Nslookup, cURL, Wafw00f, and DNSRecon. Each tool was run to gather a specific category of publicly accessible information and to gain a wider view of the target's domain, web technologies, DNS infrastructure, and security measures. First, I used WHOIS to obtain publicly available information about the domain registration and reveal the domain's associated name servers. 

The tools results revealed useful information about the domain registration, hosting, and DNS infrastructure. 

Next, I used What Web to identify the technologies and components that exposed by the target website. The results revealed WordPress 7.1 and WP Download Manager 3.3.58, in addition to other technology information that the website exposed. Such information could help a security professional comprehend the target's technological stack and identify vulnerabilities that may warrant more security investigation. Using Nslookup I performed a DNS resolution for the target domain name and found the associated address to be 192.232.216.135. This information is an important reference point to understand the publicly available infrastructure of the target. 

Third, I used cURL to interrogate the HTTP response headers returned by the web server. The headers provided additional information about the web application and exposed the presence of the /wp-json/ REST API. HTTP headers and exposed API endpoints can provide valuable information during reconnaissance that helps identify technologies or interfaces that may require additional security inspection. 

I also used Wafw00f to determine if a Web Application Firewall (WAF) was present in front of the target web application. The tool identified Mod Security (Spider Labs) as the WAF technology in use. Recognizing defensive technologies is an important part of reconnaissance as it informs the researcher of the protective measures in place around the web application. 

Lastly, I used DNSRecon to enumerated DNS and collect additional publicly accessible DNS information. The output revealed several interesting items including name servers, mail servers, SPF/TXT records, service records, and software information, all contributing to a more complete understanding of the target's DNS architecture. In overall, these reconnaissance activities provided a broad, multi-faceted snapshot of the target's public site ownership, domain information, DNS configuration, web-based information, exposed API endpoints, and security posture. The information collected can be leveraged into the subsequent stages of the authorized pentesting engagement, including scanning, enumeration, vulnerability identification, and risk analysis.

# 4.2 Network Scanning with Zenmap
This practical (2) used Zenmap (the graphical user interface for Nmap) to perform authorized network discovery in my local LAN environment. The aim of the practical was to discover local network configuration, the known hosts on the network and their associated IP and MAC address (if known), and then display the discovered network in Zenmap Topology view. The first step was to use the Windows ipconfig command to get the system's current local IP address, network configuration, and current subnet mask. 

The discovered subnet range was then used in Zenmap as the target IP address range. I then selected the Ping Scan profile for the scan; this type of scan is used to discover what systems are alive and responsive on an authorized local network, but is not a full host-service/vulnerability assessment. 
In my practical example I was able to discover the following 4 hosts on the local LAN: 
10.0.0.1 
10.0.0.2 
10.0.0.3

In addition, where the required network information was available, the example results included known MAC addresses for the discovered hosts. Both IP address and MAC address information can be useful for identifying specific devices and understanding the topology of a local network. After the host-discovery scan had completed I reviewed the results in Zenmap and then navigated to the Topology tab to view a graphic display of the discovered network. 

The topology legend was enabled to make the topology diagram more useful to interpret and the network topology was exported in PDF format, as required.

# 5. Risk Analysis
After performing the footprinting, reconnaissance, and network-scanning phases of the engagement I found the following possible security issues and risks based on the information I collected. These observations should illustrate information exposure and potentially areas that could be further investigated during your next phase of an authorized penetration test.
|#|	Finding	Evidence / Observation	|Potential Impact	|Risk Level|
|-|---------------------------------|-----------------|----------|
|1|	Web Technology Information Disclosure	WhatWeb identified WordPress and WP Download Manager technologies.|	Disclosure of webtechnologies  may assist attackers in fingerprinting the application and identifying components that require security review.	| Medium|
|2|	Publicly Identifiable Server IP Address	nslookup resolved the target domain to 192.232.216.135.|	Revealing the server's IP address provides information about the network infrastructure hosting the web service and may support further reconnaissance.	| Low|
|3|	HTTP Response Header Information Disclosure	curl -I retrieved HTTP response headers and identified the /wp-json/ endpoint.| Exposed HTTP and application information may facilitate technology fingerprinting and additional enumeration activities.	| Low|
|4|	WAF Technology Disclosure	Wafw00f identified ModSecurity (SpiderLabs) as the Web Application Firewall technology.|	Disclosure of security technologies may provide attackers with information about the application's defensive architecture.	|Low|
|5	|DNS Infrastructure Information Disclosure	DNSRecon identified DNS, mail, and other service-related DNS records.|	Exposed DNS information can assist in building a broader profile of the organization's network and service infrastructure.	| Medium|
|6|	Multiple Live Hosts Identified on Local Network	Zenmap identified four live hosts within the authorized example network.|	Unidentified or unauthorized devices on the network may increase the potential attack surface and should be reviewed by the network administrator.	| Medium|
None of the above risk observations are corroborated vulnerabilities, they are based on the footprinting, reconnaissance and scanning activity. The specific exercises at the time were primarily focusing on information gathering, technology identification, DNS enumeration and live-host discovery. No exploitation or vulnerability validation has taken place within these two modules.

While a version number, IP address, HTTP endpoint, WAF technology or DNS record was identified, this does not indicate a vulnerability is present in the system identified. Please consider the above as potential avenues of investigation, not corroborated vulnerabilities, and further penetration testing, information collection and vulnerability validation would be required to establish if any of the observations presented could lead to a vulnerability and/or a significant business impact.

# 6. Recemmendations
Based on the findings from these activities, the following security improvements are recommended:
|#|	Recommendation	|Justification|
|1|	Review Publicly Exposed Technology Information|	Organizations should regularly assess publicly discoverable information about web technologies, CMS platforms, plugins, and frameworks. Minimizing unnecessary technology disclosure can reduce opportunities for fingerprinting and targeted attacks.|
|2|	Keep Software Up to Date|	CMS platforms, plugins, frameworks, and other web technologies should be regularly updated and reviewed against current security advisories. Timely patching helps reduce exposure to known vulnerabilities.|
|3|	Review HTTP Response Headers	|HTTP response headers should be periodically reviewed to identify unnecessary technical information. Removing non-essential details can make technology fingerprinting more difficult and reduce information leakage.|
|4|	Review DNS Records Regularly	|DNS records should be audited periodically to verify that only required services and information are publicly exposed. Maintaining accurate DNS records helps reduce unnecessary infrastructure disclosure.|
|5|	Properly Configure and Monitor the WAF	|The ModSecurity Web Application Firewall (WAF) should remain enabled, properly configured, and actively monitored. Regular tuning and monitoring can strengthen the application's baseline protection against common and automated attacks.|
|6|	Perform Regular Internal Network Discovery	|Organizations should conduct periodic authorized network discovery to maintain visibility into active hosts, devices, and services. This helps identify unexpected systems and potential changes to the internal attack surface.|
|7|	Investigate Unknown Devices|	Any unexpected or unrecognized device discovered during authorized network scanning should be investigated and validated against approved asset inventories to determine whether it is legitimate.|
|8|	Maintain Accurate Network Documentation|	Network topology diagrams, device inventories, IP allocations, and system ownership information should be kept accurate and up to date. Proper documentation supports effective monitoring, troubleshooting, and incident response.|
|9|	Conduct Security Testing with Proper Authorization|	Reconnaissance and scanning activities should only be performed against systems and networks for which explicit authorization has been granted. This ensures that security assessments remain controlled, ethical, and within the approved scope.|

# 7. Conclusion
In Week 2 of my Networkwalks Cybersecurity & Ethical Hacking internship, I undertook hands-on activities around footprinting, reconnaissance and network scanning. This week's work enabled me to cover the first critical stages of the penetration-testing methodology and appreciate how a professional security analyst proceeds from collection of information on a defined target, through assessment and analysis to documentation.

In the footprinting and reconnaissance activity, I used six Kali Linux tools–WHOIS, What Web, Nslookup, cURL, Wafw00f and DNSRecon – to gather and examine publicly available information on the authorized domain name. From this experience I learned how WHOIS provides domain registration-related information; What Web helps determine what web technologies exist on an individual web server; Nslookup performs Domain Name System (DNS) resolution; cURL can reveal details on HTTP response headers; Wafw00f ascertains whether a website is protected by a Web Application Firewall; and DNSRecon identifies certain DNS record types.

Using Zenmap for the network-scanning activity, I was able to review the infrastructure of a known local network, which helped me understand how to review available IP and MAC address information and produce a visible network topology diagram for a discovered network range.

The overall lesson to me was that information gathering is a foundation of cybersecurity and penetration testing. In many cases, without exploiting the target, security practitioners can employ automated tools and manual analysis to discover network address and device information, use network capture and receive responses, analyze DNS infrastructure and leverage web technologies to draw conclusions about a target. In turn, this reconnaissance can better inform targeted security testing.

Another key takeaway from this project for me was the importance of clear and logical security reporting. A pen-testing report should be an unambiguous and comprehensive record of testing performed, observations identified, the significance of these observations, the potential impact of that observation, and steps recommended to mitigate or reduce the risk from that potential.

Finally, in keeping with a professional ethical hacker's code of conduct, all testing activities were conducted within the scope, scope, scope and scope specified by agreement.

# Author
Bibek Panth
Cybersecurity Student B083'E'
Linkedln: www.linkedin.com/in/bibek-panth-033019274

