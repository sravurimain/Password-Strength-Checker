# Password Strength Checker

## Description
This Python script is a simple yet effective password strength checker. It evaluates the strength of a password based on its length, character composition, and presence in a common password list. The script provides a score out of 7 and gives feedback on the password's strength.

## Features
- Checks password length
- Verifies the presence of uppercase letters, lowercase letters, digits, and special characters
- Compares against a list of common passwords
- Provides a strength score out of 7
- Gives feedback on password strength

## Requirements
- Python 3.x
- A file named `common.txt` containing a list of common passwords

## Installation
1. Ensure you have Python 3.x installed on your system.
2. Download the script and place it in your desired directory.
3. Create a file named `common.txt` in the same directory as the script, and fill it with a list of common passwords (one per line).

## Usage
Run the script from the command line:
```
python password_strength_checker.py
```

When prompted, enter the password you want to check. The script will then analyze the password and provide feedback.

## Code
Here's the full implementation of the password strength checker:

```python
import string

password = input("Test your password strength on a scale of 0-7: ")
upper_case = any([1 if c in string.ascii_uppercase else 0 for c in password])
lower_case = any([1 if c in string.ascii_lowercase else 0 for c in password])
special = any([1 if c in string.punctuation else 0 for c in password])
digits = any([1 if c in string.digits else 0 for c in password])

characters = [upper_case, lower_case, special, digits]

length = len(password)

score = 0

with open('common.txt', 'r') as f: 
    common = f.read().splitlines()

if password in common:
    print("Password was found in a common list. Score: 0 / 7")
    exit()

if length > 8:
    score += 1
if length > 12:
    score += 1
if length > 16:
    score += 1
if length > 20:
    score += 1
print(f"Password length is {str(length)}, adding {str(score)} points!")
if sum(characters) > 1:
    score += 1
if sum(characters) > 2:
    score += 1
if sum(characters) > 3:
    score += 1
print(f"Password has {str(sum(characters))} different character types, adding {str(sum(characters)-1)} points!")

if score < 4:
    print(f"The password is weak! Score: {str(score)} / 7")
elif score == 4:
    print(f"The password is not bad! Score: {str(score)} / 7")
elif score > 4 and score < 6:
    print(f"The password is good! Score: {str(score)} / 7")
elif score >= 6:
    print(f"The password is strong! Score: {str(score)} / 7")
```

## How it Works
1. The script first checks if the password is in the list of common passwords.
2. It then evaluates the password based on the following criteria:
   - Length (8+, 12+, 16+, 20+ characters)
   - Presence of uppercase letters
   - Presence of lowercase letters
   - Presence of digits
   - Presence of special characters
3. A score is calculated based on these criteria.
4. Finally, the script provides feedback on the password strength:
   - Weak: Score < 4
   - Not bad: Score = 4
   - Good: 4 < Score < 6
   - Strong: Score >= 6

## Example Output
```
Enter your password: MyP@ssw0rd123
Password length is 13, adding 2 points!
Password has 4 different character types, adding 3 points!
The password is strong! Score: 5 / 7
```

## Security Note
This script is for educational purposes and provides a basic assessment of password strength. For real-world applications, consider using established password strength libraries and following up-to-date security best practices.

## Future Improvements
- Implement more sophisticated scoring algorithms
- Add more detailed feedback on how to improve weak passwords
- Include checks for keyboard patterns and repeated characters
- Potentially impliment this feature into a website
