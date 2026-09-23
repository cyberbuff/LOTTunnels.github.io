---
Name: resocks
Description: resocks is a self-hosted reverse SOCKS5 proxy that turns a compromised host into a relay. The operator runs a listener, the compromised host runs the resocks client which connects back over a mutually authenticated TLS 1.3 tunnel (key-derived certificates), and the operator gets a local SOCKS5 proxy into the target network. Because the listener is operator-run, there is no vendor domain to block. It is abused for pivoting, observed with Curly COMrades, MuddyWater and ESET-tracked APT activity, among others.
Author: cyberbuff
Created: 2026-09-22
Commands:
    - Command: resocks listen
      Description: Starts the operator-controlled listener and prints a connection key; it exposes a local SOCKS5 proxy (default 127.0.0.1:1080) once a relay connects back.
      Usecase: Standing up the reverse-SOCKS entry point that compromised hosts connect back to.
      Category: Access
      Privileges: User
      OperatingSystem: Windows, Linux, MacOS

    - Command: resocks <LISTENER> --key <CONNECTION_KEY>
      Description: Runs the resocks client on a compromised host, connecting back to the operator's listener over mTLS to open the reverse SOCKS5 tunnel (the key may also be supplied via RESOCKS_KEY).
      Usecase: Establishing a SOCKS pivot into an internal network from a compromised host.
      Category: Access
      Privileges: User
      OperatingSystem: Windows, Linux, MacOS
Custom_Domain_Supported: True
Full_Path:
    - Path: Downloaded/Installed resocks binary (single executable acting as both listener and relay client), executed anywhere on the system.
Detection:
    - Command: "Execution of the resocks binary with the listen subcommand or with a listener address plus --key/RESOCKS_KEY, and the resulting local SOCKS5 listener (default 127.0.0.1:1080)."
Resources:
    - Link: https://github.com/RedTeamPentesting/resocks
    - Link: https://mallory.ai/malware/019bcc2f-c42f-7769-bfe6-71324d60f7c7
---
