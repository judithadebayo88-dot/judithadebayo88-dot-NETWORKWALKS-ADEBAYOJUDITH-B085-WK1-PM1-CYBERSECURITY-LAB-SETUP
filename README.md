## *Cybersecurity Lab Environment Setup*
## Project Overview
This report documents the design, planning, and execution of Task WK1-PM1 from the Network Walks Cybersecurity course: the setup of a personal, isolated cybersecurity testing lab using VirtualBox as the virtualization platform and Kali Linux as the primary attacking/testing machine.
A cybersecurity testing lab is a foundational requirement for anyone learning offensive security, penetration testing, or ethical hacking. 
The lab built in this task uses a custom NATNetwork inside VirtualBox to create an internal subnet (10.0.0.0/24) that is isolated from the host's physical network, while still allowing internet access for tool updates. This mirrors real-world lab environments used by security professionals and forms the base on which future target machines (Windows, Linux servers, Android) will be added for exploitation practice.

 ## Objective 
 Specific objectives defined by Task WK1-PM1 were:
 
•	Install and configure VirtualBox (latest recommended version) as the virtualization base.

•	Deploy Kali Linux as the dedicated attacking/hacker machine within the lab.

•	Create an isolated internal network on subnet 10.0.0.0/24 using a custom NATNetwork.

•	Assign Kali Linux a fixed, predictable IP address of 10.0.0.2/24.

•	Enable clipboard sharing and file drag-and-drop between host and guest for workflow efficiency.

•	Configure a shared folder mapped to the host's /downloads directory.

•	Ensure Kali Linux retains full internet access for package updates and tool installation.

The broader learning objective was to understand how isolated virtual lab networks are architected and secured, a skill directly transferable to professional penetration testing engagements where isolated client-provided environments are the norm.
 
 # Tools & Environment
Hypervisor	                            
Oracle VirtualBox (latest stable release)
 
 Attacking Machine	                     
 Kali Linux (official VirtualBox appliance)
 
 Network Mode	                           
 Custom NATNetwork
 
  Subnet	                                 
  10.0.0.0/24

 Kali Static IP	                         
 10.0.0.2/24

 Utility Software 	                     
 7-Zip (for archive extraction)

 Host Requirements	                     
 8GB+ RAM, 256GB+ SSD, Intel i3/i5 or equivalent

## Network Architecture
The lab follows a hub-and-spoke virtual network design. The host operating system runs VirtualBox as the hypervisor, which manages a single custom NATNetwork shared by all guest virtual machines. This design was chosen deliberately over the two simpler alternatives available in VirtualBox:

•	Bridged Adapter — rejected, as it would expose lab VMs directly to the physical LAN, risking accidental scans or traffic reaching real devices on the network.

• Standard NAT — rejected, as each VM would be isolated even from each other, preventing the attacker machine from reaching future target machines on the same virtual subnet.

•	NATNetwork (chosen) — provides both internet access out and free communication between VMs on the internal 10.0.0.0/24 range, matching how professional isolated test ranges are built.

Within this architecture, Kali Linux was placed at a fixed address (10.0.0.2/24) to keep it predictable as additional target machines (Windows 11/10/7, a Windows Server, and an Android emulator) are added to the same range in later phases of the course.

 ## Methodology / Implementation Steps
  Core Lab Setup

1.	Installed 7-Zip, required to extract the compressed Kali Linux VM appliance archive.

2.	Downloaded and installed the latest recommended version of VirtualBox on the host machine.

3.	Opened VirtualBox's Network Manager and created a new custom NATNetwork, scoped to the 10.0.0.0/24 range, so that all future VMs could share one addressable internal subnet.

4.	Downloaded the official Kali Linux VirtualBox appliance and imported it into VirtualBox.

5.	Edited the Kali VM's network adapter settings to attach it to the newly created NATNetwork, then manually configured its IP address as 10.0.0.2/24 (static, rather than DHCP-assigned) for predictable addressing.

6.	Enabled bidirectional clipboard sharing and drag-and-drop under the VM's General → Advanced settings, and configured a shared folder pointing to the host's /downloads directory for convenient file transfer (wordlists, payloads, notes).

7.	Verified full internet connectivity from within Kali (DNS resolution and external reachability) to confirm apt update and tool downloads would function correctly.

8.	Took a clean snapshot of the Kali VM immediately after setup, establishing a safe rollback point before any

## Key Decisions & Rationale
•	NATNetwork over Bridged/NAT: balances internet access with safe inter-VM communication, without exposing the lab to the physical network.

•	Static IP for Kali: keeps addressing consistent across reboots, which matters once multiple target machines and saved scripts/configs depend on known IPs.

•	Snapshot immediately after setup: testing tools such as Metasploit or manual exploitation techniques can leave a VM in a broken or inconsistent state; a clean snapshot allows a fast reset rather than a full rebuild from scratch.

testing or exploitation work begins.

## Results & Outcome
The lab environment was successfully built and validated against every requirement specified in Task WK1-PM1:

•	VirtualBox installed and configured as the hypervisor base.
•	Kali Linux deployed and reachable at the fixed address 10.0.0.2 on the 10.0.0.0/24 NATNetwork.
•	Clipboard sharing, drag-and-drop, and the /downloads shared folder all functioning between host and guest.
•	Full internet access confirmed from within Kali Linux.
•	A clean baseline snapshot taken, preserving a safe rollback point.

With this foundation in place, the environment is now ready to support hands-on modules such as network scanning, service enumeration, and controlled exploitation exercises against future target VMs added to the same subnet.

## Challenges & Learnings
•	Understanding the practical difference between NAT, Bridged, and NATNetwork modes required deliberate research, since the wrong choice would either break connectivity or create security risk.
•	Configuring a static IP correctly inside Kali (rather than relying on DHCP) reinforced fundamental Linux networking concepts that will be reused throughout the course.
•	Setting up shared folders and drag-and-drop surfaced the importance of installing/checking Guest Additions for smooth host-guest integration.

Overall, this task reinforced that a well-planned lab network is as much a security control as it is a convenience — isolating test activity protects both the host machine and any external network from accidental impact.

## Conclusion
Task WK1-PM1 has been completed successfully, resulting in a fully functional, isolated cybersecurity testing lab built on VirtualBox with Kali Linux as the attacking machine. The lab satisfies every stated requirement — correct network isolation, static addressing, host-guest integration, and internet access and establishes a solid, repeatable foundation for the more advanced offensive security modules that follow in the course.

## Acknowledgment
I would like to express my sincere gratitude to MR WAQAS KARIM CCIE the instructor and mentors at Network Walks for designing a structured, hands-on curriculum that made this lab setup possible. The clear task breakdowns, reference diagrams, and live class walkthroughs provided the foundation needed to complete this task independently and confidently.


# Screenshot
<img width="1162" height="1389" alt="image" src="https://github.com/user-attachments/assets/9ad935ea-d811-41b1-967f-64e126e8282c" />

<img width="1162" height="1407" alt="image" src="https://github.com/user-attachments/assets/502a963d-0a65-43f9-a4ce-99512ce5ac08" />



Author
Judith
