import csv
import random

# Đường dẫn và tên file CSV
csv_file = "data.csv"

# Tên các cột trong file CSV
column_names = ['class', 'description', 'assessment_text']

# Số lượng bản ghi muốn tạo
number_of_records = 100

# Câu hỏi bắt đầu cho việc chọn ngẫu nhiên
start_question_random = 7

# Dataframe chứa các lớp và mô tả của chúng
df_classes = ...

# Dataframe chứa ánh xạ giữa câu hỏi và câu trả lời
df_question_mapping = ...

# Hàm tạo ngẫu nhiên các câu hỏi dựa trên lớp và ánh xạ câu hỏi
def generate_assessment_text(class_row, filtered_rows, start_question_random):
    class_name = class_row['class']
    class_description = class_row['description']
    
    valid_question_numbers = [number for number in range(start_question_random, 20)]
    text = f"{class_description} "

    for question_number in range(start_question_random, 20):
        if question_number == 16 or question_number == 17:
            continue
        question_rows = filtered_rows[filtered_rows['question_number'] == question_number]
        answers = question_rows['answer'].tolist()
        labels = question_rows['label'].tolist()
        random_answer = random.choice(answers)
        random_label = labels[answers.index(random_answer)]
        text += f"{random_label} "

    return class_name, class_description, text

# Tạo các file txt
with open(csv_file, 'w', newline='') as file:
    writer = csv.DictWriter(file, fieldnames=column_names)
    writer.writeheader()

    for index, class_row in tqdm(df_classes.iterrows()):
        class_name, class_description, assessment_text = generate_assessment_text(class_row, df_question_mapping, start_question_random)

        for _ in range(number_of_records):
            writer.writerow({
                'class': class_name,
                'description': class_description,
                'assessment_text': assessment_text
            })
