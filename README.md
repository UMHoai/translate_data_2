# Tạo dataframe kết quả từ dictionary answers_dict
result_df = pd.DataFrame({'question_id': question_ids, 'answers': [';'.join(answers_dict[q_id]) for q_id in question_ids]})

# Lưu dataframe kết quả vào file CSV
