LAB 19 - DTP and VTP
Date: 11 May 2026

DTP - Dynamic Trunking Protocol:
A Cisco protocol that automatically tries to form trunk 
links with neighbouring switches by sending DTP frames.
Security risk: attackers can respond to DTP frames and 
form unauthorized trunks gaining access to all VLANs.
This attack is called VLAN hopping.
Fix: disable DTP manually on all ports.
Command: switchport nonegotiate
Verify: show interfaces [int] switchport
Look for: Negotiation of Trunking: Off

DTP Port Modes:
access           - never forms trunk
trunk            - always trunk
dynamic auto     - accepts trunk if other side initiates
dynamic desirable - actively tries to form trunk

VTP - VLAN Trunking Protocol:
Allows VLAN changes to automatically propagate across 
all switches in the same VTP domain.
Create a VLAN on the server and all clients receive it.
Switches must have same domain name to sync.
Higher revision number wins when syncing.

VTP Modes:
Server      - creates/modifies/deletes VLANs
              advertises to all switches in domain
              default mode on Cisco switches

Client      - receives VLANs from server automatically
              cannot create VLANs locally
              error: VTP VLAN configuration not allowed 
              when device is in CLIENT mode

Transparent - does not participate in VTP
              keeps its own local VLAN database
              passes VTP messages through but ignores them
              revision number resets to 0
              use this mode for security in most networks

KEY LESSONS FROM LAB:
- Wrong VTP domain name = no VLAN sync
- SW3 had domain "name" instead of "CCNA" 
  VLANs did not sync until domain was fixed
- SW3 in client mode could not create VLAN50
- VLAN40 created on SW2 transparent did not 
  appear on SW1 or SW3

COMMANDS USED:
vtp mode server
vtp mode client
vtp mode transparent
vtp domain CCNA
show vtp status
show vlan brief
show interfaces [int] switchport
switchport mode trunk
switchport nonegotiate
switchport mode access
switchport access vlan [number]
