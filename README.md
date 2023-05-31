def predict(text):
    preprocessed_text = nfx.remove_stopwords(nt.TextFrame(text).noise_scan())
    transformed_text = tfidf.transform([preprocessed_text]).toarray()
    predictions = clf_labelP_model.predict(transformed_text)
    return predictions
