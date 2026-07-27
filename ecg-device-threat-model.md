# ECG Threat Model (Lightweight Example)

**Category:** Medical Device Threat Modeling  
**Methodology:** STRIDE  
**Audience:** Security practitioners, developers, and threat modeling learners

## Purpose/Disclaimer
The purpose of this light version threat model is to demonstrate how STRIDE can be applied to an ECG device. It is intended for OWASP readers learning system decomposition and threat modeling techniques. The example includes a simplified set of components, threats, and mitigations for educational purposes and is not intended to represent a comprehensive medical device cybersecurity assessment or any regulatory submission.

## Assumption
This example models a typical ECG device, which may include network connectivity in a clinical environment.

## Trust Boundaries
Trust boundaries exist between the ECG device, hospital network, and external clinical systems.

## System Definition
ECG is the abbreviation for an Electrocardiogram. It is used to detect electrical activity of the heartbeat in the form of P wave, QRS complex and T wave to identify and diagnose irregularities in heartbeat. Electrodes are placed on patient’s limbs and chest to measure the electrical potentials. It translates tiny electrical signals into digital wave patterns. These waveforms are used by the doctors to evaluate the heart rhythm and check for cardiac damage.

## Components
- Electrodes  
- Lead wires  
- Amplifier and filters  
- Analogue-to-Digital Converter (ADC)  
- Main processing unit  
- Display/printer  
- Local storage  
- Network interface (Ethernet/Wi-Fi/Bluetooth), if supported  

## Data Flow Diagram
Electrodes → Lead wires → Amplifier and filters → Analogue-to-Digital Converter (ADC) → Main processing unit → Display / Printer / Local storage / Network interface (if supported) |TRUST BOUNDARY| → Electronic Health Record (EHR) / Clinical Information System

## STRIDE Threats

### Spoofing
**General:** Spoofing is the act of impersonating a legitimate user, device, or system to gain unauthorized access to resources or services. Violates authentication.  
**ECG:** An attacker may impersonate an authorized clinician, connected medical device, or trusted clinical system to gain unauthorized access to the ECG device or associated patient data.

### Tampering
**General:** Tampering is the unauthorized manipulation of data, software, firmware, or system configuration. Violates integrity.  
**ECG:** Manipulation of ECG signals, configuration, firmware, or stored ECG data which may lead to false-negative or false-positive diagnoses, thereby leading to incorrect medication or delayed care.

### Repudiation
**General:** Repudiation occurs when users deny performing actions due to unavailability of sufficient audit evidence. Violates non-repudiation.  
**ECG:** Insufficient audit logs prevent accountability for configuration changes or user actions.

### Information Disclosure
**General:** Information Disclosure is the unauthorized exposure of confidential or sensitive information. Violates confidentiality.  
**ECG:** Insecure storage or communication may expose ECG data or patient identifiers.

### Denial of Service
**General:** Denial of Service prevents a system from performing its intended function by making its resources or services unavailable. It may result from resource exhaustion, software crashes, hardware failures, protocol abuse, or malicious requests. Violates availability.  
**ECG:** Device or network disruption prevents ECG acquisition, processing, or monitoring.

### Elevation of Privilege
**General:** Elevation of Privilege occurs when an attacker gains permissions beyond those originally assigned. Violates authorization.  
**ECG:** Attackers obtain unauthorized administrative or firmware-level access.

## Mitigations
(Aligned with OWASP Threat Modeling cheat sheet, OWASP Threat Modeling project resources, NIST SP 800-53 Rev. 5, ISO/IEC 27001)

- Recommend strong authentication and role-based access control  
- Data encryption in transit and at rest  
- Secure boot and digitally signed firmware  
- Verification of integrity for firmware and stored ECG data  
- Audit logging for user access and configuration changes  
- Disable unnecessary services and interfaces  
- Segmentation of network for connected ECG devices  
- Authenticated and integrity-protected software updates  
- Monitoring for abnormal access or device behavior  

## Validation Checklist
- All system components and data flows are identified  
- Each STRIDE category is represented by at least one relevant threat  
- Every threat has a corresponding mitigation  
- Security controls are feasible for typical ECG devices  
- Patient safety impacts have been considered  
- Threats and mitigations are internally consistent  

## References
- OWASP Threat Modeling Cheat Sheet  
- OWASP Threat Modeling Project  
- NIST SP 800-53 Rev. 5  
- ISO/IEC 27001  
- MITRE Playbook for Threat Modeling Medical Devices  
