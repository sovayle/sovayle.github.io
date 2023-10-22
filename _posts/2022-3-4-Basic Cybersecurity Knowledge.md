---
title: "Basic Cybersecurity Knowledge"
categories: knowledge
permalink: /blogs/basic-cybersecurity-knowledge
toc: true
toc_label: "Table of Contents"
toc_icon: stream # tasks #"torii-gate"
toc_sticky: true
---

Need to understand.

# CIA Triad: Confidentiality Integrity Availability

Confidentiality: Keeping an organisation's data private & only authorized users are able to access it {style: justified}

Integrity: The data can be trusted and it has not been altered

Availability: The data is able to be accessed by the authorized users that need access to it.

# DNS

Domain Name System

Port:53

When putting a URL in the browser, it checks the browser cache for any information on the URL, if not, it goes go router cache for any information, then goes to ISP cache and if it's not there, it will query one of the DNS servers across the world to locate the IP address.

# 7 Layers of The OSI Model

Application: Human-computer-Interaction layer, what we see and what we click on a browser for example.

Presentation: Ensures data is in usable format (encryption)

Session: Maintains connections and responsible for controlling ports and sessions.

Transport: Transmission protocols: TCP/UDP

Network: The IP layer, the ARP table, routing table (router)

Data Link: The data transporting information accross the hardware. (switch)

Physical: The hardware, the wiring. (cable)

# XSS

Cross Site Scripting

Main preventative measure: Input Sanitization (starts at application layer), but there are web application firewalls that do the job as well.

# Encryption vs Hashing.

Hashing: Permanent one-way function that is designed to preserve the integrity of a file.

Encryption: Reversable function that is designed to ensure confidentiality of a file.

# Vunerability Threat Asset

Asset: Data that needs to be safeguarded

Vulnerability: Weakness in protection

Risk: Likelihood vs impact (what would happen and what would be lost)

Threat: Something that can destroy the asset such as a person or a worm or a bot.

