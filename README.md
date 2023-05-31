test_sentence = "How to connect Python to MySQL?"
prediction = predict(test_sentence)
label_names = ['mysql', 'python', 'php']
predicted_labels = [label_names[i] for i in range(len(label_names)) if prediction[0][i] == 1]
print(predicted_labels)
