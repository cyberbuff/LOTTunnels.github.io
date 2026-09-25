---
Name: ReverseSocks5
Description: ReverseSocks5 is a self-hosted reverse SOCKS5 proxy written in Go, bundled as a single executable that can act as either a server or an agent. The server listens for an agent that connects back from a network behind NAT or a firewall, then exposes a local SOCKS5 proxy through that agent. The connection can use TCP or TLS, and the tool supports pre-shared-key authentication, SOCKS5 username/password authentication, and optional server certificates. It has been observed in CL-STA-1132 activity targeting PAN-OS firewalls and in ESET research on LongNosedGoblin.
Author: cyberbuff
Created: 2026-09-24
Commands:
  - Command: "ReverseSocks5.exe -listen :10443 -socks 127.0.0.1:1080"
    Description: "Starts the operator-controlled server, listening for agents on port 10443 and exposing a local SOCKS5 proxy on 127.0.0.1:1080 once an agent connects. Server options include -psk for shared-key encryption and authentication, -username and -password for SOCKS5 authentication, and -cert and -key for TLS."
    Usecase: Standing up the reverse-SOCKS entry point that compromised hosts connect back to.
    Category: Access
    Privileges: User
    OperatingSystem: Windows, Linux

  - Command: "ReverseSocks5.exe -connect <SERVER>:10443"
    Description: "Connects an agent on a host behind NAT or a firewall to the server, making that host the egress point for the reverse SOCKS5 tunnel. The -psk option sets the pre-shared key used for encryption and authentication."
    Usecase: Establishing a SOCKS pivot into the network reachable from the agent.
    Category: Access
    Privileges: User
    OperatingSystem: Windows, Linux

  - Command: "ReverseSocks5.exe -connect <SERVER>:10443 -tls -k"
    Description: "Connects the agent over TLS and skips server certificate verification with -k. The server can provide its certificate and private key with -cert and -key; the agent can still use -psk for shared-key encryption and authentication."
    Usecase: Establishing a TLS-protected reverse SOCKS5 pivot when certificate verification is not required.
    Category: Access
    Privileges: User
    OperatingSystem: Windows, Linux
Custom_Domain_Supported: True
Full_Path:
  - Path: Downloaded/Installed ReverseSocks5 binary (single executable acting as both server and agent), executed anywhere on the system.
Detection:
  - Command: "Execution of ReverseSocks5.exe or a platform-specific ReverseSocks5 binary with -listen or -connect, SOCKS5 proxy or TLS options (-tls, -k), and credential arguments such as -psk, -username, -password, -cert, or -key."
Resources:
  - Link: https://github.com/Acebond/ReverseSocks5
  - Link: https://www.secpod.com/blog/cl-sta-1132-weaponizes-pan-os-rce-for-silent-root-level-takeovers
  - Link: https://www.welivesecurity.com/en/eset-research/longnosedgoblin-tries-sniff-out-governmental-affairs-southeast-asia-japan
---
