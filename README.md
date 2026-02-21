from flask import Flask, request, jsonify
from flask_cors import CORS
import os

app = Flask(__name__)
CORS(app)

@app.route("/")
def home():
    return "Crack Detection API Running Successfully"

@app.route("/predict", methods=["POST"])
def predict():
    try:
        # Try getting file with key "file"
        upload = request.files.get('file')

        if upload is None:
            return jsonify({"error": "No file received"}), 400
        
        # Save file temporarily
        upload.save(os.path.join("uploads", upload.filename))

        # For now, send dummy result
        return jsonify({
            "Crack_Type": "Flexural Crack",
            "Crack_Length_mm": 120,
            "Crack_Width_mm": 2.5,
            "Safety_Status": "Moderate Risk"
        })

    except Exception as e:
        return jsonify({"error": str(e)}), 500

if __name__ == "__main__":
    app.run(host="0.0.0.0", port=10000)
