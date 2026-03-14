# Web-Application-Security-Assessment
A web application security assessment project demonstrating vulnerability identification, penetration testing methodology, and mitigation recommendations based on industry best practices from the OWASP.

---

## Introduction

This Repo provides a comprehensive overview of a penetration test conducted on the web infrastructure of  [https://pingbreakers.com]() . The objective of this assessment was to evaluate the security posture of the specified domains and identify potential vulnerabilities that could expose sensitive information or lead to unauthorized access.

## Scope

The scope of this penetration test included a thorough examination of the web assets hosted on the [pingbreakers.com]() domain, as well as its subdomains. The assessment focused on identifying vulnerabilities within the web application layer, specifically targeting potential flaws in input validation, session management, and authentication mechanisms. It is important to note that this test did not encompass an analysis of the underlying network infrastructure or other services outside the scope of web applications.

## Limitations

Due to the nature of the black-box testing approach, the assessment was conducted with no prior knowledge of the internal architecture, configurations, or specifics of the target environment. As a result, certain internal controls and security measures that may be in place were not directly assessed. Additionally, the scope did not extend to testing any mobile application that may be associated with the web platform.

## Objectives
The primary objectives of this penetration test were:
1. To identify and exploit potential vulnerabilities within the web application layer.
2. To evaluate the effectiveness of existing security controls in mitigating potential threats.
3. To assess the risk of unauthorized access, data exposure, or other security breaches.
4. To provide actionable recommendations for improving the overall security posture of the web infrastructure.



## Methodology

The methodology employed in this penetration test adhered to industry best practices, utilizing a combination of established tools, techniques, and recognized standards and frameworks. The methodology adopted, aimed at ensuring a comprehensive and systematic evaluation of the web infrastructure, identifying potential vulnerabilities and providing actionable recommendations for strengthening the security posture.

## Testing Approach:
The testing approach followed a black-box testing methodology, where no specific information or constraints were provided regarding the scope of the assessment. This simulates an external attacker with no prior knowledge of the internal environment, mirroring real-world threat scenarios.

## Standards and Frameworks:

The testing process adhered to established industry standards and frameworks. The frameworks provided a structured approach to identifying and addressing potential security gaps. 
These includes:
- The Cyber Kill Chain is a concept that outlines the stages of a cyberattack from the initial reconnaissance phase to the final objective of the attacker. It provided a structured framework for understanding and analyzing the various steps an attacker might take in a targeted cyber intrusion.
- OWASP (Open Web Application Security Project) guidelines for web application security testing.
- NIST (National Institute of Standards and Technology) cybersecurity best practices.

## Tools and Techniques:

A range of widely recognized penetration testing tools were leveraged to conduct the assessment. The tools were carefully selected based on their proven effectiveness and their applicability to web application security testing. Each tool played a crucial role in enabling a comprehensive evaluation of potential vulnerabilities within the target web infrastructure. 

**The tools includes but are not limited to:**

**Reconnaissance tools:**

- **Urlscan.io** - was used to analyze the target website and gather information about domain infrastructure, requests, and external resources loaded by the application.
- **Nmap** -  was employed for network discovery and vulnerability scanning to identify open ports and services.
- **Whatweb** - was used to identify technologies used by the web application such as web servers, frameworks, CMS platforms, and plugins
- **VirusTotal** - was used to analyze domains and URLs associated with the target for any known malicious activity or security reputation issues
- **Gobuster** -  was employed for web content discovery, helping identify hidden files and directories.
Vulnerability analysis tools
-**Burp Suite**  - was utilized for comprehensive web application security testing, including vulnerability scanning, analysis, and manual testing.
- **OWASP ZAP** - was used to compare with the burp suite test results in automated and manual testing of web application security vulnerabilities.
- **Metasploit Framework** - was applied for identifying and exploiting known vulnerabilities in network services.
- **Sqlmap** - was specialized in detecting and exploiting SQL injection vulnerabilities.
- **Nikto** - was utilized for scanning web servers for known vulnerabilities and misconfigurations.
- **Hydra** - was applied for brute-force attacks on login form discovered


**Reporting tools:**

- **Google Docs** – was used to document the penetration testing process, findings, and remediation recommendations in a structured report format.
- **Screenshots and logging tools** – were used to capture proof-of-concept evidence of discovered vulnerabilities and support the analysis in the final report.

## Target Information

**Publicly available information:**

The following information is available in publicly available sources:

```
Company Name: Pingbreakers Cybersecurity Company
Website: https://pingbreakers.com 
Geo:  Mumbai, India (IN)
Social Media Profiles: linkedin as https://www.linkedin.com/in/ping-breakers-20b098257/
Contact Information: None open
Employee Names and Titles: None Open
```

**DNS Information:**

The DNS records and findings for the target domain are as follows:

```
A Records: 217.21.87.11 (AS47583 - AS-HOSTINGER, CY)
CNAME Records:
MX Records:
TXT Records:
```

**Network Information:**

```
The target network architecture includes:
Route: 217.21.80.0/20
IPv4 :  217.21.87.11 
IPv6 :  2a02:4780:11:762:0:c63:aa01
```




---

# Security Assessment Report

## Summary of Findings

These findings provide valuable insights into potential vulnerabilities and security gaps within the assessed system. Each finding should be carefully addressed to enhance the overall security posture.

---

## Findings Overview

| ID  | Vulnerability | Severity | Status |
|----|---------------|---------|--------|
| F01 | Weak Password Policy | High | Confirmed |
| F02 | Missing Security Headers | Medium | Confirmed |
| F03 | Server Banner Disclosure | Low | Confirmed |
| F04 | Incorrect Error Handling | Low | Confirmed |
| F05 | `/robots.txt` Entry `/login.php` | Low | Confirmed |
| F06 | Uncommon Header `platform` | Low | Confirmed |
| F07 | File Path Exposure via E-Tags | Low | Confirmed |
| F08 | `alt-svc` Header | Informational | Confirmed |
| F09 | Unpresent CGI Directories | Informational | Confirmed |
| F10 | SSL Negotiation Issue | Informational | Confirmed |

---

# Detailed Findings

## F01 – Weak Password Policy
The password policy could be strengthened to better protect user accounts from unauthorized access.

**Recommendation**

Implement stronger password requirements, such as:

- Minimum password length
- Complexity requirements
- Password expiration policies
- Account lockout after repeated failed login attempts

---

## F02 – Missing Security Headers

### X-Frame-Options Header Not Set
Additional measures could be taken to guard against a specific type of attack known as **clickjacking**.

**Recommendation**

Implement the `X-Frame-Options` header to prevent the site from being embedded in malicious frames.


### X-Content-Type-Options Header Not Set
Some adjustments could be made to ensure that files are interpreted correctly, reducing the risk of certain types of attacks.

**Recommendation**

Ensure files are interpreted correctly by implementing: **X-Content-Type-Options: nosniff**


### Strict-Transport-Security Header Not Defined
The **Strict-Transport-Security (HSTS)** HTTP header is not defined, potentially leaving the application vulnerable to certain types of attacks.

**Recommendation**

Implement the HSTS header: Strict-Transport-Security: max-age=31536000; includeSubDomains



## F03 – Server Banner Disclosure

Information about the server's software and version is exposed, which could be a potential risk.

**Recommendation**

Hide or obfuscate server banners to reduce exposure of sensitive infrastructure details.

---

## F04 – Incorrect Error Handling

Server errors are revealing information about underlying technologies.

**Recommendation**

Improve error handling by:

- Disabling verbose server errors
- Implementing generic error pages
- Logging detailed errors internally only

---

## F05 – `/robots.txt` Entry `/login.php`

The admin login page is referenced in a publicly accessible file (`robots.txt`), which may make it easier for attackers to discover.

**Recommendation**

Review and restrict access to sensitive administrative endpoints.

---

## F06 – Uncommon Header `platform`

A non-standard header (`platform`) reveals details about the hosting environment.

**Recommendation**

Evaluate the necessity of this header and remove it if not required.

---

## F07 – File Path Exposure via E-Tags

The server may reveal internal file system information through E-Tag responses.

**Recommendation**

Disable or properly configure E-Tag headers to avoid exposing internal file paths.

---

## F08 – `alt-svc` Header

The server indicates support for a next-generation protocol through the `alt-svc` header.

**Recommendation**

Evaluate whether exposing this capability is necessary and remove the header if not required.

---

## F09 – Unpresent CGI Directories

No sensitive CGI directories were discovered.

**Recommendation**

No immediate action required.

---

## F10 – SSL Negotiation Issue

A minor issue was encountered during SSL negotiation.

**Recommendation**

Investigate and resolve SSL configuration issues to ensure secure connections.

---

# Conclusion

The assessment identified several areas where security can be improved. Addressing the identified issues—particularly the **high and medium severity vulnerabilities**—will significantly strengthen the system's security posture.

Regular security testing and adherence to best security practices are recommended to maintain a strong defensive posture.








