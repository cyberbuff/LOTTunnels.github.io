---
Name: IOX
Description: IOX is a self-hosted Go intranet proxy and port-forwarding utility supporting TCP/UDP forwarding, SOCKS5 and reverse SOCKS5, chained relays, and optional encryption. Its endpoints are operator-run, so there is no vendor domain to block.
Author: cyberbuff
Created: 2026-09-24
Commands:
  - Command: "./iox fwd -l 8888 -l 9999"
    Description: Listens on local ports 8888 and 9999 and forwards traffic between the two connections.
    Usecase: Bridging two local listeners through an IOX forwarder.
    Category: Access
    Privileges: User
    OperatingSystem: Windows, Linux, MacOS

  - Command: "./iox proxy -l 1080"
    Description: Starts a SOCKS5 server on local port 1080.
    Usecase: Providing a local SOCKS5 proxy endpoint.
    Category: Access
    Privileges: User
    OperatingSystem: Windows, Linux, MacOS

  - Command: "./iox proxy -r <REMOTE>:9999"
    Description: Connects to a reverse SOCKS5 IOX endpoint on <REMOTE>:9999; use with the paired local command.
    Usecase: Establishing the reverse-proxy leg of a paired SOCKS5 tunnel.
    Category: Access
    Privileges: User
    OperatingSystem: Windows, Linux, MacOS

  - Command: "./iox proxy -l 9999 -l 1080"
    Description: Listens on local ports 9999 and 1080, in that order, and forwards the reverse SOCKS5 connection to the SOCKS5 listener.
    Usecase: Operating the local leg of a reverse SOCKS5 proxy.
    Category: Access
    Privileges: User
    OperatingSystem: Windows, Linux, MacOS

  - Command: "./iox fwd -l *8888 -l 33890 -k <KEY>"
    Description: Listens on encrypted local port 8888 and forwards traffic to local port 33890 using the supplied pre-shared key.
    Usecase: Creating an encrypted relay leg to an internal service such as RDP.
    Category: Access
    Privileges: User
    OperatingSystem: Windows, Linux, MacOS

  - Command: "./iox fwd -l 1000 -r *127.0.0.1:1001 -k <KEY>"
    Description: Forwards a local listener to an encrypted remote IOX endpoint as one stage of a chained relay.
    Usecase: Building a multihop encrypted relay through an intermediate host.
    Category: Access
    Privileges: User
    OperatingSystem: Windows, Linux, MacOS

  - Command: "./iox fwd -l *8888 -l *9999 -k <KEY> -u"
    Description: Enables UDP forwarding between encrypted local ports 8888 and 9999 using the supplied pre-shared key.
    Usecase: Relaying UDP traffic through an encrypted IOX tunnel.
    Category: Access
    Privileges: User
    OperatingSystem: Windows, Linux, MacOS
Custom_Domain_Supported: True
Full_Path:
  - Path: Downloaded/Installed iox binary, executed anywhere on the system.
Detection:
  - Command: "Execution of the iox binary, especially the fwd and proxy subcommands with repeated -l/-r endpoints, -k encryption keys, or -u UDP forwarding."
Resources:
  - Link: https://github.com/EddieIvan01/iox
  - Link: https://www.welivesecurity.com/en/eset-research/webworm-new-burrowing-techniques
---
