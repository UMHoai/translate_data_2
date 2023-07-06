vectors = [np.pad(vector.toarray().flatten(), (0, desired_length - len(vector)), 'constant')[:desired_length] for vector in vectors]
