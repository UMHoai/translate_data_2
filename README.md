import pandas as pd

# Tạo dataframe từ dữ liệu có sẵn
df = pd.DataFrame({
    'question_id': [4, 2, 2, 3, 3, 8, 8, 8, 6],
    'text': ['a', 'yes', 'no', 'a', 'b', 'sometime', 'often', 'usually', 'ok'],
    'member_id': [1, 1, 1, 1, 1, 2, 2, 2, 2]
})

# Tạo danh sách question_id từ 1 đến 10
question_ids = list(range(1, 11))

# Tạo dataframe mới để chứa kết quả
result_df = pd.DataFrame(columns=['member_id'] + question_ids)

# Lặp qua từng member_id trong dataframe gốc
for member_id in df['member_id'].unique():
    # Lọc dữ liệu theo member_id
    member_data = df[df['member_id'] == member_id]
    
    # Khởi tạo dictionary chứa câu trả lời của member
    member_answers = {'member_id': member_id}
    
    # Lặp qua từng question_id
    for question_id in question_ids:
        # Lấy câu trả lời cho question_id hiện tại (nếu có)
        answers = member_data[member_data['question_id'] == question_id]['text'].tolist()
        
        # Kiểm tra nếu không có câu trả lời, đặt giá trị là "no-answers"
        if not answers:
            member_answers[question_id] = 'no-answers'
        else:
            # Nối các câu trả lời lại thành một string bằng dấu phân cách ';'
            member_answers[question_id] = ';'.join(answers)
    
    # Thêm dữ liệu của member vào dataframe kết quả
    result_df = result_df.append(member_answers, ignore_index=True)

# Lưu dataframe kết quả vào file CSV
result_df.to_csv('result.csv', index=False)
