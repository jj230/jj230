# Overview

The below script is written so that a user can enter a specific directory or folder and have it be backupped to the Home Directory. There are error checks in place to ensure the file does exist and it does get backed up correctly. There are also considerations for security by using quotes, validating input, checking for existence of the file, ensuring the user has permissions for the file (through use of tar command, and exiting on errors). 

The foundation of this script was created through the SOC-100 Course by Level Effect. They created the foundation of just backing up the home directory. I added in the user input option to specify a specific directory or file, the error checks, the additional quotes and set-euo pipefail for security.

# Bash Script

```
#!/bin/bash
set -euo pipefail

echo "The backupper is running!"
echo "..."

read -rp "Enter the path to the directory or file you want to compress: " TARGET_PATH
TARGET_PATH="${TARGET_PATH/#\~/$HOME}"

echo "DEBUG: Expanded path is: '$TARGET_PATH'"

# Check if it exists
if [[ ! -e "$TARGET_PATH" ]]; then
  echo "Error: '$TARGET_PATH' does not exist."
  exit 1
fi

BASENAME="$(basename "$TARGET_PATH")"
echo "Backing up $BASENAME"
COMPRESSEDFILENAME="Backup_${BASENAME}_$(date +%A_%b_%Y_%H_%M_%S)"
tar -zcf  "$HOME/$COMPRESSEDFILENAME.tgz" "$TARGET_PATH" 2>/dev/null

if [[ $? -eq 0 ]]; then
  echo "Backup complete!"
  echo "Archive created at: $HOME/$COMPRESSEDFILENAME.tgz"
else
  echo "Backup failed. Please check the path and try again."
fi
```
