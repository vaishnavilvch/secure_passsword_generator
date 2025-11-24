import random
import string

def gen_paswd(length):
    
    # Define character sets
    uppercase = string.ascii_uppercase
    lowercase = string.ascii_lowercase
    digits = string.digits
    punctuation = string.punctuation
    
    
    all_chars = uppercase + lowercase + digits + punctuation

    
    if length < 8:
        print("Warning: Password length is too short. Resetting to minimum length of 8.")
        length = 8
        
    if length > 128:
        print("Warning: Password length is excessive. Resetting to maximum length of 128.")
        length = 128

    # Ensure the password meets complexity requirements by starting with one of each type
    required_chars = [
        random.choice(uppercase),
        random.choice(lowercase),
        random.choice(digits),
        random.choice(punctuation)
    ]

    
    remaining_length = length - len(required_chars)
    if remaining_length > 0:
        random_fill = [random.choice(all_chars) for _ in range(remaining_length)]
        password_list = required_chars + random_fill
    else:
        
        password_list = required_chars
    
    
    random.shuffle(password_list)
    
    
    return "".join(password_list)

def main():

    print("\n--- Secure Password Generator ---")
    print("This tool creates strong passwords (min 8 characters) for better security.")
    
    length = 0
    while length == 0:
        user_input = input("Enter desired password length (default 12): ").strip()
        
        if not user_input:
            length = 12
        else:
            try:
                
                temp_length = int(user_input)
                if temp_length > 0:
                    length = temp_length
                else:
                    print("Length must be a positive number.")
            except ValueError:
                
                print("Invalid input. Please enter a whole number.")
                
    
    # Generate and display the password
    password = gen_paswd(length)

    print("\n-------------------------------------")
    print(f"Generated Password (Length {len(password)}): {password}")
    print("-------------------------------------")
    print("Note: This password has high entropy and meets modern complexity requirements.")

if __name__ == "__main__":
    main()