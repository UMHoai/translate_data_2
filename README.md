import pandas as pd
import os

# Tạo danh sách question_id từ 1 đến 19
question_ids = list(range(1, 19))
question_ids.remove(16)

# Tạo dataframe mới để chứa kết quả
result_df = pd.DataFrame(columns=['question_id', 'unique_answers'])

textfile = ['file1.txt', 'file2.txt']  # Danh sách tên file văn bản

for file_path in textfile:
    file_name = os.path.basename(file_path)
    
    # Đọc dữ liệu từ file văn bản và chia cột bằng dấu "|"
    df = pd.read_csv(file_name, delimiter='|', names=['question_id', 'text', 'member_id'])
    
    # Lặp qua từng question_id
    for question_id in question_ids:
        # Lấy câu trả lời cho question_id hiện tại (nếu có)
        answers = df[df['question_id'] == question_id]['text'].tolist()

        # Kiểm tra nếu không có câu trả lời, đặt giá trị là "no-answers"
        if not answers:
            unique_answers = 'no-answers'
        else:
            # Tạo một tập hợp (set) để lưu các câu trả lời duy nhất
            unique_answers_set = set()

            # Xử lý unique() answer
            for answer in answers:
                # Tách các câu trả lời bằng dấu phẩy
                split_answers = answer.split(',')

                # Xóa ký tự '"' từ các câu trả lời và thêm vào tập hợp unique_answers_set
                unique_answers_set.update([ans.strip().replace('"', '') for ans in split_answers])

            # Nối các câu trả lời duy nhất lại thành một string bằng dấu phân cách ';'
            unique_answers = ';'.join(unique_answers_set)

        # Thêm dữ liệu của question_id vào dataframe kết quả
        result_df = result_df.append({'question_id': question_id, 'unique_answers': unique_answers}, ignore_index=True)

# Lưu dataframe kết quả vào file CSV
result_df.to_csv('result.csv', index=False)
