import pandas as pd
from sklearn.metrics.pairwise import cosine_similarity

# Định nghĩa dataframe vectorize_class
data_class = {
    'vectorize_class': [[0.1, 0.2, 0.3], [0.4, 0.5, 0.6]],
    'class': ['A', 'B']
}
df_class = pd.DataFrame(data_class)

# Định nghĩa dataframe text_vectorize
data_text = {
    'text': ['Đây là câu thứ nhất', 'Đây là câu thứ hai'],
    'text_vectorize': [[0.15, 0.25, 0.35], [0.45, 0.55, 0.65]]
}
df_text = pd.DataFrame(data_text)

# Tạo dataframe mới để lưu đoạn text, top score và class tương ứng
result_df = pd.DataFrame(columns=['text', 'top_score', 'class'])

# Tính độ tương tự và lưu vào dataframe mới
for index, row in df_text.iterrows():
    text_vectorize = row['text_vectorize']
    similarity_scores = cosine_similarity([text_vectorize], df_class['vectorize_class'])
    top_scores = pd.Series(similarity_scores[0]).nlargest(3)
    top_indices = top_scores.index
    top_classes = df_class['class'].iloc[top_indices]
    for i in range(len(top_scores)):
        result_df.loc[index*3 + i] = [row['text'], top_scores.iloc[i], top_classes.iloc[i]]

# In ra dataframe kết quả
print(result_df)
