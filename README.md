from azure.storage.blob import BlobServiceClient

def get_blob_data():
    # Thay đổi các giá trị dưới đây theo thông tin của bạn
    connection_string = 'DefaultEndpointsProtocol=https;AccountName=your_account_name;AccountKey=your_account_key'
    container_name = 'your_container_name'
    blob_name = 'your_blob_name.txt'

    # Kết nối đến Blob Storage
    blob_service_client = BlobServiceClient.from_connection_string(connection_string)
    container_client = blob_service_client.get_container_client(container_name)

    # Kiểm tra xem blob có tồn tại hay không
    blob_client = container_client.get_blob_client(blob_name)
    if blob_client.exists():
        # Tải dữ liệu từ blob
        blob_data = blob_client.download_blob().readall()
        return blob_data
    else:
        print(f"Blob '{blob_name}' không tồn tại trong container '{container_name}'.")

# Sử dụng ví dụ hàm để lấy dữ liệu từ Blob Storage
blob_data = get_blob_data()

# In ra dữ liệu
print(blob_data.decode())
