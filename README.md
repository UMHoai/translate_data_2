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


# Tạo dataframe mới với cột câu trả lời là cột mới
new_df = pd.DataFrame()

# Tạo một từ điển để lưu trữ cột câu trả lời
answer_columns = {}

# Lặp qua từng cột câu hỏi trong dataframe gốc
for column in df.columns:
    # Kiểm tra nếu cột là cột "associable_member"
    if column == 'associable_member':
        new_df[column] = df[column]
    else:
        # Tách các câu trả lời thành danh sách
        answers = df[column].str.split(';')
        
        # Lặp qua từng câu trả lời
        for i, answer in enumerate(answers):
            for ans in answer:
                # Kiểm tra nếu câu trả lời đã xuất hiện trước đó
                if ans.strip() in answer_columns:
                    # Lấy tên cột đã tồn tại cho câu trả lời
                    new_column = answer_columns[ans.strip()]
                else:
                    # Tạo tên cột mới cho câu trả lời
                    new_column = f'{column}_Answer_{len(answer_columns)+1}'
                    # Lưu trữ tên cột cho câu trả lời trong từ điển
                    answer_columns[ans.strip()] = new_column
                
                new_df.loc[i, new_column] = ans.strip()

# In dataframe mới
print(new_df)

