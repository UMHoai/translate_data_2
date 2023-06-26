if string2 in string1:
    _, _, result = string1.partition(string2)
    result = result.strip("-")  # Loại bỏ dấu gạch ngang nếu có
    print(result)  # Output: "over-night"
