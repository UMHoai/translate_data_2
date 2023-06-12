# Tạo danh sách các tên cột mới
new_columns = ['col' + str(i) for i in range(2, 9)]

# Thêm các cột mới vào DataFrame
for column in new_columns:
    df[column] = None
