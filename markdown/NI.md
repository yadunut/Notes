<!-- markdownlint-disable MD025 MD033 MD024 MD006 MD029-->

# Networking Infrastructure

- [Networking Infrastructure](#networking-infrastructure)
- [Chapter 1 - Overview](#chapter-1---overview)
  - [Transmission Media & Network Cables](#transmission-media-network-cables)
  - [OSI 7 Layers](#osi-7-layers)
  - [Structured Cabling](#structured-cabling)
    - [Demarcation Point](#demarcation-point)
    - [Equipment Room (ER)](#equipment-room-er)
    - [Telecommunications Room (TR)](#telecommunications-room-tr)
    - [Backbone / Vertical Cabling](#backbone---vertical-cabling)
    - [Distribution / Horizontal Cabling](#distribution---horizontal-cabling)
    - [Work Area](#work-area)
      - [Servicing Work Area](#servicing-work-area)
- [Chapter 2 - Ethernet Switching](#chapter-2---ethernet-switching)
  - [Hubs](#hubs)
  - [Switches](#switches)
  - [Domains](#domains)
    - [Collision Domain](#collision-domain)
    - [Broadcast Domain](#broadcast-domain)
  - [Ethernet Switching](#ethernet-switching)
  - [Switching Operations](#switching-operations)
    - [Address Learning](#address-learning)
    - [Flooding](#flooding)
    - [Forwarding](#forwarding)
    - [Filter](#filter)
  - [Switching Modes](#switching-modes)
    - [Store-and-Forward Switching](#store-and-forward-switching)
    - [Cut Through Switching](#cut-through-switching)
    - [Fragment-Free Switching](#fragment-free-switching)
  - [Redundancy](#redundancy)
    - [Problems](#problems)
    - [Solution](#solution)
  - [Spanning Tree Protocol](#spanning-tree-protocol)
    - [Rules](#rules)
    - [Switches](#switches)
    - [Algorithm](#algorithm)
  - [Ethernet](#ethernet)

# Chapter 1 - Overview

## Transmission Media & Network Cables

- Twisted Pair
- Optical Fibre
- Coaxial Cable

## OSI 7 Layers

1. Physical Layer
2. Data Link Layer
3. Network Layer
4. Transport Layer
5. Session Layer
6. Presentation Layer
7. Application Layer

## Structured Cabling

Installation of cables in building / campus in structured manner

- **Demarcation Point**
  - Point where telecom prover network ends and connects with on-premise wiring at customer premise
- **Equipment Room**
  - Large Telecom room that may hourse servers, routers, switch, etc.
- **Telecommunications Room*
  - House Equipment and wiring consolidation points that serve users inside building
- **Backbone / Vertical / Riser Wiring**
  - Connects between telecommunication rooms, as rooms are nomally on different floors
- **Horizontal Wiring**
  - Connects telecommunications rooms (may use wiring closets) to individual outlets / work areas, through wireways / conduits / ceiling spaces
- **Work Area Components**
  - Connect end-user equipment to outlets of horizontal cabling systems

### Demarcation Point

- Point which outdoor cabling interfaces with intrabuilding backbone cabling
- Boundary between service provider and responsibility of customer

### Equipment Room (ER)

- After cable enters through Demarcation point, it travels to equipment room (ER)
- Centre of voice and data network
- Effectively a large Telco room that may house servers, routers, switches, etc.
- Equipment room is different from Telco room as ER is building / campus serving vs floor serving

### Telecommunications Room (TR)

- ER feeds to one or more TRs
- TRs are where backbone cabling transitions to horizontal cabling

### Backbone / Vertical Cabling

- Any cabling between ER and another TR throughout the facility
  - Includes TRs on same floor
  - Vertical Connection(risers) between TRs on different floors
  - Inter-buildings cabling in a multibuilding campus
- Usually Fibre Optic cables

### Distribution / Horizontal Cabling

- Distributes cables from TR to work areas
  - Usually UTP cables
  - Protects against pairs that might fail during installation

### Work Area

- Area serviced by individual TR
- usually occupies 1 floor / part of 1 floor of building

#### Servicing Work Area

- Uniform wiring plan must be used through patch panel system

# Chapter 2 -  Ethernet Switching

## Hubs

- Operates at Layer 1
- Only 1 PC can transmit at a time
- Physical star logical bus topoligies
- Collison possible in the hub

## Switches

- Operate at Layer 2 (including Layer 1)
- More than 1 PC can transmit at the same time
- Dedicated paths between pairs of communicating PCs
- No collision in the switch

## Domains

### Collision Domain

- Collision occur when 2 or more ethernet hosts transmit simultaneously
- Logical area in network where data packets can collide with one another
- range in size from single segment of cable to entire network
- Layer 1 devices, such as repeaters and hubs do not break up collision domains as these devices automatically forward all data sent on cable / other media
- Layer 2 and 3 devices, such as bridges, switches, routers break up collision domains

### Broadcast Domain

- area of network composed of all computers and networking devices that can be reached by sending frame to broadcast address
- Ethernet LANs are broadcast domain - any device connected to LAN can transmit frame to any other device

## Ethernet Switching

- Break large collision domains into parts using switch
  - reduces collisions and increases reliability
- Switching - technologies that decrease congestion in LAN by reducing traffic and increasing bandwidth
- LAN switches - Operating at Layer 2, forward frames based on MAC address

## Switching Operations

### Address Learning

- Reads source MAC address of each data frame that is transmitted and noting the port where the frame enters the switch
  - Eg. Port 1 -> MAC address AA:AA:AA:AA:AA:AA, Port 2 -> MAC address BB:BB:BB:BB:BB:BB, etc
- Stored in MAC Address Table
- Learnt Dynamically

### Flooding

- Sends out on all ports(except the port that frame entered from), when destination address is broadcast / unknown address

### Forwarding

- Forwards when destination is known
- Forwards frame to appropriate segment

### Filter

- Filter happens when destination is located on same interface
- Blocks frame from going on to other segments

## Switching Modes

### Store-and-Forward Switching

- Reads entire / complete frame into memory buffer & determine whether frame is valid / invalid
- Determine whether port is available before it switches the valid frames to outgoing destination port / segment
  - Frames are corrupted by checking CFC code field
- Advantage
  - Prevent wasting of bandwidth on destination by invalid / bad frames that can adversly affect network performance
- Disadvantage
  - Increases latency / delay due to frame integrity checking and memory buffering

### Cut Through Switching

- Fast forward switching / On the fly switching
- Reads beginning of frame up to destination MAC address field in frams as traffic flows through switch
- Does not wait for entire data frame to be read in before switching frame to destination port - **Cut Through**
- Advantage
  - Fast and minimum latency between ports
  - Requires less memory
- Disadvantage
  - Lacks error detection / frame error checking
  - Forwards corrupted and truncated frames & could congest network traffic with unwanted invalid frames

### Fragment-Free Switching

- Frames are buffered until first 64 bytes have been received
- Can check for any bad frames due to collision but will not be able to check for bad frames due to CRC errors
- Results in lesser latency as frame is sent after it has read 64 bytes
- Faster switching speeds
- Advantage
  - No frames less than 64 bytes forwarded
  - Disadvantage - Errors can be forwarded

## Redundancy

- Multiple switches and trunk links
- If one device fails, another one takes over

### Problems

- Switching loops give problems if all links are active
  - Broadcast storms
    - Flood broadcast through non source ports
  - Multiple frams transmission
    - Since A doesn't know where B is, flood, causing broadcast storm
  - Inconsistent switch tables
    - End device apprears to be on multiple ports

### Solution

- 1 path ata time
- Redundant parths must be shutdown, but ready to be opened when needed
- Done quickly and automatically
- **Spanning Tree Protocol(STP)** Does this

## Spanning Tree Protocol

### Rules

- Tree topology
  - Has no loops
- All devices are connected

### Switches

- Used by switches to turn redundant topology to spanning tree
- Disables unwanted links by blocking ports
- Switch runs STP by default - no config needed

### Algorithm

1. Select 1 switch to be **root bridge**
  - Bridge ID (BID) of priority value followed by MAC address
  - Switches exchange Bridge Protocol Data Units (BPDU) to compare bridge IDs
  - Switch with lowest bridge ID becomes root bridge
  - Admins can set priority to fix selection
2. Select a **root port** on each switch
  - Every non-root switch selects a root port
  - Port with shortest distance / lowest cost path to root bridge
  - If same distance, use lowest ID
3. Select a **designated port** on each segment
  - Port with lowest cost path to root bridge becomes designated port
  - If same cost, use lowest ID
4. Close down all other redundant ports
  - Any port not a root port / designated port is put in blocking state

## Ethernet

Too lazy to fill this up

# Chapter 3 - Static Routing Protocols

## Router

- Router is internetworking device that connects 2 or more networks
- Performs forwarding / filtering of data at network layer
- decisions based on destination IP address
- routes from one network to another until it reaches its destination

### Benefits

- Seperate network logically into subnets making it more manageable
- Control trafic flow between different networks
- Firewall for broadcast traffic
- interface between LAN(Ethernet) and WAN(PPP) protocols

## Static Routing

- entries in the routing table of router that are manually set to user defined specific paths
- Administrator must know entire network and manually configure all routes if all are static
- Useful in Stub Network(network that is accessible by only 1 path)

### Advantage

- Enhance Secutiry
  - Administrator might want to hide parts of intranetwork and specify only parts that need to be revealed
  - Static route forces traffic to take specific, secure route instead of route determined dynamically which can change as network topology changes, making traffic travel over insecure route
- Does not consume as much traffic - no routing updates are transmitted

### Disadvantage

- Not suitable for large networks - administrator must know **entire** network and **manually configure** all routes if all routers are static
- Any change to network means reconfiguring all routers to reflect change
- not able to reroute traffic if link fails

## Static route Operation

1. Network admin configures route in router
2. Router installs route in routing table
3. Packets are forwarded based on static route entries in routing table

## Defining Static Route

- Specify **Next Hop** address for packet
  - Next hop address is the address of the next router to transmit data to
  - Syntax - `ip route destination-network subnet-mask gateway`
    - `ip route 172.16.1.0 255.255.255.0 172.16.2.1` - Transmit all data going to 172.16.1.0 to 172.16.2.1
    - `ip route 172.16.5.0 255.255.255.0 172.16.2.1` - transmit all data going to 172.16.5.0 to 172.16.2.1
- Default Route
  - Special staitc route that follows format `ip route 0.0.0.0 0.0.0.0 next-hop-address`
  - Route packets with destinations that do not match other toutes
  - Routers are typically configured with default route for internet-bound traffic - impractical and unnecessary to maintain routes to all networks in internet

## Commands

- `show ip route`
  - shows ip routes present in routing table
- `traceroute <ip>`
  - displays route taken by packet and measuring transit delay of packets

# Chapter 4 - Dynamic Routing Protocols

- Minimum configuration and set-up required
- Routes are automatically discovered and maintained by routers through exchange of information
- Routing decisions made based on dynamically learned routes

## Protocols

- Distance Vector
  - Routing Information Protocol (RIP)
- Link State
  - Open Shortest Path First (OSPF)

## Distance Vector Protocol

- Each router informs its neighbours of its entire routing table periodically
- Routing information sent consists of destinations, costs, and next hop to get there
- Will select neighbour advertising lowest cost / lowest hops
- E.g. Router A learns that router B can get to D in 2 hops, A can assume that path from A to D is 3 hops
- When all routers have full view of network, the network is said to have "converged"

### Advantage

- Consumes little memory and CPU

### Disadvantage

- Reacts slowly to any topology changes

### Routing Information Protocol (RIP)

- Uses hop count as routing metric to determine shortest route to destination
- Does not take *speed, delay and reliability* into consideration
- Max no of hops is 15
  - Route with hop count of 16 is considered unreachable
- Updates routing table to neighbours every 30s. **A lot** of overhead traffic

### RIP commands

- `show ip protocols`
  - shows information about routing protocols and networks it is being used for
- `router rip` 
  - goes to RIP config mode and sets RIP as routing protocol
- `network <network-address>`
  - enables RIP for the given network

## Link State Protocol

- First discover who neighbouring routers are and will exchange packets called Link State Packets (LSP)
- LSP contains info about networks the router is directly connected to
- Require routers to only send updates to other routers when there are changes

### Advantage

- Easier to debug and less bandwith-intensive than distance-vectors
- Faster convergence time (react quickly to topology changes

### Disadvantage

- more CPU and memory resources required

### Open Shortest Path First (OSPF)

- uses cost to calculate optimal route
  - cost is dependent on speed, reliability, delay
    - Speed - speed of each link
    - Delay - Time required to move packet from source to destination
    - Reliability - Dependability of each network link
