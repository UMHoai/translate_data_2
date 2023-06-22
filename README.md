# Thêm cột 'processing_order' vào df
df['processing_order'] = df['question_id'].map(dict(zip(df_mapping['question_id'], df_mapping['processing_order'])))

# Sắp xếp lại df theo 'processing_order'
df = df.sort_values('processing_order')

print(df)
