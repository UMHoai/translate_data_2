import pandas as pd

# Tạo dataframe df_class_config
class_config_data = {'question_number': [1, 1, 2, 2, 3, 3, 4, 4, 5, 5],
                     'answer': ['a', 'b', 'c', 'd', 'e', 'f', 'g', 'h', 'i', 'j'],
                     'label': ['Label1', 'Label2', 'Label3', 'Label4', 'Label5', 'Label6', 'Label7', 'Label8', 'Label9', 'Label10'],
                     'priority': [1, 1, 2, 2, 3, 3, 4, 4, 5, 5]}
df_class_config = pd.DataFrame(class_config_data)

# Tạo dataframe df_member_answer
member_answer_data = {'member_id': ['Member1', 'Member1', 'Member2', 'Member2', 'Member3', 'Member3'],
                      'question_id': [1, 2, 3, 4, 5, 1],
                      'answer': ['a', 'd', 'e', 'h', 'i', 'b']}
df_member_answer = pd.DataFrame(member_answer_data)

# Gộp thông tin với df_member_answer
merged_data = pd.merge(df_member_answer, df_class_config, left_on=['question_id', 'answer'], right_on=['question_number', 'answer'], how='left')

# Sắp xếp theo mức độ ưu tiên giảm dần
merged_data.sort_values(by='priority', ascending=False, inplace=True)

# Tạo đoạn text theo từng member_id
grouped_data = merged_data.groupby('member_id')['label'].apply(lambda x: ' '.join(x)).reset_index()

# In ra kết quả
print(grouped_data)
