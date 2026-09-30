# Volt Typhoon: IT/OT Threat analysis
Microsoft (2023) describes Volt Typhoon as a state-sponsored threat actor based in China that has been active since mid-2021. Volt Typhoon targets critical infrastructure (National Security Agency, 2025).
The major question is how this group has managed to remain active since 2021 while maintaining access to U.S. infrastructure. 

## Attack Chain
### 1. Initial Access
Volt Typhoon initially gains access by targeting organizations via Fortinet FortiGuard devices (Microsoft, 2023). 
This aligns with the MITRE ATT&CK framework’s “Initial Access” tactic, specifically technique T1190, “Exploit Public-Facing Application” whereby actors compromise networks by exploiting known vulnerabilities accessible from the internet (MITRE ATT&CK, 2025). 
They have exploited devices from various vendors, including Fortinet, Ivanti, NETGEAR, Citrix, and Cisco (MITRE ATT&CK, 2025). 
They maintain a foothold through "Living off the Land" (LotL) attacks, using existing system tools to gain access rather than relying on malware (Anson, 2020, p. 322).
### 2. Credential Access
After compromising the system and establishing a foothold, Volt Typhoon uses the "Credential Access" tactic to gain access to user accounts (Microsoft, 2023). 
They use the "OS Credential Dumping" technique (T1003), specifically the sub-techniques "LSASS Memory" (T1003.001) and "NTDS" (T1003.003) (MITRE ATT&CK, 2025). 
Microsoft (2023) documents that Volt Typhoon uses Base64-encoded commands for LSASS memory dumps and the Windows tool `ntdsutil` to copy password-containing files from compromised domains, enabling them to regain access should they lose it. 
This grants them access without resorting to brute force attacks, allowing them to fly under the radar by logging in as legitimate users.
### 3. Discovery
Next, they use the "Discovery" tactic to gather information about the system after gaining access (Microsoft, 2023). In doing so, they use several techniques, such as "System Information Discovery" (T1082) and "Remote System Discovery" (T1018) (MITRE ATT&CK, 2025). 
Various Windows commands, such as `ping`, are used to locate other machines on the network.
### 4. Collection
The next tactic is TA0009 Collection (MITRE ATT&CK, 2025). The techniques used include T1005 Data from Local System and T1056.001 Input Capture: Keylogging (MITRE ATT&CK, 2025); these are linked to the credential dumping technique, as the gathered information can be used later. 
They create files to capture keystrokes from legitimate users and package the data into password protected files (MITRE ATT&CK, 2025).
### 5. Command and Control
The final tactic Volt Typhoon relies on is Command and Control (Microsoft, 2023). This involves several techniques, primarily T1090 Proxy whereby they abuse compromised devices as proxies (such as FRP/Fast Reverse Proxy) to route traffic (MITRE ATT&CK, 2025). 
Volt Typhoon’s primary approach is "Living off the Land" (LotL): they log in using legitimate user accounts, use proxies to mask network traffic, and use native system tools such as PowerShell to evade detection (CISA, 2023, AA23-144A).

## From IT to OT
This type of threat actor can affect critical infrastructure in Norway in the same way described in the CISA report. According to CISA (CISA, 2024, AA24-038A), Volt Typhoon has compromised several critical infrastructure sectors, such as energy, transportation, communications, and water systems. 
CISA reports that they initially gain a foothold by exploiting vulnerabilities in IT environments with the goal of being able to move into OT systems. 
OT (Operational Technology) refers to systems that control physical processes such as power grids, water systems, and transportation (CISA, 2023). 
The interplay between IT and OT environments can create a significant challenge when threat actors gain access through vulnerable IT environments that communicate with OT systems.

