How many members have psychological and life problems?
How many members have access to modern payment services today?

How many members have a degree of single, or isolated muscle illness that affects recovery?

How many members have physical limitations?

How many members feel lonely and isolated from everyone around when having physical problems?

How many members because of physical problems affecting financially?

How many members have illnesses when there are physical limitations?

How many members have physical limitations that lead to a lack of reliable transportation? (People with disabilities, ...)

How many members have a degree of belief in improving health?

How many members feel that the improvement in each level proves that the use of the service is effective?

How many members need the help of others to help them understand ... ? (can be people with education level, age, complexity of specialized terminology instructions)

https://tech.trivago.com/post/2019-09-23-howtoanalyzesurveymonkeydatainpython.html

import pandas as pd
import numpy as np

df = pd.DataFrame({
    'member_id': [111, 112, 113],
    '1': ['high blood pressure; liver disease', 'high blood pressure; liver disease; high cholesterol', 'no-answers'],
    '2': ['i have a steady place to live', 'no-answers', 'i have not a steady place to live'],
    '3': ['yes', 'no-answers', 'no'],
    '4': ['no-answers', 'never', 'sometime; often'],
    '5': ['no-answers', 'no', 'no-answers']
})

# Trường hợp 1: Single-choice
single_choice_columns = ['2', '3', '5']
no_answer_value = 'no-answers'

# Xử lý câu hỏi single-choice
for column in single_choice_columns:
    # Gán giá trị -1 cho câu trả lời được chọn
    df[column] = np.where(df[column] == no_answer_value, np.nan, -1)
    # Gán giá trị 0 cho câu trả lời không được chọn
    df[column].fillna(0, inplace=True)

# Trường hợp 2: Multi-choice
multi_choice_columns = ['1', '4']
unique_values = set()

# Tách các đáp án và tạo các cột mới
for column in multi_choice_columns:
    df[column] = df[column].str.split(';')
    unique_values.update(df[column].explode().unique())

# Xóa cột 'no-answers' khỏi danh sách giá trị duy nhất
unique_values.discard(no_answer_value)

# Tạo các cột unique
for value in unique_values:
    df[value] = 0

# Gán giá trị cho các cột mới
for index, row in df.iterrows():
    for column in multi_choice_columns:
        answers = row[column]
        if isinstance(answers, list):
            for answer in answers:
                if answer in unique_values:
                    df.at[index, answer] = -1

# Xóa các cột multi-choice gốc
df.drop(multi_choice_columns, axis=1, inplace=True)
__________________
import pandas as pd
import numpy as np

df = pd.DataFrame({
    'member_id': [111, 112, 113],
    '1': ['high blood pressure; liver disease', 'high blood pressure; liver disease; high cholesterol', 'no-answers'],
    '2': ['i have a steady place to live', 'no-answers', 'i have not a steady place to live'],
    '3': ['yes', 'no-answers', 'no'],
    '4': ['no-answers', 'never', 'sometime; often'],
    '5': ['no-answers', 'no', 'no-answers']
})

# Trường hợp 1: Single-choice
single_choice_columns = ['2', '3', '5']
no_answer_value = 'no-answers'

# Xử lý câu hỏi single-choice
for column in single_choice_columns:
    # Gán giá trị -1 cho câu trả lời được chọn
    df[column] = np.where(df[column] == no_answer_value, np.nan, -1)

# Trường hợp 2: Multi-choice
multi_choice_columns = ['1', '4']
unique_values = set()

# Tách các đáp án và tạo các cột mới
for column in multi_choice_columns:
    df[column] = df[column].str.split(';')
    unique_values.update(df[column].explode().unique())

# Xóa cột 'no-answers' khỏi danh sách giá trị duy nhất
unique_values.discard(no_answer_value)

# Tạo các cột mới với tên tùy chỉnh
new_columns = {}  # Tên cột mới
for value in unique_values:
    new_columns[value] = f"{value}_column"  # Tùy chỉnh tên cột mới ở đây

# Tạo các cột unique
for value, new_column_name in new_columns.items():
    df[new_column_name] = 0

# Gán giá trị cho các cột mới
for index, row in df.iterrows():
    for column in multi_choice_columns:
        answers = row[column]
        if isinstance(answers, list):
            for answer in answers:
                if answer in unique_values:
                    df.at[index, new_columns[answer]] = -1

# Xóa cột multi-choice gốc
df.drop(multi_choice_columns, axis=1, inplace=True)
df = df.applymap(lambda x: int(x) if pd.notnull(x) else x)


