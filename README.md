result = result.groupby(['score']).sum().reset_index()