## Mitigations
In accordance with the NSM’s fundamental principles for ICT security (NSM, 2024), the following technical and organizational measures can help detect, mitigate, and manage the risk of compromise.
### Control Data Flow (NSM 2.5)
To prevent lateral movement between networks and systems, implement measure 2.5: control data flow. This involves segmenting communication between networks so that only authorized devices and services can communicate with one another, and ensuring that particularly critical services have their own dedicated data flow. 
It is important because it limits how far an attacker gets if they have already compromised a system. For instance, segmentation can stop an attacker from moving from IT to OT.
### Secure Configuration (NSM 2.3)
Maintain secure configurations, measure 2.3 (NSM, 2024). Configure systems by removing unnecessary functions. 
Configurations should be reviewed regularly, and system updates performed promptly to prevent attackers from exploiting known vulnerabilities.
### Access Control (NSM 2.6)
Manage access control, measure 2.6 (NSM, 2024). Access controls should be implemented for all users. Attackers often gain control by accessing the system through legitimate users and attempting to escalate privileges. Review all system users and restrict access and system rights based on their roles within the organization. 
Additionally, identify inactive users and immediately revoke their system access. 
### Incident Management (NSM 4.3)
By following section 4.3 on incident management (NSM, 2024), the organization learns how to handle incidents and halt their spread, while also gaining insights from these experiences to train employees and improve procedures. 
This is a crucial method for raising employee awareness and providing thorough training, thereby increasing understanding of the types of incidents that can occur within the organization.
## Geopolitical
The geopolitical situation and the current intelligence threat landscape significantly impact national cybersecurity. State-sponsored activities, such as attacks on critical infrastructure, compel nations to better protect vital systems and plan for risk management. 
Attackers can operate from countries where they face no repercussions, such as the Chinese group Volt Typhoon. The use of AI makes attacks more sophisticated and rapid, allowing them to spread quickly across multiple systems. 
This underscores the importance of international cooperation. Consequently, national defence strategies must focus on regularly updating security measures, maintaining readiness to respond swiftly to incidents, and collaborating with other nations and organizations to halt threats before they result in severe consequences (Microsoft, 2025).

In conclusion, Volt Typhoon has managed to remain active and stay hidden because they use legitimate accounts, the systems own tools (LotL) and proxies.
## References
- Anson, S. (2020). Applied Incident Response. Wiley.
- CISA. (2023). People's Republic of China state-sponsored cyber actor living off the land to evade detection (AA23-144A). 
https://www.cisa.gov/news-events/cybersecurity-advisories/aa23-144a
- CISA. (2023, June 8). Foundations of OT cybersecurity: Asset inventory guidance for owners and operators. 
https://www.cisa.gov/resources-tools/resources/foundations-ot-cybersecurity-asset-inventory-guidance-owners-and-operators
- CISA. (2024). PRC state-sponsored cyber actors exploiting management interfaces and accessing critical infrastructure organizations (AA24-038A). 
https://www.cisa.gov/news-events/cybersecurity-advisories/aa24-038a
- Microsoft. (2023, May 24). Volt Typhoon targets US critical infrastructure with living-off-the-land techniques. 
https://www.microsoft.com/en-us/security/blog/2023/05/24/volt-typhoon-targets-us-critical-infrastructure-with-living-off-the-land-techniques/
- Microsoft. (2025). MDDR 2025: Government Executive Summary. 
https://cdn-dynmedia-1.microsoft.com/is/content/microsoftcorp/microsoft/msc/documents/presentations/CSR/MDDR-2025-Government-Executive-Summary.pdf
- MITRE ATT&CK. (2025). T1003.001: OS Credential Dumping: LSASS Memory. https://attack.mitre.org/techniques/T1003/001/
- MITRE ATT&CK. (2025). T1003.003: OS Credential Dumping: NTDS. https://attack.mitre.org/techniques/T1003/003/
- MITRE ATT&CK. (2025). T1005: Data from Local System. https://attack.mitre.org/techniques/T1005/
- MITRE ATT&CK. (2025). T1018: Remote System Discovery. https://attack.mitre.org/techniques/T1018/
- MITRE ATT&CK. (2025). T1056.001: Input Capture: Keylogging. https://attack.mitre.org/techniques/T1056/001/
- MITRE ATT&CK. (2025). T1082: System Information Discovery. https://attack.mitre.org/techniques/T1082/
- MITRE ATT&CK. (2025). T1090: Proxy. https://attack.mitre.org/techniques/T1090/
- MITRE ATT&CK. (2025). T1190: Exploit Public-Facing Application. https://attack.mitre.org/techniques/T1190/
- MITRE ATT&CK. (2025). TA0009: Collection. https://attack.mitre.org/tactics/TA0009/
- MITRE ATT&CK. (2025). Volt Typhoon (G1017). https://attack.mitre.org/groups/G1017/
- National Security Agency. (2025, August 27). NSA and others provide guidance to counter China state-sponsored actors targeting critical infrastructure organizations. 
https://www.nsa.gov/Press-Room/Press-Releases-Statements/Press-Release-View/article/4287371/
- NSM. (2024). NSMs grunnprinsipper for IKT-sikkerhet (v2.1). 
https://nsm.no/getfile.php/1313975-1717589722/NSM/Filer/Dokumenter/Veiledere/NSMs%20Grunnprinsipper%20for%20IKT-sikkerhet%20v2.1.pdf
