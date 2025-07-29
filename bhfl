from flask import Flask, request, jsonify

app = Flask(__name__)

def analyze_data_list(data_list):
    odd_nums = []
    even_nums = []
    alphabets = []
    specials = []
    total_sum = 0
    alphabet_string = ""

    for item in data_list:
        try:
            number = int(item)
            total_sum += number
            if number % 2 == 0:
                even_nums.append(str(number))
            else:
                odd_nums.append(str(number))
        except (ValueError, TypeError):
            if isinstance(item, str) and item.isalpha():
                alphabets.append(item.upper())
                alphabet_string += item
            else:
                specials.append(item)

    reversed_alphas = alphabet_string[::-1]
    alternating_caps = "".join(
        c.lower() if i % 2 == 0 else c.upper() 
        for i, c in enumerate(reversed_alphas)
    )

    return {
        "odd_numbers": odd_nums,
        "even_numbers": even_nums,
        "alphabets": alphabets,
        "special_characters": specials,
        "sum": str(total_sum),
        "concat_string": alternating_caps
    }

@app.route("/bfhl", methods=["POST"])
def handle_bfhl_request():
    try:
        incoming_data = request.get_json()

        if not incoming_data or 'data' not in incoming_data:
            return jsonify({"is_success": False, "error_message": "The 'data' key is missing or the payload is invalid."}), 400

        analysis_result = analyze_data_list(incoming_data['data'])

        your_full_name = "Sachin Doe"
        your_dob = "29072004"
        your_email = "sachin.doe@example.com"
        your_roll_number = "YOUR_ROLL_NUMBER"
        
        user_id = f"{your_full_name.lower().replace(' ', '_')}_{your_dob}"

        response_data = {
            "is_success": True,
            "user_id": user_id,
            "email": your_email,
            "roll_number": your_roll_number,
            **analysis_result
        }
        
        return jsonify(response_data), 200

    except Exception as e:
        return jsonify({
            "is_success": False, 
            "user_id": "YOUR_NAME_DDMMYYYY",
            "error_message": f"An internal server error occurred."
        }), 500

if __name__ == "__main__":
    app.run(debug=True, port=5000)
