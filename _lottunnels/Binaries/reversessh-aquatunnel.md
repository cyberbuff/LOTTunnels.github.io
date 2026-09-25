---
Name: ReverseSSH (AquaTunnel)
Description: ReverseSSH (AquaTunnel) is a Go-based backdoor and reverse SSH tunnel that creates an encrypted outbound connection from a compromised host to attacker-controlled infrastructure, enabling remote access through firewalls or NAT. UAT-9686 deployed AquaTunnel, a compiled variant of the open-source ReverseSSH project, after compromising Cisco AsyncOS Secure Email Gateway and Secure Email and Web Manager appliances. It is used for attacker access rather than ordinary interactive SSH forwarding.
Author: cyberbuff
Created: 2026-09-24
Commands:
  - Command: AquaTunnel
    Description: Launches the reported AquaTunnel binary with operator-supplied C2 and SSH reverse-forward configuration; public reporting does not establish exact command-line flags.
    Usecase: Establishes an encrypted reverse SSH channel from the compromised host to attacker-controlled infrastructure.
    Category: Access
    Privileges: User
    OperatingSystem: Windows
Custom_Domain_Supported: True
Detection:
  - Command: Execution of the reported ReverseSSH or AquaTunnel binary with SSH reverse-forward or C2 configuration arguments.
  - Command: Unexpected outbound encrypted SSH connections from a compromised endpoint that do not match approved administrative activity.
Resources:
  - Link: https://www.rescana.com/post/critical-cve-2024-20353-zero-day-exploited-by-china-linked-apt-hits-cisco-secure-email-gateway-and-s
  - Link: https://thehackernews.com/2026/01/cisco-patches-zero-day-rce-exploited-by.html
  - Link: https://www.darkreading.com/endpoint-security/cisco-vpns-email-services-threat-campaigns
---
