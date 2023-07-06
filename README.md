import pandas as pd

# Tạo DataFrame ban đầu
df = pd.DataFrame({'text': ['row 1', 'row 2', 'row 3', 'row 4', 'row 5']})

# Thêm cột 'class' với giá trị từ 'class 1' đến 'class 5'
df = df.assign(class=[f'class {i}' for i in range(1, 6)])

# In DataFrame sau khi thêm cột 'class'
print(df)
