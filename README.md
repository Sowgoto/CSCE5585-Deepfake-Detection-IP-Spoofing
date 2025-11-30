# Deepfake Detection in Cybersecurity & IP Spoofing Prevention (CSCE 5585)

This repository contains the source material for **Group 4**’s course project in  
**CSCE 5585 – Security of Emerging Computing and Networking Technologies** at the University of North Texas.

The project has **two main parts**:

- **Part A – Deepfake Detection in Cybersecurity**  
  Conceptual study of how AI-generated media (deepfakes) are used in phishing and Business Email Compromise (BEC) attacks, and an overview of current detection and mitigation approaches.

- **Part B – Network Simulation: IP Spoofing & Prevention in GNS3**  
  A lab-style demonstration of IP spoofing using `iptables` and prevention using ACLs and a FortiGate firewall in a simulated network topology.

  ### Topology

- Two Alpine Linux hosts (AlpineLinux-1 and AlpineLinux-2)  
- Two switches (Switch1 and Switch2)  
- One router (R1)  
- One FortiGate firewall (FortiGate-1) placed inline between the internal LAN and router

Internal network: `192.168.2.0/24`  
External network: `200.41.3.0/24`

### Key Lab Steps

1. **Baseline connectivity**  
   - Configure IP addresses and default gateways.  
   - Verify pings between hosts before spoofing.

2. **IP spoofing with `iptables`**  
   - Apply a POSTROUTING SNAT rule to rewrite the source IP of ICMP (ping) traffic, for example:  
     ```bash
     iptables -t nat -A POSTROUTING -p icmp -j SNAT --to-source 246.79.20
     ```
   - Observe that the victim sees packets as if they came from the spoofed IP.

3. **Inspection of packet flow**  
   - Use tools like `tcpdump` or Wireshark to compare packets **before** and **after** spoofing.  
   - Note how the kernel updates checksums and how the router sees only the fake source IP.

4. **Prevention using ACLs / firewall policies**  
   - Configure ACLs or FortiGate policies that block traffic with **invalid source addresses**.  
   - Re-test pings and show that spoofed packets are no longer forwarded.

## How to Reuse This Project

This project is intended for **educational and lab use only**.  
If you want to reproduce the lab:

1. Install **GNS3** and import the required appliance images (router, FortiGate, Alpine Linux).  
2. Recreate or open the provided topology from the `gns3_project/` folder (if shared).  
3. Apply the IP addressing and `iptables`/ACL rules shown in the slides and notes.  
4. Use ping and packet captures to observe spoofing and its prevention.


## Academic Use & Citation

If you reference this work in an academic context, you may cite it informally as:

> Group 4 – Vibhav Raju, Vijay Sankar Bheemana, & Sowgoto Raha Sunny.  
> *Deepfake Detection in Cybersecurity and IP Spoofing Prevention Lab*, CSCE 5585, University of North Texas, 2025.


  ## Disclaimer

All experiments were performed in an **isolated lab environment**.  
Do **not** use IP spoofing, deepfake tools, or similar techniques on real networks or systems without **explicit authorization**. This repository is for learning and demonstration purposes only.
