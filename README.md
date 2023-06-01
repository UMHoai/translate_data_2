predicted_labels = []
    for label in label_names:
        label_model = clf_labelP_model[label]
        label_prediction = label_model.predict(transformed_text)
        predicted_labels.append(label_prediction.toarray()[0])
    return np.array(predicted_labels)
