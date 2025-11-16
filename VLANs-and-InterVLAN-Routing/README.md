## Lab: VLANs & Inter-VLAN Routing

### Purpose
This lab demonstrates how VLANs segment broadcast domains and how inter-VLAN routing enables communication between them using router-on-a-stick.

### Topology
- 1 Router  
- 1 Switch  
- Multiple PCs  
- VLAN 10  
- VLAN 20  

*(Screenshot of topology goes here once uploaded)*

### Key Tasks Completed
1. Created VLANs on the switch  
2. Assigned switchports to VLANs  
3. Configured trunking between the switch and router  
4. Set up router subinterfaces for each VLAN  
5. Assigned default gateway IPs for each VLAN  
6. Verified connectivity between VLANs using ping  

### Important Commands (Examples)
```bash
show vlan brief
show ip interface brief

interface g0/0.10
 encapsulation dot1Q 10
 ip address 192.168.10.1 255.255.255.0

interface g0/0.20
 encapsulation dot1Q 20
 ip address 192.168.20.1 255.255.255.0
```

### Issues Troubleshooted
- Ports assigned to the wrong VLAN  
- Missing or incorrect trunk configuration  
- Wrong encapsulation VLAN ID on router subinterfaces  

### What I Learned
- How VLANs isolate traffic into separate broadcast domains  
- How trunk links carry multiple VLANs between devices  
- How router-on-a-stick enables routing between VLANs  
- The importance of verifying VLAN membership and trunk status when troubleshooting
