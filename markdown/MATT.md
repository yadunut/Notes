<!-- markdownlint-disable MD025 -->

- [Malware Analysis Tools and Techniques](#malware-analysis-tools-and-techniques)
- [Introduction](#introduction)
  - [Malware](#malware)
  - [Symptoms](#symptoms)
  - [Malware Analysis Techniques](#malware-analysis-techniques)
- [Analysing Windows Malware](#analysing-windows-malware)
  - [File System Functions](#file-system-functions)
  - [Special Files](#special-files)
  - [Windows Registry](#windows-registry)
  - [Registry Terms](#registry-terms)
  - [Root Keys](#root-keys)
  - [Common Registry Functions](#common-registry-functions)
  - [Registry Tools](#registry-tools)
  - [Networking API](#networking-api)
    - [Sniffers](#sniffers)
    - [WinINET API](#wininet-api)
  - [Process Manipulation](#process-manipulation)
  - [Keyloggers](#keyloggers)
    - [Hooking the keyboard](#hooking-the-keyboard)
    - [Polling Keyboard](#polling-keyboard)
- [Basic Static Analysis](#basic-static-analysis)
  - [Malware Fingerprint](#malware-fingerprint)
    - [AV Scanning](#av-scanning)
    - [Virus Total](#virus-total)
    - [Hashing](#hashing)
  - [Strings in malware](#strings-in-malware)
  - [Portable Executable Format](#portable-executable-format)
    - [Source to Execution](#source-to-execution)
    - [Loading a PE](#loading-a-pe)
    - [Static Linking](#static-linking)
    - [Dynamic linking](#dynamic-linking)
    - [Relative Virtual Addresses (RVA)](#relative-virtual-addresses-rva)
    - [Importing Functions](#importing-functions)
    - [Base Relocation](#base-relocation)
    - [Dependency Walker](#dependency-walker)
  - [Packing Executable](#packing-executable)
    - [Detecting Packers](#detecting-packers)
- [Basic Dynamic Analysis](#basic-dynamic-analysis)
  - [Running the Malware](#running-the-malware)
  - [Process Monitoring](#process-monitoring)
    - [Procmon](#procmon)
    - [Process Explorer](#process-explorer)
  - [File Monitoring](#file-monitoring)
  - [Registry Monitoring](#registry-monitoring)
    - [Regshot](#regshot)
    - [CaptureBat](#capturebat)
  - [Network Monitoring](#network-monitoring)
    - [ApateDNS](#apatedns)
    - [Netcat](#netcat)
    - [Wireshark](#wireshark)
- [Advanced Static Analysis](#advanced-static-analysis)
  - [Preliminaries - Introduction](#preliminaries---introduction)
- [Advanced Dynamic Analysis - Debugging](#advanced-dynamic-analysis---debugging)
  - [Source Level vs Assembly Level](#source-level-vs-assembly-level)
  - [Using Debuggers](#using-debuggers)
  - [Breakpoints](#breakpoints)
- [Malicious Web Pages and Documents](#malicious-web-pages-and-documents)
  - [Browser Based Attack](#browser-based-attack)
  - [Deobfuscating Javascript](#deobfuscating-javascript)

# Malware Analysis Tools and Techniques

# Introduction

## Malware

- Malicious Software
  - Used to compromise computer functions
  - Steal data
  - bypass access controls
  - cause harm to host computer
- Adware
  - Malware that delivers advertisements
  - Pop up ads on websites that are displayed by software
- Bots
  - Programs created to automatically perform specific operations
- Bugs
  - Flaw that produces undesired outcome
  - Security bugs allow attackers to
  - Bypass user auth
  - Override access privileges
  - Steal data
- Ransomware
  - Holds computer system captive while demanding ransom
- Rootkits
  - Remotely access/control computer without being detected
- Spyware
  - Spy on user activity without knowledge
  - Activity Monitoring, Keystroke Collection, Data harvesting
- Trojan Horses
  - Malware which disguises itself as normal program/file to trick users into downloading and installing it
- Viruses
  - Capable of copying itself and spreading to other computers
  - Spread to other computers by attaching to programs and executing code when launched
- Worms
  - Most common type
  - Spread over computer network
  - Exploit OS vulnerabilities
  - Cause harm by consuming bandwidth and overload web servers

## Symptoms

- Increased CPU usage
- Slow computer/web browser speeds
- Problems connecting to networks
- Freezing or crashing
- Modified/Deleted files
- Appearance of strange files/programs/desktop icons
- Progrms running/turning off/reconfiguring themselves
- Stange behaviour
- Emails/messages sent automatically without user knowledge

## Malware Analysis Techniques

- Basic Static Analysis
  - Examining executable file without viewing actual instructions
  - confirms whether file is malicious, provide info on functionality
  - Provide info to produce simple network signatures
  - Straightforward and quick, but ineffective against complex malware
- Basic Dynamic Analysis
  - Involve running malware and observing behaviour on system
  - To remove infection
  - Produce effective signatures
  - Needs safe environment to run (VM)
- Advanced Static Analysis
  - Reverse Engineering malware internals by loading into disassembler
  - Looking at program instructions to discover what program does
  - Tells you exactly what program does
  - Stepper learning curve than basic static and requires specialized knowledge of disassembly, code constructs, windows OS concepts
- Advanced Dynamic Analysis
  - Uses debugger to examine internal state of running malicious executable
  - Provide another way to extract info from executable
  - Most useful when obtaining information that is difficult from other techniques

# Analysing Windows Malware

- Windows is most popular OS
- Malware interacts with OS via API to exectute code
- Uses its own name to represent C types
- Word(w)
  - 16 bits
- DWord(dw)
  - 32 Bit
- Handles(H)
  - Reference to object. Information stored in handles is not documented and should be manipulated only by Windows API
  - Items that have been opened by OS such as windows, process, module, file
  - Pointers and point to location in memory
  - Can only be stored. Arithmetic operations cannot be performed
  - E.g CreateWindowEx returns handle to window: HWND
  - E.g HModule, HInstance, HKey
- Long Pointer(LP)
  - Pointer to another type
  - E.g LPByte is pointer to byte
  - LPCStr pointer to cstring
- Callback
  - Function that will be called by windows API
  - E.g InternetSetStatusCallback passes a pointer to function that is called when system has update of internet status.

## File System Functions

- CreateFile
  - Creates or Opens files
  - Open existing files/pipes/streams/IO devices
- ReadFile/WriteFile
  - Read/write to files
  - Operate on files as a stream
  - First time ReadFile is called, first n bytes is read
  - Next call, next n bytes read
- CreateFileMapping and MapViewOfFile
  - Allow file to be loaded in memory to be manipulated
  - Commonly used in malware as it allows for easy manipulation
  - CreateFileMapping - Loads file from disk to memory
  - MapViewOfFile returns pointer to base addr of mapping which is used to access file
  - Pointer to the base addr can be used to read/write file and jump around easily
  - Useful for parsing files

## Special Files

- Can be accessed like regular files but without drive letters/folders
- Stealthier than regular files as they dont show up in directory listings
- Shared Files
  - \\serverName\share
- Files accessed via Namespace
  - \\.\PhysicalDisk1(where \\.\ is namespace for win32 device)
  - Allows direct access to disk bypassing the file system
  - Malware can write to unallocated space on disk
- Alternate Data Streams(ADS) allow additional data to be added to NTFS file
  - Can add one file to another as a alternate stream
  - Additional stream does not show up in directory listing
  - ADS is named according to convention normalFile.txt:Strean:$DATA
  - Allows program to read and write to a stream
  - ADS can be used to hide data.

## Windows Registry

- Used to store OS and program config info such as settings and options
- Good source of host-based indicators
- hierarchical database of info to improve performance
- Nearly all windows configs are in the registries
  - Networking, drivers, startup, user accounts
- Malware uses registry for
  - Persistence
  - Configuration

## Registry Terms

- Root Key
  - Registry is divided into 5 top level sections called root key/hives
  - term HKEY
- Sub Key
  - Like a Subfolder
- Key
  - It's folder that can contain other folder
  - Root key and sub keys are both keys
- Value entry
  - Ordered pair with a name and value
- Value/data
  - Value/data is stored in the registry entry

## Root Keys

- HKEY_LOCAL_MACHINE (HKLM)
  - Stores settings which are global to local machine
- HKEY_CURRENT_USER (HKCU)
  - Stores settings specific to current user
- HKEY_CLASSES_ROOT
  - Stores information defining types
- HKEY_CURRENT_CONFIG
  - Stores settings on current hardware config
- HKEY_USERS
  - Defines settings for current user/new user/default user

## Common Registry Functions

- RegOpenKeyEx
  - Opens registry for querying / editing
- RegSetValueEX
  - Add value to registry and sets its data
- RegGetValue
  - Returns data for value entry

## Registry Tools

- Regedit
  - Edit registry entries
- Autoruns
  - Parses registry to find entries that start applications upon booting the OS
- Regshot
  - Captures registry before and after

## Networking API

- socket
  - Create a socket
- bind
  - Attaches a socket to a particular port, prior to the accept call
- listen
  - Indicates that a socket will be listening for incoming connections
- accept
  - Opens connection to remote socket and accepts connection
- connect
  - Opens connection to remote socket;remote socket must be waiting for connection
- recv
  - Receives data from remote socket
- send
  - Sends data to remote socket

### Sniffers

- Create a RAW Socket
  - WSASocket() / socket()
- Bind socket to Interface
  - Bind()
- Put interface to promiscuous mode
  - WSAloctl() / ioctlsocket()
  - promiscuous mode is mode for NIC to cause controller to pass all traffic to CPU
  - Instead of passing only frames controller is intended to receive

### WinINET API

- Higher level API that implements higher level protocols
- `InternetOpen`
  - Initialise a connection to internet
- `InternetOpenURL`
  - Connect to a URL
- `URLDownloadToFileA`
  - Downloads file from the internet
- `InternetReadFile`
  - Reads file off the internet

- Downloaders usually consists of 2 steps
  - `URLDownloadToFile()`
  - Execute newly downloaded file
  - `ShellExecute()` / `WinExec()`

## Process Manipulation

- creates new process to by-pass host-based firewalls / hide from user
  - `CreateProcess` is used to create a new process
  - Param `STARTUPINFO` includes handle to stdin, stdout and error messages
- Malicious programs can set these to a socket, allowing attacker to execute remote shell

- Parent process can specify properties associated with main window of child process
- CreateProcess takes a pointer to STARTUPINFO struct as one of its params
  - Use members of this struct to specify characteristics of child process's main window

## Keyloggers

- Monitors user key strokes
- Many bots use this method to spy on user and collect user info
- 2 common methods: 
  - Install hook for keyboard events
  - Poll keyboard state with `GetAsyncKeyState()`

### Hooking the keyboard

- Mechanism which application can intercept events such as messages, mouse actions, keystrokes
- Hook Procedure is function that intercepts particular type of event
  - Can act on each event it receives and modify/discard event

- `SetWindowsHookExA` with `WH_KEYBOARD` param
  - Every time key pressed, event is relayed to malicious function which records key pressed
- `SetWindowsHookExA` with `WH_MOUSE` param
  - Intercepts mouse messages such as left-click/right-click

### Polling Keyboard

- Malware goes in a loop and poll state of every key
- `GetAsyncKeyState` called to get state of specific key
- Param is key being pressed

# Basic Static Analysis

## Malware Fingerprint

### AV Scanning

- 1st step to analyze a suspicious file is to scan using Antivirus Scanner
- AV Scanners
  - File signature
    - Identifies pieces of suspicious code
  - Heuristics
    - Behavioral and pattern-matching analysis

### Virus Total

- AVs are not perfect
  - Malicious file identified by AV may not be identified by another AV
- VirusTotal
  - Scans suspicious file using different AV engines
  - Generates report
  - Total no of AV which detected file as suspicious
  - Acquired by Google

### Hashing

- Hashing is common way of fingerprinting malware
- HASH is a string generated by hashing algorithm given an input
- 1 way function
  - Input cannot be recovered from hash

- Hashing Programs
  - MD5Deep
  - MD5 Calculator

## Strings in malware

- String is sequence of characters terminate with a NULL character
- Strings in program can reveal some info about what program does
- Can reveal
  - URLs
  - Filenames
  - Windows Function calls
- Represented in 2 ways
  - ASCII
    - 1 byte per character
    - Representation is in hex format
  - Unicode
- 2 bytes per character

- **Bintext** can be used to find strings in a executable

## Portable Executable Format

- Used by Windows executables, object code, DLLs
- Datastructure that contains info for Windows OS Loader to execute compiled codes
- Begins with Header
  - Info on code
  - Type of application
  - Required libraries
  - Space requirements
- Source Code --> Compiler --> Object File --> Linker --> Binary PE
- Binary PE --> Loader (<-- Libraries) --> Running Program

- PE File starts with DOS Header
  - Signature ("MZ")
  - Offset to the PE Header
- Followed by a PE Header
  - Machine type
  - No of sections
  - Timestamp
  - Data Directory
    - Table where in the image is stored
    - Export, import, resource, exception, security, base, relocation,debug
- Section Table
  - Named list of sections in PE File
    - .text
      - Executable Code
    - .data
      - Reda/write initialized data
    - .rdata
      - Read only data
    - .edata
      - to run image that requires calling a dll, the loader needs to be able to find entry points into dll. 
      - Conceptually associated with dll is list of addresses(RVAs) that other modules can call
      - Each exported entry is assigned unique ordinal value
      - Module that wants to call an entry point only needs to know dll's name and ordinal value
      - Export table assists by specifying ordinal value and their names
    - .resrc
      - Resources for image such as icons, bitmaps
      - Organized like file system
    - .debug
      - Debug info
    - .idata, .edata, .reloc, etc.
    - Module linker combines text and data from various object modules to form executable image
    - Compilers can append "$..." to end of names to dictate order within section
      - 'text$X' is before '.text$Y'

### Source to Execution

- Programmer writes Source File 
  - Helloworld.c
- Compiler translates to Object module
  - helloworld.obj
- Linker combines various object modules to a Executable Image
  - helloworld.exe
- Loader does final work in getting image executing on system

### Loading a PE

- Absolute Loading
  - Loads program at same address (Virtual/Physical) every time
- Relocatable Loading
  - Load program at different addresses based on what is available
- Dynamic run-time loading
  - Load and reload the program at different addresses while program is running

- Address Binding
  - Program to be executed must be brought to main memory
  - Insstructions that use address in program must be bound to address space in main memory
  - Address binding is a scheme that performs this task
  - Mapping one address space to another
  - Symbolic label/name is translated to actual address
  - Actual binding can be specified in program, resolved at compile/link/load/run time

### Static Linking

- When library is statically linked to binary, all executable code from library is copied to executable
- Difficult to differentiate which code belongs to statically linked code and which belongs to EXE
- PE Headers does not contain such info

### Dynamic linking

- Exe connect to libraries only when function is needed and not when Exe is loaded
- Exe searches and loads correct library at runtime
- Address of library function to connect to is resolved at runtime
- Information to resolve this address is stored in .idata section (Import section)

### Relative Virtual Addresses (RVA)

- Address where program runs may not be known at link time
- Any addersses stored in the code by the linker need to all be relative
- Virtual address that is relative to base address of executable program

### Importing Functions

- PE contains table of imported modules
- Each entry identifies the module and lists functions that need to be imported
  - Virtual Address
  - Ordinal Value
  - Function Name
- Stored in Import Address Table(IAT) and Import Name Table(INT)
  - Array of dwords(4 bytes)
  - Each dword is either function addr, ordinal, pointer to function name
  - Loader changes IAT value at load time to function addresses
  - For faster image startup, images can be bound
    - Resolving and overwriting IAT table in actual PE file
    - If imported DLL changes, binding needs to be redone. INT used for this purpose

### Base Relocation

- Each module has preferred load address
- Loader may not be able to always honor request
- If module is relocated, loader must fix up addresses
- .reloc section specifies each location that needs to be fixed if modules is moved

### Dependency Walker

- Shows dependencies


## Packing Executable

- Obfuscate / pack malware to make it hard to analyse
- means "making it unclear". Aim is to hide functionality of malware
- Packing executable is one way of achieving obfuscation
  - Compression
  - Encryption
    - EXE on disk is not as readable
- When packed, a small wrapper stub is used to decompress / decrypt the original executable before loading it in memory
- When a packed program is analysed, only the stub can be analysed

### Detecting Packers

- PEiD is software that can detect Packers
- Once packer is detected, UnPackers can be used to unpack the PE
- Popular packers
  - UPX, ASPack, PELock, Themida

# Basic Dynamic Analysis

- Any examination performed after executing malware
- Performed after static analysis has reached dead end
- Allows you to observe malware true functionality
- Put your system/network at risk. Use VM

## Running the Malware

- Many popular sandbox that automatically analyze malware and produce report
- GFI Sandbox, Anubis, Joe Sandbox
- Easy to understand output and good for initial triage
- Similar in approach

- Sandbox Overview
  1. Malware submitted to repository Via manual submission / scripted submission(honeypot/email/cron)
  2. Malware inserted into Repository
  3. Samples are retrieved by sandbox based on queue and priority
  4. Analysis results are sent back to repository
  5. User views analysis via web interface

- Provides basic static analysis 
- High level Dynamis analysis results
- Provides list of files that have been opened / read / created / deleted
- Mutexes created by malware
- Registry Activity
- Network activity
- Drawbacks
  - Command Line options
  - Waiting for Command-and-control instructions
  - Not all events may be recorded - Sandbox did not wait long enough
  - Malware may not detect it running in Sandbox
  - Conditions not met for malware to run properly
  - Sandbox OS may not be correct for malware to run properly

## Process Monitoring

### Procmon

- Combines filemon and regmon
- Monitors
  - Registry activity
  - File activity
  - Process Activity
  - Network Activity
- Procmon monitors all system calls for all processes
- Filter events

### Process Explorer

- Provides insight to running processes
- Features
  - List active processes
  - DLLs loaded for each process
  - Process properties
  - Active TCP connection
  - Create/kill/validate process

- Verify Option
  - Many malware has same name as legitimate windows processes
  - Verify allows you to verify whether a process has been digitally signed by Microsoft
  - Only applies to process on disk, not in RAM

## File Monitoring

## Registry Monitoring

### Regshot

- Regshot is open source registry comparison tool
- Compares 2 registry snapshots and reports on differences

### CaptureBat

- Behavioural analysis tool for WIN32 Apps
- Monitors state of system during execution of apps and processing of documents
- Performed at low kernel level
- Good tool to exclude event noise that natually occur in system

## Network Monitoring

- Often sends out information to another server
- Tries to connect to Command-and-control server to wait for instructions
- Fake a network - malware does not know that it is in a virtualized environment
- Can reveal most / all functions of malware

### ApateDNS

- Free tool
- Able to listen to DNS requests made by malware
- Spoof DNS responses
- NXDomain

### Netcat

- Can be used for inbound/outbound connections
  - Port scanning
  - Tunneling
  - Proxying
  - Port forwarding

### Wireshark

- Network sniffer that captures network packet
- Visualisation of network packets
- Packet stream analysis
- Indepth packet analysis

# Advanced Static Analysis

## Preliminaries - Introduction

- IDA Pro is disassembler for malware, vul analyses, debugging, reverse engineering
- Supports different file formats
  - Portable Executable(PE), Common Object File Format(COFF), Executable and Linking Format(ELF)
- Code Signatures in Fast Library Identification and Recognition Technology(FLIRT) - Allow recognition and labelling of disassembled functions

# Advanced Dynamic Analysis - Debugging

- Debugger is software/hardware used to test/examine execution of another program
- Provide different perspective from disassemblers
  - Provide info of how program looks before execution
- Debugger provides dynamic view of program as it run
  - Can show register, memory values as they change over time

## Source Level vs Assembly Level

- Source level debuggin allows a programmer to debug while coding
  - Integrated within IDE
  - Allows developer to set breakpoints for specific lines of code

- Assembly Level Debugging Operates on assembly code instead of source code
  - Used to step through assembly, one instruction at a time
  - Can set breakpoints to stop execution at specific assembly instructions

## Using Debuggers

- Single step 
  - Run 1 assembly instruction at a time
  - Can see register and memory changes
  - Good for understanding details of program code block
  - Take too long to analyze long and complex program

- When function call is made
  - Step Over
    - Bypasses detail assembly instruction of function call
    - Next instruction will be address where function call returns
    - Good for understanding big picture of what function is achieving
    - Quickly understand rough functions and features of PE
    - Some function calls never returns
      - Malware defence technique
      - Restart debugger if this occurs
  - Step Into
    - Next instruction is first assembly code of called function
    - Detailed understanding of function called

## Breakpoints

- Pause execution to examine program state
- Only view register changes and memory when program paused
- Cannot view changes when running

# Malicious Web Pages and Documents

- Malware may propagate through browser
- Browser based attacks
  - Misusing the browser
  - Privilege escalation
  - Social Engineering

## Browser Based Attack

- User directe to malicious website via link in email
- Website displayed annoying javascript base animation
- New window displayed an annoying Javascirpt based animation
- Popped up whenever the user closes one of the windows
- Could not close windows fast enough and ended up turning off PC

- Use virus total to check for malicious websites online

## Deobfuscating Javascript

- Stunnix Obfuscator
  - Obfuscating only layout of JS code
  - It removes spaces, comments, new lines
  - Renames user defined names with random srtings
  - Replace print strings with hex values
  - Replaces integers with complex equations

- Manual Deobfuscation
  - Javascript contains 3 Key elements
  - Variable, For loop, alert
