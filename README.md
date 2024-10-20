# Secure-Password-Generator
import string
import random

def generate_password(length=12, use_uppercase=True, use_numbers=True, use_special=True):
    # Define the character set based on user preferences
    lowercase = string.ascii_lowercase
    uppercase = string.ascii_uppercase if use_uppercase else ''
    numbers = string.digits if use_numbers else ''
    special = string.punctuation if use_special else ''

    # Combine all selected character sets
    all_characters = lowercase + uppercase + numbers + special

    # Ensure the password is generated from at least one of each selected type
    if not all_characters:
        raise ValueError("At least one character type must be selected.")

    password = []

    # Ensure at least one character from each selected category
    if use_uppercase:
        password.append(random.choice(uppercase))
    if use_numbers:
        password.append(random.choice(numbers))
    if use_special:
        password.append(random.choice(special))

    # Fill the remaining length with random choices from all characters
    remaining_length = length - len(password)
    password += random.choices(all_characters, k=remaining_length)

    # Shuffle the password list to ensure randomness
    random.shuffle(password)

    return ''.join(password)

def main():
    length = int(input("Enter desired password length (minimum 8): "))
    if length < 8:
        print("Password length should be at least 8.")
        return

    use_uppercase = input("Include uppercase letters? (y/n): ").lower() == 'y'
    use_numbers = input("Include numbers? (y/n): ").lower() == 'y'
    use_special = input("Include special characters? (y/n): ").lower() == 'y'

    password = generate_password(length, use_uppercase, use_numbers, use_special)
    print("Generated secure password:", password)

if __name__ == "__main__":
    main()
