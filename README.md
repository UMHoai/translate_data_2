import pandas as pd
import random

# Tạo DataFrame df_question_mapping
df_question_mapping = pd.DataFrame({
    'question_number': [1, 2, 2, 3, 3, 3, 4, 4, 4],  # Số dòng ví dụ
    'answer': ['Answer1', 'Answer2', 'Answer3', 'Answer4', 'Answer5', 'Answer6', 'Answer7', 'Answer8', 'Answer9'],  # Câu trả lời ví dụ
    'label': ['Label1', 'Label2', 'Label3', 'Label4', 'Label5', 'Label6', 'Label7', 'Label8', 'Label9']  # Label ví dụ
})

# Tạo DataFrame df_classes
df_classes = pd.DataFrame({
    'class_name': ['Class1', 'Class2', 'Class3', 'Class4', 'Class5'],  # Tên lớp
    'description': ['Description1', 'Description2', 'Description3', 'Description4', 'Description5']  # Mô tả lớp
})

# Tạo DataFrame mới để lưu tập dữ liệu
df_data = pd.DataFrame(columns=['class_name', 'description', 'answer', 'label'])

# Số question_number tối đa
max_question_number = 17

# Duyệt qua từng lớp
for _, class_row in df_classes.iterrows():
    class_name = class_row['class_name']
    description = class_row['description']
    
    # Duyệt qua các question_number từ 1 đến max_question_number
    for question_number in range(1, max_question_number + 1):
        # Lọc các câu trả lời và nhãn tương ứng với question_number
        filtered_rows = df_question_mapping[df_question_mapping['question_number'] == question_number]
        
        # Lấy ngẫu nhiên một câu trả lời và nhãn từ filtered_rows
        random_row = random.choice(filtered_rows.index)
        answer = df_question_mapping.loc[random_row, 'answer']
        label = df_question_mapping.loc[random_row, 'label']
        
        # Thêm dòng mới vào df_data
        df_data = df_data.append({'class_name': class_name, 'description': description, 'answer': answer, 'label': label}, ignore_index=True)

# In ra tập dữ liệu đã tạo
print(df_data)
