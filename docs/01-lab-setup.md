# Lab Setup

## Objective

The objective of this project is to build a Home SOC laboratory using Wazuh. 
I will use this lab to learn how to collect and analyze Windows security events
and investigate suspicious activity.

## Environment

## Ubuntu:
- OS: Ubuntu (64-bit)
- RAM: 8 GB (8192 MB)
- CPU: 4
- Storage: 50 GM
- IP: 192.168.0.193

Windows:
- OS: Windows (64-bit)
- RAM: 6 GB (6144 MB)
- CPU: 4
- Storage: 60 GB
- IP: 192.168.0.164
- Hostname: SOC-WIN11

Both virtual machines are running in VirtualBox.

The Ubuntu virtual disk was increased from 25 GB to 50 GB to provide
additional storage for Wazuh components and collected security data.

## Network Configuration

Both VMs use Bridge Adapter and are connected to the same local network. 
This allows the Windows endpoint to communicate directly with the Ubuntu
server running Wazuh.

## Connectivity Test

Network connectivity between the two virtual machines was verified using
`ping`.

The Windows endpoint was able to reach the Ubuntu server, and the Ubuntu
server was able to reach the Windows endpoint.

## Result

The basic infrastructure for the Home SOC lab was successfully configured.

Both virtual machines are running on the same local network and can
communicate with each other.

The environment is ready for Wazuh deployment and endpoint monitoring.
