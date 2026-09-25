---
Name: RevSocks
Description: RevSocks is a self-hosted, single-binary Go reverse SOCKS5 relay used for pivoting and command-and-control (C2). An operator-run listener exposes a local SOCKS5 proxy while a client connects back from a host behind NAT or a firewall. It supports TLS by default, WebSocket transport, and DNS tunneling, so there is no vendor domain to block.
Author: cyberbuff
Created: 2026-09-24
Commands:
    - Command: "revsocks -listen :8443 -socks 127.0.0.1:1080 -pass $PASSWORD"
      Description: Starts the operator-controlled RevSocks listener on port 8443 and exposes a local SOCKS5 proxy on 127.0.0.1:1080 for connections relayed by a client.
      Usecase: Standing up the reverse-SOCKS entry point that a host behind NAT or a firewall connects back to.
      Category: Access
      Privileges: User
      OperatingSystem: Windows, Linux, MacOS

    - Command: "revsocks -connect $SERVER_IP:8443 -pass $PASSWORD"
      Description: Connects the RevSocks client to an operator-controlled listener using the shared password, establishing a reverse SOCKS5 tunnel.
      Usecase: Establishing a SOCKS pivot into an internal network from a compromised or remote host.
      Category: Access
      Privileges: User
      OperatingSystem: Windows, Linux, MacOS

    - Command: "revsocks -listen :8443 -socks 127.0.0.1:1080 -pass $PASSWORD -ws"
      Description: Starts the RevSocks listener with WebSocket transport enabled, allowing clients to connect through a WebSocket-compatible endpoint while exposing the local SOCKS5 proxy.
      Usecase: Standing up a WebSocket-based reverse SOCKS relay to blend tunnel traffic with web traffic.
      Category: Access
      Privileges: User
      OperatingSystem: Windows, Linux, MacOS

    - Command: "revsocks -connect https://$SERVER_IP:8443 -pass $PASSWORD -ws"
      Description: Connects the RevSocks client to an HTTPS WebSocket endpoint using the shared password, establishing the WebSocket-based reverse SOCKS5 tunnel.
      Usecase: Connecting a host behind a restrictive firewall to a WebSocket-based SOCKS pivot.
      Category: Access
      Privileges: User
      OperatingSystem: Windows, Linux, MacOS

    - Command: "revsocks -dns example.com -dnslisten :53 -socks 127.0.0.1:1080 -pass $PASSWORD"
      Description: Runs the RevSocks DNS server for example.com, listening for DNS-tunneled client connections on port 53 and exposing a local SOCKS5 proxy.
      Usecase: Relaying SOCKS traffic over DNS when direct or WebSocket connectivity is unavailable.
      Category: Access
      Privileges: User
      OperatingSystem: Windows, Linux, MacOS
Custom_Domain_Supported: True
Full_Path:
    - Path: Downloaded/Installed revsocks binary (single executable acting as both server and client), executed anywhere on the system.
Detection:
    - Command: "Execution of the revsocks binary with -listen or -connect, SOCKS configuration, -pass, or -ws arguments, indicating a reverse SOCKS5 listener, client connection, password, or WebSocket tunnel."
Resources:
    - Link: https://github.com/kost/revsocks
    - Link: https://www.security.com/threat-intelligence/ransomware-spirals-extortion
---
