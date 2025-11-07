**A. Project Overview**
    This project is a simple Bash script that automates the backup process for files and directories. It creates
    compressed archives, verifies integrity using checksums, and keeps only a set number of recent backups. The
    script helps users easily protect and manage their data without needing complex tools.


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


 _C. How It Works_
Backup Creation
1.	Compresses the source folder into a .tar.gz file.
2.	Names the backup with a timestamp: backup-YYYY-MM-DD-HHMM.tar.gz.
3.	Creates a checksum file (.md5) to verify integrity.
4.	Excludes folders defined in backup.config (e.g., .git, node_modules, .cache).




