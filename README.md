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
df_result = pd.DataFrame(columns=['class_name', 'text', 'label'])

# Lặp qua từng class trong df_classes
for index, class_row in df_classes.iterrows():
    class_name = class_row['class_name']
    description = class_row['description']
    
    # Lấy các dòng trong df_question_mapping có question_number từ 1 đến 5
    filtered_rows = df_question_mapping[df_question_mapping['question_number'].between(1, 5)]
    
    # Tạo một đoạn text bằng cách nối description với tất cả các câu trả lời và label
    text = f"{description} "
    labels = []
    for question_number in range(1, 6):
        question_rows = filtered_rows[filtered_rows['question_number'] == question_number]
        random_answer = random.choice(question_rows['answer'])
        random_label = question_rows[question_rows['answer'] == random_answer]['label'].values[0]
        text += f"{random_answer} "
        labels.append(random_label)
    
    # Thêm đoạn text và label vào DataFrame kết quả
    temp_df = pd.DataFrame({'class_name': [class_name],
                            'text': [text],
                            'label': [', '.join(labels)]})
    df_result = df_result.append(temp_df, ignore_index=True)

# In ra kết quả
print(df_result)
