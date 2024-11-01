# Chapter 1: Security Basics

## Fundamental Concepts
#### CIA
**Confidentiality**
	Encryption:
		Encryption makes confidential information unreadable by unauthorized people. It can be decrypted by authorized personnel. 
	Access Control:
		==Identification, authentication, and authorization== are the three core identities and access management activates that help ensure only authorized personnel have access to data.
		- Identification: Unique username.
		- Authentication: password.
		- Authorization: grant or restrict access to resources(permissions).
**Integrity**
	Ensures data has not been altered, whether it be unauthorized or unintentional. ==Ensuring data has not been modified, tampered with, or corrupted.== 
	Hashing:
		Hashing techniques can be used to enforce integrity. Simply a hash is an alphanumeric string created by executing a hashing algorithm against data, such as a file or message. Hashing algorithms create a fixed-length, irreversible output. Changing even 1 bit in the data WILL create a whole different hash. By comparing data that was hashed at 2 separate times, you can confirm the integrity of the data. Variations in hashes don't tell you what was modified, only that it has changed. 
**Availability**
	Ensures systems are up and operational. Fault tolerances and redundancies, such as ==RAID, failover clusters, backups, and generators can increase availability.==
	
#### Redundancy and Fault Tolerance
**Redundancy** adds duplication to critical systems and provides fault tolerance. A common goal of fault tolerance and redundancy techniques is to each remove ==single point of failure (SPOF)==.
Common redundancy examples:
-  Disk
		RAID-1 (mirroring), RAID-5 (striping with parity), and RAID-10 (striping with a mirror).
-  Servers
-  Power
-  Networks
		Load balancing uses multiple servers to support a single service. Network interface card (NIC) teaming can provide redundancy support and increased bandwidth.

#### Scalability and Elasticity
Both contribute to availability. **Scalability** is the ability to increase the capacity of your system or services based on demand. ==Horizontal scaling== is adding additional servers. ==Vertical scaling== is the addition of resources (memory, processing power, individual servers, etc.). **Elasticity** automates scalability by having the system add and remove resources as needed. If you pull a rubber band it automatically stretches, and when you let it go, it returns to its original size.

#### Resiliency
**Resiliency** methods help systems heal themselves or recover from faults with minimal downtime. Systems may regularly perform and test full backups, have backup power sources, NIC teaming, or redundant disk. Resiliency expects components to retry failed processes. For example, if you lose Internet and visit google.com, the browser fails. However, when you regain connection the browser automatically recovers and shoes the Google home page.

#### Basic Risk Concepts
**Risk** is the likelihood of a threat exploiting a vulnerability resulting in a loss. A **threat** is any circumstance or event that has the potential to compromise the CIA triad. A **vulnerability** is a weakness in hardware, software, configuration, or even the users operating the system. A **security incident** is an adverse event or series of events that can *negatively* affect the CIA of an orgs IT systems and data. Whether it be intentional attacks, malicious software infections, accidental data loss, and more. **Risk mitigation** reduces the changes that a threat will exploit a vulnerability or the impact that the risk will have on the org if it does occur. You can't stop a tornado, or an attacker from writing malware, however, you can reduce risk by reducing vulnerabilities to the threat or reducing the threats impact.

## Effective Security Controls

**Control categories** describe how the control works. **Control types** describe the goal the control hopes to achieve. 

#### Control Categories
**Technical Controls** use technology such as hardware, software, and firmware to reduce risk.
- Encryption
- Antivirus software
- IDS/IPS
- Firewalls
- Least privilege
**Managerial Controls** primarily administrative in function, typically documented in an orgs security policy and focus on managing risk.
- Risk assessments
- Vulnerability assessments
**Operation Controls** help ensure that the day-to-day operations comply with security policy.
- Awareness and training
- Configuration management
- Media protection
**Physical Controls** physical world, locks on doors, fences, guards, cameras, etc.
- Barricades
- Lighting
- Signs
- Sensors

