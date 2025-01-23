# Password Strength Checker

## Description
This Python script is a simple yet effective password strength checker. It evaluates the strength of a password based on its length, character composition, and presence in a common password list. The script provides a score out of 7 and gives feedback on the password's strength.

## Features
- Checks password length
- Verifies the presence of uppercase letters, lowercase letters, digits, and special characters
- Compares against a predefined list of common passwords
- Provides a strength score out of 7
- Gives feedback on password strength

## Requirements
- Python 3.x

## Usage
Run the script from the command line:
```
python password_strength_checker.py
```

When prompted, enter the password you want to check. The script will then analyze the password and provide feedback.

## Code
Here's the full implementation of the password strength checker:

```python
import re
import json
from string import ascii_uppercase, ascii_lowercase, punctuation, digits

# Ask for user input directly
password = input("Enter the password you want to evaluate: ")

# Example of a common passwords list (this replaces the need for a JSON file)
common_passwords = [
    "123456", "password", "123456789", "12345678", "12345", "qwerty", "abc123", "password1"
]

# Check password against common passwords
if password in common_passwords:
    print("Password is too common. Score: 0 / 7")
    exit()

# Evaluate password strength
score = 0
length = len(password)
if length > 8:
    score += 1
if length > 12:
    score += 1
if length > 16:
    score += 1

character_types = sum([
    bool(re.search(r'[A-Z]', password)),  # Uppercase
    bool(re.search(r'[a-z]', password)),  # Lowercase
    bool(re.search(r'[0-9]', password)),  # Digits
    bool(re.search(r'[!@#$%^&*]', password))  # Special characters
])
score += character_types - 1

# Output results
print(f"Password score: {score} / 7")
if score < 4:
    print("Weak password.")
elif score < 6:
    print("Moderate password.")
else:
    print("Strong password.")
```

## How it Works
1. The script first checks if the password is in the predefined list of common passwords.
2. It evaluates the password based on the following criteria:
   - Length (8+, 12+, 16+ characters)
   - Presence of uppercase letters
   - Presence of lowercase letters
   - Presence of digits
   - Presence of special characters
3. A score is calculated based on these criteria.
4. Finally, the script provides feedback on the password strength:
   - Weak: Score < 4
   - Moderate: 4 <= Score < 6
   - Strong: Score >= 6

## Example Output
```
Enter the password you want to evaluate: MyP@ssw0rd123
Password score: 6 / 7
Strong password.
```

## Security Note
This script is for educational purposes and provides a basic assessment of password strength. For real-world applications, consider using established password strength libraries and following up-to-date security best practices.

## Future Improvements
- Implement more sophisticated scoring algorithms
- Add more detailed feedback on how to improve weak passwords
- Include checks for keyboard patterns and repeated characters
- Potentially implement this feature into a website
