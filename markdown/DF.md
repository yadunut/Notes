<!-- markdownlint-disable MD025 -->

# Digital Forensics

- [Digital Forensics](#digital-forensics)
- [Objectives of forensics](#objectives-of-forensics)
  - [What does Forensics Involve](#what-does-forensics-involve)
  - [Forensics Data](#forensics-data)
    - [Categories](#categories)
  - [Forensic Image](#forensic-image)
  - [Traditional Imaging Process](#traditional-imaging-process)
  - [Image creation Tools](#image-creation-tools)
  - [Encase Evidence File](#encase-evidence-file)
  - [Challenges](#challenges)
- [Investigative Process](#investigative-process)
  - [Key steps in FI process](#key-steps-in-fi-process)
  - [Preliminary Assessment](#preliminary-assessment)
  - [Preparation Stage](#preparation-stage)
  - [Search and Seizure](#search-and-seizure)
  - [At crime scene](#at-crime-scene)
    - [Securing the Scene](#securing-the-scene)
    - [Preliminary Interviews](#preliminary-interviews)
    - [Document Scene](#document-scene)
    - [Searching and Seizing](#searching-and-seizing)
    - [Chain of Custody](#chain-of-custody)
    - [Bagging and Tagging](#bagging-and-tagging)
    - [Transporting](#transporting)
  - [At Lab](#at-lab)
    - [Evidence Acquisition](#evidence-acquisition)
    - [Documenting and Reporting](#documenting-and-reporting)
- [Evidence Extraction and Analysis](#evidence-extraction-and-analysis)
  - [Slack Space](#slack-space)
  - [Unallocated Space](#unallocated-space)
  - [Allocated Space](#allocated-space)
  - [Evidence Examination](#evidence-examination)
    - [Manual Inspection](#manual-inspection)
    - [File Signatures](#file-signatures)
    - [Timestamp and other metadata](#timestamp-and-other-metadata)
    - [String and Keyword searching](#string-and-keyword-searching)
    - [File Carving](#file-carving)
  - [Analysis of Extracted Data](#analysis-of-extracted-data)
    - [Timeframe Analysis](#timeframe-analysis)
    - [Data Hiding Analysis](#data-hiding-analysis)
    - [Application and File Analysis](#application-and-file-analysis)
  - [Collecting evidence from OS](#collecting-evidence-from-os)
    - [Web Browser](#web-browser)
    - [Chat Logs](#chat-logs)
    - [Event Logs](#event-logs)
    - [Logon Events](#logon-events)
- [Windows Artifacts](#windows-artifacts)

# Objectives of forensics

- Recover, analyze, present computer based material
- Presented in court of law
- Help identify evidence in short time
- Eliminate potential impact of malicious activity on victim
- Assess intent and identity of the perpetrator

## What does Forensics Involve

- Involves preservation, identification, extraction, interpretation, documentation of evidence
- Legal process, integrity of evidence, factual reporting of information
- Provide expert opinion in court and administrative proceeding as to what was found

- Preservation
  - Forensic Investigator (FI) must preserve integrity of original evidence
  - Should not be modified or damaged
  - FI must make image / copy of original evidence and perform analysis
  - Compare copy with original evidence to identify modifications or damages
  - Prove evidence is exactly the same as original
    - Hash function is used

- Identification
  - Starts investigation by identifying evidence and location
    - May be in desktop/laptop server, removable media
  - Locating and identifying info is a challenge for FI

- Extraction
  - Data should be extracted immediately
  - Volatile data can be lost at any time, FI must extract these from copy he made from original evidence
  - Extracted data must be compared with original evidence and analyzed

- Interpretation
  - Interpret what has been found
  - Analysis and inspection of evidence must be interpreted in a lucid manner

- Documentation
  - Must be maintained from beginnning of investigation to the end
    - Chain of custody forms

## Forensics Data

- Digital evidence is information stored or transmitted in a digital form
  - Emails, photos, Word docs, IM history, browser history, RAM

### Categories

- Active data
  - Data that can be seen
    - Files, programs, data used by OS
- Latent Data
  - Data that exists despite bbeing deleted
    - Data that was partially overwritten / stored in slack space
    - Specialized tools required for recovering this data
- Archival Data
  - Data in backup
    - Can be stored in offshore tapes, flash drives

- Persistent Data
  - Stored in hard drive / other mediums
  - Preserved when PC is turned off
- Volatile Data
  - Data stored in memory / in transit
  - Lost when computer loses power / turned off
  - RAM / registries / cache

## Forensic Image

- Forensic image of affected / suspect computer
- Copy of original evidence collected by a tool that performs bit-level copying from one location to another

- 3 common disk image formats
  - Expert Witness/EnCase (E01)
  - Raw (DD)
  - Virtual Machine disk file (VMDK, OVF)
- Types
  - physical / logical copy of hard drive
  - Memory Dump
  - Copies of removable media

- FI should create 2 bbit stream copies of evidence

- Types of images
  - Complete disk
    - Preferred as most comprehensive
  - Partition
    - Allocation units from individual partition on driev
    - Includes unallocated space & slack within partition
    - Does not capture all data on drive
    - Taken only under certain situations 
      - Large disk
  - Logical
    - Only certain files

## Traditional Imaging Process

- Performed on hard drives
- Computer turned off and booted to forensic imaging environment
- Disk plugged into imager / examination workstation for duplication
- Hardware Write Blockers
  - device that sits in connection between computer and storage unit
  - Monitors the commands being issued and prevents computer from writing data to storage device
  - Comes with many interfaces

## Image creation Tools

- Commercial
  - Guidance Software - EnCase
- Open Source
  - DC3dd
  - dd

## Encase Evidence File

- Image file
- Contains bit-stream image of drive
- CRC verification
- Case identification info
- MD5 hash
- Header info as entered by examiner becomes part of evidence file and cannot be changed
- Computes a CRC for every block of 64 sectors
- MD5 hash is computd for entier data

## Challenges

- Growth in electronic devices
- Growth in storage fize
- Authenticity and integrity of evidence
- Special hardware and software tools used

# Investigative Process

1. Evidence Acquisition
2. Investigation and Analysis
3. Report Findings

## Key steps in FI process

1. Crime suspected
2. Preliminary assessment
   - FI should determine occurence of incident and impact
      - Know what to look out for
      - List steps to be taken during investigation
   - Evidence should be relevant and admissible
      - Evidence that proves / disprove facts in case
      - Admissible evidence that conforms to all regulations, states governing nature and manner in which it was obtained
3. Obtain search warrant for seizure
4. Perform first response procedures at crime scene
5. Forensic duplication / imaging at forensic lab
6. Generate hash value
7. Prepare Chain of Custody
8. Store evidence in secure location (Evidence bag)
9. Analyze image copy for evidence
10. Prepare forensic examiner report
11. Submit report to client
12. Attend court and testify as expert witness

## Preliminary Assessment

- FI should determine occurence of incident and impact
  - Know what to look out for
  - List steps to be taken during investigation
- Evidence should be relevant and admissible
  - Evidence that proves / disprove facts in case
  - Admissible evidence that conforms to all regulations, states governing nature and manner in which it was obtained
- Prioritise evidence
  - Location of evidence @ scene
  - Stability of media
- Establish how to document evidence
- Evaluate storage location for EM interference
- Evaluate necessity to provide power supply to battery-operated devices

## Preparation Stage

- Info to find out
  - Description of incident
  - Incident manager running incident
  - Location
  - Deatails of what to be seized
  - Other work to be performed
- What to take
  - Acquisition
    - Forensic software
    - Large capacity hard drive
    - Live response tools
    - Write block
    - Drive adapters
  - Documentation
    - Camera
    - Notepad, pens
  - Disass tools
    - Toolkits
    - Anti-static wrist straps
  - Packing
    - Anti-static bags
    - Evidence bags
    - Evidence tape
    - Cable ties
    - Sturdy box
  - Others
    - Gloves

## Search and Seizure

- Investigator has to ensure he has right to search / seize evidence in qn
- Voluntary Surrender
  - Primary owner different from suspect
  - Business critical-system, special arrangement is needed
    - Avoid disruption to business
- Search warrant
  - Allows law enforcement officers to acquire evidence from suspect's machine w/o giving suspect/owner prior notice
  - Warrants can be issued for Company/floor/room
  - Issued for all parts of a target computer
  - Only applicable for law enforcement officials

## At crime scene

1. Secure Scene
2. Conduct preliminary interviews
3. Document scene
4. Search and Seizing
5. Bagging and Tagging
6. Transport electronic evidence

### Securing the Scene

- Ensure all persons are removed from area where evidence is to be collected
- Done by security team
  - Make initial entry, secure area for search team
  - Search team will carry out actual search operations

### Preliminary Interviews

- Done in parallel with documenting scene
- Enquire about those who were present on site
- Conduct interviews and record location @ time of entry
- Gather info
  - Owner of device found
  - Password to access system
  - Offsite storage?

### Document Scene

- Before anything is touched, scene is recorded through notes / sketches / video / photos
- Document physical scene
  - Mouse location
  - Location of components near system
- Condition of computer scene, storage media
- Photo of monitor, rear of computer
- Photo of entire site, 360 degree

### Searching and Seizing

- Use latex gloves when handling evidence
- Avoid leaving fingerprints / hair / fibres
- Do not change state of device / equipment
  - If off, leave it off
  - If on, leave it on
    - Take photograph of screen
    - Record running programs

- How to handle Computer that is running
  - Freeze system by pulling power plug
    - Destroys everything in memory
    - Corrupt evidence files
  - Perform proper shutdown
    - Writes many entries to log files and changes state of evidence
    - Computer could run procedures that cleanse log files on shutdown, destruction of evidence
  - Leave system running
    - Run live forensic software
    - Good if many workstations

- Internal Hard Disk
  - Anti-static strap
  - Disassemble case to permit physical access
  - Ensure equipment is protected from magnetic fields
- Document internal storage devices
  - Drive condition
  - Internal components
- Disconnect storage devices to prevent distruction / damage / alteration

### Chain of Custody

- All evidence presented in court must exist in same condition as it was collected
- Document logs every move and access of evidence
- Starts when evidence is collected
- Used to prove integrity of evidence
  - Who collected evidence
  - Where is it stored
  - Who took possession
  - How was it stored
  - Who took it out of storage and why
- To be recorded
  - Date and time
  - Action Type
  - Personnel collecting / accessing evidence
  - Computer descriptive information
  - Disk Drive descripting information
  - Handling procedure
  - Complete description of action
  - Reason for action

### Bagging and Tagging

- Bagging - protects against contamination & tampering
- Tagging - provide means of associating evidence with location, date time, case, event, seizure agent
- First link in chain of custody
- Label all cables and photograph in ear of computer with cables and tag in palce
- Pack magnetic media in antistatic packaging
- Should be numbered in format (initials/date/exhibit no seized by person/sequence no for part in exhibit)

### Transporting

- Electronic evidence collected away from magnetic sources
- Away from high temperature and humidity
- Do not place in car boot
- Maintain chain of custody on evidence

## At Lab

### Evidence Acquisition

- Acquired in a manner that protects and preserves integrity of evidence

1. Document hardware and software config of examiner system
2. Disassembble case of computer to be examined
3. Identify storage devices that need to be acquired
4. Document Internal storage devices and hardware config
5. Disconnect storage device to prevent destruction / damage / alteration of data
6. Remove storage device and perform acquisition using examiner system (whenever possible)
7. Ensure examiner storage device is forensically clean

### Documenting and Reporting

- Actions and observations should be documented throughout forensic processing of evidence
- Conclude with written report of findings
  - Documenting steps following analysis
  - Documented and should be continuous process
- Factors to consider
  - Include dates, descriptions and results of action taken
  - Document irregularities encounted and any action taken
  - Additional info such as network topology, list of authorized users, passwords

# Evidence Extraction and Analysis

- Cluster - smallest allocation unit of hard disk
  - Minimum size is 1 sector
  - 8 sectors normally
- Sector - Smallest physical storage unit on disk
  - 512 bytes normally

## Slack Space

- Unused space between end of file and end of defined cluster
- When file is written and does not occupy entire cluster, remaining space is slack space
- Assume OS uses 4k cluster and 512 byte sector. 
  - If 2000 byte file was written to this cluster, remaining 2096 bytes would be slack
- Within slack space
  - Between end of actual file and sector in which file ends
    - AKA RAM Slack, padded with data as determined by OS
  - Remaining sectors in cluster that contains no data
    - OS dependent
    - Can be untouched / wiped
    - Remnants of previous file
    - Analysis of slack space could expose sensitive info

## Unallocated Space

- Space on hard drive that is available to write data to
- Not viewable to the typical user and requires specialized forensic software to view
- Can contain deleted files / partially deleted file
  - When file deleted, pointer to file is removed, but data remains in unallocated space until OS stores another file in the same space

## Allocated Space

- Allocated / Active space
  - Area/space on drive contains the OS and user data
  - Easily accessible to computer user

## Evidence Examination

- Extract and analyze digital evidence
  - FI should generate hash of image copy. 2 hashes should be the same
  - Examination on image to avoid tampering
- Extraction - recovery of data from its media
- Analysis refers to interpretation of recovered data and putting it in a logic useful format

### Manual Inspection

- If size of data is small, might be faster than figuring out a better way
- Provides increased confidence in results
- Commonly used to validate result

### File Signatures

- Attackers rename files to disguise themselves as another file
  - Windows names temp files with .TMP even though they may be word/exel documents when user opens email attachment
- Just examining file extension is risky way to perform analysis

### Timestamp and other metadata

- Full filename, file sizes, MAC times, MD5 hash
- Based on last accessed / modified
- Search for known files by comparing MD5 / SHA1 hash of file content

### String and Keyword searching

- Most basic extraction method
- List of keywords that are used to search evidence
- Common techniques
  - Based on file names / patterns in file names
  - Keyword in content
- Certain conditions such as encoding / formatting can render search string useless
- Important FI understand how string is represented in the data

### File Carving

- Combines aspects of several methods
- Saerch for unique sequence of bytes that correspond with header / first few bytes of file
- Most common file formats have standardized header that marks beginning of file, footer that marks end of file

## Analysis of Extracted Data

- Understand what syspect was trying to do
  - Timeframe analysis
  - Data hiding analysis
  - Application and File analysis

### Timeframe Analysis

- Determine when events occured in computer
- Can be used to associate usage of computer to time that event occured
- Review time stamps and date stamps found in file metadata
  - Last modified, last accessed, created, change of status
  - Review event logs

### Data Hiding Analysis

- Useful in detecting concealed data and may indicate knowledge, ownership or intent
- Identify mismatched file headers against file extensions - presence of mismatch nidicates malicious intent to conceal data
- Access all password-protected, encrypted and compressed files 
  - Illegitimate user has tried to conceal data from unauthorized users
- Steganography

### Application and File Analysis

- Inference from files identified provide details such as proficiency of user
- Review file namses for relevance and patterns
- Examine file contents
- Co-relating files to applications installed on target computer
- Look for similarities between files 
  - E.g. co-relating internet history to cache files and email attachments

## Collecting evidence from OS

### Web Browser

- May contain indirect evidence of specific crimes
  - Suspected having cracked password to hack server
  - Indirect evidence may be found in his browser
- Check browser history
  - IE browser history

### Chat Logs

- Criminal activities facilated via chat room discussions
- Most chat software keep temporary log of conversations

### Event Logs

- Generated by system-wide auditing and monitoring mechanisms built into Windows OS
- By reviewing logs
  - Identify success/fail logon attempts and their origin
  - Track create/start/stop of system service
  - Track usage of specific apps
  - Track alterations to audit policy
  - Track changes to user permissions
  - Monitor events generated by installed apps
  - 3 Event Logs
    - Application
      - Activities related to user programs
      - Include any errors / information app wants to report
      - Antivirus, IPS record to this log
    - System
      - log events reported by a variety of core OS components
      - Windows service events, changes to time, driver loads, network config issues
    - Security
      - Auth and security processes recorded here
      - Include user logon / logoff attempts, account creation, user priviledge changes, etc
    - Local / group policy can be configured to show which security events are captured and logged
- Log stored in root\system32\winevt\logs\security.evtx

- Every event tracked in Windows has associated ID
- Often more useful than event message

### Logon Events

- Logon type useful datapoint when searching / filtering security logs
  - If you know attacker accesses the system using stolen credentials via "net use" command, you can disregard unlock and console logons
- Logon Process - Process that initiated logon event
- Authentication Package - Secutity authentication prococol used to process logon event
- Workstation Name - Source system from which logon originated
- Source Network Address - Source IP from which logon originated

# Windows Artifacts

- 
