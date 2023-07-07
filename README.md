# Đếm số lượng người có bệnh "a" trong cột số 1
count_a = df[df['1'].str.contains('a')]['associated_member'].count()
print("Số người có bệnh 'a' trong cột số 1:", count_a)
