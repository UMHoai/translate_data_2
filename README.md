# Sắp xếp dataframe theo độ ưu tiên giảm dần
question_mapping.sort_values(by='priority', ascending=False, inplace=True)

# Nối các câu trả lời theo độ ưu tiên và question number
joined_answers = question_mapping.groupby('question_number')['answer'].apply(' '.join).reset_index()
