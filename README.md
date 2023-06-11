from azure.storage.blob import BlobServiceClient
import pandas as pd

STORAGEACCOUNTURL = "<storage_account_url>"
STORAGEACCOUNTKEY = "<storage_account_key>"
CONTAINERNAME = "<container_name>"
OUTPUT_FOLDER = "<output_folder>"

# Kết nối đến Blob Storage
blob_service_client_instance = BlobServiceClient(account_url=STORAGEACCOUNTURL, credential=STORAGEACCOUNTKEY)
container_client = blob_service_client_instance.get_container_client(CONTAINERNAME)

# Lấy danh sách các blob trong container
blobs = container_client.list_blobs()

# Lấy dữ liệu từ blob và lưu vào các file .txt
for blob in blobs:
    # Lấy tên của blob
    blob_name = blob.name
    
    # Kiểm tra nếu blob là file .txt
    if blob_name.endswith(".txt"):
        # Tạo đường dẫn đầy đủ cho file đích
        output_file_path = os.path.join(OUTPUT_FOLDER, blob_name)
        
        # Tải dữ liệu từ blob và xử lý
        blob_client_instance = blob_service_client_instance.get_blob_client(CONTAINERNAME, blob_name, snapshot=None)
        blob_data = blob_client_instance.download_blob()
        data = blob_data.content_as_text()
        
        # Xử lý dữ liệu và lưu vào file đích
        # Chỉ định các trường cần thiết trong mỗi file ở đây
        # Ví dụ: Lấy cột "name" và "age" từ dữ liệu và lưu vào file đích
        df = pd.DataFrame([x.split(",") for x in data.split("\n")], columns=["name", "age"])
        df.to_csv(output_file_path, sep="\t", index=False)  # Lưu dữ liệu vào file .txt

        print(f"Đã lưu blob {blob_name} thành công!")
