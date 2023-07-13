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


result_df = pd.DataFrame()
result_df['member_id'] = df['member_id']
result_df['NA'] = df.isna().sum(axis=1)
result_df['Negativity'] = df.select_dtypes(include=[np.number]).apply(lambda row: row[row < 0].sum(), axis=1)
result_df['Positivity'] = df.select_dtypes(include=[np.number]).drop('member_id', axis=1).apply(lambda row: row[row > 0].sum(), axis=1)
