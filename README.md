import os
import shutil
import zipfile

def backup_csv_files(folder_path, backup_folder, zip_filename):
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
    
    # Zip the backup folder
    zip_path = os.path.join(folder_path, zip_filename)
    with zipfile.ZipFile(zip_path, 'w') as zip_file:
        for root, dirs, files in os.walk(backup_folder):
            for file in files:
                file_path = os.path.join(root, file)
                # Add each file to the zip archive
                zip_file.write(file_path, arcname=os.path.relpath(file_path, backup_folder))
    
    print(f"Zipped files to: {zip_path}")

# Specify the folder path, backup folder, and zip filename
folder_path = 'path/to/folder'
backup_folder = 'path/to/backup/folder'
zip_filename = 'backup.zip'

# Call the backup_csv_files function
backup_csv_files(folder_path, backup_folder, zip_filename)
