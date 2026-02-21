# crack-detection-api
@app.route("/predict", methods=["POST"])
def predict():
    try:
        # MIT App sends raw data
        file = request.files.get('file')
        
        if file:
            result = {
                "Crack_Type": "Flexural Crack",
                "Crack_Length_mm": 120,
                "Crack_Width_mm": 2.5,
                "Safety_Status": "Moderate Risk"
            }
            return jsonify(result)
        else:
            return jsonify({
                "Crack_Type": "No Crack Detected",
                "Crack_Length_mm": 0,
                "Crack_Width_mm": 0,
                "Safety_Status": "Safe"
            })
    except Exception as e:
        return jsonify({"error": str(e)})
