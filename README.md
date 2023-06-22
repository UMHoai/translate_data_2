import csv
import pandas as pd

csv_file = ""
column_names = ['timestamp', 'source', 'description']

# Read the question mapping dataframe
df_question_mapping = pd.read_csv("df_question_mapping.csv")  # Adjust the filename as per your actual file

with open(csv_file, 'w', newline='') as file:
    writer = csv.DictWriter(file, fieldnames=column_names)
    writer.writeheader()

    for file in text_file:
        if "Assessment" in file:
            df = pd.read_csv(file, delimiter="|")
            df = df.dropna(axis=0)
            description = ""
            lst = []

            for idx, row in df.iterrows():
                question_number, answer = row["question_id"], row["text"]
                answers = answer.split(",\\")
                selected_label = []

                for ans in answers:
                    result = ans.lower().replace("\\", "").replace("\"", "")
                    condition = (df_question_mapping.question_number == question_number) & (df_question_mapping.answer.str.lower() == result)
                    selected_label.append(str(df_question_mapping.loc[condition, 'label']))

                extracted_label = [text.split('   ')[1].split('\n')[0] for text in selected_label]
                lst.append(extracted_label)

            result = [' '.join(arr) for arr in lst]
            result.sort(key=lambda x: df_question_mapping.loc[df_question_mapping['label'] == x, 'priority'].values[0], reverse=True)
            descriptions = ' '.join(result)

            # Write the description to the CSV file
            writer.writerow({'timestamp': '', 'source': '', 'description': descriptions})
