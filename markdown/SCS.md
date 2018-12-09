<!-- markdownlint-disable MD025 -->
<!-- markdownlint-disable MD024 -->

# Server and Cloud Security

# Introduction to Servers

## Server Hardware Types

### Tower Servers

- Most basic of servers
- Costs and takes up as much space as the average desktop
- Great for Small businesses
  - Limited space concerns and need centralized processing without data room
  - Easier monitoring and maintenance of network resources
  - Reduce susceptibility to intrusion attack through central location

### Rack Servers

- Stacks servers in racks
- Space saving option
- Companies that
  - Maximize space in a centralized data center
  - Mix and match servers to match workload
  - Require large dedicated storage internal to server

### Blade Server

- Most compact
- Multiple blade servers can fit vertically into a single enclosure
  - Share hardware components
- Fit more servers into less space
- More processing
- Less space
- Less power
- Less time and money spent on management

## Common Server Types

- Database Server
- File Server
- Mail Server
- Print Server
- Proxy Server
- Web Server

## Client Server Architecture

- Clients specialize in User Interface
- Server specialize in managing data and application logic
- Many clients supported by few servers
- Data and logic shared among application and users
- Client and Server platform can be different
  - Doesn't matter as long as they both use the same communication protocol(e.g. HTTP)
- Actual functions split up between client and server to optimize resource usage
- Optimize ability of users to perform various tasks and cooperate using shared resources
- Heavy emphasis on user-friendly GUI on client

## Multi-Tier Architecture

Principle that data access should be seperated into multiple tiers (usually 3).

### 1 Tier Architecture

- Installed programs
- Access data locally
- E.g. MS Excel

### 2 Tier Architecture

- Client-Server Architecture
- Client runs application: business logic & presentation
- Server handles data persistence
- Secure : Authentication & Role based data protection
- Distributed, supports concurrency

Drawbacks

- Business logic implemented on Client app
- Changes to business logic meant redeploying new client software to users
- With client software deployed on while network, difficult to prevent attackers hacking client software / write replacement software, bypassing business rules altogether

### 3 Tier Architecture

- Client, Middle, Database tier
  - Client interfaces between user and system (presentation)
  - Middle contains business logic and communicates between client and data
  - Database tier manages data
- Allows for modularity on large scale
- Each tier can be different technologies
- Middle tier deployed in secure location.
  - Exposes limited interface to network
  - Provides nothing more than what is needed by clients
- Make use of standardized internet protocol such as HTTP

# Group Policy and Active Directory

## Legend

|       |                     |
| :---: | :-----------------: |
| AD    | Active Directory    |
| DC    | Domain Controller   |
| GP    | Group Policy        |
| GPO   | GP Object           |
| OU    | Organisational Unit |

- Local Group Policy
  - Without AD, there's only one Group policty available on the workstatoin
  - When GP is created at local level, everyone who uses machine is affected
- Active Directory Group Policy
  - Domain-based / AD-based group policy
  - Selectively decide which users/computers will get into GPO

## AD Levels

- 4 Levels for Group Policy
  - Local Computer
  - Site
  - Domain
  - Organizational Unit
- Rules
  - Every server and workstation must be a member of one (only one) domain and Located in one (only one) site
  - User must be a member of one(only one) domain
  - User may be located in OU

## AD Site

- Site is a set of computers in a LAN. 
- All computers within site reside in same building

- Site Maps physical structure of network
- Domain maps logical/admin structure of organization
- Benefits
  - Design and maintain logical & physical structure independently
  - Base domain namespace on physical network
  - Deploy DCs for multiple domains within site. 
  - Deploy multiple DCs for same domain in multiple sites

## GP Inheritance

- When GPO linked to domain, GPO applies to computer and users in every OU and child OU in domain
- When GPO is linked to OU, GPO applies to computers and users in every child OU

## GP Precedence

