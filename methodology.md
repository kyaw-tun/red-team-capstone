# Methodology

## Assessment Overview

This assessment was conducted against an intentionally vulnerable Ubuntu virtual machine provided by WithYouWithMe as part of the Red Team Essentials capstone.

The goal was to identify exposed services, find vulnerabilities, gain access to the system, and see whether that access could be used to gain higher privileges. After completing the technical assessment, I reviewed the findings and documented recommendations for improving the security of the system.

## Assessment Phases

### 1. Reconnaissance and Enumeration

The assessment began with network reconnaissance using Nmap to identify exposed ports and services on the target.

Service and version detection were used to identify the software versions running on the discovered ports. The results were then reviewed to determine which services required further investigation.

### 2. Web Application Identification and Vulnerability Research

After completing the initial Nmap scan, I accessed the HTTP service running on port 80 and manually inspected the website to understand what application was being hosted.

Further investigation identified the application as phpTax. I then used SearchSploit to search for known vulnerabilities affecting phpTax and identified three relevant exploit entries.

I initially investigated and tested the second and third exploit entries because they provided approaches that could be attempted directly through the web application. These approaches were tested against the target but did not result in successful exploitation.

After the initial approaches were unsuccessful, I then tried the Metasploit approach for the identified phpTax vulnerability. This approach was successful and provided initial access to the target.

### 3. Exploitation and Initial Access

After identifying a suitable phpTax exploit, I used the Metasploit Framework to attempt exploitation of the vulnerable application.

The exploitation was successful and provided initial access to the target system as the `www-data` user.

After obtaining access, I verified the current user and located the `local.txt` flag as evidence that the initial-access objective had been achieved.

### 4. Local Enumeration

Following initial access, I performed enumeration of the compromised system to identify potential privilege-escalation paths.

I first checked the `sudo` permissions available to the compromised user. I then used LinPEAS and LinEnum to gather additional information about the system, including permissions, binaries, configurations, and other potential privilege-escalation opportunities.

This enumeration identified a SUID-enabled `find` binary as a potential privilege-escalation vector.

### 5. Privilege Escalation

I investigated the SUID permission on the `find` binary and tested whether it could be used for privilege escalation. Successful exploitation of the SUID configuration resulted in escalation from the `www-data` user to `root`.

### 6. Verification and Objective Completion

After achieving `root` access, I verified the elevated privileges and accessed the `/root` directory.

I then located and retrieved the `proof.txt` file, confirming successful privilege escalation and completion of the final compromise objective.

## Tools Used

- **Nmap** — network and service enumeration
- **SearchSploit** — searching for known exploits
- **Exploit-DB** — researching identified exploits
- **Metasploit Framework** — exploitation and gaining initial access
- **LinPEAS** — local privilege escalation enumeration
- **LinEnum** — additional Linux enumeration
- **GTFOBins** — researching techniques for abusing permitted Unix binaries for privilege escalation
