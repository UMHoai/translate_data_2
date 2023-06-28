import pandas as pd

df = pd.DataFrame({'associated_member': [1, 2, 3], 1: ['no-answer', 'yes', 'no'], 2: ['no-answer', 'yes', 'no'], 3: ['no-answer', 'yes', 'no']})

df_mapping = pd.DataFrame({'question_number': [1, 1, 2, 2, 2, 3], 'answer': ['no-answer', 'yes', 'no', 'never', 'ok', 'good'], 'label': ['aaa', 'bbb', 'ccc', 'ddd', 'fff', 'eeee']})

# Tạo một Series để chứa các đoạn text được map từ df_mapping
labels = []

# Duyệt qua từng dòng của DataFrame df
for index, row in df.iterrows():
    label = ''
    
    # Duyệt qua các cột từ cột thứ 2 trở đi
    for col in df.columns[1:]:
        answer = row[col]
        question_number = col
        
        # Tìm kiếm trong df_mapping dựa trên question_number và answer
        mapping = df_mapping[(df_mapping['question_number'] == question_number) & (df_mapping['answer'] == answer)]
        
        if not mapping.empty:
            # Nếu có mapping, thêm label vào đoạn text
            label += mapping['label'].values[0] + ' '
        else:
            # Nếu không có mapping, thêm "no-answer" vào đoạn text
            label += 'no-answers '
    
    # Gán đoạn text vào Series labels
    labels.append(label.strip())

# Thêm cột 'labels' vào DataFrame df
df['labels'] = labels

# Hiển thị DataFrame sau khi đã thêm cột 'labels'
print(df)
