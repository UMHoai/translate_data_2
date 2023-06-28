else:
                # Tạo một tập hợp (set) để lưu các câu trả lời duy nhất
                unique_answers = set()

                # Xử lý unique() answer
                for answer in answers:
                    # Tách các câu trả lời bằng dấu phẩy
                    split_answers = answer.split(',')

                    # Xóa ký tự '"' từ các câu trả lời và thêm vào tập hợp unique_answers
                    unique_answers.update([ans.strip().replace('"', '') for ans in split_answers])

                # Nối các câu trả lời duy nhất lại thành một string bằng dấu phân cách ';'
                member_answers[question_id] = ';'.join(unique_answers)
        
        # Thêm dữ liệu của member vào dataframe kết quả
        result_df = result_df.append(member_answers, ignore_index=True)
