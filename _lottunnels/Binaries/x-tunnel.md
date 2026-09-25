---
Name: X-Tunnel
Description: X-Tunnel is a custom encrypted Windows proxy and pivot utility associated with APT28, also reported as Trojan.Shunnael and XAPS. It relays traffic between a C2 server and a victim and can support multiple tunnels for access to internal networks.
Author: cyberbuff
Created: 2026-09-24
Commands:
  - Command: xtunnel
    Description: Launches the X-Tunnel binary using an operator-supplied C2 or proxy configuration; public reporting does not establish a stable command-line flag syntax.
    Usecase: Establishes an encrypted relay or pivot between a C2 server and a Windows victim or internal network.
    Category: Access
    Privileges: User
    OperatingSystem: Windows
Custom_Domain_Supported: True
Full_Path:
  - Path: X-Tunnel/xtunnel Windows binary executed anywhere on the system.
  - Filename: VmUpgradeHelper.exe
Detection:
  - Command: Execution of an X-Tunnel/xtunnel binary with C2 or proxy arguments, including observed implant names such as VmUpgradeHelper.exe, followed by outbound encrypted relay behavior.
Resources:
  - Link: https://attack.mitre.org/software/S0117/
  - Link: https://www.welivesecurity.com/wp-content/uploads/2016/10/eset-sednit-part-2.pdf
  - Link: https://www.crowdstrike.com/en-us/blog/bears-midst-intrusion-democratic-national-committee/
---
