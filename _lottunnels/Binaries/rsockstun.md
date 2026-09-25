---
Name: Rsockstun
Description: Rsockstun is a self-hosted, Go-based reverse SOCKS5 tunneler with SSL and upstream proxy support. It is distinct from the similarly named resocks and revsocks tools. A modified variant was observed as rr.exe in BadPilot activity.
Author: cyberbuff
Created: 2026-09-24
Commands:
  - Command: "rsockstun -listen :8443 -socks 127.0.0.1:1080 -cert $CERT"
    Description: "Starts the self-hosted rsockstun server on port 8443, with a SOCKS listener on 127.0.0.1:1080 and the supplied certificate."
    Usecase: Standing up the operator-controlled tunnel endpoint and its reverse SOCKS listener.
    Category: Access
    Privileges: User
    OperatingSystem: Windows, Linux

  - Command: "rsockstun -connect $SERVER_IP:8443"
    Description: "Connects to the rsockstun server and establishes the reverse SOCKS tunnel. Optional flags include -proxy, -proxyauth, -pass, -recn, -rect, and -agentpassword for upstream proxying, authentication, and reconnection."
    Usecase: Maintaining a reverse SOCKS connection from a host to an operator-controlled server.
    Category: Access
    Privileges: User
    OperatingSystem: Windows, Linux
Custom_Domain_Supported: True
Full_Path:
  - Path: Downloaded/Installed rsockstun binary, executed anywhere on the system.
  - Filename: rsockstun
  - Filename: rsockstun.exe
  - Filename: rr.exe
Detection:
  - Command: "Execution of rsockstun or the modified rr.exe variant with -listen/-connect, -socks, -cert, or -recn/-rect arguments; -proxy, -proxyauth, -pass, and -agentpassword may also appear."
Resources:
  - Link: https://github.com/llkat/rsockstun
  - Link: https://www.microsoft.com/en-us/security/blog/2025/02/12/the-badpilot-campaign-seashell-blizzard-subgroup-conducts-multiyear-global-access-operation
  - Link: https://www.cisa.gov/news-events/cybersecurity-advisories/aa23-347a
---
