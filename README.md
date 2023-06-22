import pandas as pd

# Tạo dataframe ban đầu
data = {
    'question_id': [2, 6, 8, 12, 13, 15, 19],
    'text': ['text1', 'text2', 'text3', 'text4', 'text5', 'text6', 'text7'],
    'priority': [1, 2, 3, 4, 5, 6, 7]
}
df = pd.DataFrame(data)

# Tạo danh sách question_id đã có trong dataframe ban đầu
existing_ids = df['question_id'].tolist()

# Tạo danh sách các question_id chưa có từ 1 đến 19
missing_ids = list(set(range(1, 20)) - set(existing_ids))

# Tạo dataframe mới chứa các question_id chưa có
missing_df = pd.DataFrame({
    'question_id': missing_ids,
    'text': 'no-answer',
    'priority': [10] * len(missing_ids)  # Mức độ ưu tiên mặc định là 10
})

# Ghép dataframe mới vào dataframe ban đầu
df = pd.concat([df, missing_df], ignore_index=True)

# Sắp xếp lại dataframe theo question_id
df = df.sort_values('question_id')

# In kết quả
print(df)
