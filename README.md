# Tạo DataFrame mới để chứa dữ liệu tạo ra
df_generated_data = pd.DataFrame(columns=['class_name', 'description', 'question_number', 'answer', 'label'])

# Generate dữ liệu cho từng class
for _, class_row in df_classes.iterrows():
    class_name = class_row['class_name']
    description = class_row['description']
    
    # Lấy các câu trả lời tương ứng với class từ df_question_mapping
    matching_answers = df_question_mapping[df_question_mapping['label'] == class_name]['answer']
    
    # Lấy ngẫu nhiên một số câu trả lời
    random_answers = random.sample(list(matching_answers), random.randint(1, 17))
    
    # Tạo DataFrame mới chứa dữ liệu cho class hiện tại
    df_class_data = pd.DataFrame({
        'class_name': [class_name] * len(random_answers),
        'description': [description] * len(random_answers),
        'question_number': df_question_mapping['question_number'],
        'answer': random_answers,
        'label': [class_name] * len(random_answers)
    })
    
    # Gộp DataFrame mới vào df_generated_data
    df_generated_data = pd.concat([df_generated_data, df_class_data], ignore_index=True)

# Hiển thị kết quả
print(df_generated_data)
