import pandas as pd
from sklearn.feature_extraction.text import TfidfVectorizer
import numpy as np

# Định nghĩa dataframe ban đầu
data = {
    'text': ['Đây là câu thứ nhất', 'Đây là câu thứ hai', 'Đây là câu thứ ba'],
    'class': ['A', 'B', 'A']
}
df = pd.DataFrame(data)

# Tạo một vectorizer và fit với dữ liệu văn bản
vectorizer = TfidfVectorizer()
vectorizer.fit(df['text'])

# Vector hóa các câu trong cột 'text' thành các vector
vectors = vectorizer.transform(df['text'])

# Tính độ dài tối đa và trung bình của các vector hóa
max_length = int(np.max([len(vector.toarray().flatten()) for vector in vectors]))
avg_length = int(np.mean([len(vector.toarray().flatten()) for vector in vectors]))

# Sử dụng độ dài tối đa hoặc trung bình để làm độ dài cố định cho vectorize
desired_length = max_length
# desired_length = avg_length

# Chuyển đổi ma trận thành mảng một chiều với độ dài cố định
vectors = [np.pad(vector.toarray().flatten(), (0, desired_length - len(vector)), 'constant')[:desired_length] for vector in vectors]

# Tạo cột 'vectorize' trong dataframe và gán giá trị vector tương ứng
df['vectorize'] = vectors

# In ra dataframe kết quả
print(df)
