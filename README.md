else:
                # Tách các câu trả lời khi có nhiều hơn một tùy chọn
                processed_answers = []
                for answer in answers:
                    # Tách các câu trả lời bằng dấu phẩy
                    split_answers = answer.split(',')

                    # Xóa ký tự '"' từ các câu trả lời
                    cleaned_answers = [ans.strip().replace('"', '') for ans in split_answers]

                    # Thêm các câu trả lời đã được xử lý vào danh sách
                    processed_answers.extend(cleaned_answers)

                # Nối các câu trả lời lại thành một string bằng dấu phân cách ';'
                member_answers[question_id] = ';'.join(processed_answers)
