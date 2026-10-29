# Enterprise Cybersecurity Homelab

A hands-on enterprise lab built with VMware Workstation, OPNsense, Windows Server, Active Directory, Splunk, Azure, and Microsoft Sentinel. The goal: simulate a realistic enterprise environment, monitor it, attack it in a controlled way, and investigate the results like a SOC analyst.

> **Status:** Phase 1 in progress. Items are marked complete only after they are implemented and validated.

## Objectives

- Build and troubleshoot an enterprise network (firewall, routing, DHCP, DNS)
- Administer Windows Server and Active Directory (OUs, groups, GPOs, least privilege)
- Collect and analyze security telemetry (Windows auditing, Sysmon)
- Engineer detections with Splunk (SPL) and Microsoft Sentinel (KQL)
- Extend into Azure and hybrid identity (Entra ID)
- Investigate incidents end to end and document them with evidence

## Roadmap

| Phase | Focus | Status |
|---|---|---|
| 1 | Infrastructure and identity (OPNsense, AD, DNS, DHCP, GPO) | In progress |
| 2 | Security monitoring and Windows telemetry | Planned |
| 3 | Splunk SIEM and detection engineering | Planned |
| 4 | Azure administration and Microsoft Sentinel | Planned |
| 5 | Hybrid identity and cross-environment monitoring | Planned |
| 6 | SOC investigations and threat hunting | Planned |

Each phase has its own folder with full build steps, configs, and evidence (see [Documentation](#documentation)).

## Architecture (target)

```text
        Internet
           |
   OPNsense Firewall
           |
   Internal LAN 10.10.10.0/24
   ├── DC01  (AD DS + DNS, corp.local)
   ├── WS01  (domain-joined client)
   └── Other lab VMs
           |
   Windows Security + Sysmon logs
      ├── Splunk
      └── Azure / Entra ID → Microsoft Sentinel
           |
   Detection and investigation
```

This is the intended design, not a claim that every integration is deployed yet.

## Phase 6 Investigation Scenarios (planned)

- Multi-stage intrusion reconstruction
- Active Directory attack paths
- Lateral movement and credential misuse
- Persistence and defense evasion
- Network threat hunting (DNS, beaconing, C2)
- Hybrid identity and cloud privilege escalation

Each investigation follows: **Detection → Evidence → Timeline → Analysis → Impact → Response → Detection improvement.**

## Technologies

VMware Workstation · OPNsense · Kea DHCP · Windows Server · Active Directory · Group Policy · PowerShell · Wireshark · Sysmon · Splunk · Azure · Entra ID · Microsoft Sentinel · MITRE ATT&CK

## Certification Alignment

| Certification | Related work |
|---|---|
| AZ-104 | Azure administration, networking, identity |
| SC-200 | Sentinel, KQL, incident investigation |
| Splunk Core Certified Power User | SPL, reports, dashboards |

Verify exam codes and requirements on the vendors' official pages before scheduling.

## Documentation

Detailed build notes live in the phase folders:

```text
├── architecture/
├── phase-01-enterprise-infrastructure/
├── phase-02-security-monitoring/
├── phase-03-splunk-siem/
├── phase-04-azure-sentinel/
├── phase-05-hybrid-identity/
├── phase-06-soc-investigations/
├── evidence/
├── configs/
└── scripts/
```

Folders are added as content is published.

## Security Notes

- Keep the lab isolated from production networks.
- Use test accounts and non-sensitive data only.
- Redact credentials, tokens, and keys from screenshots and configs.
- Never commit VM disks, secrets, or private keys.
- Remove unused cloud resources to control cost.

## Principle

Success is measured by the ability to build, secure, monitor, troubleshoot, and investigate the environment, and to explain every decision with evidence.
