import tarfile

# Đường dẫn đến tệp tar
tar_file_path = "path/to/your/file.tar"

# Tạo một đối tượng tarfile
tar = tarfile.open(tar_file_path)

# Giải nén tất cả các tệp trong tệp tar
tar.extractall()

# Đóng tệp tar
tar.close()
