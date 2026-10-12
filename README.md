# Telnet Lab Using Cisco Packet Tracer

## 1. Introduction
This project demonstrates how to configure and access a Cisco router or switch remotely using the Telnet protocol in Cisco Packet Tracer. It helps students understand remote device management, IP addressing, password configuration, and basic network troubleshooting.

## 2. Objectives
- Understand the Telnet protocol.
- Configure IP addresses on network devices.
- Enable Telnet access on a Cisco router or switch.
- Configure console and virtual terminal (VTY) passwords.
- Establish remote connections from a PC.
- Verify connectivity and troubleshoot errors.

## 3. Requirements
- Cisco Packet Tracer
- 1 Router
- 1 PC
- Copper straight-through cable

## 4. Network Topology

PC → Router

| Device | Interface | IP Address |
|---|---|---|
| PC | FastEthernet0 | 192.168.1.2 |
| Router | GigabitEthernet0/0 | 192.168.1.1 |
| Subnet Mask | — | 255.255.255.0 |

*Note: Interface names may vary depending on the router model.*

## 5. Step-by-Step Configuration

### Step 1: Create the Topology
1. Open Cisco Packet Tracer.
2. Add one router and one PC to the workspace.
3. Connect the PC to the router using a copper straight-through cable.
4. Select the appropriate router interface, such as GigabitEthernet0/0.

### Step 2: Configure the PC
1. Click the PC.
2. Open **Desktop → IP Configuration**.
3. Enter the following details:

- IP Address: `192.168.1.2`
- Subnet Mask: `255.255.255.0`
- Default Gateway: `192.168.1.1`

### Step 3: Configure the Router Interface
Click the router, open the CLI, and enter:

```text
enable
configure terminal
interface gigabitEthernet 0/0
ip address 192.168.1.1 255.255.255.0
no shutdown
exit
```

If your router uses a different interface name, replace `gigabitEthernet 0/0` accordingly.

### Step 4: Configure the Enable Password

```text
enable secret class123
```

This sets the password required to enter privileged EXEC mode.

### Step 5: Configure the VTY Lines for Telnet

```text
line vty 0 4
password telnet123
login
transport input telnet
exit
```

These commands configure the virtual terminal lines to accept Telnet connections and require a password.

### Step 6: Save the Configuration

```text
end
copy running-config startup-config
```

Press Enter to accept the default destination filename if prompted.

### Step 7: Verify the Router Configuration

```text
show ip interface brief
show running-config
```

Confirm that the router interface has the correct IP address and is up.

### Step 8: Test Connectivity
On the PC:
1. Open **Desktop → Command Prompt**.
2. Run:

```text
ping 192.168.1.1
```

Successful replies indicate that IP connectivity is working.

### Step 9: Connect Using Telnet
In the PC command prompt, enter:

```text
telnet 192.168.1.1
```

When prompted, enter the VTY password:

```text
telnet123
```

After successful authentication, enter privileged EXEC mode:

```text
enable
```

Enter the enable secret:

```text
class123
```

You can now execute permitted router commands remotely.

## 6. Verification Commands

```text
show users
show ip interface brief
show running-config
```

These commands help verify active sessions and router configuration.

## 7. Troubleshooting
- **Ping fails:** Check IP addresses, cabling, and interface status.
- **Connection fails:** Verify the router IP and interface configuration.
- **Password rejected:** Check the VTY password and `login` command.
- **Telnet unavailable:** Verify `transport input telnet` and the VTY configuration.
- **Interface down:** Check the interface name and use `no shutdown`.

## 8. Security Note
Telnet sends data without encryption. It is suitable for a controlled educational simulation, but SSH should be used for secure remote administration in real networks.

## 9. Learning Outcomes
After completing this lab, students can configure router interfaces, enable Telnet, establish remote sessions, verify connectivity, and troubleshoot basic networking problems.

## 10. Conclusion
This lab demonstrates remote router management through Telnet in Cisco Packet Tracer and builds practical knowledge of IP addressing, VTY configuration, authentication, and network troubleshooting.
