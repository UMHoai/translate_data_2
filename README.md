
                # Join the extracted labels into a single string
                joined_labels = '-'.join(extracted_labels)

                # Store the joined labels in the answers dictionary
                if question_number in answers_dict:
                    answers_dict[question_number].append(joined_labels)
                else:
                    answers_dict[question_number] = [joined_labels]

            # Process the answers dictionary to create the final descriptions
            descriptions = []
            for question_number in sorted(answers_dict.keys()):
                joined_answers = '-'.join(answers_dict[question_number])
                descriptions.append(joined_answers)
