---
Name: RoadK1ll
Description: RoadK1ll is a malicious Node.js WebSocket reverse-tunnel implant that establishes an outbound WebSocket C2 connection to attacker-controlled infrastructure and brokers outbound TCP connections through the compromised host. Its custom channel protocol multiplexes CONNECT, DATA, CLOSE/CLOSED, and ERROR messages so an operator can pivot to internal systems without an inbound listener. The reported incident was observed on Windows, and no public CLI syntax is established.
Author: cyberbuff
Created: 2026-09-24
Commands:
  - Command: node index.js
    Description: Launches the RoadK1ll Node.js implant script with operator-supplied connection configuration; the script establishes the outbound WebSocket C2 tunnel.
    Usecase: Running the implant on a compromised Windows host to provide a reverse-tunnel pivot.
    Category: Access
    Privileges: User
    OperatingSystem: Windows
Custom_Domain_Supported: True
Full_Path:
  - Path: Downloaded RoadK1ll Node.js implant script, executed anywhere on the system.
  - Filename: index.js
  - Filename: node.zip
Detection:
  - Command: "Execution of the Node.js runtime or the RoadK1ll implant script, including reported indicators index.js and node.zip."
  - Command: "Outbound WebSocket C2 to attacker-controlled infrastructure with proxy/pivot behavior, including operator-requested outbound TCP connections to internal targets."
Resources:
  - Link: https://blackpointcyber.com/blog/roadk1ll-a-websocket-based-pivoting-implant
  - Link: https://www.bleepingcomputer.com/news/security/new-roadk1ll-websocket-implant-used-to-pivot-on-breached-networks
---
