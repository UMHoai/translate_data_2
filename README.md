unique_b = df['b'].unique()
result = df.loc[(df['a'] == 1) & (df['b'].isin(unique_b)), :]
