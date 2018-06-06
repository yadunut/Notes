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