#### Control Types
**Preventive controls** attempt to prevent an incident from occurring.
- Hardening (defense-in-depth)
- Training
- Security guards
- Account disablement process
- IPS
**Deterrent controls** attempt to discourage individuals from causing an incident. Often describable as preventive controls. 
- Warning signs
- Login banners
**Detective controls** attempt to detect incidents after they have occurred.
- Log monitoring
- Security information and event management (SIEM) systems
- Security audit
- Video surveillance
- Motion detection
- IDS
**Corrective controls** attempt to restore normal operations after an incident occurs.
- Backups and system recovery
- Incident handling processes
**Compensating controls** are alternative controls used when a primary control is not feasible. Temporary solution to an issue. 
- EX: Employees use smart card when authenticating to a system. However, it might take time for new users to receive their smart card. To maintain a high level of security and give the new user access to the network, a ==Time-based One-Time Password (TOTP)== can be implemented as a compensating control.
**Directive controls** instructs individuals on how to handle security situations when they arise. Generally written documents.
- Policies, standards, procedures, and guidelines
	- *Policies* provide high-level goal statements.
	- *Standards* describe how to configure systems, applications, and security controls properly.
	- *Procedures* offer step-by-step guidance on achieving a goal.
	- *Guidelines* offer advice on achieving goals.
- Change management
	- Ensures that changes don't result in unintended outages. Instead of admins making changes whenever they'd like, they submit the change to a change management process. It is an ==operational and directive control==.

## Logging and Monitoring

For the "Log Basics" appendix: https://getcertifiedgetahead.com/

Log entries help admins and security investigators determine what happened, when, where, and who or what did it.

#### Operating System/Endpoint Logs
##### Windows Logs
Windows logs are viewable in the Windows Event Viewer, primary logs are:
- **Security log:** Functions as a security log, an audit log, and an access log. It records *auditable events* such as successes or failures. A success indicates an event completed successfully such as a user logging in, or a file being deleted successfully. A failure means that a user tried to perform an action, but failed. 
- **System log:** Used to record events related to the functioning of the OS. System start up and shut downs, info on services starting and stopping, or drivers loading or failing.
- **Application log:** Records events sent to it by applications or programs running on the system. Any application has the capability of writing events in the Application log ==(Seems like a possible vulnerability, I wonder what the parameters around this are.)== such as warnings, errors, and routine messages.
##### Linux Logs
Linux systems store logs in /var/log. Some logs vary between different versions of Linux. Common logs include:
- **/var/log/syslog** and/or **/var/log/messages:** General system messages logged during startup, relating to mail, the kernel, and other system activities. 
- **/var/log/secure**: Information related to the authentication and authorization of user sessions. 

#### Network Logs
Network logs record traffic on the network. On devices such as routers, firewalls, web servers, IDS/IPSs. Useful when troubleshooting connectivity issues and identifying potential intrusions or attacks.

**Firewall Logs:** Serve as border guards for the network, decide what traffic is allowed to enter and leave the network. Keep track of every attempt to access the network and create detailed logs recording when recording that information.
**IDS/IPS Logs:** Monitor networks for malicious activity. Great source of security log data.
**Packet Captures:** Protocol analyzers (sniffers) capture network traffic allowing the viewing and analyzing of individual packets. Tools like Wireshark can be used to capture network traffic related to an incident that can later be examined to reconstruct what happened.

#### Application Logs
Some applications store log info in system logs, but many applications also manage their own log files. Web servers typically log request to the web server for pages. These often follow the Common Log format standardized by the World Wide Web Consortium (W3C) A typical entry includes the following data:
- **host:** IP address or hostname of the client requesting the page.
- **user-identifier:** Name of user requesting the page (if known).
- **authuser:** User's logon name requesting the page if logged on.
- **date:** Date and time of request.
- **request:** Actual request line sent by the client.
- **status:** HTTP status code returned to the client.
- **bytes:** Byte length of the reply.
##### Metadata
Data that provides information about other data. Many applications store metadata about files and messages that can be helpful in investigations. 
- For example metadata from an email includes detailed information about how the email was routed. 
- Similarly, metadata from image files contain information about the camera, geographic location, date, time, and other details.

