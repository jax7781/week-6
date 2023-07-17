# week-6
Scripts for week 6
def caesar_cipher(plaintext, distance):
    encrypted_text = ""
    for char in plaintext:
        if char.isalpha():
            if char.isupper():
                encrypted_char = chr((ord(char) - ord('A') + distance) % 26 + ord('A'))
            else:
                encrypted_char = chr((ord(char) - ord('a') + distance) % 26 + ord('a'))
        else:
            encrypted_char = char
        encrypted_text += encrypted_char
    return encrypted_text

plaintext = input("Enter the plaintext: ")
distance = int(input("Enter the distance value: "))
encrypted_text = caesar_cipher(plaintext, distance)
print("Encrypted text:", encrypted_text)

def caesar_decipher(encrypted_text, distance):
    decrypted_text = ""
    for char in encrypted_text:
        if char.isalpha():
            if char.isupper():
                decrypted_char = chr((ord(char) - ord('A') - distance) % 26 + ord('A'))
            else:
                decrypted_char = chr((ord(char) - ord('a') - distance) % 26 + ord('a'))
        else:
            decrypted_char = char
        decrypted_text += decrypted_char
    return decrypted_text

encrypted_text = input("Enter the encrypted text: ")
distance = int(input("Enter the distance value: "))

plaintext = caesar_decipher(encrypted_text, distance)

print("Decrypted text:", plaintext)

def copy_file(source_file, destination_file):
    try:
        with open(source_file, 'r') as source:
            with open(destination_file, 'w') as destination:
                destination.write(source.read())
        print("File copied successfully.")
    except FileNotFoundError:
        print("One or both files not found.")

source_file = input("Enter the name of the source file: ")
destination_file = input("Enter the name of the destination file: ")

copy_file(source_file, destination_file)

def parse_employee_details(line):
    components = line.strip()[1:-1].split('<>')
    
    last_name = components[0]
    hourly_wage = float(components[1])
    hours_worked = float(components[2])
    
    return last_name, hourly_wage, hours_worked

def print_payroll_report(filename):
    try:
        with open(filename, 'r') as file:
            print("Payroll Report")
            print("-----------------------")
            print("Name\t\tHours Worked\tWages Paid")
            print("-----------------------")
            
            total_wages = 0
            
            for line in file:
                last_name, hourly_wage, hours_worked = parse_employee_details(line)
                wages_paid = hourly_wage * hours_worked
                total_wages += wages_paid
                
                print(f"{last_name}\t\t{hours_worked}\t\t{wages_paid}")
            
            print("-----------------------")
            print(f"Total Wages Paid: {total_wages}")
            
    except FileNotFoundError:
        print("File not found.")

filename = input("Enter the filename: ")

print_payroll_report(filename)
