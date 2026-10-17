# Netcore Systems Ltd. Network Configuration and Access Control

A professional network configuration project for Netcore Systems Ltd. using Cisco Packet Tracer. The project demonstrates departmental network segmentation, DHCP configuration, routing, internal web services, and ACL-based access control.

## Table of Contents
- Project Overview
- Network Topology
- Tools and Technologies
- Configuration Steps
- Challenges and Solutions
- Results and Findings
- Author

## Project Overview

The purpose of this project was to design and configure a departmental network for **Netcore Systems Ltd.** using Cisco Packet Tracer. The network consists of three departmental LANs—**IT, Sales, and HR**—connected through a Cisco 2911 router.

The project focused on:

- Creating separate networks for **IT, Sales, and HR**
- Configuring routing between departmental networks
- Assigning IP addresses through **DHCP**
- Providing DNS/web-server services from the IT department
- Implementing an **extended ACL** to restrict Sales department access to the IT network
- Verifying network connectivity and access to the internal web server

## Network Topology

The network uses a **Cisco 2911 router** as the central Layer 3 device. Three Cisco 2960-24TT switches provide connectivity for the individual departments.

### Network Structure

- **IT Department**
  - Network: `192.168.10.0/24`
  - Default Gateway: `192.168.10.1`
  - Server: `192.168.10.2`
  - Switch: Cisco 2960-24TT
  - End devices: PC0 and PC1

- **Sales Department**
  - Network: `192.168.20.0/24`
  - Default Gateway: `192.168.20.1`
  - Switch: Cisco 2960-24TT
  - End devices: PC2 and PC3

- **HR Department**
  - Network: `192.168.30.0/24`
  - Default Gateway: `192.168.30.1`
  - Switch: Cisco 2960-24TT
  - End devices: PC4 and PC5

### Router Interfaces

- `GigabitEthernet0/0` — IT Department
- `GigabitEthernet0/1` — Sales Department
- `GigabitEthernet0/2` — HR Department

### Example DHCP Assignments

- PC0: `192.168.10.5`
- PC2: `192.168.20.5`
- PC4: `192.168.30.5`
- Subnet mask: `255.255.255.0`
- DNS Server: `192.168.10.2`

## Tools and Technologies

- **Cisco Packet Tracer 9.0**
- **Cisco 2911 Router**
- **Cisco 2960-24TT Switches**
- **IPv4 addressing**
- **DHCP**
- **DNS**
- **HTTP/Web Server**
- **Extended IP Access Control Lists (ACLs)**
- **Cisco IOS CLI**
- **FastEthernet**
- **GigabitEthernet**

## Configuration Steps

1. **Created the network topology** in Cisco Packet Tracer using one Cisco 2911 router, three Cisco 2960-24TT switches, six PCs, and one server.

2. **Created separate departmental networks** using:
   - IT: `192.168.10.0/24`
   - Sales: `192.168.20.0/24`
   - HR: `192.168.30.0/24`

3. **Connected the router to each departmental switch** using:
   - `GigabitEthernet0/0` for IT
   - `GigabitEthernet0/1` for Sales
   - `GigabitEthernet0/2` for HR

4. **Configured DHCP addressing** so client devices could automatically obtain their IPv4 configuration.

5. **Configured the IT server** with the address `192.168.10.2`.

6. **Configured client devices for DHCP** and verified that they received addresses from their respective departmental networks.

7. **Configured an extended ACL** named `Sales-ACL` to deny ICMP traffic originating from the Sales network and destined for the IT network.

8. The ACL configuration included:

   `enable`

   `configure terminal`

   `ip access-list extended Sales-ACL`

   `deny icmp 192.168.20.0 0.0.0.255 192.168.10.0 0.0.0.255`

   `permit ip any any`

   `interface GigabitEthernet0/1`

   `ip access-group Sales-ACL in`

   `exit`

   `end`

9. **Verified the ACL configuration** using:

   `show access-lists`

10. **Tested access to the internal web server** using the Packet Tracer web browser and the server address `192.168.10.2`.

## Challenges and Solutions

The supplied project documentation does not explicitly provide a separate list of problems encountered. However, the configuration and verification steps indicate several key configuration challenges that had to be addressed during the project.

- **Challenge: Managing multiple departmental networks**
  - **Solution:** Each department was assigned a separate `/24` subnet with its own default gateway. This provided clear network segmentation between IT, Sales, and HR.

- **Challenge: Ensuring clients received the correct network configuration**
  - **Solution:** **DHCP** was configured so client devices could automatically receive IP addresses and network configuration appropriate for their respective departments.

- **Challenge: Restricting Sales access to the IT network**
  - **Solution:** An **extended ACL** named `Sales-ACL` was created. The ACL specifically denied ICMP traffic from `192.168.20.0/24` to `192.168.10.0/24` while allowing other IP traffic through the `permit ip any any` statement.

- **Challenge: Applying the ACL to the correct traffic**
  - **Solution:** The ACL was applied **inbound** to `GigabitEthernet0/1`, which connects the router to the Sales network. This allows traffic originating from Sales to be evaluated before being routed to other networks.

- **Challenge: Verifying that the ACL was configured correctly**
  - **Solution:** The `show access-lists` command was used to inspect the configured ACL and confirm that the intended deny and permit statements were present.

- **Challenge: Verifying internal web-server access**
  - **Solution:** The IT server was configured at `192.168.10.2`, and connectivity was tested through the Packet Tracer web browser to confirm that the internal web service could be reached.

## Results and Findings

- The network was successfully divided into **three departmental IPv4 subnets**.
- DHCP was configured to provide network addressing to client devices.
- The IT server was configured with the address `192.168.10.2`.
- Clients received the expected network configuration for their respective departments.
- The router successfully displayed the configured **Sales-ACL** using `show access-lists`.
- The ACL was applied **inbound on `GigabitEthernet0/1`**, the interface connected to the Sales department.
- The ACL specifically denies **ICMP traffic from the Sales subnet (`192.168.20.0/24`) to the IT subnet (`192.168.10.0/24`)** while permitting other IP traffic.
- The internal web server at `192.168.10.2` was successfully accessed through the Packet Tracer web browser during testing.

## Author

**Opeyemi A. Ojelabi**

- IT / Cybersecurity
- Network Administration & Security
- Cisco Packet Tracer
- Goal: **Governance, Risk & Compliance (GRC) Analyst**
