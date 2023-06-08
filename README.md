import csv
import random

# Đường dẫn đến file csv chứa câu hỏi và câu trả lời
csv_file = 'path_to_your_csv_file.csv'

# Đọc dữ liệu từ file csv
with open(csv_file, 'r') as file:
    reader = csv.DictReader(file, delimiter='|')
    questions = list(reader)

# Số lượng câu trả lời tối đa để chọn ngẫu nhiên
max_choices = 3

# Số lượng file txt cần tạo
num_files = 5

# Lặp qua số lượng file cần tạo
for i in range(1, num_files + 1):
    # Tạo tên file txt
    txt_file = f'output_file_{i}.txt'

    # Mở file txt để ghi dữ liệu
    with open(txt_file, 'w') as file:
        # Lặp qua danh sách câu hỏi
        for question in questions:
            question_id = question['question_id']
            question_text = question['text']

            # Ghi câu hỏi vào file
            file.write(f'{question_id}|{question_text}\n')

            # Chọn ngẫu nhiên số lượng câu trả lời từ 0 đến max_choices
            num_choices = random.randint(0, max_choices)

            # Lặp qua số lượng câu trả lời và ghi vào file
            for j in range(1, num_choices + 1):
                choice = f'Choice {j}'
                file.write(f'{question_id}|{choice}\n')
