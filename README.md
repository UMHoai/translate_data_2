import pandas as pd
import numpy as np
import random
import string

df = pd.DataFrame({'1': ["Yes", "No"], '2': ["No", "No"], '3':["Often", "Sometime"], '4':["",""], '5':["",""]})

map_df = pd.DataFrame({'question_number': [1, 2, 3], 'answer': [['Option 1', 'Option 2'], ['Option 1', 'Option 2', 'Option 3'], ['Option 1', 'Option 2']]})

def generate_member_id():
    return ''.join(random.choices(string.digits, k=4))

def random_answer(question_number):
    options = map_df[map_df['question_number'] == question_number]['answer'].values[0]
    if len(options) == 0:
        return ""
    elif len(options) == 1:
        return options[0]
    else:
        return random.choice(options)

for index, row in df.iterrows():
    file_name = f"file_{index}.txt"
    with open(file_name, 'w') as file:
        member_id = generate_member_id()
        for col in df.columns:
            question_number = int(col)
            answer = random_answer(question_number)
            if col != '4' and col != '5':
                file.write(f"Question {question_number}: {answer}\n")
        file.write(f"Member ID: {member_id}\n")
