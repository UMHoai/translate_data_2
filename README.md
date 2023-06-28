for question_id in question_ids:
        # Lấy câu trả lời cho question_id hiện tại (nếu có)
        answers = df[df['question_id'] == question_id]['text'].tolist()

        # Xử lý unique() answer
        for answer in answers:
            # Tách các câu trả lời bằng dấu phẩy
            split_answers = answer.split(',')

            # Xóa ký tự '"' từ các câu trả lời và thêm vào tập hợp answers_dict[question_id]
            unique_answers = set([ans.strip().replace('"', '') for ans in split_answers])
            answers_dict[question_id].update(unique_answers)

# Tạo dataframe kết quả từ dictionary answers_dict
result_df = pd.DataFrame({'question_id': question_ids, 'answers': [';'.join(answers_dict[q_id]) for q_id in question_ids]})
