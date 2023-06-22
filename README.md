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
            with open(file, 'r') as assessment_file:
                lines = assessment_file.readlines()
                member_ids = []
                for line in lines:
                    if "member id" in line.lower():
                        member_id = line.split(":")[-1].strip()
                        member_ids.append(member_id)
                member_ids = list(set(member_ids))  # Remove duplicates

                df_filtered = df[df['associabled_menber'].isin(member_ids)]
                df_filtered = df_filtered[df_filtered['question_id'].between(1, 17)]  # Filter questions from 1 to 17
                df_filtered = df_filtered.sort_values(by='processing_order')

                descriptions = ' '.join(df_filtered['text'])

                # Write the description to the CSV file
                writer.writerow({'timestamp': '', 'source': '', 'description': descriptions})
