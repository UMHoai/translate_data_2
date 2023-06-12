import pandas as pd
import numpy as np
import random
import string
import json

df = pd.DataFrame({'1': ["Yes", "No"], '2': ["No", "No"], '3':["Often", "Sometime"], '4':["",""], '5':["",""]})

map_df = pd.DataFrame({'question_number': [1, 2, 2, 3], 'answer': ['Option 1', 'Option 2', 'Option 3', 'Option 1']})

def generate_member_id():
    return ''.join(random.choices(string.digits, k=4))

def random_answer(question_number):
    options = map_df.loc[map_df['question_number'] == question_number, 'answer'].values
    if len(options) == 0:
        return ""
    else:
        return random.choice(options)

for index, row in df.iterrows():
    file_name = f"file_{index}.txt"
    with open(file_name, 'w') as file:
        num_users = random.randint(1, 3)  # Số lượng người dùng ngẫu nhiên từ 1 đến 3
        user_data = []
        for _ in range(num_users):
            member_id = generate_member_id()
            user_answers = []
            for col in df.columns:
                question_number = int(col)
                answer = random_answer(question_number)
                if col != '4' and col != '5':
                    user_answers.append({"question": question_number, "answer": answer})
            user_data.append({"Member ID": member_id, "answers": user_answers})

        json.dump(user_data, file, indent=4)
