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

# alarm clock
import datetime
import time
import winsound  # For Windows users, for other OS use alternative sound libraries

def set_alarm(alarm_time):
    while True:
        current_time = datetime.datetime.now().strftime("%H:%M:%S")
        if current_time == alarm_time:
            print("Wake up! It's time!")
            frequency = 2500  # Set frequency (2500 Hz)
            duration = 2000  # Set duration (2000 ms or 2 seconds)
            winsound.Beep(frequency, duration)
            break
        time.sleep(1)  # Check time every second

if __name__ == "__main__":
    alarm_time = input("Enter the alarm time in HH:MM format (24-hour): ")
    set_alarm(alarm_time)