#### Centralized Logging and Monitoring (SIEM Systems)
A *security information and event management (SIEM)* system provides a centralized solution for collecting, analyzing, and managing data from systems, applications, and infrastructure devices. It combines the services of security event management (SEM) and security information management (SIM) solutions. 
- **SEM** provides real-time monitoring, analysis, and notification of security events.
- **SIM** provides long-term storage of data, along with methods of analyzing data to look for trends or creating reports.
##### SIEM Application Capabilities
- **Log collectors:** Log data form devices throughout the network and stores these logs in a searchable database.
- **Data inputs:** Log entries from sources such as firewalls, routers, IDS/IPS systems. Also from any system or application the org wants to manage like web servers, proxy servers, or database servers.
- **Log aggregation:** Aggregation refers to combining several dissimilar items into a single similar format. Different systems typically format log entries differently, the SIEM system can aggregate the data and store it so it is easy to analyze and search.
- **Correlation engine:** Software component used to collect and analyze event log data from various systems within the network. Aggregates data looking for common attributes. Detects patterns of potential security events and raises alerts. 
- **Automated reports:** Grouped in different categories such as network traffic event monitoring, device events, threat events, logon/logoff events, compliance, and more are included in SIEM system built-in reports.
- **User behavior analysis (UBA):** UBA watches what users are doing, such as critical files. Looking for who accessed them, what they did, and how frequently they access these files. Looks for abnormal patterns of user activity.
- **Security alerts:** Predefined (or created) alerts that provide continuous monitoring of systems with notifications of suspicious events. EX. If there is a port scan on a server, it might email the admin group.
- **Automated triggers:** An action caused in response to a predefined number of repeated events. EX. There is a trigger of failed logins set to 5. If an attacker repeatedly tries to log on to a server using SSH, when the SIEM detects more than five failed, it can change the environment and stop the attack. It might modify a firewall to block these SSH login attempts or send a script to the server to temporarily disable SSH. 
- **Time synchronization:** Servers sending data to the SIEM should be synchronized with the same time, even if coming from another time zone. An organization could be sending all data from different locations to a centralized SIEM. The Network Time Protocol (NTP) provides a way of keeping system clocks of all devices synchronized.
- **Archiving:** The ability to move older logs offline to cheap storage where they are not immediately accessible, but can be restored. 
##### SIEM Dashboards
Similar to a car dashboard, SIEM dashboards provide administrators with a view of meaningful activity. Common elements are:
- **Sensors:** Agents are placed on systems throughout a network, they collect logs from devices and send these logs to the SIEM system.
- **Alerts:** Alerts are sent out when triggers are set and events occur.
- **Correlation:** As log entries arrive, it correlates and analyzes the data. 
- **Trends:** As the SIEM system is analyzing data it can identify trends. Many system display trends in graphs allowing users to digest a lot of information in a single picture. 

#### Syslog
The *syslog* protocol specifies a general log entry format and the details on how to transport log entries. Any system sending syslog messages are *originators*. They send syslog log entries to a *collector* (a syslog server). The syslog protocol only defines how to ==FORMAT== the syslog messages and send them to a collector. It doesn't define how the syslog server ==HANDLES== these log entries. 

## Chapter 1 Practice Questions
1.  C
2.  B
3.  A
4.  A
5.  D
6.  C
7.  D
8.  A
9.  B
10. A: Technical **(D):** Managerial because vulnerability assessments are an assessment method used to reduce risk and are an example of a managerial control. You could argue that since they use vulnerability scanners they are also an example of a technical control. The clue is that there is no mention of the technology being used to complete the assessments, and there is a focus on policy and procedure. Also remember the difference between control *type* and control *category*. Vulnerability assessment is detective, but detective is a control *type*. The question is asking about the control *category*.
11. C
12. D
13. B
14. A
15. D 
