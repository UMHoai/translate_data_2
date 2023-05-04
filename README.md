result = result.groupby(['score']).sum().reset_index()

df_merged = df_merged.sort_values(['id_question', 'id', 'text'], ascending=[True, True, True])
