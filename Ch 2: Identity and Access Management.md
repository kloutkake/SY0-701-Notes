# Chapter 2: Identity and Access Management

## Authentication Management
**Authentication** proves an identity with some sort of credentials. **Identification** occurs when users make a claim about their identity with unique identifiers. Other forms of authentication techniques are based on something you know, something you have, something you are, and somewhere you are. 
==Authentication is not limited to people.== Services, processes, workstations, servers, and network devices all use authentication to prove their identities. 

### Comparing Identification and AAA
**Authentication, authorization, and accounting (AAA)** work together with identification to provide a comprehensive access management system. After identity is proven, **authorization** is grated to access resources ==based on their proven identity.== Just because identity is proven, doesn't mean they are automatically granted access to all resources. **Accounting** methods track user activity and record the activity in logs. For example audit logs track activity, and admins use these to create an *audit trail* to allow security processionals to re-create the event that preceded a security incident.
Effective access control starts with strong authentication mechanisms, such as robust passwords, smart cards, digital certificates, or biometrics. 

### Comparing Authentication Factors
The four authentication factors described by CompTIA are: 
- **Something you know** such as a password or personal identification number (PIN).
- **Something you have** such as a smart card, a phone, or a USB token.
- **Something you are** such as a fingerprint or other biometric identification.
- **Somewhere you are** such as your home or office.
Most cybersecurity professionals recognize three types of authentication factors: something you know, something you have, and something you are. Location is not a strong authentication factor by itself. If someone is in my office, is that proof they are me? Location-based authentication is typically paired with another factor for added assurance. 

#### Something You Know
This authentication factor typically refers to a *shared secret*, like a password or PIN. It is the ==LEAST== secure form because knowledge can be stolen. NIST SP 800-63B, "Digital Identity Guidelines", recommends users create easy-to-remember and hard-to-guess passwords. Consider the following NIST, Microsoft, and U.S. DHS' current password recommendations: 
- Hash all passwords.
- Require MFA.
- Don't require mandatory password resets.
- Require passwords to be at least eight characters.
- Check for common passwords and prevent their use.
- Tell users not to use the same passwords on more than one site.
- Allow all special characters, including spaces, but don't require them.
##### Password Length and Complexity
The longer the password, the harder it is to guess. A one character password that was lowercase has 26 possible passwords. Add another lowercase letter it goes to *26 * 26 = 676* possible passwords. An eight-character password consisting of only lowercase letters has over ==200 billion== possible values.
Password complexity policies require that passwords contain several different types of characters, which increases the number of possible values for each character of the password. The four common character types include:
- Uppercase characters
- Lowercase characters
- Numbers
- Special characters
##### Password Expiration/Age
These days the best practice for password security is ==NOT== to have password expiration polices. This is based upon the idea that users are more likely to use strong, secure passwords if they don't need to keep changing them. This advice is only true if the organization is using multifactor authentication.
##### Password History and Password Reuse
A **password history** system remembers past passwords and prevents users from reusing them. Often when using password history there is a minimum password age setting. This prevents people from changing their password over and over again to fulfill the limit, and end up back at their original password. 
##### Password Managers
A password manager or vault is a single source designed to keep most your passwords. Instead of remember all your passwords, you just need to remember the password to your vault. The vault keeps the passwords encrypted. 
##### Knowledge-Based Authentication 
There are two types of **knowledge-based authentication (KBA)**, Static KBA and dynamic KBA.
**Static KBA** is typically used when you forgot your password. You are prompt with questions about yourself that you will have to answer later in-order to restore your password.
**Dynamic KBA** identifies individuals without an account. Organizations use this for high-risk transactions. The site queries public and private data sources like credit reports, vehicle registrations, and property records. It then crafts multiple-choice questions that only the use would know. It often includes answers similar to the real answer to deter attackers. There are typically time limits on the questions.
Knowledge-based authentication is also used to confirm new users identities. This is called *identity proofing*. Identity proofing is an important step in the *provisioning* process that creates accounts for new users as they join an organization. 
##### Implementing Account Lockout Policies
Accounts typically have lockout policies preventing users from guessing passwords. Two key phrases associated with account lockout policies on Microsoft systems are:
- **Account lockout threshold** which is the maximum number of times the wrong password can be entered. 
- **Account lockout duration** which is how long the account remains locked.
##### Changing Default Passwords
A basic security practice is to change the default password that some systems and devices come with before connect to the network. Many wireless routers have default accounts named "admin" or "administrator" with the default passed of "admin". Changing defaults also includes changing the default name of the Administrator account. Many Administrator accounts ==CAN NOT== be locked through regular lockout policies, an attacker could take advantage of that. 
##### Training Users About Password Behaviors
Pretty self-explanatory, but some users don't understand the importance or potential damage of giving out their password, creating strong passwords, or not using the same password with other systems. 
It's important to remember that "123456" frequently appears on lists as the most common password in use. A little training can go a long way.

