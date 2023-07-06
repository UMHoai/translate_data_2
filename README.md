import pandas as pd
import numpy as np
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

# Tính độ tương tự giữa tất cả các text_vectorize và vectorize_class
similarity_scores = cosine_similarity(df_text['text_vectorize'].tolist(), df_class['vectorize_class'].tolist())

# Lấy top 3 scores và indices tương ứng
top_scores = np.apply_along_axis(lambda row: np.sort(row)[-3:], 1, similarity_scores)
top_indices = np.apply_along_axis(lambda row: np.argsort(row)[-3:], 1, similarity_scores)

# Tạo dataframe mới để lưu đoạn text, top score và class tương ứng
result_df = pd.DataFrame(columns=['text', 'top_score', 'class'])

# Lặp qua mỗi text_vectorize và gán kết quả vào dataframe mới
for i in range(len(df_text)):
    text = df_text['text'][i]
    scores = top_scores[i]
    indices = top_indices[i]
    classes = df_class['class'].iloc[indices]
    result_df = result_df.append(pd.DataFrame({'text': [text] * 3, 'top_score': scores, 'class': classes}))

# Đặt lại chỉ mục cho dataframe mới
result_df.reset_index(drop=True, inplace=True)

# In ra dataframe kết quả
print(result_df)
