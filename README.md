x = df3.to_string(header=False,
                  index=False,
                  index_names=False).split('\n')
vals = [','.join(ele.split()) for ele in x]
print(vals)
