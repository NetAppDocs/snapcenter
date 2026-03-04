# Copilot instructions for SnapCenter software documentation

## Repository overview

Product: SnapCenter software

SnapCenter software provides application-consistent data protection for applications, databases, host file systems, and VMs running on ONTAP systems anywhere in the hybrid cloud. It delivers backup, restore, and clone capabilities through a server-plus-plug-in architecture.

## Repository structure

- `get-started/` – Overviews, licensing, RBAC, supported storage systems, and quick-start content
- `install/` – Server installation on Windows and Linux, high availability, CA certificates, and disaster recovery setup
- `protect-scsql/` – Plug-in for Microsoft SQL Server: install, backup, restore, clone, and disaster recovery
- `protect-hana/` – Plug-in for SAP HANA databases: install, backup, restore, and clone
- `protect-sco/` – Plug-in for Oracle databases: install, backup, restore, clone, and application volumes
- `protect-scw/` – Plug-in for Microsoft Windows file systems: install, backup, restore, and clone
- `protect-sce/` – Plug-in for Microsoft Exchange Server: install, backup, restore, and granular mail recovery
- `protect-db2/` – Plug-in for IBM Db2: install, backup, restore, and clone
- `protect-postgresql/` – Plug-in for PostgreSQL: install, backup, restore, and clone
- `protect-mysql/` – Plug-in for MySQL: install, backup, restore, and clone
- `protect-nsp/` – NetApp supported plug-ins framework for custom and community plug-ins
- `protect-scu/` – Plug-in for Unix file systems: install, backup, restore, and clone
- `protect-azure/` – Protecting SQL Server, SAP HANA, and Oracle workloads on Azure NetApp Files
- `admin/` – Dashboard, reporting, RBAC management, host and storage management, and job monitoring
- `upgrade/` – Upgrade workflows for SnapCenter Server and plug-ins
- `tech-refresh/` – Technology refresh procedures for server hosts, plug-in hosts, and storage systems
- `uninstall/` – Uninstallation procedures
- `sc-automation/` – REST API reference and automation guidance
- `release-notes/` – What's new and known issues per release
- `_include/` – Reusable content fragments shared across multiple plug-in directories

## Product-specific context

- **Server + plug-in architecture:** SnapCenter Server is the central management plane; data protection operations are performed by plug-ins installed on application hosts.
- **Resources, resource groups, and policies:** A *resource* is an individual database, file system, or application instance. A *resource group* is a collection of resources backed up together. A *policy* defines backup schedules, retention, and replication settings and is attached to a resource group.
- **Plug-in naming conventions:** Plug-ins are referred to as "SnapCenter Plug-in for <technology>" with the exact technology name. Use these approved names:
  - SnapCenter Plug-in for Microsoft SQL Server
  - SnapCenter Plug-in for Oracle Database
  - SnapCenter Plug-in for SAP HANA Database
  - SnapCenter Plug-in for Microsoft Windows
  - SnapCenter Plug-in for Microsoft Exchange Server
  - SnapCenter Plug-in for IBM Db2
  - SnapCenter Plug-in for PostgreSQL
  - SnapCenter Plug-in for MySQL
  - SnapCenter Plug-in for Unix
  - SnapCenter Plug-in for MongoDB
  - SnapCenter Plug-in for Oracle Applications
  - SnapCenter Plug-in for SAP ASE
  - SnapCenter Plug-in for SAP MaxDB
  - SnapCenter Plug-in for Storage
  
  Avoid shortening to just "the plug-in" without the qualifier on first reference. Do not shorten technology names (for example, use "Oracle Database" not "Oracle"). When referring to a specific plug-in in context, use "the SnapCenter Plug-in for [technology]" with the article "the."

- **NetApp supported plug-ins:** A SnapCenter component that provides a framework for plug-ins not included in the dedicated plug-in offerings. The framework ships with several pre-built plug-ins (MongoDB, Oracle Applications, SAP ASE, SAP MaxDB, Storage). Always use the exact capitalization "NetApp supported plug-ins" (only "NetApp" is capitalized). When referring to this component in general text, use "NetApp supported plug-ins" without inserting "SnapCenter" into the phrase; if context requires mentioning SnapCenter, use patterns like "NetApp supported plug-ins in SnapCenter" or "NetApp supported plug-ins for SnapCenter." Do not use "custom plug-ins" as a synonym for this component.

- **Plug-ins Package:** When referring to plug-in installation packages, use "the Plug-ins Package for [platform]" (for example, "the Plug-ins Package for Linux"). Always include the article "the" before "Plug-ins Package."

- **SnapCenter Server:** When referring to the server component in context, use "the SnapCenter Server" or "SnapCenter Server" (both are acceptable, but "the" is preferred when referring to a specific instance).

- **Snapshot-based backups:** All backups are ONTAP Snapshot copies; the terms "backup" and "Snapshot copy" are used deliberately—do not substitute "snapshot" (lowercase) unless quoting UI text.
- **SnapMirror and SnapVault:** Secondary protection is achieved via SnapMirror (replication) or SnapVault (backup to secondary); these are distinct and should not be used interchangeably.
- **ASA r2 systems:** A subset of SnapCenter operations are supported on NetApp ASA r2 all-flash SAN arrays; content specific to ASA r2 is in dedicated files named `create-resource-groups-secondary-protection-for-asa-r2-*.adoc`.
- **Clone lifecycle:** Clones created from backups can be split (made independent) or refreshed; "clone split" and "clone refresh" are distinct operations.
- **CA certificates:** Each plug-in section contains a standard set of CA certificate tasks (generate CSR, import, configure, enable); reusable versions live in `_include/`.
- **gMSA:** Group Managed Service Accounts (gMSA) are a Windows authentication option for plug-in host services; configuration tasks appear in most Windows plug-in sections.
- **PowerShell cmdlets:** Most operations can be automated via SnapCenter PowerShell cmdlets; cmdlet-based task files are a standard complement to UI-based task files in each plug-in section.

## Typical user workflows

- **Protect a database:** Install plug-in on host → add host to SnapCenter → discover or add resources → create policy → create resource group and attach policy → run on-demand or scheduled backup
- **Restore a database:** Identify backup in topology view → run restore wizard → select restore scope and recovery point → verify restore
- **Clone a database:** Select backup → run clone wizard → specify clone target host and configuration → optionally split clone
- **Upgrade SnapCenter:** Run pre-upgrade checks → upgrade SnapCenter Server → upgrade plug-ins on all hosts