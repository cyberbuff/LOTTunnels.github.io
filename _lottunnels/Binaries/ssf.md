---
Name: SSF
Description: Secure Socket Funneling (SSF) is a self-hosted, cross-platform TLS tunneling toolkit that forwards TCP and UDP connections, provides local or remote SOCKS proxies, supports remote shells and file transfer, and can chain multiple relay servers. It has been observed in MuddyWater and Blue Mockingbird intrusions for pivoting and proxying. Because the SSF client and server are operator-run, there is no vendor domain to block.
Author: cyberbuff
Created: 2026-09-25
Commands:
    - Command: ssfd -p 9000 -l 192.168.0.1
      Description: Starts the operator-controlled SSF server on port 9000 and binds it to the specified address, allowing a remote SSF client to establish the encrypted tunnel.
      Usecase: Establishing the server endpoint for an SSF tunnel.
      Category: Access
      Privileges: User
      OperatingSystem: Windows, Linux, MacOS

    - Command: ssf -D 9000 -c config.json -p 8000 192.168.0.1
      Description: Connects to an SSF server and exposes a SOCKS proxy on local port 9000, forwarding SOCKS requests through the encrypted tunnel to the server network.
      Usecase: Pivoting through a compromised host with a local SOCKS proxy.
      Category: Access
      Privileges: User
      OperatingSystem: Windows, Linux, MacOS

    - Command: ssf -F 9000 -c config.json -p 8000 192.168.0.1
      Description: Runs a SOCKS proxy on the SSF client that is reachable from the server side, allowing the operator to route traffic through the client into its local network.
      Usecase: Pivoting from a server-side operator into a client-side network.
      Category: Access
      Privileges: User
      OperatingSystem: Windows, Linux, MacOS

    - Command: ssf -L 9000:127.0.0.1:22 -c config.json -p 8000 192.168.0.1
      Description: Forwards local TCP port 9000 to a service such as SSH on port 22 through the SSF server, exposing a client-side service to the remote side of the tunnel.
      Usecase: Reaching an internal service through a compromised SSF client.
      Category: Access
      Privileges: User
      OperatingSystem: Windows, Linux, MacOS

    - Command: ssf -R 9000:127.0.0.1:22 -c config.json -p 8000 192.168.0.1
      Description: Forwards a TCP port on the SSF server to a service on the client side, providing remote access to a service behind the client’s network boundary.
      Usecase: Maintaining remote access to an internal host through the tunnel.
      Category: Access
      Privileges: User
      OperatingSystem: Windows, Linux, MacOS

    - Command: ssf -U 5353:127.0.0.1:53 -c config.json -p 8000 192.168.0.1
      Description: Forwards local UDP port 5353 to a service such as DNS on port 53 through the encrypted SSF tunnel.
      Usecase: Relaying UDP traffic to an internal service through a compromised host.
      Category: Access
      Privileges: User
      OperatingSystem: Windows, Linux, MacOS
Custom_Domain_Supported: True
Full_Path:
    - Path: Downloaded SSF binaries named ssf, ssfd, and optionally ssfcp, executed from an arbitrary directory with a config.json file.
Detection:
    - Command: Execution of ssf or ssfd with SOCKS (-D or -F), TCP (-L or -R), UDP (-U or -V), shell (-X or -Y), or circuit configuration arguments; presence of ssf, ssfd, ssfcp, config.json, or SSF certificate files.
Resources:
    - Link: https://github.com/securesocketfunneling/ssf
    - Link: https://securesocketfunneling.github.io/ssf/
    - Link: https://www.sentinelone.com/labs/wading-through-muddy-waters-recent-activity-of-an-iranian-state-sponsored-threat-actor
---
