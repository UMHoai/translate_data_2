import pandas as pd

# Tạo dataframe question_mapping
data = {'question_number': [1, 1, 2, 2, 3, 3, 4, 4, 5, 5],
        'answer': ['a', 'b', 'c', 'd', 'e', 'f', 'g', 'h', 'i', 'j']}
question_mapping = pd.DataFrame(data)

# Xác định độ ưu tiên cho từng câu hỏi
priority_mapping = {5: 1, 3: 2}  # Thiết lập độ ưu tiên cho câu 5 và câu 3

# Tính độ ưu tiên cho các câu hỏi còn lại
default_priority = 3  # Độ ưu tiên mặc định cho các câu hỏi không được chỉ định
question_mapping['priority'] = question_mapping['question_number'].apply(
    lambda x: priority_mapping.get(x, default_priority))

# In ra dataframe đã thêm cột độ ưu tiên
print(question_mapping)
