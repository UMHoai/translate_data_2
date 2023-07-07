import pandas as pd
import numpy as np

# Định nghĩa dataframe df_classes
data_classes = {
    'text': ['Text 1', 'Text 2', 'Text 3', 'Text 4', 'Text 5'],
    'class_name': [1, 2, 3, 4, 5],
    'vectorize': [[0.1, 0.2, 0.3, 0.4, 0.5], [0.2, 0.3, 0.4, 0.5, 0.6], [0.3, 0.4, 0.5, 0.6, 0.7],
                  [0.4, 0.5, 0.6, 0.7, 0.8], [0.5, 0.6, 0.7, 0.8, 0.9]]
}
df_classes = pd.DataFrame(data_classes)

# Định nghĩa dataframe df_parsed
data_parsed = {
    'text': ['Parsed Text 1', 'Parsed Text 2', 'Parsed Text 3'],
    'vectorize': [[0.15, 0.25, 0.35, 0.45, 0.55], [0.25, 0.35, 0.45, 0.55, 0.65], [0.35, 0.45, 0.55, 0.65, 0.75]]
}
df_parsed = pd.DataFrame(data_parsed)

# Tạo dataframe mới để lưu kết quả
result_df = pd.DataFrame(columns=['parsed_text', 'class_name', 'similarity'])

# Tính điểm độ tương tự cho mỗi row trong df_parsed
for idx, row_parsed in df_parsed.iterrows():
    parsed_text = row_parsed['text']
    parsed_vectorize = row_parsed['vectorize']
    
    # Tính điểm độ tương tự với mỗi class trong df_classes
    similarity_scores = []
    for _, row_class in df_classes.iterrows():
        class_name = row_class['class_name']
        class_vectorize = row_class['vectorize']
        
        similarity = np.dot(parsed_vectorize, class_vectorize)
        similarity_scores.append((class_name, similarity))
    
    # Sắp xếp và lấy 3 điểm độ tương tự cao nhất
    similarity_scores.sort(key=lambda x: x[1], reverse=True)
    top_3_similarities = similarity_scores[:3]
    
    # Thêm kết quả vào dataframe mới
    for class_name, similarity in top_3_similarities:
        result_df = result_df.append({'parsed_text': parsed_text, 'class_name': class_name, 'similarity': similarity}, ignore_index=True)

# In ra dataframe kết quả
print(result_df)
