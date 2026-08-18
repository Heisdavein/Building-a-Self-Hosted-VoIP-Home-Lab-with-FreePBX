# FreePBX VoIP Home Lab
Full Documentation Attached as PDF.

A hands-on self-hosted Voice over IP (VoIP) home lab documenting the deployment of FreePBX inside Oracle VirtualBox on Windows 11, the creation and configuration of a SIP extension, softphone registration using MicroSIP, real SIP call testing, two-way audio verification, Call Detail Record (CDR) analysis, and troubleshooting.

The project also includes an optional Cisco Packet Tracer section that explores the network infrastructure surrounding an enterprise VoIP deployment, including voice and data VLANs, DHCP, trunking, access ports, Router-on-a-Stick, and voice-network segmentation.

---

## Table of Contents

- [Project Overview](#project-overview)
- [Why I Built This](#why-i-built-this)
- [What I Built](#what-i-built)
- [Lab Environment](#lab-environment)
- [Technologies and Tools](#technologies-and-tools)
- [Architecture](#architecture)
- [End-to-End Deployment Plan](#end-to-end-deployment-plan)
- [Part A — FreePBX VoIP Server](#part-a--freepbx-voip-server)
  - [1. System Requirements](#1-system-requirements)
  - [2. Hardware Virtualization](#2-hardware-virtualization)
  - [3. Installing VirtualBox](#3-installing-virtualbox)
  - [4. Downloading FreePBX](#4-downloading-freepbx)
  - [5. Creating the Virtual Machine](#5-creating-the-virtual-machine)
  - [6. Virtual Machine Networking](#6-virtual-machine-networking)
  - [7. Installing FreePBX](#7-installing-freepbx)
  - [8. First Boot and IP Address](#8-first-boot-and-ip-address)
  - [9. FreePBX Web Interface](#9-freepbx-web-interface)
  - [10. Creating SIP Extension 1001](#10-creating-sip-extension-1001)
  - [11. Installing MicroSIP](#11-installing-microsip)
  - [12. Configuring the Softphone](#12-configuring-the-softphone)
  - [13. SIP Registration](#13-sip-registration)
  - [14. Echo Test](#14-echo-test)
  - [15. Two-Way Audio Verification](#15-two-way-audio-verification)
  - [16. CDR Verification](#16-cdr-verification)
- [Part B — VoIP Network Simulation](#part-b--voip-network-simulation)
  - [17. Cisco Packet Tracer](#17-cisco-packet-tracer)
  - [18. VoIP Network Topology](#18-voip-network-topology)
  - [19. Voice and Data VLANs](#19-voice-and-data-vlans)
  - [20. DHCP and Voice Networking](#20-dhcp-and-voice-networking)
  - [21. Router-on-a-Stick](#21-router-on-a-stick)
- [Troubleshooting](#troubleshooting)
- [Verification](#verification)
- [Skills Demonstrated](#skills-demonstrated)
- [Key Lessons Learned](#key-lessons-learned)
- [Security Considerations](#security-considerations)
- [Future Improvements](#future-improvements)
- [Project Status](#project-status)
- [Final Reflection](#final-reflection)

---

# Project Overview

This project documents the process of building a working VoIP phone system from the ground up.

The core of the lab is FreePBX, a free and open-source phone system built on top of Asterisk.

Because I did not have a dedicated physical server available, I deployed FreePBX inside a virtual machine running on my Windows 11 laptop using Oracle VirtualBox.

After installing and configuring FreePBX, I created a SIP extension and registered a softphone to the PBX.

The deployment was then tested using FreePBX's built-in Echo Test.

The successful test confirmed that:

- The FreePBX server was running.
- The virtual networking was working.
- The SIP extension was configured correctly.
- The softphone could authenticate.
- SIP registration was successful.
- SIP signalling was functioning.
- Audio could travel from the softphone to the PBX.
- Audio could return from the PBX to the softphone.
- The call was recorded in the FreePBX Call Detail Records.

The final communication path was:

```text
Windows 11 Host
       ↓
Oracle VirtualBox
       ↓
FreePBX Virtual Machine
       ↓
FreePBX Server
       ↓
SIP Extension 1001
       ↓
MicroSIP Softphone
       ↓
SIP Registration
       ↓
Echo Test (*43)
       ↓
Two-Way Audio
       ↓
Call Detail Record
