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

# Tạo DataFrame
df = pd.DataFrame({
    'associable_member': [1, 2, 3],
    '1': ['high blood pressure; liver disease', 'high blood pressure; liver disease; high cholesterol', 'liver disease', 'high blood pressure; high cholesterol'],
    '2': ['Tình hình tài chính 1', 'Tình hình tài chính 2', 'Tình hình tài chính 3'],
    '3': ['yes', 'no', 'no; yes'],
    '4': ['often; often', 'never', 'sometime; often'],
    '5': ['no', 'yes', 'no']
})

# Tách các câu trả lời đa lựa chọn thành các cột riêng biệt
new_columns = []
for column in df.columns:
    if column != 'associable_member':
        new_column_values = df[column].str.split('; ').explode().reset_index(drop=True)
        new_columns.extend([f"{column}_{i+1}" for i in range(len(new_column_values))])
        df = pd.concat([df, pd.Series(new_column_values, name=f"{column}_{i+1}")], axis=1)

# Xóa các cột cũ
df = df.drop(columns=df.columns[1:-1])

print(df)

