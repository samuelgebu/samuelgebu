# Troubleshooting notes

## Public IP quota

The VM setup reported no remaining quota for a new public IP. An existing unassociated Standard public IP in South Africa North was reused. Its numeric address is omitted here.

**Lesson:** Check regional quota and existing resources before deployment. Track shared or reused resources so that cleaning up one lab does not disrupt another.

## Failed duplicate backup requests

Several manual requests appeared as Failed while an earlier job remained In progress. The details showed:

`UserErrorBackupOperationInProgress`

The message indicated that another backup operation was running. The rejected request finished in approximately one second with no backup data transferred.

I stopped issuing new requests and allowed the existing operation to complete. A later VM Backup screen showed Success.

**Lesson:** Read the individual job error and check active jobs before retrying. A rejected duplicate request does not establish that the original running backup failed.

## Remote Desktop clipboard

Clipboard copy and paste did not reliably transfer the recovery executable. I enabled local drive redirection and accessed the local computer's redirected drive from the VM to copy the executable.

**Lesson:** File transfer and clipboard text transfer are different capabilities. Drive redirection provided a workable transfer route for this exercise.

## Finding the backed-up file

After mounting the selected recovery point, I located the `BackupLab` folder on the mounted recovery volume. I copied `BusinessRecords.txt` back to `C:\BackupLab`, opened it, and checked its contents. I then unmounted the recovery disks through Azure File Recovery.

**Lesson:** Recovery volumes can use different drive letters. Identify the correct folder and recovery point before copying files.

## Improvements for another test

- Capture redacted evidence of the final NSG rule, saved policy, restored file and unmount confirmation.
- Record recovery start and completion times.
- Calculate a hash before deletion and compare it after restoration.
- Test a full VM restore as a separate exercise.
