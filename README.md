import pandas as pd

# Tạo dataframe mẫu
data = {
    'question_id': [1, 2, 3],
    'availabel_responses': [["abc", "bcd"], ["def", "efg"], ["hij", "ijk"]]
}
df = pd.DataFrame(data)

# Tạo dataframe mới để lưu từng available_response trên 1 row
new_data = []
for _, row in df.iterrows():
    question_id = row['question_id']
    available_responses = row['availabel_responses']
    for response in available_responses:
        new_data.append({'question_id': question_id, 'availabel_response': response})

new_df = pd.DataFrame(new_data)

# In kết quả
print(new_df)
