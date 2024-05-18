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

# voice assistant
import speech_recognition as sr
import pyttsx3
import datetime
import webbrowser

recognizer = sr.Recognizer()

engine = pyttsx3.init()

def speak(text):
    engine.say(text)
    engine.runAndWait()

def listen():
    with sr.Microphone() as source:
        print("Listening...")
        recognizer.adjust_for_ambient_noise(source)
        audio = recognizer.listen(source)
        try:
            print("Recognizing...")
            query = recognizer.recognize_google(audio)
            print(f"User said: {query}")
            return query.lower()
        except sr.UnknownValueError:
            print("Sorry, I couldn't understand.")
            return ""
        except sr.RequestError:
            print("Request error.")
            return ""

def handle_command(command):
    if "hello" in command:
        speak("Hello! How can I help you?")
    elif "time" in command:
        current_time = datetime.datetime.now().strftime("%H:%M:%S")
        speak(f"The current time is {current_time}")
    elif "date" in command:
        current_date = datetime.date.today().strftime("%B %d, %Y")
        speak(f"Today's date is {current_date}")
    elif "search" in command:
        speak("What would you like me to search for?")
        query = listen()
        if query:
            search_url = f"https://www.google.com/search?q={query}"
            webbrowser.open(search_url)
            speak(f"Here are the search results for {query}")
    elif "exit" in command:
        speak("Goodbye!")
        exit()
    else:
        speak("I'm sorry, I don't understand that command.")

if __name__ == "__main__":
    speak("Hello! I am your voice assistant.")
    while True:
        user_input = listen()
        if user_input:
            handle_command(user_input)