#### Something You Have
This authentication factor refers to something you can physically hold. Common items are smart cards, security keys, software tokens, and hardware tokens. 
##### Smart Card Authentication
Very similar to credit cards, smart cards are credit card-sized cards with embedded microchips and a certificate. Smart card readers read the card's information, which provides certificate based authentication. 
Covered more later, **certificates** are digital files that support cryptography. The embedded certificate allows for complex encryption.
Smart cards are often paired with a PIN, combining *something you know* with *something you have*.
Requirements for a smart card are:
- **Embedded certificate:** Holds a user's private key that matches with their public key.
- **Public Key Infrastructure (PKI):** Supports issuing and managing certificates. 
##### Security Keys
Electronic device about the size of a remote key for a car. Contains cryptographic information used to complete the authentication process.
##### Hard Tokens
A hard token (or hardware token) is an electronic device about the size of a remote key for a car. Includes a liquid crystal display (LCD) that displays a number on the screen. The number is known as a **one-time password (OTP)**, it is provided to the authentication server to prove they currently have possession of the token.
##### Soft Tokens
A soft token (or software token) is an application that runs on a user's smartphone and generates one-time passwords, similar to hard tokens. Ex. Google Authenticator app.
###### HOTP and TOTP
How do hard and soft tokens know what numbers to display? How does the remote authentication server know what numbers are displaying on the tokens? Especially because the tokens don't have to be connected to a network, or even communicate with the authentication server. Simply put, two shared private keys, with a changing algorithm based on a factor. The two factors are as follows:
**HMAC-based One-Time Password (HTOP):** HTOP is an algorithm that changes the token code ==based upon a moving counter==. Each time the code is used, both the authentication server and the token use the algorithm with a shared secret key to generate the next code. Often HTOP devices require the user to press a button to generate the next password.
**Time-based One-Time Password (TOTP):** TOTP is an algorithm that changes the token code ==based upon the current time==. TOTP tokens codes often change automatically every 30-60 seconds. 
##### SMS/Push Notifications
*Short Message Service (SMS)* is used to send one-time passwords to user's phones. NIST SP-800-63B discourages SMS for two-step authentication and points out several vulnerabilities. Devices can be stolen, or attackers could hijack your phone number to reroute the text message to their own device. *Push notification* send a message to users on another device but instead of including a code, they ask the user to acknowledge the request on their phone. 

#### Something You Are
This authentication factor uses biometrics. **Biometrics** measure some physical characteristic of the user to confirm their identity. Often considered the strongest form of authentication.
##### Biometric Methods
- **Fingerprints:** Many laptop computers, tablet devices and smartphones include fingerprint scanners or fingerprint readers. They are store multiple fingerprints. 
- **Vein matching:** Systems identify individuals using near-infrared light to view their vein patterns. Most vein recognition systems measure veins in an individuals palm, because there are more veins in the palm than the finger. 
- **Retina imaging:** The retina of one or both eyes are scanned and the pattern of blood vessels at the back of the sys are used for recognition. Some will not sure retina scanners because the scan can identify certain medical issues, and you typically need to make physical contact with the scanner.
- **Iris scanners:** Infrared camera technology is used to capture the unique patterns of the iris around the pupil. Used in many passport-free border crossings. They can take pictures from about 3 to 10 inches away. 
- **Facial recognition:** Systems identify people based on facial features. Size, shape, and position of their eyes, nose, mouth, cheekbones, and jaw are used. 
- **Voice recognition:** Identifies individuals based on the way they speak. Differences in the mouth and throat, and behavioral patterns affect speaking style, which cause voices to vary from one another. 
- **Gait analysis:** Identifies individuals based on the way they walk or run. It measures how someone's feet hit and leave the ground while walking. Some methods focus on feet, knees, and hips. Others examine silhouette sequences of individuals for identification. However, a person can change their gait intentionally, like adding a limp. Fingerprints or iris cannot be changed at will.
##### Biometric Efficacy Rates
*Efficacy rates* refer to the performance of the system under ideal conditions. If a system is implemented correctly, it can be very exact. However, if it isn't implemented correctly, its real-world effectiveness may not match the *efficacy rate*. 
Four possibilities when a biometric system tries to authenticate a user:
- **False acceptance:** System incorrectly identifies unknown user as a registered user. The *false acceptance rate (FAR)* identifies the percentage of times false acceptance occurs. 
- **False rejection:** System incorrectly rejects a registered user. The *false rejection rate (FRR)* collects percentage of false rejections.
- **True acceptance:** System correctly identified a registered user.
- **True rejection:** System correctly rejected an unknown user.

