@app.route("/predict", methods=["POST"])
def predict():
    try:
        if len(request.files) == 0:
            return jsonify({"error": "No file received"})

        # Get first uploaded file (any key name)
        upload = list(request.files.values())[0]

        os.makedirs("uploads", exist_ok=True)
        upload.save(os.path.join("uploads", upload.filename))

        return jsonify({
            "Crack_Type": "Flexural Crack",
            "Crack_Length_mm": 120,
            "Crack_Width_mm": 2.5,
            "Safety_Status": "Moderate Risk"
        })

    except Exception as e:
        return jsonify({"error": str(e)})
    except Exception as e:
        return jsonify({"error": str(e)}), 500

if __name__ == "__main__":
    app.run(host="0.0.0.0", port=10000)
