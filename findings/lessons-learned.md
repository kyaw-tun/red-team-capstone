## Lessons Learned

This assessment demonstrated the importance of evaluating vulnerabilities as part of a complete attack path rather than considering each issue in isolation.

The initial web application vulnerability provided remote access to the system, but the compromise would not have reached root-level access without the insecure SUID configuration. This highlighted the importance of performing thorough local enumeration after obtaining an initial foothold.

The assessment also reinforced the value of researching potential attack techniques when a suspicious configuration is identified. In this case, identifying the SUID-enabled find binary during enumeration led to further investigation and ultimately demonstrated that it could be used for privilege escalation.

Finally, the assessment showed the importance of documenting both successful and unsuccessful steps. Failed exploit attempts provided useful information that helped narrow the investigation and eventually led to the successful phpTax exploitation path.
