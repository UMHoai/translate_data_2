import pandas as pd
import matplotlib.pyplot as plt

# Tạo dataframe kết quả từ file CSV
result_df = pd.read_csv('result.csv')

# Tạo biểu đồ cột thống kê số lượng câu trả lời cho mỗi question_id
plt.bar(result_df['question_id'], result_df['answers'].str.count(';') + 1)

# Đặt tên cho trục x và trục y
plt.xlabel('Question ID')
plt.ylabel('Number of Answers')

# Đặt tiêu đề cho biểu đồ
plt.title('Number of Answers per Question ID')

# Hiển thị biểu đồ
plt.show()
