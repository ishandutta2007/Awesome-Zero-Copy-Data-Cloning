# Awesome-Zero-Copy-Data-Cloning

## Top Zero-Copy Data Cloning Ecosystem



**Curated List of SaaS Products & Open-Source GitHub Projects**  

*Focused on Copy-on-Write Snapshots, Instant Database Clones & Self-Hosted Data Virtualization*  

**Last updated: October 2026**



This repository tracks notable **SaaS platforms** and **open-source projects** for **Zero-Copy Data Cloning**. These tools enable organizations to create instant, space-efficient copies of databases, filesystems, and volumes by sharing underlying data blocks rather than duplicating them—accelerating development, testing, analytics, and disaster recovery without multiplying storage costs.



**Examples** include Snowflake Zero-Copy Clone, Actifio (Google Cloud), Delphix Dynamic Data Platform, NetApp SnapMirror, Pure Storage FlashRecover, Cohesity, Rubrik, K2View, Nutanix Era, and Redgate SQL Clone (the category leaders).



**Open-source emphasis**: Zero-Copy Data Cloning is a domain where open-source tooling is **emerging at the filesystem and database-specific layers**, but **fragmented across platforms**. The strongest active projects are **cubecow** (a Rust library leveraging XFS/Btrfs FICLONE for O(1) snapshots) , **pgclone** (a PostgreSQL extension for native SQL-based cloning with data masking) , and **StagDB** (a self-hosted platform orchestrating ZFS-backed PostgreSQL clones in ~5 seconds) . For filesystem-level cloning, **go-zfsutils** provides Go bindings for ZFS operations including clone management , and **vibe-native** offers Node.js bindings for APFS clonefile and Linux FICLONE . The critical gap: **no open-source project replicates the cross-platform, application-aware data virtualization** of Delphix or Actifio—those platforms virtualize entire application stacks (Oracle, SQL Server, SAP) with masking and orchestration that open-source tools address only piecemeal.



Contributions welcome! Open a PR to add/update entries. Keep descriptions factual and link to official sites.



## Table of Contents

