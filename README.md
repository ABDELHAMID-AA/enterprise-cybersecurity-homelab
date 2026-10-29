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
| 1 | Infrastructure and identity | In progress |
| 2 | Security monitoring and Windows telemetry | Planned |
| 3 | Splunk SIEM and detection engineering | Planned |
| 4 | Azure administration and Microsoft Sentinel | Planned |
| 5 | Hybrid identity and cross-environment monitoring | Planned |
| 6 | SOC investigations and threat hunting | Planned |

Full build steps, configs, and evidence live in each phase folder (see [Documentation](#documentation)).

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

---

## Phase 1: Enterprise Infrastructure and Identity

Build the foundation of a virtual enterprise network.

- **Network core:** OPNsense firewall, routing, segmentation, and Kea DHCP
- **Identity:** Windows Server, Active Directory DS, internal DNS with external forwarding
- **Endpoints:** Domain-joined Windows client with validated DHCP/DNS settings
- **Structure:** OUs, security groups (AGDLP), and least-privilege administration
- **Policy:** Group Policy baselines, password and lockout policies
- **Troubleshooting:** Documented DHCP, gateway, DNS forwarding, and connectivity cases

**Target outcome:** A working, validated domain environment with documented design decisions and troubleshooting evidence.

## Phase 2: Security Monitoring

Establish visibility into what happens across the infrastructure.

- **Auditing:** Windows Security and AD audit policy via GPO
- **Authentication:** Collect and analyze logon, failure, and lockout events
- **Change tracking:** Account, group, and policy changes
- **Endpoint telemetry:** Sysmon for process, network, and registry activity
- **Event generation:** Controlled test activity to produce known-good and suspicious events
- **Mapping:** Link observed behavior to MITRE ATT&CK

**Target outcome:** A documented baseline of normal activity and a catalog of suspicious behavior with the events that reveal it.

## Phase 3: Splunk SIEM

Deploy Splunk as the central monitoring and investigation platform.

- **Ingestion:** Forward Windows Security and Sysmon logs
- **Data model:** Indexes, sourcetypes, fields, and timestamps
- **Searching:** SPL for authentication and endpoint activity
- **Visualization:** Dashboards and reports
- **Detections:** Alerts for lockouts, privilege changes, suspicious process execution
- **Tuning:** False-positive analysis and documented limitations

**Target outcome:** A tested detection set with documented logic, tuning notes, and recommended responses.

## Phase 4: Microsoft Azure and Sentinel

Extend the lab into the cloud and build cloud security monitoring.

- **Azure admin:** Resource groups, VNets, VMs, storage, RBAC, and cost control
- **Controls:** Network security, least privilege, and activity monitoring
- **Sentinel:** Workspace, data connectors, tables, and analytics rules
- **KQL:** Queries for investigation and hunting
- **Response:** Incident management, workbooks, and automation where available

**Target outcome:** A working Sentinel workspace with documented KQL queries, analytics rules, and cloud investigation procedures.

## Phase 5: Hybrid Identity and Security

Connect on-premises identity with the cloud.

- **Sync:** Supported hybrid synchronization between AD DS and Entra ID
- **Cloud identity:** Role administration, sign-in logs, and audit logs
- **Monitoring:** Correlate on-prem and cloud authentication events
- **Investigation:** Suspicious identity activity across both environments

**Target outcome:** A verified hybrid deployment. Having AD and Entra ID side by side does not count until sync and monitoring workflows are validated.

## Phase 6: Advanced SOC Investigations and Threat Hunting

Run realistic multi-stage investigations by correlating endpoint, AD, network, SIEM, and cloud telemetry.

- **Multi-stage intrusion reconstruction** across hosts
- **Active Directory attack-path investigation** (privileges, delegation abuse)
- **Living-off-the-land activity** (admin vs. malicious PowerShell and utilities)
- **Lateral movement and credential misuse**
- **Persistence and defense evasion** (tasks, services, registry, logging tampering)
- **Insider threat and compromised account** analysis
- **Network threat hunting** (DNS, beaconing, C2)
- **Hybrid identity incident investigation** (AD + Entra ID)
- **Cloud privilege escalation and persistence** (Azure roles, service principals)
- **Detection engineering** with SPL and KQL, including false-positive measurement and gap analysis

Each investigation follows: **Detection → Evidence → Timeline → Analysis → Impact → Response → Detection improvement.**

**Target outcome:** A portfolio of evidence-based investigations showing threat hunting, SIEM analysis, and incident response reasoning.

---

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
