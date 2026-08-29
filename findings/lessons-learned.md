# Lessons Learned

This assessment helped me understand that identifying a vulnerability and successfully exploiting it are two different parts of the penetration-testing process.

## Exploit Research and Validation

During the assessment, I found three SearchSploit results related to the phpTax vulnerability. I tested the available exploit options, but two of them did not successfully exploit the target, even though they were associated with the same underlying vulnerability. The corresponding Metasploit module, however, was successful.

I did not determine exactly why the other exploit implementations failed while the Metasploit module worked. However, this taught me that finding a matching vulnerability or exploit does not guarantee that every available exploit implementation will work against a particular target. Exploits may differ in their implementation, requirements, payload handling, or compatibility with the target environment.

## Understanding SUID Privilege Escalation

The second major lesson came from the local enumeration stage. After discovering that the `find` binary had SUID privileges, I initially thought that I would need to use the binary to access `/etc/shadow` and then crack the root user's password hash.

I later learned that this was not necessary. A SUID binary can sometimes be abused directly to execute commands with the privileges of its owner. In the case of `find`, GTFOBins provided a technique for using the SUID-enabled binary to obtain a root shell.

This also taught me how to use GTFOBins more effectively. When I initially looked up `find`, I did not know how the SUID configuration could be used for privilege escalation. The relevant technique was listed under the SUID section, which was something I did not initially recognize or look for.

Overall, the assessment taught me to investigate not only what a vulnerability or misconfiguration is, but also how it can actually be used in the context of the target system.## Lessons Learned

This assessment demonstrated the importance of evaluating vulnerabilities as part of a complete attack path rather than considering each issue in isolation.

The initial web application vulnerability provided remote access to the system, but the compromise would not have reached root-level access without the insecure SUID configuration. This highlighted the importance of performing thorough local enumeration after obtaining an initial foothold.

The assessment also reinforced the value of researching potential attack techniques when a suspicious configuration is identified. In this case, identifying the SUID-enabled find binary during enumeration led to further investigation and ultimately demonstrated that it could be used for privilege escalation.

Finally, the assessment showed the importance of documenting both successful and unsuccessful steps. Failed exploit attempts provided useful information that helped narrow the investigation and eventually led to the successful phpTax exploitation path.
