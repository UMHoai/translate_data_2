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

# Tạo DataFrame ban đầu
df = pd.DataFrame({
    'associable_member': [1, 2, 3],
    '1': ['high boold pressure; liver disease', 'high boold pressure; liver disease; high choresterol', 'no-answers'],
    '2': ['Tình hình tài chính 1', 'Tình hình tài chính 2', 'Tình hình tài chính 3'],
    '3': ['yes', 'no', 'no; yes'],
    '4': ['often; often', 'never', 'sometime; often'],
    '5': ['no', 'yes', 'no-answers']
})

# Tạo từ điển để theo dõi các cột đã được tạo
created_columns = {}

# Tạo các cột mới cho câu hỏi đa lựa chọn
multi_choice_columns = ['1', '3', '4', '5']

for column in multi_choice_columns:
    # Tách các đáp án bằng dấu chấm phẩy
    split_values = df[column].str.split(';')
    
    # Duyệt qua từng giá trị đáp án
    for row_idx, row_values in enumerate(split_values):
        for value in row_values:
            # Xóa khoảng trắng ở đầu và cuối giá trị
            value = value.strip()
            
            # Kiểm tra nếu giá trị là "no-answers"
            if value == 'no-answers':
                # Kiểm tra nếu câu hỏi đã được tạo cột mới
                if column in created_columns:
                    # Lấy tên cột tương ứng
                    new_column = created_columns[column]
                    
                    # Gán giá trị là 0 cho cột tương ứng
                    df.loc[row_idx, new_column] = 0
                break  # Thoát khỏi vòng lặp nếu giá trị là "no-answers"
            
            # Kiểm tra nếu giá trị đã có cột tương ứng
            if value in created_columns:
                # Lấy tên cột tương ứng
                new_column = created_columns[value]
                
                # Gán giá trị vào cột tương ứng
                df.loc[row_idx, new_column] = value
            else:
                # Tạo cột mới và gán giá trị vào
                new_column = f'{column}_answer_{len(created_columns)+1}'
                df[new_column] = np.nan
                df.loc[row_idx, new_column] = value
                
                # Cập nhật từ điển với tên cột mới
                created_columns[value] = new_column

# Xóa các cột cũ
df.drop(columns=multi_choice_columns, inplace=True)

print(df)

---------------
import pandas as pd

# Tạo DataFrame ban đầu
df = pd.DataFrame({
    'member_id': [111, 112, 113],
    '1': ['high blood pressure; liver disease', 'high blood pressure; liver disease; high cholesterol', 'no-answers'],
    '2': ['i have a steady place to live', '', 'i have not a steady place to live'],
    '3': ['yes', 'no-answers', 'no'],
    '4': ['no-answers', 'never', 'sometimes; often'],
    '5': ['no-answers', 'no', 'no-answers']
})

# Trường hợp 1: Xử lý câu hỏi single-choice
single_choice_columns = ['2', '3', '5']
no_answer_value = 'no-answers'

for column in single_choice_columns:
    df[column] = df[column].apply(lambda x: -1 if x and x != no_answer_value else 0)
    df[column] = df[column].replace({0: pd.NA})

# Trường hợp 2: Xử lý câu hỏi multi-choice
multi_choice_columns = ['1', '4']

for column in multi_choice_columns:
    unique_values = set(';'.join(df[column].dropna()).split(';'))
    unique_values.discard(no_answer_value)

    for value in unique_values:
        new_column = f"{column}_{value}"
        df[new_column] = df[column].apply(lambda x: -1 if x and value in x else 0)
        df[new_column] = df[new_column].replace({0: pd.NA})

    df.drop(column, axis=1, inplace=True)

print(df)