|                 | Biometric System Not Accurate | Biometric System Accurate |
| --------------- | ----------------------------- | ------------------------- |
| Registered User | **False Acceptance**          | True Acceptance           |
| Unknown User    | **False Rejection**           | True Rejection            |

Biometric systems allow for the sensitivity or threshold level where errors occur to be adjusted. Increased sensitivity decreases the number of false matches and increases the number of false rejections. Reducing sensitivity increases false matches and decreases false rejections. 
#### Somewhere You Are
This authentication attribute identifies a user's ==location==. Geolocation is a group of technologies used to identify a user's location. Many systems use the IP address for geolocation. IP provides information of country, region, state, city, and sometimes even the zip code.
This authentication attribute can also be used to identify *impossible travel time* or risky login situations. MAC addresses can also be used to for the somewhere you are factor.
It is worth noting that using an IP address for geolocation isn't foolproof. VPNs can be used to change ones IP. 

#### Two-Factor and Multifactor Authentication
Sometimes called dual-factor authentication, two authentication factors are used: *something you have* and *something you know*, or *something you know* and *something you are*. Examples:
- A soft token (something you have) and a password (something you know)
- A fingerprint (something you are) and a PIN (something you know)
- A security key (something you have) and a retinal scan (some you are)
Using two methods of authentication in same ==same factor== is ==NOT== two-factor authentication. 
#### Password-less Authentication
Considering users dislike passwords, and they are one of the least secure ways to authenticate, many organizations are trying to ==get rid of them==. 

### Authentication Log Files
**Authentication log files** can track both successful and unsuccessful login attempts. Most important to monitor login activity for privileged accounts. Common to send entries from authentication logs to a SIEM for analysis. 

Log entries help administrators determine what happened, when it happened, where it happened, and who or what did it. For authentication log entries:
- **What** happened is either a login success or failure
- **When** it happened is determined by the time and data stamps
- **Where** it happened is typically an IP address or computer name
- **Who** or **what** did it refers to the user account

