##########Dual-Link Hot Standby (HSB) Architecture for Huawei AirEngine APs#########

This project demonstrates a Dual-Link Hot Standby (HSB) Wireless Controller architecture using Huawei Access Controllers (ACs) and AirEngine 5761 Wi-Fi 6 Access Points.
The design ensures high availability, seamless failover, and zero session loss in enterprise wireless networks.

If the primary controller (AC1) fails, the standby controller (AC2) immediately takes over without dropping AP connections or client sessions.

1. Deployment Architecture
Active / Standby Controllers

AC1 → Master (Active)

AC2 → Backup (Standby)

Both controllers operate in Hot Standby (HSB) mode with real-time synchronization.

Heartbeat Link

A dedicated Layer 2 or direct link between AC1 and AC2

Used for:

Health monitoring

Configuration synchronization

Client session state synchronization

VRRP (Virtual Router Redundancy Protocol)

AC1 and AC2 share a Virtual IP (VIP) using VRRP

All AirEngine 5761 APs register to the VIP

Hardware redundancy remains transparent to the APs

2. Configuration Logic (High Level)
HSB Service

Huawei HSB Service is enabled on both controllers

Synchronizes:

Configuration

AP state

Client session information

VRRP Configuration

VRRP is configured on the management VLAN

Controller	Role	VRRP Priority
AC1	Master	120
AC2	Backup	100
CAPWAP Configuration

CAPWAP source address is set to the VRRP Virtual IP

Ensures APs automatically reconnect to the active AC

AP Provisioning

AirEngine 5761 APs authenticate using:

MAC address or

Serial Number (SN)

Once joined:

AC pushes VAP profiles (SSID, Security, VLANs)

Centralized control is maintained

3. Seamless Connectivity & Failover Features
CAPWAP Keep-Alive

APs continuously monitor controller availability

If AC1 fails:

CAPWAP tunnel immediately switches to AC2

No manual intervention required

Session Persistence

Client sessions are synchronized via HSB

End users do not need to re-authenticate

Ongoing traffic remains uninterrupted

AirEngine 5761 Advantages

Wi-Fi 6 (802.11ax) support

Smart Antennas

Lossless roaming

Works with AC mobility features for:

Zero packet loss

Seamless Layer 2 / Layer 3 roaming

4. End-to-End Workflow

AP boots and discovers the AC using the VRRP Virtual IP

CAPWAP tunnel is established to the active controller (AC1)

AC pushes:

SSID

Security policies

VLAN configuration

Clients connect to the AirEngine 5761 AP

HSB continuously synchronizes:

AP state

Client sessions

If AC1 fails:

VRRP shifts VIP to AC2

APs re-anchor CAPWAP tunnel to AC2

Clients remain connected with no session drop

5. Key Highlights (For Slides / Portfolio)

Redundancy: Dual-AC Hot Standby (HSB) with VRRP Virtual IP

Control: Centralized AirEngine 5761 management via CAPWAP

Reliability: Real-time session synchronization for hitless failover

Performance: Wi-Fi 6 optimization with seamless roaming

Enterprise-Ready: High availability design for mission-critical WLANs
