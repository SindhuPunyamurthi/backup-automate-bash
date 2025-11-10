**A. Project Overview**
    This project is a simple Bash script that automates the backup process for files and directories. It creates
    compressed archives, verifies integrity using checksums, and keeps only a set number of recent backups. The
    script helps users easily protect and manage their data without needing complex tools.

**Why is this Useful?**
It prevents data loss and also prevents the storage from being filled with old backups.


**B. How to Use It**
  * Protects your data from accidental loss  
  * Automates backup process  
  * Keeps backups organized and cleaned automatically

**B. How to Use It**
   **Installation**
1. Clone the repository:
```bash
git clone <your-repo-url>
cd backup-system

2. Make the script executable:
   chmod +x backup.sh

3.Edit backup.config if needed to set backup destination, exclusions, and retention.

**Basic Usage**
 * Backup a folder:
     ./backup.sh /path/to/source_folder

 * Dry run (simulate actions):
     ./backup.sh --dry-run /path/to/source_folder

  * List available backups: 
      ./backup.sh --list

 * Restore a backup:
     ./backup.sh --restore backups/backup-2025-11-07-1500.tar.gz --to /path/to/restore


 **C. How It Works**
Backup Creation
1.	Compresses the source folder into a .tar.gz file.
2.	Names the backup with a timestamp: backup-YYYY-MM-DD-HHMM.tar.gz.
3.	Creates a checksum file (.md5) to verify integrity.
4.	Excludes folders defined in backup.config (e.g., .git, node_modules, .cache).

**Backup Rotation**
•	Keeps the last 7 daily backups, last 4 weekly backups, and last 3 monthly backups.
•	Deletes older backups automatically to save disk space

Verification
•	Checks the backup checksum.
•	Extracts a test file to ensure backup is not corrupted.
•	Prints SUCCESS if verified, FAILED otherwise.


**backup-system/**
├── backup.sh
├── backup.config
├── backups/        # Stores backup archives
└── logs/           # Stores backup.log

**D. Design Decisions**
•	Lock file prevents multiple runs at the same time.
•	Configuration file allows easy customization without modifying the script.
•	Dry run mode enables safe testing.
•	Logging records all actions and errors in logs/backup.log.
Challenges faced:
•	Handling simultaneous script execution → solved using lock file.
•	Deleting old backups correctly → solved using sorted find and retention policy.

E. Testing
•	Created backups for a test folder.
•	Verified checksum and extraction.
•	Simulated multiple backups to test automatic deletion.
•	Tested dry run mode.
•	Tested restoring backups to a separate folder.
•	Tested error handling for non-existing source folder

**Example outputs:**
   [2025-11-07 15:00:01] INFO: Starting backup of /home/user/test_folder
[2025-11-07 15:00:05] SUCCESS: Backup created: backup-2025-11-07-1500.tar.gz
[2025-11-07 15:00:06] INFO: Checksum verified successfully
[2025-11-07 15:00:10] INFO: Deleted old backup: backup-2025-10-01-1400.tar.gz


F. Known Limitations
•	Incremental backups (only changed files) not yet implemented.
•	Email notifications are optional and not fully implemented.
•	Large backups may take longer depending on disk speed.
•	Currently only supports local backup destinations.



**Conclusion**
This project demonstrates a reliable and automated backup system using simple Bash scripting. It ensures
data safety through compression, checksum verification, and rotation logic — all in a lightweight, easy-to-
use design.







