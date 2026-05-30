## DNS and Phishing Infrastructure Investigation
Analyst: Roland A. Apambilla, PhD
Date: May 2026
Environment: Ubuntu 24.04 Virtual Machine (VirtualBox)
Tools Used: WHOIS, DIG, CURL, Linux Terminal
## Executive Summary
This report documents two cybersecurity investigations conducted in a controlled lab environment.
The first investigation analyzed a legitimate domain associated with OpenAI to understand DNS infrastructure and domain registration information.
The second investigation focused on a malicious domain that was used in a phishing scam targeting the analyst. DNS records, web server responses, and infrastructure characteristics were examined to determine whether the domain was malicious.
The investigation concluded that the Booking.com-themed domain exhibited multiple indicators of phishing activity and was assessed as a high-confidence malicious domain.
## Case 001: OpenAI Domain Investigation
## Objective
To understand how legitimate organizations configure and maintain their internet-facing infrastructure.
## Domain Investigated
openai.com
WHOIS Analysis
Command:
whois openai.com
## Findings
Domain is registered through a legitimate registrar.
Registration records were publicly available.
Domain ownership information was consistent with a legitimate organization.
## Assessment
The WHOIS record showed characteristics expected of a legitimate and professionally managed domain.
DNS A Record Analysis
Command:
dig openai.com
## Findings
Multiple valid IP addresses were returned.
Interpretation
Domain resolves successfully. DNS infrastructure is active. Multiple IP addresses suggest load balancing and high availability.
## Name Server Analysis
Command:
dig NS openai.com
Findings
OpenAI uses Microsoft Azure DNS infrastructure.
## Interpretation
Use of enterprise-grade DNS services is consistent with a large technology company.
## Mail Exchange Analysis
Command:
dig MX openai.com
## Findings
Google mail infrastructure was identified.
Interpretation
Email services appear professionally configured and operational.
## Conclusion
The domain displayed characteristics consistent with a legitimate, professionally managed organization.
Risk Assessment: Low

## Case 002: Phishing Domain Investigation
## Objective
To investigate a suspicious domain associated with a real phishing incident.
Domain Investigated
booking.com-approve-reservation.com
## Background
The analyst encountered this domain during a scam attempt impersonating Booking.com.
The investigation aimed to determine whether the domain demonstrated indicators of phishing activity.
Visual Domain Assessment
Legitimate Domain
booking.com
Investigated Domain
booking.com-approve-reservation.com
## Observation
The investigated domain incorporates the trusted brand name "Booking.com" while extending it with additional misleading text.
## Assessment
This naming pattern is commonly associated with phishing and brand impersonation campaigns.
WHOIS Analysis
Command:
whois booking.com-approve-reservation.com
## Findings
The WHOIS query produced limited information and did not reveal clear legitimate ownership details.
## Assessment
Lack of transparent ownership information increases suspicion and complicates attribution efforts.

## DNS A Record Analysis
Command:
dig booking.com-approve-reservation.com
## Findings
The domain resolved successfully and returned active IP addresses.
Example:
104.21.62.80
172.67.221.208
## Interpretation
The domain is active and operational.

## Name Server Analysis
Command:
dig NS booking.com-approve-reservation.com
## Findings
The domain utilized Cloudflare infrastructure.
## Assessment
Cloudflare is commonly used by legitimate organizations; however, threat actors also use Cloudflare to conceal origin server information and resist takedown efforts.
## Mail Exchange Analysis
Command:
dig MX booking.com-approve-reservation.com
## Findings
ANSWER: 0
No MX records were present.
## Interpretation
The domain does not host dedicated email infrastructure.
This suggests that the domain's primary purpose may be hosting phishing content rather than sending or receiving email.
HTTP Header Analysis
Command:
curl -I https://booking.com-approve-reservation.com
## Findings
HTTP/2 403
server: cloudflare
cf-mitigated: challenge
## Interpretation
The website actively blocks automated access attempts and uses Cloudflare challenge mechanisms. This behavior is frequently observed on phishing infrastructure attempting to avoid automated scanning and investigation.

## Indicators of Compromise (IOCs)
Domain
booking.com-approve-reservation.com
IP Addresses
104.21.62.80
172.67.221.208
Infrastructure
Cloudflare

## Threat Assessment
The investigated domain demonstrates multiple indicators consistent with phishing activity.
Evidence includes:
Brand impersonation
Misleading domain naming convention
Active DNS infrastructure
Cloudflare-protected hosting
Lack of dedicated mail infrastructure
Real-world phishing incident
Restricted automated access through challenge mechanisms

## Risk Rating
Category	   Assessment
Threat     : Type	Phishing
Technique  :	Brand Impersonation
Severity	 : High
Confidence :	High
Status	   : Malicious

## Key Skills Demonstrated
Threat Analysis
Domain investigation
Phishing detection
Brand impersonation analysis
Network Security
DNS enumeration
WHOIS analysis
MX record analysis
Web Security
HTTP header inspection
Infrastructure fingerprinting
Linux
Command-line investigation
OSINT collection
Documentation and reporting

## Lessons Learned
This investigation demonstrated how publicly available DNS and web infrastructure information can be used to identify malicious domains. Even without direct access to website content, analysts can often determine whether a domain is suspicious by examining registration details, DNS records, email infrastructure, naming conventions, and server responses.
