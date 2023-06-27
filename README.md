arr = ["apple", "banana", "banana", "orange", "apple"]
unique_arr = [x for i, x in enumerate(arr) if x not in arr[:i]]
