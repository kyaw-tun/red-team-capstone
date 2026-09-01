# Red Team Capstone

A penetration testing assessment completed as part of the Red Team Essentials course from WithYouWithMe (WYWM).

## Project Overview

After completing the Red Team Essentials course, I was provided with an intentionally vulnerable Ubuntu virtual machine as the capstone assessment. The assessment involved identifying vulnerabilities, gaining initial access, and investigating how that access could be leveraged to obtain higher privileges.

The assessment was carried out as a practical penetration testing exercise, starting with reconnaissance and service enumeration and progressing through vulnerability research, exploitation, local enumeration, and privilege escalation.

The assessment ultimately resulted in initial access to the target as the `www-data` user and successful escalation to `root`.

## Assessment Objectives

The main objective of the capstone was to compromise the provided Ubuntu virtual machine and retrieve two files:

- `local.txt` — obtained after gaining initial access to the system.
- `proof.txt` — obtained after successfully escalating privileges to `root`.

To achieve these objectives, I investigated the services exposed by the target, identified the phpTax web application, researched and tested available exploits, and used a successful Metasploit exploit to gain initial access. I then performed local enumeration and identified a SUID-enabled `find` binary that could be leveraged for privilege escalation.

## Target Environment

The assessment was performed against an intentionally vulnerable Ubuntu virtual machine provided by WithYouWithMe as part of the Red Team Essentials capstone.

The virtual machine was provided as an `.ova` image and was deployed locally for the assessment. The scope of the assessment was limited to the provided virtual machine and its exposed services.

The initial network scan identified an HTTP service running on port `80`, which led to the discovery of the phpTax web application. Further investigation of the target focused on identifying vulnerabilities in the exposed services, gaining initial access, and investigating how the compromised system could be escalated to root-level access.

## Methodology

The assessment followed a step-by-step approach, beginning with reconnaissance and service enumeration before moving into vulnerability research and exploitation. After gaining initial access, I performed local enumeration to identify potential privilege-escalation paths and then verified the final objectives after obtaining root access.

The main phases of the assessment were:

1. Reconnaissance and service enumeration
2. Web application identification and vulnerability research
3. Exploitation and initial access
4. Local enumeration
5. Privilege escalation
6. Verification and objective completion

For a more detailed description of the approach and tools used, see the [Methodology](/methodology.md).

## Attack Path

The assessment followed this attack path:

```text
Nmap reconnaissance
        ↓
HTTP service on port 80
        ↓
phpTax identified
        ↓
SearchSploit / Exploit-DB research
        ↓
Web-based exploit attempts unsuccessful
        ↓
Metasploit exploitation
        ↓
Initial access as www-data
        ↓
local.txt obtained
        ↓
Local enumeration
        ↓
SUID-enabled find identified
        ↓
GTFOBins research
        ↓
Privilege escalation
        ↓
Root access
        ↓
proof.txt obtained
```
This attack path demonstrates how the initial web application vulnerability could be followed by local enumeration and privilege escalation to obtain root-level access.

## Assessment Findings

The assessment identified vulnerabilities and misconfigurations that could be chained to achieve full compromise of the target.

### Initial Access — phpTax

The exposed phpTax web application contained a known vulnerability that could be exploited to gain initial access to the system. Multiple exploit implementations were investigated and tested. The Metasploit implementation was ultimately successful and provided access as the `www-data` user.

### Privilege Escalation — SUID `find`

After gaining initial access, local enumeration identified a SUID-enabled `find` binary. The SUID configuration allowed the binary to be abused to execute commands with elevated privileges, resulting in escalation from `www-data` to `root`.

### Overall Impact

By chaining the initial-access vulnerability with the SUID misconfiguration, it was possible to progress from an exposed web application to root-level access on the target system.

For the detailed risk assessment, see [Risk Assessment](/findings/risks-assessment.md).

For a reflection on the assessment and the lessons learned during the process, see [Lessons Learned](/findings/lessons-learned.md).

## Remediation

The assessment identified several actions that could reduce the risk of the attack paths demonstrated during the assessment:

- Remove or replace phpTax with a supported and actively maintained web application to eliminate the initial-access vulnerability.
- Review and remove unnecessary SUID permissions from the `find` binary to prevent privilege escalation through the identified misconfiguration.
- Upgrade the Ubuntu operating system to a supported LTS release and maintain regular security updates.

The recommendations are prioritized based on their potential impact and can be found in the detailed [Recommendations document](/remediation/recommendations.md).

## Repository Structure

The repository is organized to separate the assessment methodology, technical evidence, findings, recommendations, and supporting documentation.

```text
red-team-capstone/
├── evidence/
├── exploitation/
├── findings/
├── privilege-escalation/
├── reconnaissance/
├── remediation/
├── methodology.md
├── references.md
└── README.md
```

### Directory and File Overview

- `reconnaissance/` — Documentation and evidence from the initial reconnaissance and service enumeration stage.
- `exploitation/` — Documentation and evidence related to identifying and exploiting the phpTax vulnerability.
- `privilege-escalation/` — Documentation and evidence from the local enumeration and privilege-escalation stages.
- `evidence/` — Supporting evidence collected throughout the assessment.
- `findings/` — Risk assessment and lessons learned from the assessment.
- `remediation/` — Recommendations for addressing the vulnerabilities and misconfigurations identified.
- `methodology.md` — Detailed methodology and assessment process.
- `references.md` — References and external resources used during the assessment.
- `README.md` — Overview of the project, assessment objectives, attack path, findings, and remediation.

## Disclaimer

This project was completed as part of the Red Team Essentials course and capstone assessment provided by WithYouWithMe (WYWM).

The assessment was performed against the intentionally vulnerable virtual machine provided for the course and was conducted for educational and portfolio purposes only.

The contents of `local.txt` and `proof.txt` have not been published to preserve the integrity of the original assessment.

All testing documented in this repository was performed within the intended scope of the provided lab environment.
