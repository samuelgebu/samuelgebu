# Evidence and validation record

This record was prepared from the guided lab history and screenshots reviewed during the exercise. A subsequent live portal review on 14 October 2026 verified the configuration items noted below. See the [verification addendum](portal-verification.md).

| Check | Evidence status |
| --- | --- |
| VM region, operating system and size | Verified in live portal and earlier configuration screenshots |
| Backup precheck | Passed in live portal |
| Backup policy name and schedule | Daily at 22:00 UTC, verified live |
| Vault LRS | User confirmed the setting was saved |
| Final policy retention | Verified live: daily recovery points 30 days, instant snapshots 2 days |
| RDP limited to user's public IP | Verified live: priority 100, TCP 3389, one IPv4 /32 source; source ownership not independently checked |
| Last backup status | Success in live portal and supplied screenshot, 14 October 2026, 12:55:35 AM as displayed |
| Selected recovery point | Application consistent, 14 October 2026, 12:55:51 AM as displayed |
| Sample file deleted after backup | Confirmed during the guided exercise |
| File found and restored | User confirmed |
| Restored contents checked | User confirmed manual check; no hash comparison recorded |
| Recovery disks unmounted | User confirmed |
| Recovery duration/RTO | Not measured |
| Actual data loss interval/RPO | Not measured |
| Full VM or cross-region restore | Not tested |
| Resource cleanup | Pending verification |

The screenshot display timezone was not separately recorded. A daily backup schedule is not proof of a measured 24-hour RPO; recovery depends on the last usable recovery point.

## Public evidence handling

Raw screenshots contain private account or subscription information and are not included. This repository also excludes public IP values, passwords, recovery executables and session-specific recovery credentials.

The report and notes preserve the test sequence and known limitations without exposing those details.
