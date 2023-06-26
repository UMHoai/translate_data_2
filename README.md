import csv
import pandas as pd

csv_file = ""
column_names = ['timestamp', 'source', 'description']

with open(csv_file, 'w', newline='') as file:
    writer = csv.DictWriter(file, fieldnames=column_names)
    writer.writeheader()

    for file_name in text_file:
        df = pd.read_csv(file_name, delimiter="|")
        df = df.dropna(axis=0)

        member_ids = df['associated_member'].unique()

        for member_id in member_ids:
            df_filtered_member = df[df['associated_member'] == member_id]

            existing_ids = df_filtered_member['question_id'].tolist()
            missing_ids = list(set(range(1, 20)) - set(existing_ids) - set(range(16, 18)))
            missing_ids = list(map(int, missing_ids))

            missing_df = pd.DataFrame({
                'question_id': missing_ids,
                'text': 'no-answer',
                'associated_member': member_id,
            })

            df_filtered_member_new = pd.concat([df_filtered_member, missing_df], ignore_index=True)
            df_filtered = df_filtered_member_new[df_filtered_member_new['associated_member'] == member_id]
            df_filtered = df_filtered[df_filtered['question_id'].between(1, 19)]
            df_filtered['processing_order'] = df_filtered['question_id'].map(
                dict(zip(df_question_mapping.question_number, df_question_mapping.processing_order)))

            df_filtered = df_filtered.sort_values('processing_order')

            result = {}
            for _, row in df_filtered.iterrows():
                question_number, answer = row["question_id"], row["text"]
                answers = answer.split(",\\")
                selected_label = []

                for ans in answers:
                    if ans == "no-answers":
                        selected_label.append(ans)
                    else:
                        result_key = f"{question_number}_{member_id}"
                        if result_key not in result:
                            result[result_key] = []
                        result[result_key].append(ans)

            descriptions = []
            for key, answers in result.items():
                question_number, member_id = key.split("_")
                label = "-".join(answers).replace(" ", "-")
                if question_number == "1":
                    descriptions.append(f"physical-problem-{label}")
                elif question_number == "5":
                    descriptions.append(f"mental-problem-{label}")

            descriptions = ' '.join(descriptions).strip()

            # Print the answer text
            print(descriptions)

            writer.writerow({
                'timestamp': '',
                'source': file_name,
                'description': descriptions
            })
