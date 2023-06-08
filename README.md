txt_file = f'output_file_{question_id}.txt'

    # Mở file txt để ghi dữ liệu
    with open(txt_file, 'w') as file:
        # Ghi câu hỏi vào file
        file.write(f'{question_id}|{question_text}\n')

        # Lặp qua các câu trả lời và ghi vào file
        for i in range(1, len(question)):
            answer_key = f'answer_{i}'
            answer_text = question[answer_key]
            file.write(f'{question_id}|{answer_text}\n')
