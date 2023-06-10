import pandas as pd
import random

# Tạo DataFrame df_question_mapping
df_question_mapping = pd.DataFrame({
    'question_number': [1, 1, 2, 2, 2, 3, 3, 3, 4, 5],
    'answer': ['Answer 1', 'Answer 2', 'Answer 3', 'Answer 4', 'Answer 5',
               'Answer 6', 'Answer 7', 'Answer 8', 'Answer 9', 'Answer 10'],
    'label': ['Label 1', 'Label 2', 'Label 3', 'Label 4', 'Label 5',
              'Label 6', 'Label 7', 'Label 8', 'Label 9', 'Label 10']
})

# Tạo DataFrame df_classes
df_classes = pd.DataFrame({
    'class_name': ['Class 1', 'Class 2', 'Class 3', 'Class 4', 'Class 5'],
    'description': ['Description 1', 'Description 2', 'Description 3',
                    'Description 4', 'Description 5']
})

# Tạo empty DataFrame để lưu kết quả
df_result = pd.DataFrame()

# Lặp qua từng class trong df_classes
for index, class_row in df_classes.iterrows():
    class_name = class_row['class_name']
    description = class_row['description']
    
    # Lấy các dòng trong df_question_mapping có question_number từ 1 đến 5
    filtered_rows = df_question_mapping[df_question_mapping['question_number'].between(1, 5)]
    
    # Tạo một Series chứa câu trả lời ngẫu nhiên từ filtered_rows
    random_answers = filtered_rows.groupby('question_number')['answer'].apply(lambda x: random.choice(x))
    
    # Tạo một Series chứa label từ filtered_rows
    labels = filtered_rows.groupby('question_number')['label'].first()
    
    # Tạo DataFrame tạm thời từ các Series trên
    temp_df = pd.DataFrame({'description': [description],
                            'answer': random_answers.values,
                            'label': labels.values})
    
    # Tạo cột class_name trong DataFrame tạm thời
    temp_df['class_name'] = class_name
    
    # Nối DataFrame tạm thời vào df_result
    df_result = pd.concat([df_result, temp_df])

# In ra kết quả
print(df_result)
