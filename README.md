import os
import shutil
import zipfile

def backup_csv_files(folder_path, zip_filename):
    # Create a temporary folder for storing the CSV files
    temp_folder = os.path.join(folder_path, '__temp')
    os.makedirs(temp_folder, exist_ok=True)
    
    # Iterate over all files and subdirectories in the folder
    for root, dirs, files in os.walk(folder_path):
        for file in files:
            # Check if the file is a CSV file
            if file.endswith('.csv'):
                file_path = os.path.join(root, file)
                # Copy the file to the temporary folder
                shutil.copy(file_path, temp_folder)
                print(f"Backed up: {file_path}")
    
    # Zip the temporary folder
    zip_path = os.path.join(folder_path, zip_filename)
    with zipfile.ZipFile(zip_path, 'w') as zip_file:
        for root, dirs, files in os.walk(temp_folder):
            for file in files:
                file_path = os.path.join(root, file)
                # Add each file to the zip archive
                zip_file.write(file_path, arcname=os.path.relpath(file_path, temp_folder))
    
    # Remove the temporary folder
    shutil.rmtree(temp_folder)
    
    print(f"Zipped files to: {zip_path}")

# Specify the folder path and zip filename
folder_path = 'path/to/folder'
zip_filename = 'backup.zip'

# Call the backup_csv_files function
backup_csv_files(folder_path, zip_filename)
