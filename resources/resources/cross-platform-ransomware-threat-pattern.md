---
title: Cross-Platform Ransomware Threat Pattern
layout: col-sidebar
tags: threatmodeling
---

> **Status:** Proposed Threat Pattern  
> **AI Transparency:** AI was used for wording and structure; content reviewed by the contributor.

## Threat Pattern (STRIDE: Tampering / Denial of Service)

An attacker gains access to an environment through compromised credentials, exposed remote services, or other initial access methods. The attacker then deploys ransomware that encrypts data across multiple systems, potentially affecting different operating systems and connected storage resources.

---

## Why This Matters for Threat Modeling

Threat models should consider dependencies between applications, servers, and shared storage, rather than treating systems in isolation:

- Initial access conditions  
- Identity and privilege boundaries  
- Lateral movement opportunities  
- Critical data and service dependencies  
- Availability impact and recovery requirements  

This helps practitioners evaluate not only the final impact of ransomware, but also the conditions that allow the attack to progress.

---

## Attack Scenario

1. An attacker obtains access through compromised credentials or an exposed remote access service.  
2. The attacker uses available privileges and access paths to reach additional affected systems.  
3. Ransomware is deployed to encrypt application data and connected storage resources.  
4. Critical services become unavailable due to loss of data availability.

---

## Mitigations

- Require multi-factor authentication for remote access and privileged accounts.  
- Disable unnecessary remote services and protect required remote services with appropriate access controls.  
- Apply least privilege to limit the impact of compromised accounts.  
- Segment networks and restrict unnecessary communication between systems.  
- Monitor authentication activity and suspicious changes to critical systems.  
- Maintain regular, offline, and tested backups to support recovery.

---

## References

- **MITRE ATT&CK – Data Encrypted for Impact (T1486)**  
  https://attack.mitre.org/techniques/T1486/  
  Supports the use of data encryption as an impact technique.

- **MITRE ATT&CK – Valid Accounts (T1078)**  
  https://attack.mitre.org/techniques/T1078/  
  Supports attacker use of legitimate credentials for access.

- **MITRE ATT&CK – Remote Services (T1021)**  
  https://attack.mitre.org/techniques/T1021/  
  Supports attacker use of remote services for access and movement.

- **CISA – Stop Ransomware**  
  https://www.cisa.gov/stopransomware  
  Supports ransomware mitigation practices including MFA, access controls, segmentation, monitoring, and backups.

- **NIST SP 800-61 Rev. 3 – Incident Response Recommendations and Considerations**  
  https://csrc.nist.gov/pubs/sp/800/61/r3/final  
  Supports incident response preparation, containment, and recovery considerations.
