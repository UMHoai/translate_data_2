import pandas as pd

df = pd.DataFrame({'associated_member': [1, 2, 3],
                   1: [['no-answer', 'bad', 'no'], 'yes', 'no'],
                   2: ['no-answer', 'yes', 'no'],
                   3: ['no-answer', 'yes', 'no']})

df_mapping = pd.DataFrame({'question_number': [1, 1, 2, 2, 2, 3],
                           'answer': ['no-answer', 'yes', 'no', 'never', 'ok', 'good'],
                           'label': ['aaa', 'bbb', 'ccc', 'ddd', 'fff', 'eeee'],
                           'category': ['cau1', 'cau1', 'cau2', 'cau2', 'cau2', 'cau3']})

# Function to map answers to labels
def map_answers_to_labels(answers, columns):
    labels = []
    for answer, col in zip(answers, columns):
        if answer == 'no-answer':
            labels.append('no-answer')
            labels.append('no-answers')
        else:
            mapping = df_mapping[df_mapping['answer'] == answer]
            if not mapping.empty:
                labels.append('-'.join(mapping['label'].tolist()))
            else:
                question_category = df_mapping[df_mapping['question_number'] == col]['category'].values[0]
                labels.append(question_category + '-' + answer)
    return labels

# Apply mapping function to each row
df['labels'] = df.apply(lambda row: map_answers_to_labels(row[1:], df.columns[1:]), axis=1)

# Combine labels into a single text
df['labels_text'] = df['labels'].apply(lambda labels: ' '.join(labels))

print(df)
