# Chapter 3: Network Technologies ad Tools
## Reviewing Basic Networking Concepts
### OSI Model
*Open Systems Interconnection (OSI) model* is a theoretical way to describe all of the different activities that happen on a network. The model consist of 7 layers, the lower the layer, the closer you are to the actual wires and cabling. The higher the layer, the closer you are to the end user and software running on a computer system. **Please Do Not Throw Sausage Pizza Away**.
###### Layer 1: Physical
Basic equipment of networking: copper wires, fiber optic cables, and radio waves.
###### Layer 2: Data Link
Where network switches reside. It formats data into data frames and routes it between systems on the ==LOCAL== network using their MAC.
###### Layer 3: Network
Introduces IP addresses. Routers use IP addresses to send information between systems that are ==NOT== on the local network. The internet protocol **IP** is the primary protocol of this layer. 
###### Layer 4: Transport
Provides end-to-end communications services for applications. The Transmission Control Protocol **TCP** and User Datagram Protocol **UDP** exist on this layer.
###### Layer 5: Session
Establishing, terminates, and manages sessions between applications running on different devices. Allowing them to communicate and exchange data.
###### Layer 6: Presentation
Translates data into a standard format that can be understood by the application layer, and provides *encryption, compression*, and other data transformation services. 
###### Layer 7: Application
Provides network services to applications, allowing them to communicate with other applications over the network. 
### Basic Networking Protocols
TCP/IP isn't a single protocol, it is a full suite of protocols. 
##### Transmission Control Protocol (TCP)
Provides connection oriented traffic (guaranteed delivery). Uses three-way handshake. Sends SYN (synchronize) packet to start a session, responds with SYN/ACK packet, and the client completes the third part with an ACK packet to establish to connection. 
##### User Datagram Protocol (UDP)
Provides connectionless sessions with no three-way handshake, so no guaranteed delivery. UDP makes the best effort to deliver data without using extra traffic to ensure delivery. 
##### The Internet Protocol (IP)
Identifies hosts in a TCP/IP network and delivers traffic from one host to another using IP addresses. 
##### Internet Control Message Protocol (ICMP)
Test basic connectivity and includes tools like ping and tracert. 
##### Address Resolution Protocol (ARP)
Resolves IPv4 addresses to MAC addresses. MAC addresses are also called physical addresses or hardware addresses because they are assigned to the devices network interface card (NIC).
### Implementing Protocols for Use Cases
Networks don't automatically support all the available protocols. Instead, IT professionals identify a need based on organizational goals and enable the best protocols to meet that need. 
#### Data in Transit Use Case
**Data in transit** is any traffic sent over a network. When data is sent in clear text anyone can use a packet capture tool to read it. You can protect **Personally Identifiable Information (PPI)** and any other sensitive data in transit by encrypting it. 

###### Insecure Protocols
- **File Transfer Protocol (FTP)** transmits in clear text. Port 20/21.
- **Trivial File Transfer Protocol (TFTP)** is used in many attacks, and it is not an essential protocol on most networks. 
- **Secure Sockets Layer (SSL)** was the primary method used to secure JTTP traffic as HTTPS. It can also encrypt other traffic such as SMTP and LDAP. However, SSL has been compromised and it is not recommended for use. (Now TLS is in use).
###### Secure Alternatives
- **Transport Layer Security (TLS)** is the replacement for SSL and should be used for browsers using HTTPS. Port 443 (HTTPS). 
- **Internet Protocol Security (IPsec)** is used to encrypt IP traffic. 
- **Secure Shell (SSH)** encrypts traffic in transit and can be used to encrypt other protocols such as FTP. *Secure Copy (SCP)* is based on SSH, used to copy encrypted files over a network. TCP port 22.
- **Secure File Transfer Protocol (SFTP)** is a secure implementation of FTP. It is an extension of SSH, using SSH to transmit. TCP port 22.
- **File Transfer Protocol Secure (FTPS)** is a secure implementation of FTP. It uses TLS to encrypt traffic.
#### Email and Web Use Cases

- **Simple Mail Transfer Protocol (SMTP)** The original version, SMTP, used TCP port 25. *Simple Mail Transfer Protocol Secure (SMTPS)* adds TLS encryption and uses TCP port 587. 
- **Post Office Protocol (POP3)** transfers emails from servers to end users. POP3 uses TCP port 110 for unencrypted connections. The secure version uses TCP port 995 for encrypted connections.
- **Internet Message Access Protocol (IMAP)** used to store emails on a mail server on TCP port 143, and TCP port 993 for encrypted.
- **Hypertext Transfer Protocol (HTTP)** Transmits web traffic between web servers and browsers. TCP port 80.
- **Hypertext Transfer Protocol Secure (HTTPS)** adds TLS on TCP port 443.
###### Enhancing Email Security
- **Sender Policy Framework (SPF)** uses DNS records to define which IP addresses are authorized to send emails on behalf of a domain.
- **Domain Keys Identified Mail (DKIM)** uses public key cryptography to sign and verify an email's domain and content. 
- **Domain-based Message Authentication, Reporting, and Conformance (DMARC)** builds on top of SPF and DKIM by allowing domain owners to set policies for how to handle emails that fail authentication.
#### Directory Use Cases
- **Lightweight Directory Access Protocol (LDAP)** on TCP port 389 and **LDAP Secure (LDAPS)** with TLS on TCP port 636, both for AD. 
#### Voice and Video Use Cases
- **Voice over Internet Protocol (VoIP)** used for transmitting communications, streaming media, video teleconferencing applications, and devices using web-based push-to-talk features in real-time. 
	- !! VoIP IS A CONCEPT, it refers to the methods and standards used. Think of it as a technology framework. !!
- **Real-time Transport Protocol (RTP)** delivers audio and video over IP networks. Used in *VoIP*.
	- A specific protocol that implements part of the VoIP functionality. 
- **Secure Real-Time Transport Protocol (SRTP)** provides encryption, authentication, and integrity for RTP.
- **Session Initiation Protocol (SIP)** used to initiate, maintain, and terminate voice, video, and messaging sessions. Do not contain data, but do contain metadata about sessions.
#### Remote Access Use Case
###### Remote Desktop Protocol (RDP)
Used to connect to other systems from remote locations. TCP port 3389.
###### OpenSSH
Suite of tools that simplifies the use of SSH. Supports SCP and SFTP.

```ssh remoteServer```
Initiates ssh connection to remote server using default port 22 on the client. 

```ssh root@remoteServer```
Remote server will prompt for a password.

```ssh-keygen -t rsa```
Create a matched pair of public/private keys under
- **id_rsa.pub** Copied onto your remote server
- **id_rsa** private key stored on client 

```ssh-copy-id root@remoteServer```
This command knows the public keys default location, and where to store it on the remote server. Now when connecting ssh will automatically use the key pair for authentication. 
#### Time Synchronization Use Case
