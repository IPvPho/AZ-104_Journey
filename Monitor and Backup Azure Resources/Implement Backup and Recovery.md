(AZ-104 | Michael Bender | Pluralsight)

# <ins>***Implement Backup and Recovery***</ins>
---

## <ins>*Business Continuity and Disaster Recovery*</ins>

- File and Folder Recovery
- VM Recovery
- Site-wide Recovery
- DC Fire or Azure Region down
- Recovery Point Objective (RPO)
  - What point at which you need to recover from
- Recovery Time Objective (RTO)
  - How quickly services need to be back up and running


### *Backup and Disaster Recovery Options in Azure*

- Azure Backup 
  - Cloud based backup for VMs and Files
  - On-prem VM's using MARS agents, VMware and Hyper-V
- Azure Site Recovery (ASR)
  - Provides site-to-site recovery of workloads in Azure, On-prem and in other clouds
  - Failover for full-site recovery


### <ins>*Recovery Services Vault*</ins>

- Storage Entity for backup and recovery resources
  - VMs and Files
- Centralized management for BCDR
- Work with on-premises and cloud-based workloads
- Can ONLY backup resources in the same region
- Site recovery resources must be in different region than original


## <ins>*Azure Backup*</ins

- Supports on-premises, Azure workloads, and other cloud workloads
- Scales with your organization
- Centralized monitoring and management
- App-Consistent backups
- Encrypted-at-rest by default
- Require resources and vault in the same region

### <ins>*Backup Policy*</ins>

- Stored in Recovery Services Vault
  - What is backed up, when it is backed up, and how long backup data is kept
- Defines how a backup plan is implemented
- Policy for each resource type
  

### <ins>*Backup Vault*</ins>

- Storage Entity for backup and recovery of newer Azure Workloads
- Supports Azure Backup security capabilities and RBAC
- Requires access to target resources 
- Redundancy of storage based on backup storage needs
  - Locally Redundant (LRS)
    - 3 copies of data synced in same DC
    - Recommended if Azure is NOT used a primary backup endpoint
  - Geo Redundant (GRS)
    - Azure is primary backup endpoint
    - Syncs backups to another Azure region 
  - Cannot changes redundancy after initial selection


### <ins>*Azure VM Restore Options*</ins>

- Can recover entire VM with OLR if source VM still exists and is being restored to original location or ALR where VM is restored to a different location
- Disk
- Files
  - All or a subset of files as selected
    - Can do this through scripting by temp mounting the files
- Cross-Region restore
  - Can pair with a second region 


### <ins>*Virtual Machine Soft Delete*</ins>

- Enabled by defaults
- Protects against unintended VM deletions
- Stored for up to 14 days 
- Requires a backup to have been completed
- Multiple tools for completing
  - PowerShell
  - AZ CLI
  - API
- Disabling not recommended


### <ins>*Azure Files Backup*</ins>

- Cloud-based backup for Azure Files
- Integrates with Azure File Sync (Hybrid Environments)
- Customized Retention
- Instant Restore
- Protects against accidental deletion with Soft Delete
- Snapshot-based

