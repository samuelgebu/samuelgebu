I finally got my deleted file back.

That was the goal of my fifth Azure project: build a Windows Server lab, back it up, delete a sample business file, and see whether I could recover it.

I built the lab in South Africa North and used Azure Backup with a Recovery Services vault.

The setup took more patience than I expected. I hit a public IP quota limit. Then several backup requests showed Failed, and I kept trying again. Reading the job details helped: another backup was already running. I needed to let it finish instead of submitting more requests.

Even after the backup succeeded, copy and paste in Remote Desktop gave me trouble. I eventually used drive redirection to move the recovery executable onto the VM.

Once the recovery volumes were mounted, I found BusinessRecords.txt, copied it back to its original folder, and opened it to check the contents. Then I unmounted the recovery disks.

It was a small text file with fictional data, but seeing it restored made the exercise worthwhile. Enabling backup was only part of the job. I also needed to work through the recovery process.

This was a file recovery lab, and I still have more to practise, including a full VM restore and measuring recovery time. For now, I've documented what worked, what went wrong, and what I would improve next time.

Project notes: https://github.com/samuelgebu/samuelgebu/tree/main/projects/azure-backup-restore-lab

#Azure #AzureBackup #WindowsServer #CloudComputing #SystemAdministration #LearningInPublic
