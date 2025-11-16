# Inter-VLAN Routing — Pure Legacy Method (Separate Router Interfaces)

This lab demonstrates the original, pure legacy method of inter-VLAN routing, where each VLAN connects to a dedicated physical router interface. No trunking, no subinterfaces, no dot1q encapsulation, no Router-on-a-Stick. This method works for small networks but does not scale because it requires one physical router interface per VLAN.

---

## 🎯 Purpose

This lab demonstrates:

- How VLANs were routed before trunking and Router-on-a-Stick existed  
- How a switch segments broadcast domains  
- How a router routes between VLANs using **separate physical interfaces**  
- How to verify VLAN membership and switchport status  
- How to test inter-VLAN connectivity  

You will configure:

- VLAN creation  
- Assigning switchports to VLANs  
- Router interface IP addressing  
- Switchport verification  
- Inter-VLAN ping tests  

---

## 🗂 Topology

- VLAN 10 (Development) → connected to Router G0/0  
- VLAN 20 (Marketing) → connected to Router G0/1  
- 1 Layer 2 Switch  
- No trunk links  
- No subinterfaces  
- No dot1q  

![Topology](Screenshots/InterVLAN_Legacy_Topology.png)

---

# ⚙️ Configuration Steps

## 1️⃣ Create VLANs

```bash
Switch(config)# vlan 10
Switch(config-vlan)# name DEVELOPMENT
Switch(config-vlan)# exit

Switch(config)# vlan 20
Switch(config-vlan)# name MARKETING
Switch(config-vlan)# exit
```

---

## 2️⃣ Assign Access Ports to VLANs

### VLAN 10 Ports  
```bash
Switch(config)# interface fa0/2
Switch(config-if)# switchport mode access
Switch(config-if)# switchport access vlan 10

Switch(config)# interface fa0/3
Switch(config-if)# switchport mode access
Switch(config-if)# switchport access vlan 10
```

### VLAN 20 Ports  
```bash
Switch(config)# interface fa0/13
Switch(config-if)# switchport mode access
Switch(config-if)# switchport access vlan 20

Switch(config)# interface fa0/14
Switch(config-if)# switchport mode access
Switch(config-if)# switchport access vlan 20
```

---

## 3️⃣ Configure Router Interfaces (Pure Legacy — One Interface per VLAN)

### Router Interface for VLAN 10  
```bash
Router(config)# interface g0/0
Router(config-if)# ip address 10.1.1.1 255.255.255.0
Router(config-if)# no shutdown
```

### Router Interface for VLAN 20  
```bash
Router(config)# interface g0/1
Router(config-if)# ip address 10.1.2.1 255.255.255.0
Router(config-if)# no shutdown
```

---

# 🔍 Verification

## Verify VLANs  
```bash
Switch# show vlan brief
```

## Verify Access Ports  
```bash
Switch# show interfaces switchport
```

## Verify Router Interfaces  
```bash
Router# show ip interface brief
```

---

# 📡 Inter-VLAN Connectivity Test

### From a VLAN 10 PC:  
```bash
ping 10.1.2.100
```

### From a VLAN 20 PC:  
```bash
ping 10.1.1.100
```

Successful replies confirm that routing between VLANs is functioning through **separate router physical interfaces**.

---

## ✔ Lab Complete

You now have a fully working **Pure Legacy Inter-VLAN Routing** configuration using:
- 2 VLANs  
- Separate router interfaces  
- No trunking  
- No subinterfaces  
- Basic segmentation and routing principles  
