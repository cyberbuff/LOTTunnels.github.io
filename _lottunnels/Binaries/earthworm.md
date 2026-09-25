---
Name: EarthWorm
Description: EarthWorm (EW) is a self-hosted SOCKS v5 and TCP port-transfer utility supporting forward, reverse and multi-hop modes. Its endpoints are operator-run, so no vendor relay domain is required. The author retired distribution after documenting abuse, and EarthWorm has been observed in ProxyShell/UNC2980, Volt Typhoon and Earth Estries post-compromise activity.
Author: cyberbuff
Created: 2026-09-24
Commands:
  - Command: ew -s ssocksd -l 1080
    Description: Starts a local SOCKS v5 listener on port 1080 that relays connections through the host running the forward SOCKS mode.
    Usecase: Establishing a SOCKS proxy on a compromised host for lateral access.
    Category: Access
    Privileges: User
    OperatingSystem: Windows, Linux, MacOS, ARM-Linux

  - Command: ew -s rcsocks -l 1080 -e 8888
    Description: Starts the public-endpoint side of a backward SOCKS v5 tunnel, listening for SOCKS traffic on port 1080 and transferring data through port 8888.
    Usecase: Establishing the operator-controlled side of a reverse SOCKS pivot.
    Category: Access
    Privileges: User
    OperatingSystem: Windows, Linux, MacOS, ARM-Linux

  - Command: "ew -s rssocks -d $HOST_A_IP -e 8888"
    Description: Starts a SOCKS v5 server on the internal host and transfers its traffic to port 8888 on the public EarthWorm endpoint, completing the reverse SOCKS path.
    Usecase: Pivoting through a host that cannot accept inbound connections.
    Category: Access
    Privileges: User
    OperatingSystem: Windows, Linux, MacOS, ARM-Linux

  - Command: "ew -s lcx_slave -d $HOST_A_IP -e 8888 -f $HOST_B_IP -g 9999"
    Description: Runs the slave side of a documented multi-transfer chain, connecting to one EarthWorm hop and forwarding TCP traffic toward another hop.
    Usecase: Creating a multi-hop path to an internal TCP service such as SSH or RDP.
    Category: Access
    Privileges: User
    OperatingSystem: Windows, Linux, MacOS, ARM-Linux
Custom_Domain_Supported: True
Full_Path:
  - Filename: ew
  - Path: Downloaded or installed EarthWorm binary executed from a local directory.
Detection:
  - Command: 'Execution of an EarthWorm (ew) binary, including renamed copies, with documented SOCKS or LCX transfer modes such as -s ssocksd, rcsocks, rssocks, lcx_slave, lcx_listen or lcx_tran; correlate with SOCKS listener or TCP port-forwarding behavior.'
Resources:
  - Link: https://rootkiter.com/EarthWorm/en/index.html
  - Link: https://github.com/rootkiter/Binary-files
  - Link: https://www.trendaisecurity.com/en-us/resources-insights/trendai-security-blog/premier-pass-as-a-service
  - Link: https://www.secpod.com/blog/cl-sta-1132-weaponizes-pan-os-rce-for-silent-root-level-takeovers
  - Link: https://www.synacktiv.com/en/publications/open-source-toolset-of-an-ivanti-csa-attacker
  - Link: https://www.cisa.gov/news-events/cybersecurity-advisories/aa23-144a
---