## Managing Accounts
**Account management** is concerned with creating, managing, disabling, and terminating accounts. Access controls are used to control what users can do on an active account. It is important to remember new accounts only need permissions to perform their job, and no more *(least privilege)*. 
### Credential Policies and Account Types
**Credential policies** define login policies for different personnel, devices, and accounts. Different types of accounts need different types of credential policies. Example of different account types and credential policies associated with each:
- **Personnel or end-user accounts:** Appropriate privileges are assigned based on the user's job responsibilities. This policy could define things like the minimum password length, password history, and account lockout policies. 
- **Administrator and root accounts:** This accounts are privileged beyond regular users. Stronger authentication methods like multifactor authentication, and privileged access management techniques are needed to protect these accounts.
- **Service accounts:** Some applications and services need to run under the context of an account, and a service account fills this need. As an example, SQL Server is a database application that runs on a server, and it needs access to resources on the server and the network. Admins create a regular user account, name is something like sqlservice, assign it appropriate privileges, and configure SQL Server to use this account. Passwords should be long, complex, and should ==NEVER== expire, or else the account can no longer log on, and the service or application will stop.
- **Device accounts:** Computers and other devices also have accounts though it isn't always apparent. Microsoft AD only allows users to log on to computers joined to the domain. 
- **Third-part accounts:** Accounts from external entities that have access to a network. An example is security applications that have administrative access to a network. 
- **Guest accounts:** Windows includes a guest account, it is useful if you want to grant someone limited access to a computer or network without creating a new account. 
- **Shared and generic account/credentials:** An organization can create a regular user account that temporary workers will share. 
### Privileged Access Management
**Privileged access management (PAM)** allows an organization to apply more stringent security controls over accounts with elevated privileges, such as administrator or root-level accounts. PAM implements the concept of *just-in-time permissions*.In other words, administrators don't have administrative privileges until they need them. When they need them, their account send a request for the elevated privileges. After a pre-set time, the account is automatically removed from the group, revoking the elevated privileges. Some capabilities of PAM are:
- Allow users to access the privileged account without knowing the password
- Automatically change privileged account passwords periodically
- Limit the time users can use the privileged account
- Allow users to check out credentials
- Log all access of credentials
#### Requiring Administrators to Use Two Accounts
One account for day-to-day work, same limited privileges as a regular end user. Another account with elevated privileges for admin work. This reduces risk for various reasons such as forgetting to lock your computer, or malware. 
#### Prohibiting Shared and Generic Accounts
If multiple users share a single account, you cannot implement basic authorization controls. 
#### Deprovisioning
**Deprovisioning** is the process used to disable a user's account when they leave the organization. Disabled is preferred over deleting the account, at least initially. Some accounts have encryption and security keys associated with them. 
#### Time-based Logins
**Time-based logins** (sometimes referred to as time-of-day restrictions) ensures that users can only log on to computers during specific times. If a user tries to log on to a system outside the restricted time, the system denies access to the user. 
#### Account Audits
An **account audit** looks at the rights and permissions assigned to users and helps enforce the least privilege principle. The audit identifies the privilege grated to the users and compares it against what the user needs. It can detect *privilege creep*, a common problem that violates the principle of least privilege. It occurs when privileges are added to a user due to changing job requirements, but unneeded privileges are not removed. 
**Attestation** is the formal process for reviewing user permissions. The process involves managers reviewing each user permission and certifying that those permissions are necessary to carry out the user's job responsibilities. 
## Comparing Authentication Services
### Single Sign-On
**Single sign-on (SSO)** refers to a user's ability to log on once and access multiple systems without logging on again. SSO increases security because the user only needs 1 set of credentials and are less likely to write them down. The power off SSO systems lies in their interoperability with many devices/systems/apps/services. 
#### LDAP
**Lightweight Directory Access Protocol (LDAP)** is a core component of many SSO systems. It allows users and applications to retrieve information about users from the organization's directory. Windows domains use LDAP to handle queries for information from Active Directory. 
#### SSO and a Federation
Some SSO systems can connect authentication mechanisms from different environments, such as different OSs' or different networks. A **federation**requires a federated identity management system that all members of the federation use. EX: A towing company wants to establish a relationship with an apartment complex. You can create a federation of the two networks, and each organization can login with their respective accounts and access the shared resources. This eliminates the need for and management of two separate accounts on different networks. 
#### SAML
**Security Assertion Markup Language (SAML)** is an *Extensible Markup Language(XML)*-based data format used for SSO on web browsers. If an organization trust each other, they can use SAML as a federated identity management system. This eliminates the need for two different sets of credentials on two different websites hosted by two different organizations. 
SAML defines three roles:
- **Principal:** Typically a user
- **Identity provider:** AN idP creates, maintains, and manages identity information, authentication, and authorization for principals. 
- **Service provider:** Entity that provides services to principals. 
This process sends several XML-based messages between the systems. 
##### SAML and Authorization
SSO does not provide authorization, the primary purpose of it is for the identification and authentication of users. 
### OAuth
**OAuth** is an open standard for authorization that many companies use to provide secure access to protected resources. It ==allows users be granted access to something== without having to disclose their login credentials. 
## Authorization Models
Access control ensures that only authenticated and authorized entities can access resources. Some authorization models we see are:
- *Role-based access control*
- *Rule-based access control*
- *Discretionary access control (DAC)*
- *Mandatory access control (MAC)*
- *Attribute-based access control (ABAC)*
Each authorization model makes it easier to apply access policies to users within a network. Often, you'll run across the following terms:
- **Subjects:** Users or groups that access an object. Occasionally a service that is using an account to access an object.
- **Objects:** Items such as files, folders, shares, and printers that subjects access. The access control scheme determines how systems grants authorization to objects. Or, how a system grants users access to files and other objects.
#### Role-Based Access Control
**Role-BAC** uses roles to manage rights and permissions for users. This is useful for users with who perform the same job functions. 
##### Using Roles Based on Jobs and Functions
Assign roles to the users in your organization based on their department, where each departments files are hosted on a different server. An example is using Microsoft Project Server which can host multiple projects managed by different project managers, including the following roles:
- **Administrators:** Access and control over everything on the server, including all projects managed on the server.
- **Executives:** Access data from any project held on the server but cannot modify server settings.
- **Project Managers:** Full control over their own projects, but not projects owned by others.
- **Team Members:** Can report on work that project managers assign to them, but have little access outside the scope of their assignments. 
##### Documenting Roles with a Matrix
Identify roles in application, identify privileges each role requires, then document. Role-BAC is also called hierarchy-based/job-based:
- **Hierarchy-based:** Top level roles, like Administrator, have more permission, so that should mimic the hierarchy in the matrix. E.g. the more permission, the higher you are on the list.
- **Job-,task-, or function-based:** Roles are centered on jobs or functions that users need to perform.
##### Establishing Access with Group-Based Privileges
U make a role and treat it as a group, put people of that group (e.g. Sales in the Sales role) in that role. How is this different from groups? idk. u get it tho. I think it is just groups wtf.
#### Rule-Based Access Control
**Rule-BAC** uses rules, SURPRISE. Most common example is in routers and firewalls. However, more advanced implementations cause rules to trigger within applications too.
- Routers and firewalls use rules within *access control lists (ACLs)*. These rules define traffic that the devices allow into the network, such as HTTP traffic for web browsers. 
- IPS systems can detect attacks and modify rules to block traffic from attackers. The attack triggers a change in the rules.
#### Discretionary Access Control
In the **DAC** scheme, objects (files and folders) have an owner, and the owner establishes access for the objects. OSs' like Windows and most Unix-based systems use DAC scheme. 
- A common example is *New Technology File System (NTFS)* used in Windows. NTFA provides security by allowing users and admins to restrict access to files and folders with permissions. 
##### Filesystem Permissions
NTFS describes the actions that users are permitted to take on files and folders. Basic NTFS permissions are:
- **Write**
- **Read**
- **Read & Write**
- **Modify**
- **Full control**
The file system uses a ==deny by default== policy. Firewalls often refer to this as implicit deny.
##### SIDs and DACLs
Microsoft systems identify users with ==security identifiers (SIDs)==, though you will rarely see an SID. Ex: S-1-5-21-399-1871189-223218.
Every object (file folder) includes a ==discretionary access control list (DACL)== that identifies who can access it in a system using the DAC scheme. DACL is a list of **access control entries (ACE).

