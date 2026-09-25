---
Name: Go2Tunnel
Description: >-
  Go2Tunnel is a Go-based Windows utility observed in Armored Likho (also known as
  Eagle Werewolf) campaigns for creating reverse SSH tunnels. Reporting describes
  it reading a local ssh_tunnel_config and launching an SSH remote forward; the
  same capability was later integrated into BusySnake Stealer.
Author: cyberbuff
Created: 2026-09-24
Commands:
  - Command: go2tunnel
    Description: >-
      Conservative invocation for the reported executable. The Windows sample
      reads local tunnel configuration and launches an SSH remote forward.
    Usecase: >-
      Maintaining remote access through a reverse SSH tunnel to a Windows host
      behind NAT or a firewall.
    Category: Access
    Privileges: User
    OperatingSystem: Windows
Custom_Domain_Supported: True
Full_Path:
  - Path: >-
      Windows executable executed from an attacker-controlled installation
      directory; reporting identifies a local ssh_tunnel_config and a nearby
      ssh.exe used for the forward.
Detection:
  - Command: >-
      Execution of the go2tunnel binary or its reported sample filename, with a
      local ssh_tunnel_config and an ssh.exe SSH remote forward (-R).
Resources:
  - Link: https://www.securityweek.com/armored-likho-apt-targeting-government-electric-power-entities
  - Link: https://bi.zone/expertise/blog/triedinoe-zlo-oborotni-atakuyut-sotrudnikov-silovykh-struktur
  - Link: https://securelist.com/armored-likho-apt-with-busysnake-stealer/120292/
---