- [SaaS/Hosted Platforms](#saas-products)

- [Open-Source GitHub Projects](#open-source-github-projects)

- [How to Contribute](#how-to-contribute)

- [Disclaimer](#disclaimer)



## SaaS/Hosted Platforms



- **[Snowflake Zero-Copy Clone](https://docs.snowflake.com/en/user-guide/object-clone)**  

  Native zero-copy cloning within Snowflake; creates instant clones of databases, schemas, and tables that share the same micro-partitions as the source, consuming no additional storage until changes are made. Clone operations are metadata-only, enabling rapid dev/test environments and point-in-time snapshots without data duplication. **A key differentiator that open-source warehouses like ClickHouse do not replicate** .



- **[Actifio (Google Cloud)](https://cloud.google.com/actifio)**  

  Copy Data Management (CDM) platform (now part of Google Cloud) that virtualizes application data to create instant, space-efficient copies for backup, DR, dev/test, and analytics. Actifio GO provides cloud-based backup and recovery for Google Cloud and hybrid workloads (VMware, SAP HANA, Oracle, SQL Server) with SLA-driven policies and incremental-forever backups .



- **[Delphix Dynamic Data Platform](https://www.delphix.com/)**  

  Enterprise data virtualization platform that creates virtual copies of databases (Oracle, SQL Server, PostgreSQL, SAP) with built-in masking and orchestration. Deployed as a proprietary appliance; positions itself as accelerating DevOps and AI workflows with compliant, on-demand data. Competitors note its appliance-based model and $500K+/year pricing as barriers .



- **[NetApp SnapMirror](https://www.netapp.com/)**  

  Storage-level replication and cloning technology within ONTAP; creates space-efficient FlexClone volumes that share blocks with the parent until modified. Enables instant clones for dev/test, backup, and disaster recovery at the storage layer.



- **[Pure Storage FlashRecover](https://www.purestorage.com/)**  

  Snapshot and replication technology within Pure Storage arrays; provides space-efficient, instant clones of volumes and consistent point-in-time copies across on-premises and cloud environments.



- **[Cohesity](https://www.cohesity.com/)**  

  Data management platform with instant mass restore and space-efficient clones for backup, DR, and dev/test; unifies data protection across on-premises, cloud, and edge environments.



- **[Rubrik](https://www.rubrik.com/)**  

  Cloud data management platform with instant recovery and live mounts for dev/test; provides zero-copy access to backups via Rubrik CDM.



- **[K2View](https://www.k2view.com/)**  

  Data product platform with Micro-Database technology that holds entity-level data (one customer, one order) separately; supports data virtualization, masking, tokenization, and synthetic data generation for operational, analytical, and AI systems. **Closed-source and vendor-hosted**; the platform is not open source .



- **[Nutanix Era](https://www.nutanix.com/)**  

  Database automation and copy data management platform for Nutanix AHV and VMware; provides one-click database clones, time machine snapshots, and copy data management for Oracle, SQL Server, PostgreSQL, MySQL, and SAP HANA.



- **[Redgate SQL Clone](https://www.redgate.com/)**  

  Windows-based SQL Server cloning tool that creates virtual database copies in seconds using differential disk images; enables dev/test environments with minimal storage overhead.



## Open-Source GitHub Projects



### Database Cloning Extensions & Platforms



- **[pgclone](https://github.com/valehdba/pgclone)**  

  PostgreSQL extension (PostgreSQL Licence) for **native SQL-based database cloning** without `pg_dump`/`pg_restore` or shell scripts . Features: clone databases, schemas, and objects via SQL commands; **integrated data masking** (emails, names, phone numbers, hashes) during cloning with auto-discovery of sensitive columns and suggested masking rules; parallel background workers for high performance; full DDL support (indexes, constraints, triggers, views, sequences); configurable conflict resolution (error, skip, replace, rename); tested on PostgreSQL 14–18. **The most mature open-source PostgreSQL cloning tool**—but PostgreSQL-specific and does not provide cross-database or application-aware virtualization.



- **[StagDB (Community Edition)](https://github.com/abuta-labs/stagdb-ce)**  

  Self-hosted platform for **instant PostgreSQL database clones** using Docker + ZFS (Django orchestration) . Creates clones in ~5 seconds via ZFS snapshot/clone operations; each clone runs in its own PostgreSQL container backed by a dedicated ZFS dataset. Features: web dashboard, clone-from-database or restore-from-snapshot, PostgreSQL 11–16 support, health checks, and copy-paste connection strings. **The simplest self-hosted clone orchestration layer** for teams already running ZFS—but limited to PostgreSQL and requires ZFS infrastructure.



### Filesystem & Storage-Level Cloning



- **[cubecow (Tencent Cloud)](https://github.com/tencentcloud/cubesandbox/tree/master/cubecow)**  

  Rust library crate providing **Copy-On-Write storage engine** built on xfs-reflink (FICLONE) . Features: **O(1) snapshots and clones** via kernel `FICLONE` ioctl; thin-provisioned volume management; flat snapshot model (deleting one snapshot never affects others); backend-agnostic API via `Engine` trait; simple crash recovery (volumes and snapshots are files). **The cleanest low-level building block** for implementing zero-copy cloning in Rust applications—but it is a library, not a complete data management platform.



- **[go-zfsutils](https://pkg.go.dev/github.com/vansante/go-zfsutils)**  

  Go library providing bindings for ZFS operations including **clone creation** (`CloneOptions`), filesystem/dataset management, snapshots, and send/receive . **For Go developers** building custom ZFS-based cloning workflows—provides the primitives without a UI or orchestration layer.



- **[vibe-native (@kexi/vibe-native)](https://www.npmjs.com/package/@kexi/vibe-native)**  

  Node.js native module for **Copy-on-Write file cloning** using Rust (napi-rs) . Uses `clonefile()` on macOS APFS and `FICLONE` ioctl on Linux Btrfs/XFS; provides async and sync APIs with TypeScript support. **For Node.js applications** needing instant file/directory clones—not database-aware, but useful for artifact and workspace cloning.



- **[reflink (egladman/magus)](https://pkg.go.dev/github.com/egladman/magus@v0.2.1/internal/cache/reflink)**  

  Go package that copies files using the most efficient mechanism available: **FICLONE reflink on Linux, clonefile on APFS**, falling back to zero-copy splice or userspace copy . Includes `Probe()` to detect filesystem support. **A minimal utility** for Go projects needing reflink-aware file copying.



### Additional Strong Open-Source Options



- **Dremio** — Data lakehouse platform with **data virtualization** capabilities (virtual views over federated sources without materialization) . Not zero-copy cloning in the storage sense, but provides logical data abstraction that avoids physical copies for analytics. **Apache-licensed** but heavier infrastructure.

- **No open-source equivalent to Delphix or Actifio exists** — The application-aware virtualization (Oracle, SQL Server, SAP), cross-platform orchestration, and enterprise masking policies of these CDM platforms are not replicated by any active open-source project. pgclone and StagDB address PostgreSQL cloning; cubecow provides filesystem primitives; none provide the full CDM stack.



**Frameworks for building custom systems**: For **PostgreSQL cloning with masking**, pgclone provides the most complete native extension . For **self-hosted PostgreSQL clone orchestration**, StagDB with ZFS offers a working platform . For **custom storage-layer cloning**, cubecow (Rust) or go-zfsutils (Go) provide the primitives . For **Snowflake environments**, zero-copy clone is native and requires no open-source alternative . No open-source project delivers the full application-aware data virtualization of Delphix—organizations requiring that depth should evaluate commercial platforms or build custom orchestration atop these primitives.



## How to Contribute



1. Fork the repo.

2. Add/edit entries in `README.md` (follow existing format).

3. Include: name, link, 1–2 sentence description, and whether it's SaaS or open-source.

4. Submit PR with a short explanation.



Star the repo if you find it useful!



## Disclaimer



- This is a **community-curated** list — not exhaustive and not an endorsement.

- Zero-copy cloning tools handling production data must implement proper access controls and data masking; clones that share underlying blocks with production can expose sensitive data if masking is not applied before provisioning to non-production environments.

- **Open-source zero-copy cloning is fragmented across layers**—pgclone and StagDB address PostgreSQL , cubecow provides filesystem primitives , and go-zfsutils/vibe-native offer language bindings . However, **no open-source project replicates the application-aware, cross-platform data virtualization** of Delphix or Actifio, and **Snowflake's zero-copy clone remains a proprietary differentiator** that open-source warehouses do not match . Organizations requiring enterprise-scale CDM should evaluate commercial platforms.

- Verify license terms for commercial use; pgclone uses the PostgreSQL Licence , cubecow is an open-source Rust crate , and StagDB Community Edition is open-source (check repository) .



---



**Made for database administrators, DevOps engineers, data platform architects, and test environment managers.**  

Let's make zero-copy data cloning more open, but with clear eyes about the application-aware virtualization gap that commercial CDM platforms still fill.
