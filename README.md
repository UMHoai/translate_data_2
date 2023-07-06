import pandas as pd
from sklearn.feature_extraction.text import TfidfVectorizer

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

# Tạo cột 'vectorize' trong dataframe và gán giá trị vector tương ứng
df['vectorize'] = [vector.toarray() for vector in vectors]

# In ra dataframe kết quả
print(df)
