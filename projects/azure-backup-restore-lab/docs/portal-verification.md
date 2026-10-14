# Live Azure portal verification — 14 October 2026

This addendum records a signed-in portal review performed after the original Word report was prepared. It supersedes the report's pending verification notes for the saved backup policy and inbound RDP rule.

| Item | Live observation |
| --- | --- |
| VM | `vm-backup-lab`, Running |
| Region | South Africa North, Zone 1 |
| OS | Windows Server 2025 Datacenter Azure Edition |
| Size | Standard DS1 v2, 1 vCPU, 3.5 GiB RAM |
| Security | Trusted Launch, Secure Boot and vTPM enabled |
| Backup precheck | Passed |
| Last backup | Success, 14/10/2026 00:55:35 as displayed |
| Recovery points | Four application-consistent points listed; newest 14/10/2026 00:55:51 |
| Vault | `rsv-backup-lab`, South Africa North |
| Saved policy | `policy-backup-lab-daily`, Enhanced |
| Schedule | Daily at 22:00 UTC |
| Instant snapshots | 2 days |
| Daily retention | 30 days |
| Network security | `nsg-backup-lab` attached to the VM NIC |
| Custom inbound rule | `Allow-RDP-MyIP`, priority 100, TCP 3389, Allow, one IPv4 /32 source |
| Other inbound rules | Default VNet and Azure Load Balancer allows, then default deny |
| VM tags | Environment=Lab, Owner=Samuel-Gebu, Purpose=Portfolio; Project tag still has the documented `Aazure` typo |

The source address is omitted; its present ownership was not independently checked. No custom inbound HTTP or HTTPS allow rule was listed. This is a configuration review, not an effective-connectivity test.

Vault redundancy remains based on the user's earlier confirmation that LRS was saved. Restoring the file and unmounting recovery disks remain user-confirmed outcomes from the exercise; this review did not repeat recovery or inspect the guest filesystem.

The VM was still running at review time. Cleanup and resource deletion were not performed. Recovery executables, credentials, IP values, subscription IDs and account identifiers are excluded from public documentation.
