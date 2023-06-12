import random
import os

# Đường dẫn thư mục để lưu các file txt
directory = "data_directory"

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

# Tạo thư mục để lưu các file txt
os.makedirs(directory, exist_ok=True)

# Tạo các file txt cho mỗi associate_member_id
for associate_member_id in range(1, 3):
    file_name = f"{directory}/data_{associate_member_id}.txt"

    with open(file_name, 'w') as file:
        for index, class_row in tqdm(df_classes.iterrows()):
            class_name, class_description, assessment_text = generate_assessment_text(class_row, df_question_mapping, start_question_random)

            for _ in range(number_of_records):
                file.write(f"associate_member_id: {associate_member_id}\n")
                file.write(f"class: {class_name}\n")
                file.write(f"description: {class_description}\n")
                file.write(f"assessment_text: {assessment_text}\n\n")
