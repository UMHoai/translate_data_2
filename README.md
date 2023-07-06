from sklearn.feature_extraction.text import TfidfVectorizer

# Tạo một instance của TF-IDF Vectorizer
vectorizer = TfidfVectorizer()

# Vectorize cột "text" trong dataframe
text_vectorized = vectorizer.fit_transform(grouped_df['text'])

# Tạo dataframe mới từ ma trận vectorized
df_vectorized = pd.DataFrame(text_vectorized.toarray(), columns=vectorizer.get_feature_names())

# Kết hợp dataframe vectorized với dataframe gốc
grouped_df_vectorized = pd.concat([grouped_df, df_vectorized], axis=1)

# In kết quả
print(grouped_df_vectorized)
