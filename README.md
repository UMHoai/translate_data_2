descriptions = []
            for arr in result:
                unique_labels = set(arr)  # Loại bỏ các nhãn trùng lặp
                label_string = '-'.join(unique_labels)  # Nối các nhãn thành một từ
                descriptions.append(label_string)
