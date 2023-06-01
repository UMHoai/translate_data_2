predicted_labels = [label_names[i] for i in range(len(label_names)) if prediction[i] == 1]
print(predicted_labels)
