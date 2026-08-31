# Recommendations

Based on the vulnerabilities and attack paths identified during the assessment, the following recommendations are advised.

## 1. Remove or Replace the phpTax Web Application

The phpTax web application should no longer be used. The phpTax project was last updated in February 2013 and is no longer actively maintained. The application also contains publicly documented vulnerabilities, including the remote code execution vulnerability exploited during this assessment. [CVE-2012-10037](https://nvd.nist.gov/vuln/detail/CVE-2012-10037).

During this assessment, the vulnerable phpTax application was used as the initial entry point to obtain remote code execution on the target system. Removing the application, or replacing it with a supported and actively maintained alternative, would eliminate this attack path.

Priority: Critical

## 2. Secure the `find` Binary

The permissions and configuration of the `find` binary should be reviewed and corrected to prevent it from being abused for privilege escalation.

During the assessment, the `find` binary was identified as a potential privilege-escalation path. Its permissions should follow the principle of least privilege, and unnecessary special permissions should be removed.

Priority: High

## 3. Upgrade and Maintain the Ubuntu Operating System

At the time the original lab was created, Ubuntu 18.04 LTS was still within its standard support life-cycle. However, Ubuntu 18.04 reached the end of standard security support on May 31, 2023. At the time of this assessment, the system was therefore running an operating system that was no longer receiving standard security updates.

[Ubuntu 18.04 LTS Standard Support](https://ubuntu.com/blog/18-04-end-of-standard-support)

The system should be upgraded to a currently supported Ubuntu LTS release. Security updates should also be applied regularly after the upgrade to ensure that the operating system and installed software remain protected against known vulnerabilities.

Priority: High
