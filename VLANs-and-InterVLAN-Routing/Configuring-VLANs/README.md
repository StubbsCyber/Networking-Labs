# Lab: Configuring VLANs

This lab demonstrates how to create VLANs, assign switchports to VLANs, and verify VLAN segmentation in a small network using Cisco Packet Tracer.

---

## 🎯 Purpose

Virtual LANs (VLANs) allow a physical switch to be divided into multiple logical networks. VLANs improve:

- **Security** by separating broadcast domains  
- **Broadcast domain reduction**  
- **Network organization** by grouping devices logically  

In this lab, you will practice:

- Creating VLANs  
- Assigning switchports to VLANs  
- Verifying VLAN membership using CLI commands  
- Testing communication within and across VLANs  

---

## 🗺 Topology

The network consists of:

- 1 Layer 2 switch  
- 2 devices in the **Development** VLAN  
- 2 devices in the **Marketing** VLAN  
- No routing between VLANs  
- No trunk links  

![Topology](./Screenshots/Config_Vlan_Topology.png)

---

## 🛠 Configuration Steps

### 1️⃣ Create VLANs

```bash
Switch(config)# vlan 10
Switch(config-vlan)# name DEVELOPMENT
Switch(config-vlan)# exit

Switch(config)# vlan 20
Switch(config-vlan)# name MARKETING
Switch(config-vlan)# exit
```

---

### 2️⃣ Assign Access Ports to VLANs

#### **VLAN 10 (Development)**  
Assign PCs on fa0/2 and fa0/3:

```bash
Switch(config)# interface fa0/2
Switch(config-if)# switchport mode access
Switch(config-if)# switchport access vlan 10
Switch(config-if)# exit

Switch(config)# interface fa0/3
Switch(config-if)# switchport mode access
Switch(config-if)# switchport access vlan 10
Switch(config-if)# exit
```

#### **VLAN 20 (Marketing)**  
Assign PCs on fa0/13 and fa0/14:

```bash
Switch(config)# interface fa0/13
Switch(config-if)# switchport mode access
Switch(config-if)# switchport access vlan 20
Switch(config-if)# exit

Switch(config)# interface fa0/14
Switch(config-if)# switchport mode access
Switch(config-if)# switchport access vlan 20
Switch(config-if)# exit
```

---

### 3️⃣ Verify VLAN Membership

Screenshot:

![VLAN Brief](./Screenshots/Config Vlan VLAN Brief.png)

Command:

```bash
Switch# show vlan brief
```

You should see VLAN 10 and VLAN 20 with correct ports assigned.

---

### 4️⃣ Verify Interfaces & Status

Screenshot:

![Interfaces Switchport](./Screenshots/Config_Vlan_Interfaces_Switchport.png)

Command:

```bash
Switch# show interfaces switchport
```

---

### 5️⃣ Test Connectivity

#### **Within the same VLAN → should succeed**
Screenshot:

![Ping](./Screenshots/Config_Vlan_Ping.png)

Example:
- PC in VLAN 10 ping another PC in VLAN 10  
- PC in VLAN 20 ping another PC in VLAN 20  

#### **Across VLANs → should fail**  
Devices in VLAN 10 cannot ping VLAN 20 (no routing yet).

---

## 📁 Files Included

```
Configuring-VLANs/
│
├── README.md
├── Stubbs-Configuring_VLANs_Fall_25_A.pka
└── Screenshots/
      ├── Config_VLAN_Topology.png
      ├── Config_VLAN_VLAN_Brief.png
      ├── Config_Vlan_Interfaces_Switchport.png
      ├── Config_Vlan_Ping.png
```

---

## ✅ End of Lab

You have successfully:

- Created VLANs  
- Assigned ports to VLANs  
- Verified VLAN membership  
- Tested inter-device connectivity within and across VLANs  

This completes the **Configuring VLANs** lab.
