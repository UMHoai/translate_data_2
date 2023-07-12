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

# Tạo DataFrame ban đầu
df = pd.DataFrame({
    'associable_member': [1, 2, 3],
    '1': ['high boold pressure; liver disease', 'high boold pressure; liver disease; high choresterol', 'liver disease'],
    '2': ['Tình hình tài chính 1', 'Tình hình tài chính 2', 'Tình hình tài chính 3'],
    '3': ['yes', 'no', 'no; yes'],
    '4': ['often; often', 'never', 'sometime; often'],
    '5': ['no', 'yes', 'no']
})

# Tạo các cột mới cho câu hỏi đa lựa chọn
multi_choice_columns = ['1', '3', '4', '5']

for column in multi_choice_columns:
    # Tách các đáp án bằng dấu chấm phẩy
    split_values = df[column].str.split(';')
    
    # Tạo danh sách tên cột mới dựa trên giá trị đáp án
    new_columns = []
    
    # Duyệt qua từng giá trị đáp án
    for row_values in split_values:
        for value in row_values:
            # Xóa khoảng trắng ở đầu và cuối giá trị
            value = value.strip()
            
            # Kiểm tra nếu giá trị đã có cột tương ứng
            if value in df.columns:
                # Gán giá trị vào cột tương ứng
                df[value] = value
            else:
                # Tạo cột mới và gán giá trị vào
                new_column = f'{column}_answer_{len(new_columns)+1}'
                df[new_column] = value
                new_columns.append(new_column)

# Xóa các cột cũ
df.drop(columns=multi_choice_columns, inplace=True)

print(df)
