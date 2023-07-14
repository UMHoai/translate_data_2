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

new_columns = ['member_id', 'NA', 'Negativity', 'Positivity']
new_df = pd.DataFrame(columns=new_columns)

# Tính toán giá trị 'NA', 'Negativity' và 'Positivity' cho mỗi member
for index, row in df.iterrows():
    member_id = row['member_id']
    na_count = row.isna().sum() - 1  # Trừ đi cột 'member_id'
    negativity = row[row < 0].sum()
    positivity = row[row > 0].sum()
    
    # Thêm hàng mới vào DataFrame mới
    new_row = pd.DataFrame([[member_id, na_count, negativity, positivity]], columns=new_columns)
    new_df = new_df.append(new_row, ignore_index=True)