- When policy is set at one level, levels below inherit from above it. Earlier and later settings are aggregated
- Local GPO --> Site --> Domain --> OU --> Child OU
  - GPO in child OU have higher precedence than parent OU

## Computer/User config settings

- Software settings
  - Deployment of software to specific user/computer
- Windows Settings
  - Script: Startup, shutdown, logon, logoff
  - Security: Account Policy, User rights, Software restriction
- Administrative Template
  - Local registry settings that affect appearance, application settings, system events and services

# Server Security Basics

- To secure server, threats to mitigate must be defined
- Threats against data and resources are possible due to mistakes
  - Bugs on OS
  - Software with vulnerabilities
  - Errors made by end users
- Organisations should conduct risk assessment
  - Identify threats against server and determine effectiveness of existing security controls
  - Perform risk mitigation - decide what measures to implement

## Principles

- Simplicity
  - Security mechanisms should be as simple as possible. Complexity is root of many security issues
- Fail-Safe
  - System should fail in secure manner 
  - Security controls and settings remain in effect
  - Better to lose functionality than security
- Complete Mediation 
  - Mediators that enforce access policy should be enforced
  - File system permissions, firewalls, proxies, etc.
- Open Design
  - Should not depend on secrecy of implementation
- Separation of Priviledge
  - Functions should be separate to provide granularity
  - In system, read, edit,write, execute should bbe seperate
  - System operators vs users, roles should be as seperate as possible
- Least Privilege
  - Each task/process/user is granted minimum rights to perform job
- Physhological Acceptability
  - Should understand necessity of security
  - Train and educate users to design security mechanisms that are **usable** and **effective**
- Defence-in-Depth
  - Single security mechanism is insufficient
  - Needs to be layered so that compromise of single mechanism is insufficient to compromise netowork
- Compromise Recording
  - Records and logs maintained, so that in case of compromise, evidence is available to organisation

## Securing Server OS

- Patch and upgrade OS
- Server Harding
- Install and configure additional security controls
- OS Security Testing

### Patch and upgrade OS

- Needs patches/upgrades to correct for known vulnerabilities
- Known vulnerabilities OS has should be corrected before hosting
- Server admins should
  - Create, document, implement a patching process
  - Identify vulns and applicable patches
  - Mitigate vulns temporarily if needed & if feasible
  - Install permanent fixes

### Server OS Hardening

- Securing system by reducing suface of vulnerabilities
- Hardened system is configured and updated to protect against attacks
- Remove unncessary service
  - Server should be on a dedicated, single-purpose host
  - Common types of service should be removed if not required
  - E.g. Printer, Remote access programs, Directory Services, Email Services
- Configure OS user auth
  - Authorized users who can configure OS are limited to small no. of server admins
  - Remove/Disable unneeded default accounts
  - Check organisation's password policy
  - E.g. Min length, complexity, age, reuse
- Configure resource control
  - OS provides capability to specify access privileges for files/directories/devices
  - By carefully setting acces controls, server admin can reduce intentional & unintentional security breaches
  - E.g. Deny read access to files and directories helps to protect confidentiality of info
  - Deny write access can help maintain integrity of info
- Install and Configure Additional Security Controls
  - Anti-malware software, antivirus, anti-spyware, rootkit detectors, etc. to protect OS from malware and to detect and eradicate any infections that occur
  - Host based Intrusion detection/prevention software (HIDS/HIPS) to detect attacks performed against server, including DoS attacks
  - Host-based firewalls to protect server from unauthorized access
  - Patch/Vulnerability management software to ensure vulnerabilities are addressed promptly
  - Disk encryption technologies to protect stored data from attackers who gain physical access to servers

## Firewalls

- Helps screen out malicious users, virus, worms that try to access network
- Hides information on your LAN from Internet such as names, network topology
- Log traffic to and from LAN
- Help prevent unauthorized access to LAN by blocking incoming network traffic attempting to use port that is not open

