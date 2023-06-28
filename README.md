import pandas as pd
import os

# Tạo danh sách question_id từ 1 đến 19
question_ids = list(range(1, 19))
question_ids.remove(16)

# Tạo dictionary để lưu trữ answer cho mỗi question_id
answers_dict = {q_id: [] for q_id in question_ids}

textfile = ['file1.txt', 'file2.txt']  # Danh sách tên file văn bản

for file_path in textfile:
    file_name = os.path.basename(file_path)
    
    # Đọc dữ liệu từ file văn bản và chia cột bằng dấu "|"
    df = pd.read_csv(file_name, delimiter='|', names=['question_id', 'text', 'member_id'])
    
    # Lặp qua từng question_id
    for question_id in question_ids:
        # Lấy câu trả lời cho question_id hiện tại (nếu có)
        answers = df[df['question_id'] == question_id]['text'].tolist()

        # Xử lý unique() answer
        for answer in answers:
            # Tách các câu trả lời bằng dấu phẩy
            split_answers = answer.split(',')

            # Xóa ký tự '"' từ các câu trả lời và thêm vào danh sách answers_dict[question_id]
            answers_dict[question_id].extend([ans.strip().replace('"', '') for ans in split_answers])

# Tạo dataframe kết quả từ dictionary answers_dict
result_df = pd.DataFrame({'question_id': question_ids, 'answers': [';'.join(answers_dict[q_id]) for q_id in question_ids]})

# Lưu dataframe kết quả vào file CSV
result_df.to_csv('result.csv', index=False)
