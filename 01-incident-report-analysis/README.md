# Incident Report Analysis

## Objective
Analyze a documented security incident from detection through recovery, applying the NIST Cybersecurity Framework core functions (Identify, Protect, Detect, Respond, Recover) as covered in the Google Cybersecurity Certificate.

## Tools & frameworks used
<div>
    <img src="https://img.shields.io/badge/-NIST_CSF-D85A30?style=for-the-badge" />
    <img src="https://img.shields.io/badge/-Firewall_Configuration-2C3E50?style=for-the-badge" />
    <img src="https://img.shields.io/badge/-Network_Monitoring-1D9E75?style=for-the-badge" />
    <img src="https://img.shields.io/badge/-Incident_Playbooks-1D9E75?style=for-the-badge" />
</div>

## Summary
The organization's network services suddenly stopped responding due to a flood of incoming ICMP packets, preventing normal internal traffic from reaching any network resources. Investigation revealed that a malicious actor had exploited an improperly configured firewall to send a sustained flood of ICMP pings, saturating the network in a denial-of-service (DoS) attack. The incident response team contained the attack by blocking incoming ICMP traffic, took non-critical services offline to reduce load, and restored critical services — resulting in a temporary slowdown of operations but no lasting damage.

## Process (NIST Cybersecurity Framework)

### 1. Identify
The incident response team recognized that a flood of incoming ICMP packets was overwhelming the network, preventing internal traffic from accessing resources. The immediate response was to block the incoming ICMP packets, take non-critical services offline, and restore critical services — which caused a temporary slowdown but no serious damage.

### 2. Protect
The threat was identified as a malicious ICMP flood attack affecting the entire internal network. Priority was placed on securing and restoring all critical network resources to a functioning state.

### 3. Detect
The cybersecurity team configured **source IP address verification** on the firewall to catch spoofed IP addresses on incoming ICMP packets, and implemented **network monitoring software** to flag abnormal traffic patterns going forward.

### 4. Respond
For future events of this kind, the response plan is to: isolate affected systems to prevent further disruption, restore disrupted critical systems and services, analyze network logs for suspicious or abnormal activity, and report the incident to upper management and appropriate legal authorities when applicable.

### 5. Recover
Recovery from an ICMP-flood DoS attack follows this order:
1. Block external ICMP flood traffic at the firewall.
2. Stop all non-critical network services to reduce internal traffic load.
3. Restore critical network services first.
4. Once the flood of ICMP packets has timed out, bring remaining non-critical systems and services back online.

## Key takeaways
- A single misconfigured firewall rule (allowing unrestricted ICMP traffic) was enough to let an attacker saturate the entire internal network — reinforcing the importance of least-privilege firewall rules even for seemingly harmless protocols like ICMP.
- Recovery order matters: restoring critical services before non-critical ones minimizes business impact while the network is still under load.
- Source IP verification and network monitoring are low-cost, high-value detection controls that would have flagged this attack earlier.

## Files
- [Full report (PDF)](./incident-report-analysis.pdf) — original write-up
