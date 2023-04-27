#Get last row of dataframe
last_row = df.iloc[-1]

#Get last row of dataframe as string
last_row_as_string = last_row.to_string(index=False)

#Replace '\n' with comma
last_row_as_string = last_row_as_string.replace('\n', ',')

#Display the result
print(last_row_as_string)
