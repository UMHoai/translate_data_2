import os
import shutil

def backup_csv_files(folder_path, backup_folder):
    # Create the backup folder if it doesn't exist
    if not os.path.exists(backup_folder):
        os.makedirs(backup_folder)
    
    # Iterate over all files and subdirectories in the folder
    for root, dirs, files in os.walk(folder_path):
        for file in files:
            # Check if the file is a CSV file
            if file.endswith('.csv'):
                file_path = os.path.join(root, file)
                # Copy the file to the backup folder
                shutil.copy(file_path, backup_folder)
                print(f"Backed up: {file_path}")

# Specify the folder path and backup folder
folder_path = 'path/to/folder'
backup_folder = 'path/to/backup/folder'

# Call the backup_csv_files function
backup_csv_files(folder_path, backup_folder)
