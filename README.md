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

# Số members trả lời đầy đủ (có đầy đủ 5 câu trả lời)
full_responses_count = df[df.notna().all(axis=1)].shape[0]

# Số member trả lời 5, 4, 3, 2, 1 câu hỏi
answers_counts = df.notna().sum(axis=1).value_counts().sort_index()

# Min negativity, Max negativity
min_negativity = df[single_choice_columns + new_columns].sum(axis=1).min()
max_negativity = df[single_choice_columns + new_columns].sum(axis=1).max()

# Min positivity, Max positivity
min_positivity = df[single_choice_columns + new_columns].sum(axis=1).where(df[single_choice_columns + new_columns] > 0).min()
max_positivity = df[single_choice_columns + new_columns].sum(axis=1).where(df[single_choice_columns + new_columns] > 0).max()

# Thống kê số member theo từng điểm negativity
negativity_counts = df[single_choice_columns + new_columns].sum(axis=1).value_counts().sort_index()

# Hiển thị kết quả
print("Số members trả lời đầy đủ:", full_responses_count)
print("Số member trả lời 5, 4, 3, 2, 1 câu hỏi:")
print(answers_counts)
print("Min negativity:", min_negativity)
print("Max negativity:", max_negativity)
print("Min positivity:", min_positivity)
print("Max positivity:", max_positivity)
print("Thống kê số member theo từng điểm negativity:")
print(negativity_counts)
