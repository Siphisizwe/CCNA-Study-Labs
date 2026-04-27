 Lab 17 – VLANs Part 2: Router on a Stick (ROAS)

Source: Jeremy's IT Lab – Day 17  
Tool: Cisco Packet Tracer  

---

 Topology
- 1 Router (R1) connected to 1 Switch (SW1) via a single trunk link
- VLANs: VLAN 10, VLAN 20, VLAN 30
- Subinterfaces on R1 handle inter-VLAN routing

---

 Key Concepts
- ROAS uses subinterfaces on a router to route between VLANs over one physical link
- Each subinterface maps to one VLAN using 802.1Q encapsulation
- The switchport connected to the router must be a trunk port
- ROAS is suitable for small networks; Layer 3 switches are preferred for larger ones
- Native VLAN must match on both ends of a trunk to avoid mismatches

---
Commands Used
 Router – Subinterface Configuration
 interface g0/0.10
encapsulation dot1Q 10
ip address 192.168.1.1 255.255.255.0
interface g0/0.20
encapsulation dot1Q 20
ip address 192.168.2.1 255.255.255.0
interface g0/0.30
encapsulation dot1Q 30
ip address 192.168.3.1 255.255.255.0

 Switch – Trunk Port to Router
 interface g0/1
switchport mode trunk

 Switch – Access Ports
 interface g0/2
switchport mode access
switchport access vlan 10
interface g0/3
switchport mode access
switchport access vlan 20
interface g0/4
switchport mode access
switchport access vlan 30

---

 Outcome
- Devices in different VLANs can communicate through R1
- Verified with ping between hosts in VLAN 10, 20, and 30

---

 Lessons Learned
- Always bring up the physical interface first (`no shutdown` on g0/0)
- Subinterface numbers don't have to match VLAN IDs but it's best practice
- ROAS creates a single point of failure — one link handles all VLAN traffic
 

## Commands Used

### Router – Subinterface Configuration