### Hardware Firewall

- Specialized network boxes containing customized hardware and software
- Provide protective barrier from outside world
- Can hide one department to another
- Great solution for organizations thatt want single security that protects multiple systems
- Palo Alto Firewall
- Disadvantages
  - Expensive
  - Complicated
  - Difficult to upgrade
  - Tricky to configure
  - Limited protection range (Won't work from outside the network)

### Software Firewall(Host Firewall)

- Software firewall installs on individual's PC
- More ideal for individual users/small businesses
- Even with hardware firewalls, software frewalls should still be used
  - Mobile users
- Ease of upgrade - Download patches, fixes, updates

- Windows firewall is turned on by default
- Once properly configured, it can stop many malware before it infects server
- Protect Windows server by preventing unwanted inbound
- Prevent unauthorized network traffic from accessing server
- Prevent unauthorized network traffic from leaving local networ
- Restrict other OS resources if they behave unexpectedly

## Antivirus

Software intended to identify and eliminate computer viruses

- Acts as guard over system, scanning incoming files & applications, quarantining/cleaning up viruses
- Aid that detects, fixes and prevents viruses and worms from spreading

### Specific Scanning

- AKA Signature Detection
- Scans files to look for known viruses matching definition
- Refers to a dictionary of known viruses and matches a piece of code from new file to dictionary
- After recognizing malicious software
  - Attempt to repair file by removing virus from file
  - Quarantine file
  - Delete file completely
- Not always reliable - Virus disguising itself to it doesnt match virus signature

### Generic Scanning

- Suspicious behaviour approach
- Used when new virus appear
- Software monitors behaviour of all applications
  - If suspicious found, application is quarantined and warning broadcasted. 
  - If virus, user can send to virus vendor
  - Researchers examine, determine signature, name and catalogue it and release antivirus software to stop spread

## Vulnerability Scanning

- Automated tools used to identify vulnerabilities and misconfigured hosts
- Provide information about mitigating vulnerabilities
- Assist server admin in identifying vulns and verify whether existing security measures are effective
- Significant weaknesses
  - Identify only surface vulns and are unable to address overall risk level
  - Often better at detecting well known vulns - Impossible for 1 product to incorporate all vulns

## Penetration Testing

- Exercise system protection using common tools and techniques developed by attackers
- Benefits
  - Tests network using same methodologies and tools employed by attackers
  - Verifies whether vulns exist
  - Goes beyong surface vulns and demonstrates how these vulns can be exploited
  - Demonstrates that vulns are not purely theoretical
  - Provides realism to address security issues
  - Allows for testing of procedures and susceptibility of human element to social engineering

# Server Security Best Practices

## Core Security Principle

- Apply security measures and controls to whole infrastructure
  - End (endpoint) to Edge (border, firewall, router) and Beyond (cloud)
- Baked in all process and procedures in company

## Policies, Procedures, Standards and Guidelines

- Policies are high-level plans that describe goals of procedures
  - Describe security in general terms
  - Provide blueprint for overall security program
- Standards describe specific products, configs, or other mechanisms to secure system
  - Access policy requires one-time-use passwords, standars will specify using a particular token device
- Procedures describe how to use standards and guide-lines to implement countermeasures
- Guidelines are recommendations to the user community as reference to proper security

## Edge Security - Demilitarized Zone (DMZ)

- DMZ describes a host/network segment inserted as a "neutral zone" between private network and internet
- Prevents outside users of Web server from gaining direct access to organizations internal network
- Mitigates risks of locating web server on an internal network/exposing it directly to the internet
- Involves placing firewall between organizations rounter and internal netowrk, and creating new network segment that can only be reached through DMZ
- Web server is placed in new segment, with network infrastructure components that need to be externally accessible
- Advantage
  - Web server may be better protected
  - Network traffic to and from server can be monitored
  - Compromise of web server does not threaten internal network
  - Greater control over security of Web Server as traffic to and from web server can be controlled
  - DMZ network config can be optimized to support and protect web server

### Single Firewall DMZ

- Single Firewall DMZ is low cost approach as it only needs 1 firewall
- Uses existing border router to provide protection to DMZ
- Border router with ACL to restrict certain types of network traffic to and from DMZ
- Internet --> Border Router with IP Filter --> DMZ (Servers to be accessed from the outside) --> Firewall --> Intranet
- Usually appropriate for small organizations
- Weakness
  - Router able to protect against most network attacks
  - Not aware of the Web server application layer protocols (HTTPS)
  - Cannot protect against these attacks

### 2 Firewalls

- Adds second firewall between internet and DMZ
- Commonly used by companies with no budget restraint
- Internet --> Border Router --> Firewall --> DMZ --> Firewall --> Intranet
- Advantage
  - Improves protection as dedicated firewall can have more complex/powerful security rules
  - Dedicated firewall often can analyse incoming & outgoing HTTP traffic, it can detect against application layer attacks
- Disadvantage
  - May result in performance degradation
  - Costly

### 1 Firewall, 3 legs

- Firewall with 3 or more network interfaces
- 1 Network interface attached to border router, another attached to internal network, 3rd connected to DMZ
- Internet --> Border Router --> Firewall --> Intranet
- ----------------------------------|--> DMZ --> Servers
- Advantage
  - More for organizations that desire security of 2 firewall, but no resources
- Disadvantage
  - Increased risk of service degradaion during DoS attack


## Security practices for Server Operations

## User Account Control (UAC)

- Future needs to install additional software
- Malicious software runs their own installer to be installed on server
- UAC is security feature which prompts user for admin credentials
- enables users to perform common tasks as non-admin users

## Admin Accounts

- Admin Account carry higher degree of risk. 
  - When signed in, privileges allow access to entire OS, including registry, system files, config settings
  - As long as admin account is signed in, system is vulnerable to attacks
- By default, standard users and admins run apps and access resources in context of standard user
- UAC provides way for user to elevate his/her status from standard user account to admin account
- If user is admin, user confirms to elevate permission level and continue
  - AKA Admin approval mode
- If not admin, username and password for admin account needs to be entered
  - Temporarily gives user admin provileges, but only to complete current task
  - After task is complete, permissions change back to normal user
  - UAC creates more secure environment to run and install apps

## Logging

- Record of events occuring within organizations systems and networks
- Composed of log entries 
  - Contains information related to specific event
- Security software logs primarily contain security-related info

## Security Software Logs

- Anti-malware software
  - Log records all instances of detected malware, file and system disinfection attempts
  - Record when malware scans were performed
  - Antivirus software updates
- Intrusion detection and Intrusion Prevention Systems
  - Log records detailed info on suspicious behaviour and detcted attacks
  - Any actions performed by the IPS to stop malicious activity
- Vulnerability Management Software
  - Logs patch installation history and vulnerability status of each host
  - Known vulnerabilities
  - Missing software updates
- Firewalls
  - Permit or block activity based on policy
  - Track state of network traffic and have more complex policies to generate detailed logs

## OS Logs

- System Events
  - Operational actions performed by OS such as shutting down or starting service
- Audit Records
  - Successful/failed authentication attempts, file access, policy changes, use of privileges

## Log management

- Help ensure computer security records are stored in sufficient detail for appropriate period of time
- Routine log reviews and analysis are beneficial for identifying security incidents
- Challenges
  - Potential problems with initial generation of logs due to variety and prevalence
  - Confidentiality, Integrity, Availability of logs can be breached
  - People responsible for log analysis are often inadequately prepared

## Security Information Event Management (SIEM)

- Logging and Event Aggregation
  - Network (router, switch, firewall)
  - System (server, workstation)
  - Application (web, DB)
- Correlation Engine
  - 2+ Related events = higher alarm
- Management layer above existing systems and security controls
- Connects and unifies information contained
- Allowing to be analyzed and cross-referenced from single interface

# Virtualization and Cloud Computing

- Before
  - Single OS per machine
  - Hardware and Software tightly coupled
  - Running multiple apps often created conflicts
  - Under-utilized resources
  - Inflexible and costly infrastructure
  - 
- After
  - Hardware-independence of OS and application
  - Can be easily provisioned to any system
  - Can manage OS and application as a single unit (encapsulating into VM)

## Hypervisor

- AKA Virtual Machine Manager/monitor(VMM)
- Program that allows multiple OS to share hardware host
- Each guest OS appears to have all host resources(processor/memory) to itself
- Hypervisor actually controls host process and resources, allocating what is necessary
- Roles
  - Isolate/Emulating resources
  - CPU: Scheduling virutal machines
  - Memory: Managing memory
  - I/O: Emulating I/O devices
  - Networking
  - Managing VMs

## Virtualization Approaches

- Hosted Architecture
  - Install and runs as application
  - Relies on host OS for device support and physical resource management
  - VMware Workstation, VMware player
- Base-Metal(Hypervisor) Architecture
  - Hypervisor runs directly on host's hardware to control it and manage guest OS
  - VMwaer ESX/ESXi, Microsoft Hyper-V

## Benefits

- Server Consolidation and Containment
  - Deployment of systems as VMs that can run safely and move transpare
- Test and Development Optimization
  - Rapidly provision test and dev servers by reusing pre-configured systems
- Business Continuity
  - Reducing cost and complexity of business continuity
  - High availability & disaster recovery
  - Encapsulating entire systems into single files that can be replicated and restored.

## Challenges

- Cost
  - High initial investment
  - Software licensing cost
- Single Point of Failure
  - Many servers on one host machine
  - Hardware or software failures are critical
  - Backup servers needed
- Security
  - Hypervisor Vulnerabilities

## Virtualized Resources

- Servers: Physical server can be abstracted to virtual server
- Storage: Physical storage device abstracted to a virtual storage device / virtual disk
- Network: Physical routers & switches can be abstracted to logical network(VLANs)

## Infrastructure

- Infrastructure connects resources to business
- Virtualized Infrastructure
  - Dynamic mapping of resources to business

## Hypervisor Vulnerabilities

- Malicious software can run on same server
  - Attack hypervisor
  - Access/Obstruct other VMs

## Cloud Computing

- Virtualization is enabling tech for Cloud Computing
- Broad Network Access
  - Capabilities available over network
  - Access through standard mechanisms that promote use through thin/thick clients (mobile phones, tablets, laptops)
- Rapid Elasticity
  - Capabilities expanded or released automatically (More CPU Power, etc.)
  - Appears seamless, limitless and responsive to customer
- Measured Service
  - Customers are charged for service they use and amount
  - metering where customer resource usage is monitored, controlled and reported
- On-Demand Self-service
  - Consumer can provision computing capabilities, such as server time and storage as needed, automatically. 
- Resource Pooling
  - Computing resources are pooled to serve multiple consumers
  - Resource dynamically assigned and reassigned according to customer demand
  - May not care where resources are physically located but should be aware of risks

## Cloud Service Models

- Software as a Service(SAAS)
  - Capability provided to consumer is providers application running on cloud infrastructure
  - Gmail, facebook, etc
- Platform as a Service(PaaS)
  - Deploys self created/acquired apps using programming languages/tools provided by provider
  - Google App Engine, Azure
- Infrastructure as a Service(IaaS)
  - Aple to access processing, storage, network and other resources from provider
  - AWS, Rackspace cloud

## Scope and Control

- Higher level of support available from cloud provider, more narrow the scope and control the cloud subscrire has over the system

## Cloud Deployment Models

- Private
  - Infrastructure provisioned for exclusive use by single organization
- Community
  - Provisioned for specific community of consumers from orgs that have shared concerns
- Pulic
  - Provisioned for open use by public
- Hybrid
  - 2 or more distinct cloud infrastructures - private/community/public which remain unique entities

# Cloud Security Basics

## On Premise

Computing in which all computing resource accessed and managed by/from the premises

- Overall cost incurred by premise that owns it
- Diminished returns in long run

## Cloud Computing

- Pool of resources accessed online
- Usage on demand service

### Pros

- Universal access
  - Platform independent - Accessible across many devices with internet connection
  - Increases mobility and productivity - allows staff to collab on projects
- More storage capacity
  - Unlimited storage as long as you can afford it
- Easy and Quick setup
  - Only internet connection needed
  - Register and adjust simple configs and you're done
- Automatic updates
  - Done by provider
- Cost effective
  - Only pay for what you use
  - Don't incur other costs such as maintenance, security, storage

### Cons

- Security Risk
  - Malware, MITM, eavesdropping can be experienced
- Privacy issues
  - Availability of information can be breached
  - Accessed/Modified by unauthorized entities
- Loss of Control
  - Entities dictate on how they'll be used as cloud uses on-demand service model
- Internet Reliance
  - Can't access cloud without internet
- Cloud Provider Reliability
  - Full reliability on cloud provider
  - If anything happens to provider, you'll also be affected

In the long run, Cloud Computing is cost effective as compared to on-premise. Reduces expenditure while maximizing efficiency and productivity

## Governance in the cloud

- Traditionally, most IT orgs govern 5 tech layers
- From LaaS to Paas to SaaS, IT org's level of control diminishes and the Cloud Service Provider(CSP) level of control increase
- Although control increases for CSP, it is still IT orgs responsibility
- Important to develop strong monitoring framework
  - Ensure service levels and contractual oblications are met

## Cause of Security Concerns

### Loss of Control

- Data, applications, resourecs located with provider
- User identity management handled by cloud
- User access control rules, security policies and enforcements managed by cloud provider
- Relies on provider for CIA

### Multi-tenancy

- Software archictecture pattern
  - Single application used by multiple customers at the same time

Single tenancy - Each customer has their own server and DB

## Security Concerns

- Insider Threats
  - Underestimated
  - Rogue cloud service employee has a lot of access that outside cyber attacker would have to work harder to acquire
- Compliance Issues
  - Means conforming to a rule, such as specification/policy/standard/law
  - Principle that cloud systems must be compliant with standards cloud customers face
- Data Breaches
  - biggest threat in cloud
  - happen daily over the world and there are always huge financial loss associated
- Sophisticated Attacks
  - Cyber-criminals able to operate as legitimate orgs, devoting time and resources into finding methods of cracking security systems
  - Pick up wide inventory of innovative, developed underground tools

## Managing Security

### Managing Access

- Network access control will play a diminishing role
  - Traditional network-based access control focus on protecting resource from unauthorized access based on host-based attributes
  - Usually inadequate, is not unique across users, and can cause incorrect accounting
- User access control should be emphasised as it can strongly bind users identity to resource
- CSP should ensure that only limited set of users has admin access to resources

### Protect Data

- Protect Data
  - Subtle disclosures of info are possible when data is stored in cloud
  - Customer should access whether providers data protection mechanisms, data location config, processing tech meet needs of organization
  - Customer should require that provider offer mechanism for reliably deleting data

### Gain Visibility

- Provide customers with visibility into
  - Resource Utilization
  - Operational Performance
  - Overall demand patterns
  - CPU utilization
  - Disk read/writes
  - Network Traffic

### Optimize Operations

- Automating and refining standardization of infrastructure and cloud operations
- Cloud user should 
  - Plan and deploy security across its environment
  - Utilize security experts
  - Enhance security monitoring to achieve holistic view of what is happning in and around cloud
