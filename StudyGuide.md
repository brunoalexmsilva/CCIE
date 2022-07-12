# Network Infrastructure
## Switched campus
### Switch administration
1. Managing MAC address table
>Adds a static address to the MAC address table.
> 
>**mac address-table static** *mac-addr* **vlan** *vlan-id* **interface** *interface-id*

>Enables unicast MAC address filtering and configure the device to drop a packet with the specified source or destination unicast static address.
>
>**mac address-table static** *mac-addr* **vlan** *vlan-id* **drop** 

>Sets the length of time that a dynamic entry remains in the MAC address table after the entry is used or updated. Default is 300 secs
>
>**mac address-table aging-time** *[0 | 10-1000000] [routed-mac | **vlan** vlan-id]*

>### Troubleshooting Commands
>
>**clear mac address-table ?**
> - Removes MAC address table entries. 
>
>**show mac address-table ?** 
> - Displays MAC address table information.


2. Errdisable recovery
- Reasons for interface err-disable
    - Duplex mismatch
    - Port channel misconfiguration
    - BPDU guard violation
    - UniDirectional Link Detection (UDLD) condition
    - Late-collision detection
    - Link-flap detection
    - Security violation
    - Port Aggregation Protocol (PAgP) flap
    - Layer 2 Tunneling Protocol (L2TP) guard
    - DHCP snooping rate-limit
    - Incorrect GBIC / Small Form-Factor Pluggable (SFP) module or cable
    - Address Resolution Protocol (ARP) inspection
    - Inline power

>**show interface status**
> - Verify interface status for err-disable
>
>**no errdisable detect**
> - Verify if errdisable is enable/disable for each err-disable reason and the mode in which it is enabled
>
>**(config)# no errdisable detect** *cause*
> - Disable error-disable detection. Error-disable detection is enabled for all of these reasons by default.
>
>**show errdisable recovery**
> - Verify if errdisable recovery is enable/disable for each err-disable reason. Err-Disable recovery is disable by default.
>
>**(config)# errdisable recovery cause** *cause*
> - Activate err-disable for a particular reason
>
>**(config)# errdisable recovery interval** *seconds*
> - Configure the recovery interval

Troubleshoot

> **show interfaces status err-disabled** 
>
> - Shows which local ports are involved in the errdisabled state.

3. L2 MTU
>**system mtu jumbo** *size* 
>
> - To increase the ethernet mtu for 1Gbps and 10Gbps interfaces on a Catalyst L3 switch
>
>**system mtu** *size*
> - To increase it for 10 and 100Mbps interfaces use 
>
>**system mtu routing** *size*
> - To increase the IP MTU for routing, sourcing and replying to traffic 
>
>**show system mtu**
> - Verify MTU on a catalyst L3 switch? 


### Layer 2 protocols
1. CDP, LLDP
>**no cdp run**
> - CDP is enabled by default use no to deactive glabally
>
>**no cdp enable**
> - Disable cdp per interface.

Verification Commands
>**show cdp** 
> - It shows if CDP is enabled or not, also the timers, etc.
>
>**show cdp neighbors** 
> - It is used to verify the attached devices. It will give you a nice brief summary view.
>
>**show cdp neighbors detail**
> - It is used to verify the attached devices. It will give more detail, including the IP addresses of the neighbors.
2. UDLD
>**(no) lldp run**
> - LLDP is not enabled by default.
>
>**no lldp transmit** and **no lldp receive**
> - To disable it at the interface level, we do it for both transmit and receive separately. 

Verification Commands
>**show lldp**
> - It will show if LLDP is enabled or not.
>
>**show lldp neighbors**
> - It will show a summary of our neighbors.
>
>**show lldp neighbors detail** 
>- It will show more verbose output, including the IP addresses configured on those devices.


