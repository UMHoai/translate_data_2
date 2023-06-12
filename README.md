def random_answer(question_number):
    options = map_df.loc[map_df['question_number'] == question_number, 'answer'].values
    if len(options) == 0:
        return ""
    elif len(options) == 1:
        return options[0]
    else:
        return random.choice(options)