The DAC scheme is significantly more flexible than the MAC scheme. MAC has predefined access privileges, and the admin is required to make changes. 
#### Mandatory Access Control
The **MAC** scheme uses labels (sometimes referred to as sensitivity labels or security labels) to determine access. Admins assign labels to both subjects (users) and objects (files or folders). ==When they match==, the system grants a subject access to an object.
**Security-enhanced Linux(SELinux**) is one of the few operating systems using the MAC scheme. Windows uses DAC.
An SELinux policy is a set of rules that override standard Linux permissions. SELinux has three modes:
- *Enforcing mode* will enforce the SELinux policy and ignore permissions. 
- *Permissive mode* does not enforce SELinux policy, instead it uses the permissions. However, the system logs any access that would normally be blocked.
- *Disabled mode* does not enforce SELinux and does not log anything related to the policy. 
##### Labels and Lattice
The MAC scheme uses different levels of security to classify users and the data. These levels are contained in a lattice(basically a table), which defines the ==levels of security== that are possible for an object and the security levels(rows in the table) that a user is cleared to access. Users are only allowed to access an object if their security clearance is equal to or higher than **the level of the object**. Each level is defined with a specific security boundary(Top Secret, Secret, Confidential, and For Official Use).
##### Establishing Access
Typically, a security professional identifies the specific access individuals are authorized to access (via paperwork, then the admin assigned the rights and permissions based on the security professional).
#### Attribute-Based Access Control
An **ABAC** system evaluates attributes and grants access based on the value of these attributes. Attributes can be *almost any* characteristic of a user, the environment, or the resource. 
Many **software-defined networks (SDNs)** use ABAC schemes. Instead of rules on physical routers, policies in the ABAC system control the traffic. 
## Analyzing Authentication Indicators
Authentication systems provide a rich source of information for cybersecurity analysts looking for signs of potentially malicious activity. Sometimes signs are buried in otherwise innocent-looking log entries. Some key things to look out for when reviewing auth logs: 
- **Account lockouts:** Accounts locked cuz repeated fail login attempts.
- **Concurrent session usage:** Same user logged into same (or different) system from different locations at the same time.  
- **Impossible travel time:** Users completes login from one location and then another without having spent enough time to travel.
- **Blocked content:** Content filters are screening out unusual levels of malicious code.
- **Resource consumption:** Processor time, memory, storage, or other resources being used excessively (without explanation).
- **Resource inaccessibility:** Services suddenly become unavailable.
- **Log anomalies:** Logging levels are out-of-cycle, meaning entries are appearing at unusual times or log files have gone missing.

## Chapter 2 Practice Questions
1. D & C | **D & F, not C because it involves an enrollment process.**
2. B | **A, because although the application logs their location using GPS, there is no indication the location is being used for authentication...**
3. C **B because it's time based u dummy**
4. A? **C, a lower crossover error rate (CER) indicates a more accurate biometric system. The FAR and FRR rates vary based on the sensitivity of the biometric system and don't indicate accuracy by themselves. **
5. B 
6. D
7. C
8. D
9. B
10. D
11. C
12. A
13. D
14. B
15. C
