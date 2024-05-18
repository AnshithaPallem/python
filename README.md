# BMI calculator
def calculate_bmi(weight_kg, height_m):
    bmi = weight_kg / (height_m ** 2)
    return bmi

def interpret_bmi(bmi):
    if bmi < 18.5:
        return "Underweight"
    elif bmi >= 18.5 and bmi < 25:
        return "Normal Weight"
    elif bmi >= 25 and bmi < 30:
        return "Overweight"
    else:
        return "Obese"

def main():
    print("BMI Calculator")
    weight = float(input("Enter your weight in kilograms: "))
    height = float(input("Enter your height in meters: "))
    
    bmi = calculate_bmi(weight, height)
    bmi_category = interpret_bmi(bmi)
    
    print(f"Your BMI is: {bmi:.2f}")
    print(f"You are in the '{bmi_category}' category.")

if __name__ == "__main__":
    main()

# random password generator
import random
import string

def generate_random_password(length=12):
    # Define character sets for password generation
    letters_upper = string.ascii_uppercase
    letters_lower = string.ascii_lowercase
    digits = string.digits
    special_chars = string.punctuation

    # Combine all character sets
    all_chars = letters_upper + letters_lower + digits + special_chars

    # Generate random password using all_chars
    password = ''.join(random.choice(all_chars) for _ in range(length))
    return password
    
random_password = generate_random_password()
print("Random Password:", random_password)

# basic weather app
import requests

def get_weather(city, api_key):
    base_url = "http://api.openweathermap.org/data/2.5/weather"
    params = {
        "q": city,
        "appid": api_key,
        "units": "metric"  # You can change units to "imperial" for Fahrenheit
    }
    response = requests.get(base_url, params=params)
    if response.status_code == 200:
        data = response.json()
        weather_info = {
            "city": data["name"],
            "description": data["weather"][0]["description"],
            "temperature": data["main"]["temp"],
            "humidity": data["main"]["humidity"],
            "wind_speed": data["wind"]["speed"]
        }
        return weather_info
    else:
        print("Error fetching weather data:", response.status_code)
        return None

def main():
    city = input("Enter city name: ")
    api_key = "YOUR_API_KEY"  # Replace with your actual API key from OpenWeatherMap
    weather_info = get_weather(city, api_key)
    if weather_info:
        print("\nWeather Information for", weather_info["city"])
        print("Description:", weather_info["description"])
        print("Temperature:", weather_info["temperature"], "°C")
        print("Humidity:", weather_info["humidity"], "%")
        print("Wind Speed:", weather_info["wind_speed"], "m/s")
    else:
        print("Weather information not available.")

if __name__ == "__main__":
    main()
