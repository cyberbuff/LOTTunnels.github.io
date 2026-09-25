---
Name: CurlCat
Description: CurlCat is a custom ELF/libcurl companion implant used by Curly COMrades for bidirectional stdin/stdout-to-C2 HTTPS relay and SSH reverse-proxy tunnel management. It is often deployed as /root/updater in a hidden Hyper-V Alpine VM. C2 and relay configuration are operator-supplied, so it has no vendor domain.
Author: cyberbuff
Created: 2026-09-24
Commands:
  - Command: /root/updater
    Description: Launches the CurlCat companion implant with operator-supplied C2 and relay configuration. This is the conservative observed invocation; no public CLI flags are established.
    Usecase: Relay stdin and stdout to C2 over HTTPS and manage an SSH reverse-proxy tunnel from the compromised host.
    Category: Access
    Privileges: User
    OperatingSystem: Linux
Custom_Domain_Supported: True
Full_Path:
  - Path: /root/updater
Detection:
  - Command: Execution of /root/updater, or the reported executable name, as a custom libcurl ELF companion implant.
  - Command: Outbound HTTPS relay traffic and SSH reverse-proxy tunnel activity to operator-supplied C2 and relay endpoints.
Resources:
  - Link: https://aws.amazon.com/blogs/security/amazon-threat-intelligence-identifies-russian-cyber-threat-group-targeting-western-critical-infrastructure
  - Link: https://thehackernews.com/2025/11/hackers-weaponize-windows-hyper-v-to.html
  - Link: https://www.bleepingcomputer.com/news/security/russian-hackers-abuse-hyper-v-to-hide-malware-in-linux-vms
---
