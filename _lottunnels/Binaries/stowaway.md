---
Name: Stowaway
Description: Stowaway is a self-hosted Go multi-hop proxy/RAT for operator-controlled remote access and tunneling. It supports SOCKS5 proxying, local and remote port forwarding, reverse and SSH tunneling, TCP, HTTP, and WebSocket transports, encrypted communication, and remote shell access. Because the admin endpoint is operator-controlled and there is no vendor domain to block, it can be used to build a tunneled pivot through hosts behind NAT or firewalls.
Author: cyberbuff
Created: 2026-09-24
Commands:
    - Command: "./stowaway_admin -l 9999"
      Description: Starts the operator-controlled Stowaway admin node in passive mode, listening for agent connections on port 9999.
      Usecase: Standing up the admin endpoint that Stowaway agents connect back to.
      Category: Access
      Privileges: User
      OperatingSystem: Windows, Linux, MacOS

    - Command: "./stowaway_agent -c <ADMIN_IP>:9999"
      Description: Connects an agent to the operator-controlled admin node at the supplied address, enabling remote control and tunneling through the agent.
      Usecase: Establishing an outbound Stowaway session from a host behind NAT or a firewall.
      Category: Access
      Privileges: User
      OperatingSystem: Windows, Linux, MacOS

    - Command: "./stowaway_agent -c <ADMIN_IP>:9999 -s 123"
      Description: Connects an agent to the admin node with the shared key 123, enabling encrypted Stowaway communication.
      Usecase: Establishing an encrypted session between an agent and the operator-controlled admin node.
      Category: Access
      Privileges: User
      OperatingSystem: Windows, Linux, MacOS

    - Command: "./stowaway_agent -c 127.0.0.1:9999 --reconnect 10"
      Description: Runs an agent with a 10-second reconnect interval so it retries the admin connection after a network interruption.
      Usecase: Maintaining a resilient Stowaway connection through changing network conditions.
      Category: Access
      Privileges: User
      OperatingSystem: Windows, Linux, MacOS

    - Command: "./stowaway_agent -c <ADMIN_IP>:9999 --up ws"
      Description: Uses WebSocket for the agent-to-parent transport, allowing Stowaway traffic to traverse HTTP/WebSocket-aware infrastructure.
      Usecase: Establishing a Stowaway session with a WebSocket upstream transport.
      Category: Access
      Privileges: User
      OperatingSystem: Windows, Linux, MacOS

    - Command: "socks 7777"
      Description: Starts a SOCKS5 service on admin port 7777 through the selected Stowaway node.
      Usecase: Establishing a SOCKS pivot through an agent and its downstream nodes.
      Category: Access
      Privileges: User
      OperatingSystem: Windows, Linux, MacOS

    - Command: "forward 9000 127.0.0.1:22"
      Description: Maps admin-local port 9000 to the selected agent's 127.0.0.1:22 service.
      Usecase: Reaching an internal service such as SSH through the Stowaway network.
      Category: Access
      Privileges: User
      OperatingSystem: Windows, Linux, MacOS

    - Command: "backward 9001 22"
      Description: Maps selected-agent port 9001 to admin-local port 22, exposing a service such as SSH.
      Usecase: Publishing an agent-side service back to the operator's admin host.
      Category: Access
      Privileges: User
      OperatingSystem: Windows, Linux, MacOS

    - Command: "sshtunnel <IP:SSH_PORT> <AGENT_PORT>"
      Description: Connects a new agent through an SSH tunnel to the Stowaway network using the specified SSH endpoint and agent port.
      Usecase: Adding a downstream agent to a multi-hop Stowaway topology through an SSH tunnel.
      Category: Access
      Privileges: User
      OperatingSystem: Windows, Linux, MacOS
Custom_Domain_Supported: True
Full_Path:
    - Path: Downloaded/Installed stowaway_admin and stowaway_agent Go binaries, executed anywhere on the system.
    - Filename: stowaway_admin
    - Filename: stowaway_agent
Detection:
    - Command: Execution of stowaway_admin or stowaway_agent, including SOCKS/forward/reconnect arguments such as socks 7777, forward 9000 127.0.0.1:22, backward 9001 22, sshtunnel <IP:SSH_PORT> <AGENT_PORT>, and --reconnect 10.
Resources:
    - Link: https://github.com/ph4ntonn/Stowaway
    - Link: https://securityonline.info/goserpent-backdoor
---
