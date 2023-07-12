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


import pandas as pd

# Tạo DataFrame ví dụ
data = {
    'associable_member': ['A', 'B', 'C'],
    '1': ['answer1', 'answer2;answer3', ''],
    '2': ['answer4;answer5', '', 'answer6'],
    '3': ['', 'answer7', 'answer8'],
    '4': ['answer9', '', 'answer10'],
    '5': ['', '', '']
}

df = pd.DataFrame(data)

# Tách câu trả lời trong DataFrame
for column in df.columns[1:]:
    df[column] = df[column].str.split(';')

# Chuyển đổi các cột thành các cột mới
new_columns = []
for column in df.columns[1:]:
    new_columns.extend(df[column].explode().unique())

df = df.reindex(columns=['associable_member'] + new_columns)

# Đặt các câu không có câu trả lời thành NaN
df = df.replace('', pd.NA)

print(df)
