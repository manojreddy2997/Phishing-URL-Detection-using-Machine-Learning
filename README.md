 Phishing-URL-Detection-using-Machine-Learning
 
This project detects whether a given website URL is legitimate or phishing using a machine learning model. It’s simple, beginner-friendly, and useful for showcasing cybersecurity and ML skills.

Code Snippet (app.py)
python
Copy
Edit
from flask import Flask, render_template, request
import pickle
import feature_extraction

app = Flask(__name__)
model = pickle.load(open("phishing_model.pkl", "rb"))

@app.route('/')
def home():
    return render_template('index.html')

@app.route('/predict', methods=['POST'])
def predict():
    url = request.form['url']
    features = feature_extraction.extract(url)
    prediction = model.predict([features])[0]
    result = "Phishing" if prediction == 1 else "Legitimate"
    return render_template('index.html', prediction=result)

if __name__ == "__main__":
    app.run(debug=True)
