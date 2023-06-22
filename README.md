import csv
import pandas as pd

csv_file = ""
column_names = ['timestamp', 'source', 'description']

with open(csv_file, 'w', newline='') as file:
    writer = csv.DictWriter(file, fieldnames=column_names)
    writer.writeheader()

    for file_name in text_file:
        if "Assessment" in file_name:
            df = pd.read_csv(file_name, delimiter="|").dropna(axis=0)
            df_question_mapping['answer'] = df_question_mapping['answer'].str.lower()
            
            def extract_labels(row):
                question_number, answer = row["question_id"], row["text"]
                answers = answer.split(",\\")
                result = [ans.lower().replace("\\", "").replace("\"", "") for ans in answers]
                condition = (df_question_mapping['question_number'] == question_number) & (df_question_mapping['answer'].isin(result))
                selected_labels = df_question_mapping.loc[condition, 'label'].astype(str)
                extracted_labels = selected_labels.str.split('   ').str[1].str.split('\n').str[0]
                return ' '.join(extracted_labels)

            df['description'] = df.apply(extract_labels, axis=1)
            descriptions = df['description'].str.cat(sep=' ')

            # Write the description to the CSV file
            writer.writerow({'timestamp': '', 'source': '', 'description': descriptions})
