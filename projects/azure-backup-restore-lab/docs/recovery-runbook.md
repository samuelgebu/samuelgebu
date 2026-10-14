# Recovery runbook: lab sample file

This records the procedure used in the lab. Portal labels and recovery requirements may change; check the current prompts when repeating the exercise.

## Before deleting test data

1. Use a fictional, disposable sample file and record its original location and contents.
2. Confirm the VM has a successful backup containing that file.
3. Record the recovery point and verify that it predates the planned deletion.
4. Delete only the disposable sample file.

## Restore the file

1. Open the protected VM's backup view and choose File Recovery.
2. Select the recovery point that contains the sample file.
3. Download the Azure-generated recovery executable and obtain its password through the portal. Keep both out of source control.
4. Transfer the executable to the recovery machine. In this exercise, Remote Desktop drive redirection was used after clipboard transfer failed.
5. Run it as administrator and follow Azure's prompts to mount the recovery volumes.
6. Find the sample folder on the mounted backup volume. Its drive letter may differ from the original.
7. Copy `BusinessRecords.txt` to `C:\BackupLab` on the VM.
8. Open the restored file and check the sample contents. For a future test, compare a previously recorded hash as well.
9. Close files on the recovery volumes and use Unmount Disks in File Recovery.
10. Record the result and remove transient recovery downloads when no longer needed.

## Recorded outcome

The user confirmed that the file was found, restored and checked, and that the temporary disks were unmounted. No timed recovery measurement or hash comparison was recorded.
