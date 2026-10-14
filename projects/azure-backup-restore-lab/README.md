# Project 5: Azure Backup and Restore Lab

**Author:** Samuel Gebu  
**Lab dates:** 13–14 October 2026  
**Region:** South Africa North  
**Outcome:** Successful VM backup and user-confirmed recovery of a deleted sample file.

## Why I built this

I wanted to practise the part of backup administration that matters when something goes wrong: getting a file back. I deployed a Windows Server VM, protected it with Azure Backup, deleted a fictional business record after a successful backup, and recovered it using Azure File Recovery.

This is a personal lab. It demonstrates file recovery within one region, with the verification limits described below.

## Environment

| Component | Lab configuration |
| --- | --- |
| Resource group | `rg-backup-restore-lab` |
| VM | `vm-backup-lab` |
| Location | South Africa North, Zone 1 |
| OS | Windows Server 2025 Datacenter Azure Edition |
| VM size | Standard DS1_v2 |
| OS disk | Standard SSD, platform-managed encryption key |
| Security | Trusted Launch, Secure Boot and vTPM |
| NSG | `nsg-backup-lab` |
| Recovery Services vault | `rsv-backup-lab` |
| Backup policy | `policy-backup-lab-daily`, Enhanced |
| Vault redundancy | LRS, saved during the guided setup |
| Sample file | `C:\BackupLab\BusinessRecords.txt` |

The saved policy was verified in the live Azure portal on 14 October 2026: daily at 22:00 UTC, 30 days for daily recovery points, and 2 days for instant recovery snapshots. LRS does not provide regional disaster recovery.

The live network settings showed `Allow-RDP-MyIP` at priority 100, allowing TCP 3389 from one explicit IPv4 `/32` source. The source address itself is withheld. This confirms the configured single-IP restriction; current ownership of that source IP was not independently checked. Public IP values, subscription identifiers and credentials are excluded from this repository.

## What I did

1. Deployed the VM and connected through Remote Desktop.
2. Created `BusinessRecords.txt` containing fictional invoice data.
3. Created a Recovery Services vault and saved LRS before enabling backup.
4. Enabled VM protection with the Enhanced backup policy.
5. Investigated failed duplicate backup requests and waited for the existing operation to complete.
6. Confirmed the portal showed a successful backup before deleting the sample file.
7. Selected a recovery point from before deletion and downloaded the Azure File Recovery executable.
8. Used Remote Desktop drive redirection when clipboard transfer did not work.
9. Ran the executable as administrator on the VM, mounted the recovery volumes, and located the backed-up file.
10. Copied the file to its original folder, opened it to check its contents, and unmounted the recovery disks.

## Problems I worked through

| Problem | What I learned and did |
| --- | --- |
| No quota available for a new public IP | Reused an existing unassociated Standard public IP in the same region. It belongs to another lab resource group and needs separate review during cleanup. |
| Repeated manual backup attempts showed Failed | Job details reported `UserErrorBackupOperationInProgress`. Another backup was already running, so I stopped submitting duplicate requests and waited for it to finish. |
| Clipboard copy and paste failed in Remote Desktop | Enabled local drive redirection and transferred the recovery executable through the redirected drive. |
| Needed to locate the file after mounting recovery volumes | Browsed the mounted backup volume, found the sample folder, and copied the file back to the VM's original path. |

See the [troubleshooting notes](docs/troubleshooting.md) for more detail.

## Result and evidence

- The live portal and the screenshot reviewed during the exercise showed **Last backup status: Success** on 14 October 2026 at 12:55:35 AM.
- The selected application-consistent recovery point was displayed as 14 October 2026 at 12:55:51 AM.
- Finding the file, restoring it, checking its contents, and unmounting the recovery disks were confirmed during the guided exercise.

Times above are recorded as displayed by the portal; the display timezone was not separately recorded. The schedule itself was configured in UTC.

No file hashes or timed recovery measurements were captured. This exercise did not test a full VM restore, database recovery, or cross-region recovery. The [evidence and validation record](docs/evidence-and-validation.md) separates observed portal evidence from user-confirmed results and pending checks.

## Documentation

- [Live portal verification addendum](docs/portal-verification.md)
- [Portfolio report (Word)](Samuel_Gebu_Azure_Project_5_Portfolio.docx)
- [Recovery runbook](docs/recovery-runbook.md)
- [Troubleshooting notes](docs/troubleshooting.md)
- [Evidence and validation record](docs/evidence-and-validation.md)
- [LinkedIn post draft](LINKEDIN_POST.md)

The Word report records the earlier exercise. The live verification addendum supersedes its pending checks for the saved policy and RDP rule.

Raw portal screenshots and recovery executables are excluded because they may expose private account, infrastructure or recovery-session information.

## Remaining checks

- Correct the observed Project tag typo from `Aazure-Backup-Restore-Lab` to `Azure-Backup-Restore-Lab` where present.
- Retain redacted evidence for future review.
- Review ongoing VM, disk, public IP and backup storage costs. Resource deletion and backup cleanup have not been confirmed.
- Review the reused public IP separately before removing anything from another lab.

## Skills practised

Azure VM administration, vault and backup policy configuration, recovery point selection, backup-job diagnosis, Remote Desktop drive redirection, file recovery, and documenting verification limits.
