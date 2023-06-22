import pandas as pd

# Tạo dataframe question_mapping
data = {'question_number': [1, 1, 2, 2, 3, 3, 4, 4, 5, 5],
        'answer': ['a', 'b', 'c', 'd', 'e', 'f', 'g', 'h', 'i', 'j']}
question_mapping = pd.DataFrame(data)

# Tính độ ưu tiên cho mỗi câu hỏi
priority_mapping = {}
for question_num in question_mapping['question_number'].unique():
    priority_mapping[question_num] = question_mapping[question_mapping['question_number'] == question_num].index.min()

# Sắp xếp độ ưu tiên theo thứ tự tăng dần
sorted_priority = sorted(priority_mapping.values())

# Xác định độ ưu tiên cho từng câu hỏi
question_mapping['priority'] = [sorted_priority.index(priority_mapping[question_num]) + 1
                                for question_num in question_mapping['question_number']]

# In ra dataframe đã thêm cột độ ưu tiên
print(question_mapping)
