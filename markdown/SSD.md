<!-- markdownlint-disable MD025 MD033 MD024 MD006 MD029-->

# Secure Software Development

- [Secure Software Development](#secure-software-development)
- [Chapter 1 - Secure Software Concepts](#chapter-1---secure-software-concepts)
  - [Iron Triangle Constraints](#iron-triangle-constraints)
  - [Security as an afterthought](#security-as-an-afterthought)
  - [Security vs Usability](#security-vs-usability)
  - [Attacker Vs Defender](#attacker-vs-defender)
    - [Defender](#defender)
    - [Attacker](#attacker)
  - [Secure Software Concepts](#secure-software-concepts)
    - [Confidentiality](#confidentiality)
    - [Integrity](#integrity)
    - [Availability](#availability)
    - [Authentication](#authentication)
    - [Authorization](#authorization)
    - [Accountability](#accountability)
    - [Auditing](#auditing)
    - [Non-Repudiation](#non-repudiation)
    - [Data Privacy](#data-privacy)
    - [Data Anonymization](#data-anonymization)
    - [PDPA](#pdpa)
- [Chapter 2 - Secure Software Requirements 1](#chapter-2---secure-software-requirements-1)
  - [Quality Attributes of Secure Software](#quality-attributes-of-secure-software)
    - [Eg of explicit software security requirement vs high level security requirements](#eg-of-explicit-software-security-requirement-vs-high-level-security-requirements)
  - [Types of Software Security Requirements](#types-of-software-security-requirements)
    - [Authentication Requirements](#authentication-requirements)
    - [Common Forms of authentication](#common-forms-of-authentication)
    - [Forms Authentication](#forms-authentication)
    - [Authorization Requirements](#authorization-requirements)
    - [Availability Requirements](#availability-requirements)
    - [Accountability Requirements](#accountability-requirements)
    - [Session management requirements](#session-management-requirements)
    - [Error and Exception Management Requirements](#error-and-exception-management-requirements)
    - [Confidentiality Requirements](#confidentiality-requirements)
    - [Integrity Requirements](#integrity-requirements)
- [Chapter 3 - Secure Software Requirements 2](#chapter-3---secure-software-requirements-2)
  - [Protection Needs Elicitation (PNE)](#protection-needs-elicitation-pne)
  - [Surveys, Questionnaires and Interviews](#surveys--questionnaires-and-interviews)
  - [Data Classification](#data-classification)
    - [Types of Data](#types-of-data)
    - [Labeling](#labeling)
    - [Data Ownership](#data-ownership)
    - [Use Case Modeling](#use-case-modeling)
    - [Misuse Case Modeling](#misuse-case-modeling)
    - [Determining Misuse Case](#determining-misuse-case)
    - [Subject / Object Matrix](#subject---object-matrix)
      - [Role Vs Group](#role-vs-group)
      - [Subject-Object Matrix](#subject-object-matrix)
- [Chapter 4 - Secure Software Design 1](#chapter-4---secure-software-design-1)
  - [Benefits of Secure Design](#benefits-of-secure-design)
  - [Designing Confidentiality Techniques](#designing-confidentiality-techniques)
    - [Symmetric Key Cryptosystem](#symmetric-key-cryptosystem)
    - [Goals](#goals)
    - [Popular Cryptosystems](#popular-cryptosystems)
  - [Asymmtric Key Cryptosystem](#asymmtric-key-cryptosystem)
    - [Popular Asymmtric Key Cryptosystems](#popular-asymmtric-key-cryptosystems)
    - [Goals](#goals)
    - [Satisfies Confidentiality](#satisfies-confidentiality)
    - [Satisfies Authenticity and Non-Repudiation](#satisfies-authenticity-and-non-repudiation)
    - [Limitations](#limitations)
  - [Symmetric vs Asymmetric](#symmetric-vs-asymmetric)
  - [Combining Symmetric and Asymmetric](#combining-symmetric-and-asymmetric)
  - [Digital Certificates and Public Key Infrastructure (PKI)](#digital-certificates-and-public-key-infrastructure-pki)
    - [Defining Digital Certificate](#defining-digital-certificate)
    - [Public Key Infrastructure (PKI)](#public-key-infrastructure-pki)
    - [Managing Digital Certificates](#managing-digital-certificates)
    - [Certificate Authority](#certificate-authority)
    - [Registration Authority (RA)](#registration-authority-ra)
    - [Certificate Revocation List (CRL)](#certificate-revocation-list-crl)
    - [Certificate Repository (CR)](#certificate-repository-cr)
    - [Managing Digital Certificates](#managing-digital-certificates)
    - [Tyoes of Digital Certificates](#tyoes-of-digital-certificates)
    - [X.509 Digital Certificate Standard](#x509-digital-certificate-standard)
    - [Public KEy Cryptogtaphy Standards (PKCS)](#public-key-cryptogtaphy-standards-pkcs)
  - [Cryptographic Hash Functions](#cryptographic-hash-functions)
    - [Characteristics of Cryptographic Hash Functions](#characteristics-of-cryptographic-hash-functions)
    - [Example of Hash Function](#example-of-hash-function)
    - [Popular hash functions](#popular-hash-functions)
  - [Digital Signature](#digital-signature)
    - [How to digitally sign message](#how-to-digitally-sign-message)
    - [Verify digitally signed message](#verify-digitally-signed-message)
    - [Code Signing](#code-signing)
  - [Referential Integrity](#referential-integrity)
  - [Resource Locking](#resource-locking)
  - [Availability Techniques](#availability-techniques)
    - [Failover](#failover)
    - [Replication](#replication)
    - [Scalability](#scalability)
  - [Authentication Design](#authentication-design)
    - [Multi-Factor Authentication](#multi-factor-authentication)
    - [Single Sign On (SSO)](#single-sign-on-sso)
    - [Federation](#federation)
  - [Key Secure Design Principles](#key-secure-design-principles)
    - [Least Privilege](#least-privilege)
    - [Separation of Duties](#separation-of-duties)
    - [Defense in Depth](#defense-in-depth)
    - [Fail Safe](#fail-safe)
    - [Economy of Mechanisms](#economy-of-mechanisms)
    - [Complete Mediation](#complete-mediation)
    - [Open Design](#open-design)
    - [Least Common Mechanisms](#least-common-mechanisms)
    - [Psychological Acceptability](#psychological-acceptability)
    - [Weakest Link](#weakest-link)
    - [Leveraging Existing Components](#leveraging-existing-components)

# Chapter 1 - Secure Software Concepts

## Iron Triangle Constraints

If projects **scope**, **schedule**, and **budget** are ridgidly defined, it gives little to no room to incorporate even basic security requirements into the software, and unfortunately, what is typically overlooked in security

## Security as an afterthought

- Important that security features are built into the software, instead of being added later on
- Cost to fix insecure software earlier in the software development life cycle(SDLC) is insignificant when compared to having same issue addressed at a later stage

## Security vs Usability

- Incorporation of security features is viewed as making software complex, restrictive and unusable
- Incorporation of security comes at cost of performance and usability
  - Occurs when software design does not factor in psychological acceptability
- Security must be balanced with usability and performance

## Attacker Vs Defender

### Defender

- Play vigilante 24x7
- Guarding against all attacks
- Constrained to play by rules of engagement

### Attacker

- Can strike anytime
- Needs to be able to exploit just 1 weakness
- Need not play by rules

## Secure Software Concepts

### Confidentiality

- Security concept to do with protection against unauthorized information disclosure
- Viewing of data
- Confidentiality assure secrecy of data, but also can help in maintaining data privacy

### Integrity

- Integrity is security concept that assures protection against unauthorized alterations / modifications of data
- 2 Aspects
  - Ensure that data is transmitted, processed and stored is as accurate as original
  - Software performs reliably as it was intended to

### Availability

- Related to access of the software / data / information it handles
- Assures protection against Denial of Service
- Ensures business continuity program(BCP), where system downtime is minimized and that impact upon business disruption is minimal

### Authentication

- Concept that verifies and validates identity of information supplied
- Answers qn - "Are you who you claim to be"
- Factors of Authentication
  - What you know? - Password, PIN(memory)
  - What you have? - Security Token, Smartcard(physical)
  - Who you are? - Fingerprint, Iris scanner (Biometrics)

### Authorization

- Checking of a subjects rights and privileges before granting access to the objects that the subject requests
- Requestor is referred to as subject and requested resource is object
- Subject may be human or non human (process / another object)
- Categorized by privilege level - admin user, manager, anonymous user
- Object e.g. - table in a databse, file, view
- Eg of authorization based on privilege level of subject
  - admin user who may be able to create read update delete (CRUD) data
  - anonymous user may only be allowed to read (R) the data
  - manager may be allowed to create, read, update (CRU) data

### Accountability

- Protects against repudiation threats
- Non-repudiation addresses deniability of actions taken by either user or software on behalf of user
- Accountability to ensure non-repudiation can be accomplished by auditing when used in conjunction with identification

### Auditing

- Addresses logging of transactions so that at a later time a history of transactions can be built, if needed
- Answers qn - "Who *(subject)* did what *(action)* when *(timestamp)* and where *(object)* ?"
- detective control and can be a deterrent control as well

### Non-Repudiation

- Security control that addresses deniability of actions taken by software or user
- ensures that actions taken by software on behalf of user cannot be refuted or denied

### Data Privacy

- suitably defined as appropriate use of data
- When companies and merchants use data / information provided / entrused to them, the data should be used according to agreed purpose
- companies have sold, disclosed, rented vlues of consumer info that was entrused to other parties without prior approval

### Data Anonymization

- Act of permanently and completely removing personal identifiers from data, such as converting personally identifiable information (PII) into aggregated data
- Anonymized data cannot be linked to any one individual account
- Anonymization techniques are useful to assure data privacy
- Techniques include
  - Replacement
  - Suppression
  - Generalization
  - Pertubation

### PDPA

# Chapter 2 - Secure Software Requirements 1

## Quality Attributes of Secure Software

- Reliability
  - Software functions as its expected to
- Resiliency
  - Software does not violate any security policy and is able to withstand actions of threat agents that are posed intentionally (attacks and exploits) or accidentally (user errors)
- Recoverability
  - Software is able to restore operations to what business expects by containing, limiting and remediating damage caused by threats that materialize

### Eg of explicit software security requirement vs high level security requirements

- Explicit software requirement
  - User password will be needed to be protected against disclosure by masking it while it's input and hashed when it's stored
  - Change in pricing information of a product needs to be tracked and audited, recording the timestamp and individual who performed that operation
  - Usually **not** found within software requirements specification document
- High-level security requirements
  - high level non testable implementation mechanisms
  - listing of security features
    - passwords need to be protected
    - Secure Socket Layer (SSL) needs to be inplace
    - Web application firewall needs to be installed infront of public facing websites

## Types of Software Security Requirements

### Authentication Requirements

- Process of validating an entity's claim is authentication
- Entity may be person / process / hardware device
- Common mean by which authentication occurs - entity provides identity claims / credentials which are validated and verified against a trusted source holding those credentials

### Common Forms of authentication

- Anonymous
- Basic
- Digest
- Integrated
- Client cerificates
- Forms
- Token
- Smart cards
- Biometrics

### Forms Authentication

- Observed in web apps, require user to supply username and password for auth purposes, and these credentials are validated against directory store - active directory, database, configuration file
- Since credentials collected are supplied in clear text form, advised to first cryptographiaclly protect data being transmitted in addition to implementing Transport Layer Security (TLS) such as SSL or Network Layer Security such as IPSec
- E.g. of username and password - login box used in Forms authentication

### Authorization Requirements

- Role Based Access Control (RBAC)
  - Individuals *(subjects)* have access to a resource *(object)* based on their assigned role
  - Permission to operate on objects such as CRUD are also defined and determined based on responsibilities and authority (permissions) within job function

### Availability Requirements

- *Software shall ensure high availability of five 9's (99.999%) as defiend in the SLA*
- No of users at any one given point of time who should be able to use software can be up to 300 users
- Software and data should be replicated across data centers to provide load balancing and redundancy
- Mission *Critical* functionality in software should be restored to normal operation within 1h of desruption
- Mission *Essential* functionality in software should be restored to normal operations within 4h of desruption
- Mission *Support* functionality in software should be restored to normal operations within 24h of disruption

### Accountability Requirements

- Accountability requirements are those that assist in building a historical record of user actions
- Audit trails can help detect when unauthorized user makes change / authorized user makes unauthorized change, both of which are cases of integrity violations
- Identity of subject (user or process) performing an action *(who)*
- The action *(what)*
- Object on which action was performed *(where)*
- Timestamp of action *(when)*

### Session management requirements

- Each user activity will need to be uniquely tracked
- User should not be required to provide user credential once authenticated with internet banking application
- Sessions must be explicitly abandoned when user logs off / closes browser window
- Session identifiers used to identify user sessions must not be passed in clear text / easily guessable

### Error and Exception Management Requirements

- All exceptions are to be explicitly handled using try, catch, and finally blocks
- Error messages that are displayed to end user will reveal only needed information without disclosing any internal system error details
- Security exception details are to be audited and monitored periodically

### Confidentiality Requirements

- Requirements are those that address protection against unauthorized disclosure of data / information that are either private (non-public) or sensitive (public) in nature
- Need to be defined throughout the information life cycle from origin of data to its retirement
- Necessary to explicitly state confidentiality requirements for non-public data
  - In Transit - When data is transmitted over unprotected networks : Data in Motion
  - In Procesing - When data is held in computer memory / media for processing
  - In Storage - When data is at rest, within transactional systems including archives - data at rest
- E.g.
  - Personal health information must be protected against disclosure using approved encryption mechanisms
  - Password and other sensitive input fields need to be masked
  - Passwords must not be stored in the clear in backend systems and when stored must be hashed with at least equivalent to the SHA-256 Hash function
  - Transport Layer Security (TLS) such as Secure Socket Layer (SSL) must be in place to protect against insider man-in-the-middle(MITM) threats for all credit card information that is transmitted
  - Log files must not store any sensitive information as defined by the business in humanly readable or easily decipherable form

### Integrity Requirements

- security requirements that address 2 primary areas of software security
  - reliablity assurance
  - protection / prevention against unauthorized modifications
- refers not only to system / software modification protection (system integrity) but also data that system / software handles (data integrity)
- E.g.
  - All input forms and Query strings need to be validated against a set of alloable inputs before software accepts it for processing
  - Software that is published should provide recipient with computed checksum and hash function used to compute checksum, so that recipient can validate its accuracy and completeness

# Chapter 3 - Secure Software Requirements 2

## Protection Needs Elicitation (PNE)

Refer to **PDFs**

- Process of eliciting security requirements
  - Sueveys and Questionnaires
  - Brainstorming
  - Policy Decomposition
  - Data Classification
  - Subject-Object Matrix
  - Use Case and Misuse Case Modelling

## Surveys, Questionnaires and Interviews

- What kind of data will be processed, transmitted or stored by software?
- Data highly sensitive or confidential in nature?
- Will software handle personally identifiable information / privacy replicated information?
- Who are all the users who will be allowed to make alterations and will they need to be audited and monitored?
- What is the max tolerable downtime for software?
- How quickly should software be able to recover and restore normal operations when disrupted
- Is there need for single sign-on authentication?
- What are roles of users that ened to be established and what privileges and rights (such as CRUD) will each role have?

## Data Classification

### Types of Data

- Structured Data
  - Data organised into identifiable structure
  - Database in which all information is stored in columns and rows
- Unstructured Data
  - Data has no identifiable structure
  - Unstructured data include images, videos, emails, documents and text

### Labeling

- Not all data need same level of protection
- Public data require minimal to no protection against disclosure
- Main objective of data classification is to lower cost of data protection and maximuze return on investment when data is protected
- Accomplished by implementing only the needed levels of security controls on data assets based on categorization

### Data Ownership

- Business/data owner has responsibility for following
  - Ensure that information assets are appropriately classified
  - Validate security controls are implemented as needed - reviewing classification periodically
  - Define authorized list of users and access criteria based on information classifications
    -   Supports Seperation of Duties principle of secure design
  - Ensure appropriate backup and recovery mechanisms are in place
  - Delegate as needed the classification of responsibility, access approval authority, backup and recovery duties to data custodian

### Use Case Modeling

- Use case models intended behavior of software or system
- This behavior describes the sequence of actions and events that are to be taken to address a business need
- Use case modeling and diagramming is very useful for specifying requirements
- Use case modeling includes identifying actors, intended system behavior (use cases), and requences and relationships between actors and the use cases
- Actors may be an individual, a role, or non-human in nature
  - As an example, the individual John, an administrator or a backend batch process can all be actors in a use case

### Misuse Case Modeling

- Misuse cases, AKA abuse cases can help identify security requirements by modeling negative scenarios
- Negative scenario is an unintended behavior of the system, one that the system owner does not want to occur within the context of use case
- Misuse cases provide insight into the threats that can occur against the system or software
- Misuse case modeling is similar to use case modeling, except that in misuse case modeling, misactors and unintended scenarios or behavior are modeled
- Misuse cases may be intentional or accidental

### Determining Misuse Case

- Negation (negate intended functionality)
- Inversion (change the actor)
- Example
  - Functionality - Administrators can create CC info
  - Negation
    - Administrators **CANNOT** create CC info
  - Inversion
    - Non-Administrators CAN create CC info

### Subject / Object Matrix

- When there are multiple subjects (roles) that require access to functionality within software, it is critical to understand what each subject is allowed to do
- Objects (Components) are those items that a subject can act upon
- Building blocks of software
- Higher level objects must be broken down into more granular objects for better accuracy of subject-object relationship representation

#### Role Vs Group

- Role
  - Collection of Permissions
  - Permissions are assigned to roles, never directly to users
    - Access is granted through roles
- Group
  - Collection of Users
  - Permission can be assigned to bboth users and groups

#### Subject-Object Matrix

- 2-dimentional matrix
- Subjects (roles) across the column
- Objects (components) down the row
- Shows wich subjects/roles can take what action (CRUD) on which object

# Chapter 4 - Secure Software Design 1

## Benefits of Secure Design

- Minimizes the time needed to fix identitied security issues
- Assures stakeholders trust because software is
  - Reliable - Functioning as expected and less prone to errors
  - Resilient - Less likeyly to be successfully exploited
  - Recoverable - More prone to be able to restore itself to normal business operations upon error or exploitation
- Requires minimal redesign when software is designed with future threats in mind
- Designing software with security in mind, business logic flaws and other architectural design issues may be uncovered

## Designing Confidentiality Techniques

### Symmetric Key Cryptosystem

- Same shared key used to encrypt and decrypt data
- AKA Secret-key cryptosystem/cryptography
- Longer key length, exponential increase in time to crack
- Advantages
  - Secure
  - Fast
    - Due to simple substitution, permutation, and modular arithmetic operations
- Disadvantages
  - Key Distribution
    - Requires secure communication channel to share key between parties
  - Key management
    - Each party have to maintain a unique shared key with every other communicating party
  - If "n" is no of parties in a group whi want to use symmetric key cryptosystem
    - total no of keys = n * (n-1) / 2

### Goals

| Goals           | Symmetric Key |
| :-------------- | :------------ |
| Confidentiality | Yes           |
| Integrity       | No            |
| Availability    | No            |
| Authentication  | No            |
| Non-Repudiation | No            |

### Popular Cryptosystems

- 3DES
- AES

## Asymmtric Key Cryptosystem

- Public key to encrypt and private key to decrypt
- AKA public key cryptosystem/cryptography

### Popular Asymmtric Key Cryptosystems

- RSA
  - Most common asymmtric cryptography algorithm
  - Uses 2 large prime numbers
- Elliptic Curve Cryptography(ECC)
  - Users share 1 elliptic curve and 1 point on curve
  - Uses less computing power than prime number-based asymmetric cryptography
    - Key size smaller

### Goals

| Goals           | Symmetric Key |
| :-------------- | :------------ |
| Confidentiality | Yes           |
| Integrity       | No            |
| Availability    | Yes           |
| Authentication  | Yes           |
| Non-Repudiation | Yes           |

### Satisfies Confidentiality

- Alice's public-private key pair
  - Public key is shared publicly
    - Whoever wants to send alice secure message, encrypt message using public key
  - Private key secret with Alice
    - Alice is only one who can decrypt message
- Charlie may capture message for Alice, but he cannot decrypt them as he does not have alice private key
- Impossible for charlie to generate Alice's private key based on public key

### Satisfies Authenticity and Non-Repudiation

- Public-private key pair are 2 mathamatically related keys
  - When alice wants to prove message is from her, alice encrypts it with her private key
  - Whoever wants to verify it, would be able to decrypt message **ONLY** with Alice's public-key
  - Since message could ONLY be decrypted by Alice's public-key, and also Alice **ALONE** hold private-key, it proves message came from Alice

### Limitations

- Longer Key Length
  - Uses longer key length than symmtric encryption
  - Effectiveness depends on intractability of certain maths problems such as integer factorization
  - Time consuming to solve, but faster than trying all possible keys
  - Asymmetric algorithm keys must be longer for equivalent resistance to attack than symmetric algorithm keys
    - Symmetric Key - AES
      - 128,192,256 bit key length
    - Asymmetric Key - RSA
      - 1024, 2048, 3072, 15360 bit key length
      - NIST key management guidelines state that 15360 bit RSA key == to 256-bit symmetric key
- Slower encryption speeds
  - Slower than symmetric encryption due to
    - Longer key length
    - Complexity of algorithm used
  - Both these requirements du to fact that 1 key is public.
    - To maintain security, asymmetric encryption must make it too difficult for hacker to crack public key and discover private key
- Asymmetric Key Cryptosystems are slow.
- Not designed as a full-speed data transport cipher.
- Only encrypt "messages" of limited size
  - RSA - encrypt data as large as key length
    - For a 2048 bit RSA key, you can only encrypt messages up to 1960 bits (245 bytes) long

## Symmetric vs Asymmetric

| Symmetric                                                                      | Asymmetric                                                                                                                                        |
| :----------------------------------------------------------------------------- | :------------------------------------------------------------------------------------------------------------------------------------------------ |
| Uses a secret key to encrypt and to decrypt messages.                          | Uses two keys, one by the sender and one by the receiver to encrypt and to decrypt messages respectively. The two keys are mathematically related |
| The secret key cannot be made public and known only to the sender and receiver | One of the keys, i.e. the public key can be made known to all parties concerned. While the sender keeps the other key, i.e. private key.          |
| Secure channel to distribute the key                                           | Public key can be exchanged in open over insecure communication channel                                                                           |
| Perform faster                                                                 | Perform slower                                                                                                                                    |
| N(N-1)/2, where N is the number of users in the group                          | 2N, where N is no of users in group                                                                                                               |
| Only Confidentiality, Availability                                             | Confidentiality, Availability, Authentication, Non-Repudiation                                                                                    |

## Combining Symmetric and Asymmetric

*done by me*

- Encrypt symmtric key with receiver's public key
- decriver decrypts symmetric key with his private key
- send messages by enctypting with shared private key

## Digital Certificates and Public Key Infrastructure (PKI)

### Defining Digital Certificate

- Trusted third party
  - Used to help solve the problem of verifying identity
  - Verifies the owner and that the public key belongs to owner
  - Helps prevent MITM attack that impersonates owner of public key
  - Information in Digital Certificate
    - Owner's name / alias
    - Owner's public key
    - Issuer's Name
    - Issuer's digital signature
    - Digital Certificate's serial no
    - Expiration date of public key

### Public Key Infrastructure (PKI)

### Managing Digital Certificates

- Technologies used for managing digital certificates
  - Certificate Authority (CA)
  - Registration Authority (RA)
  - Certificate Revocation List (CRL)
  - Certificate Repository (CR)
  - Web Browser

### Certificate Authority

- Trusted Third Party
- Responsible for issuing digital certificates
- Can be internal or external organisation
- Duties
  - Generate, issue and distribute Public Key Certificates
  - Distribute CA certificates
  - Generate and Publish certificate status info
  - Provide a means for subscribers to request revocation
  - Revoke public-key certificates
  - Maintain security, availabiloty, and continuity of certificate issuance signing functions
- Subscriber requesting digital certificate
  - Generate public and private keys
  - Send public key to CA
  - CA may in some instance create keys
  - CA inserts public key into certificate
  - Certificates are digitally signed with private key of issuing CA

### Registration Authority (RA)

- Subordinate entity designed to handle specific CA tasks
  - offloading registration functions create improved workflow for CA
- Duties
  - Receive, authenticate, process certificate revocation requests
  - Identify and authenticate subscribers

### Certificate Revocation List (CRL)

- Lists digital certificates that have been revoked
- Reasons for revoke
  - Certificate no longer used
  - Details of certificate changed, such as user's address
  - Private key has been lost / exposed

### Certificate Repository (CR)

- Publicly accessible centralized directory of digital certificates
- Used to view certificate status
- Can be managed locally as a storage area connected to CA server
- Can be made available through a web browser interface

### Managing Digital Certificates

- Web browser management
  - Modern web prosers preconfigured with default list of CAs
- Advantages
  - Users can take advantage of digital certifcates without need ot manually load information
  - Users do not need to install CRL manually
    - Automatic updates feature will install them automatically

### Tyoes of Digital Certificates

- DIfferent categories
  - Class 1-5
    - Class 1  - Personal Certificate
    - Class 2  - Server Certificate
    - Class 3  - Software publisher Certificate
- Other uses
  - Secure communication between clients and servers by encrypting channels
  - Encrypt messages for secure internet email communication
  - Verify identity of clients and servers on web
  - Verify source and integrity of signed executable code

### X.509 Digital Certificate Standard

- Standard for most widely accepted format of digital certificate

### Public KEy Cryptogtaphy Standards (PKCS)

- Numbered set of PKI standards defined by RSA corporation
  - Widely accepted in industry
  - Based on RSA algorithm

## Cryptographic Hash Functions

- Used for creating a unique digital fingerprint for set of data
  - Output of hash function cannot be used to reveal original data set
  - Primarily used for comparison purposes
- Data Integrity
  - Send message digest along with messsage
  - If hash match, data is unaltered
- Unsalted vs Salted
  - When salt is added, even if both people have same password, hash output is different

### Characteristics of Cryptographic Hash Functions

- Secure hashing algorithm characteristics
  - Fixed Size
    - Short and long data sets have same size hash
  - Unique
    - 2 different data sets cannot produce same hash
  - Original
    - Dataset cannot be created to have predefined hash
  - Secure
    - Resulting hash cannot be reversed to determine original plaintext

### Example of Hash Function

- ATM
  - Bank customer has PIN of 93542
  - No is hashed and stored in magnetic stripe
  - User inserts card and enters pin
  - ATM hashes pin using same algorithm that was used to store PIN on card
  - If values match, user may access ATM

### Popular hash functions

- Message Digest 5
  - Weakness on compression function could lead to collisions
- Secure Hash Algorithm(SHA)
  - More secure than MD
  - No Weakness identified
  - SHA-1, 2, 3
    - SHA-1 to be phased out by 2017
  - SHA-2
    - Consists of 6 hash functions with digest (hash values) that are 224,256,384,512 bits

## Digital Signature

- Verifies the sender
  - Authentication
- Prevents sender from disowning message
  - Non-Repudiation
- Proves message integrity
  - Integrity

### How to digitally sign message

*done by me*

- Message to hash algoritm
- Message digest to be encrypted by sender's private key --> digital signature
- Attach Digital Signature to message --> Digitally signed message
- Digitally signed message send to receiver

### Verify digitally signed message

*done by me*

- Hash message and get the message digest --> MD1
- Decrypt the digital signature with sender's public key --> MD2
- Compare MD1 and MD2

### Code Signing

- Process that software publishers use to publish code over internet
- Ensure that code is from authentic publisher and also ensure integrity of code after it was published
- Advantages
  - Authentication - Verify who author of software is
  - Integrity - Verify software hasn't been tampered with
- Provides ability to trust updates
  - If update is released and is signed using same key as original, update can be trusted as it couldn't have come from elsewhere
  - All major operating systems and web browsers support code signing
    - use code signing to ensure malicious code cannot be distributed through patch system

## Referential Integrity

- Integrity assurance of data, especially in relational database management system(RDBMS) is made possible by referential integrity - ensures data is not left in orphaned state
- uses primary keys and related foreign keys in the database to assure data integrity
- Eg: If customer orders are tied to a customer and the customer is deleted/updated from the database, the order records must be deleted/updated as well (cascading deletes/updates)
- Failure to have referential integrity would lead to order (child) records existing in the database without being tied to a customer (parent)

## Resource Locking

- Used to assure data or information integrity
- When 2 concurrent operations are not allowed on same object, because 1 of the operations locks that record from allowing any changes to it, until it completes its operation, it is known as resource locking
- If resource locking protection is not properly designed, it can lead to potential deadlocks and DoS
- Deadlock is condition where 2 operations are racing each other to change state of shared object and each is waiting for other to release object

## Availability Techniques

### Failover

- Automatic switching from active transactional software/server/system/hardware component to standby/redundant system
- To assure high availability using failover techniques, important that all potential single points of failure are addressed in the design of the software solution
- eliminate potential single point of failure by single database server in data tier by adding a server to the data tier and creating a failover cluster from existing database server, the new server, and shared storage device

### Replication

- Single point of failure is characterized by having no redundancy capabilities and this can affect end-users when failure occurs
- By replicatint data, databases and software across multiple computer systems, a degree of redundancy is made possible
- Replication usually follows a master-slave or primary-secondary backup scheme in which there is one master or primary node and updates are propagated to the slaves or secondary node either actively or passively
- Active replication implies that updates are made to both the master and slave systems at the same time.
- In the case of Active/Passive replication, the updates are made to the master node first and then the replicas are pushed the changes subsequently.
- When replication of data is concerned, special considerations need to be given to address the integrity of data as well, especially in active/passive replication schemes.


### Scalability

- In computing, scalability is the ability of the system or software to handle increasing amount of work without degradation in its functionality or performance.
- Vertical Scaling
  - Additioal resources added to existing node
    - Adding additional memory and storage to existing application server
    - Increase the cnonection pool settings to handle greater connections to backend Database
- Horizontal Scaling
  - Newer nodes are added to existing nodes
    - Installing additional copies of same software
    - Add proxy cache server to existing deployment of application and web servers from 1 to 2 or more

## Authentication Design

### Multi-Factor Authentication

- Multi-factor or the use of more than one factor to authenticate a principal (user or resource) provides heightened security and is recommended.
  - Eg - Validate fingerprint (something u are) and pin code (something u know) before granting access provides more defense in depth than merely using username and password (something u know)

### Single Sign On (SSO)

- principal’s asserted identity is verified once and the verified credentials are passed on to other systems or applications, usually using tokens, then it is crucial to factor into the design of the software both the performance impact and its security.
- SSO simplifies credential management and improves user experiences and performance because the principal’s credential is verified only once.
- Improper design of SSO can result in security breaches that have colossal consequences. A breach at any point in the application flow can lead to total compromise

### Federation

- Extends SSO across enterprises
- In federated system, individual can log into 1 site and access services at another affiliated site without having to log in each time or re-establish identity

## Key Secure Design Principles

### Least Privilege

- Security principle in which a person or process is given only minimum level of access rights that is necessary for person / process to complete assigned operation. This right must be given only for a minimum amount of time that is necessary to complete the operation.

### Separation of Duties

- AKA compartmentalization principle / separation of privilege
- security principle which states that the successful completion of a single task is dependent upon two or more conditions that need to be met and just one of the conditions will be insufficient in completing the task by itself.

### Defense in Depth

- AKA layered defence
- security principle where single points of complete compromise are eliminated or mitigated by the incorporation of a series or multiple layers of security safeguards and risk-mitigation countermeasures.

### Fail Safe

- aims to maintain confidentiality, integrity and availability by defaulting to a secure state, rapid recovery of software resiliency upon design or implementation failure
- fail secure is commonly used interchangeably with fail safe, which comes from physical security terminology.

### Economy of Mechanisms

- Keep it simple
- the likelihood of a greater number of vulnerabilities increases with the complexity of the software architectural design and code
- By keeping the software design and implementation details simple, the attackability or attack surface of the software is reduced

### Complete Mediation

- Ensures that authority is not circumvented in subsequent requests of an object by a subject, by checking for authorization (rights and privileges) upon every request for the object
- The access requests by a subject for an object is completed mediated each time, every time.

### Open Design

- Implementation details of the design should be independent of the design itself, which can remain open
- unlike in the case of security by obscurity wherein the security of the software is dependent upon the obscuring of the design itself
- When software is architected using the open design concept, the review of the design itself will not result in the compromise of the safeguards in the software.

### Least Common Mechanisms

- disallows the sharing of mechanisms that are common to more than one user or process if the users and processes are at different levels of privilege
- Eg the use of the same function to retrieve the bonus amount of an exempt employee and a non-exempt employee will not be allowed.
  - calculation of the bonus is the common mechanism.

### Psychological Acceptability

- maximizing the usage and adoption of the security functionality in the software by ensuring that the security functionality is easy to use and at the same time transparent to the user
- Ease of use and transparency are essential requirements for this security principle to be effective

### Weakest Link

- resiliency of your software against hacker attempts will depend heavily on the protection of its weakest components, be it the code, service or an interface

### Leveraging Existing Components

- focuses on ensuring that the attack surface is not increased and no new vulnerabilities are introduced by promoting the reuse of existing software components, code and functionality.h