### VLAN technologies
1. Access ports
2. Trunk ports (802.1Q)
3. Native VLAN
4. Manual VLAN pruning
5. VLAN database
6. Normal range and extended range VLANs
7. Voice VLAN
8. VTP
### EtherChannel
1. LACP, static
2. Layer 2, Layer 3
3. Load balancing
4. EtherChannel Misconfiguration Guard
### Spanning Tree Protocol
1. PVST+, Rapid PVST+, MST
2. Switch priority, port priority, path cost, STP timers
3. PortFast, BPDU Guard, BPDU Filter
4. Loop Guard, Root Guard
## Routing Concepts
### Administrative distance
### VRF-lite
### Static routing 
### Policy Based Routing
### VRF-aware routing with any routing protocol
### Route filtering with any routing protocol
### Manual summarization with any routing protocol
### Redistribution between any pair of routing protocols
### Routing protocol authentication
### Bidirectional Forwarding Detection
## EIGRP 
### Adjacencies
### Best path selection
1. RD, FD, FC, successor, feasible successor
2. Classic Metrics and Wide Metrics
### Operations
1. General operations
2. Topology table
3. Packet types
4. Stuck In Active
5. Graceful shutdown
### EIGRP load balancing
1. Equal-cost
2. Unequal-cost
3. Add-path
### EIGRP Named Mode
### Optimization, convergence and scalability
1. Fast convergence requirements
2. Query propagation boundaries
3. IP FRR (single hop)
4. Leak-map with summary routes
5. EIGRP stub with leak map
## OSPF (v2 and v3)
### Adjacencies
### Network types, area types
### Path preference
### Operations
1. General operations
2. Graceful shutdown
3. GTSM (Generic TTL Security Mechanism)
### Optimization, convergence and scalability
1. Metrics
2. LSA throttling, SPF tuning, fast hello
3. LSA propagation control (area types)
4. Stub router
5. Loop-free alternate
6. Prefix suppression
## BGP
### IBGP and EBGP peer relationships
1. Peer-group/update-group, template
2. Active, passive
3. Timers
4. Dynamic neighbors
5. 4-byte AS numbers
6. Private AS
### Path selection
1. Attributes
2. Best path selection algorithm
3. Load balancing
### Routing policies
1. Attribute manipulation
2. Conditional advertisement
3. Outbound Route Filtering
4. Standard and extended communities
5. Multi-homing
### AS path manipulations
1. local-as, allowas-in, remove-private-as
2. Prepend
3. Regexp
### Convergence and scalability
1. Route reflector
2. Aggregation, as-set
### Other BGP features
1. Multipath, add-path
2. Soft reconfiguration, Route Refresh
## Multicast
### Layer 2 multicast
1. IGMPv2, IGMPv3
2. IGMP Snooping, PIM Snooping
3. IGMP Querier
4. IGMP Filter
5. MLD
### Reverse path forwarding check
### PIM
1. Sparse Mode
2. Static RP, BSR, AutoRP
3. Group to RP Mapping
4. Bidirectional PIM
5. Source-Specific Multicast
6. Multicast boundary, RP announcement filter
7. PIMv6 Anycast RP
8. IPv4 Anycast RP using MSDP
9. Multicast multipath
# Software Defined Infrastructure (25%)
## Cisco SD Access
### Design a Cisco SD Access solution
1. Underlay network (IS-IS, manual/PnP)
2. Overlay fabric design (LISP, VXLAN, Cisco TrustSec)
3. Fabric domains (single-site and multi-site using SD-WAN transit)
### Cisco SD Access deployment
1. Cisco DNA Center device discovery and device management
2. Add fabric node devices to an existing fabric
3. Host onboarding (wired endpoints only)
4. Fabric border handoff
### Segmentation
1. Macro-level segmentation using VNs
2. Micro-level segmentation using SGTs (using Cisco ISE)
### Assurance
1. Network and client health (360)
2. Monitoring and troubleshooting
## Cisco SD-WAN
### Design a Cisco SD-WAN solution
1. Orchestration plane (vBond, NAT)
2. Management plane (vManage)
3. Control plane (vSmart, OMP)
4. Data plane (vEdge/cEdge)
### WAN edge deployment
1. Onboarding new edge routers
2. Orchestration with zero-touch provisioning/Plug-And-Play
3. OMP
4. TLOC
### Configuration templates
### Localized policies (only QoS)
### Centralized policies
1. Application Aware Routing
2. Topologies
# Transport Technologies and Solutions
## MPLS
### Operations
1. Label stack, LSR, LSP
2. LDP
3. MPLS ping, MPLS traceroute
### L3VPN
1. PE-CE routing
2. MP-BGP VPNv4/VPNv6
3. Extranet (route leaking)
## DMVPN
### Troubleshoot DMVPN Phase 3 with dual-hub
1. NHRP
2. IPsec/IKEv2 using pre-shared key
3. Per-Tunnel QoS
### Identify use-cases for FlexVPN
1. Site-to-Site, Server, Client, Spoke-to-Spoke
2. IPsec/IKEv2 using pre-shared key
3. MPLS over FlexVPN
# Infrastructure Security and Services
## Device Security on Cisco IOS XE
### Control plane policing and protection
### AAA
## Network Security
### Switch security features
1. VACL, PACL
2. Storm control
3. DHCP Snooping, DHCP option 82
4. IP Source Guard
5. Dynamic ARP Inspection
6. Port Security
7. Private VLAN
### Router security features
1. IPv6 Traffic Filters
2. IPv4 Access Control Lists
3. Unicast Reverse Path Forwarding
### IPv6 infrastructure security features
1. RA Guard
2. DHCP Guard
3. Binding table
4. Device tracking
5. ND Inspection/Snooping
6. Source Guard
### IEEE 802.1X Port-Based Authentication
1. Device roles, port states
2. Authentication process
3. Host modes
## System Management
### Device management
1. Console and VTY
2. SSH, SCP
3. RESTCONF, NETCONF
### SNMP
1. v2c
2. v3
### Logging
1. Local logging, syslog, debugs, conditional debugs
2. Timestamps
## Quality of Service
### End to end L3 QoS using MQC
1. DiffServ
2. CoS and DSCP Mapping
3. Classification
4. Network Based Application Recognition (NBAR)
5. Marking using IP Precedence, DSCP, CoS
6. Policing, shaping
7. Congestion management and avoidance
8. HQoS, Sub-rate Ethernet Link
## Network Services
### First Hop Redundancy Protocols
1. HSRP, GLBP, VRRP
2. Redundancy using IPv6 RS/RA
### Network Time Protocol
1. Master, client
2. Authentication
### DHCP on Cisco IOS
1. Client, server, relay
2. Options
3. SLAAC/DHCPv6 interaction
4. Stateful, stateless DHCPv6
5. DHCPv6 Prefix Delegation
### IPv4 Network Address Translation
1. Static NAT, PAT 
2. Dynamic NAT, PAT
3. Policy-based NAT, PAT
4. VRF-aware NAT, PAT
5. IOS-XE VRF-Aware Software Infrastructure (VASI) NAT
## Network optimization
### IP SLA
1. ICMP probes
2. UDP probes
3. TCP probes
### Tracking object
### Flexible NetFlow
## Network operations
### Traffic capture
1. SPAN
2. RSPAN
3. ERSPAN
4. Embedded Packet Capture
### Cisco IOS-XE troubleshooting tools 
1. Packet Trace
2. Conditional debugger (debug platform condition)
# Infrastructure Automation and Programmability
## Data encoding formats
### JSON
### XML
## Automation and scripting
### EEM applets
### Guest shell
1. Linux environment
2. CLI Python module
3. EEM Python module
## Programmability
### Interaction with vManage API
1. Python requests library and Postman
2. Monitoring endpoints
3. Configuration endpoints
### Interaction with Cisco DNA Center API
1. HTTP request (GET, PUT, POST) via Python requests library and Postman
### Interaction with Cisco IOS XE API
1. Via NETCONF/YANG using Python ncclient library
2. Via RESTCONF/YANG using Python requests library and Postman
### Deploy and verify model-driven telemetry
1. Configure on-change subscription using gRPC
