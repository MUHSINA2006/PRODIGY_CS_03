# PRODIGY_CS_03
import re

def password_strength(password):
    # Criteria checks
    length_error = len(password) < 8
    lowercase_error = re.search(r'[a-z]', password) is None
    uppercase_error = re.search(r'[A-Z]', password) is None
    digit_error = re.search(r'\d', password) is None
    special_char_error = re.search(r'[!@#$%^&*(),.?":{}|<>]', password) is None
    
    # Count the number of failed criteria
    errors = sum([length_error, lowercase_error, uppercase_error, digit_error, special_char_error])
    
    # Strength classification
    if errors == 0:
        strength = "Strong"
    elif errors == 1:
        strength = "Moderate"
    else:
        strength = "Weak"
    
    # Feedback for user
    feedback = []
    if length_error:
        feedback.append("- Your password must be at least 8 characters long.")
    if lowercase_error:
        feedback.append("- Your password must include at least one lowercase letter.")
    if uppercase_error:
        feedback.append("- Your password must include at least one uppercase letter.")
    if digit_error:
        feedback.append("- Your password must include at least one number.")
    if special_char_error:
        feedback.append("- Your password must include at least one special character.")
    
    return strength, feedback


# Example Usage
password = input("Enter your password: ")
strength, feedback = password_strength(password)

print(f"\nPassword Strength: {strength}")
if feedback:
    print("Feedback:")
    for f in feedback:
        print(f)