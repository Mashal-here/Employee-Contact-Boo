# Employee-Contact-Boo


def validate_name(name):
    """Check if the name contains only alphabetic characters."""
    if name.isalpha():
        return True
    else:
        raise ValueError("Name must contain only alphabetic characters.")

def validate_phone_number(phone_number):
    """Check if the phone number contains only numeric characters."""
    if phone_number.isdigit():
        return True
    else:
        raise ValueError("Phone number must contain only numeric characters.")

def validate_email(email):
    """Check if the email follows the standard format."""
    pattern = r'^[\w\.-]+@[\w\.-]+\.\w+$'
    if re.match(pattern, email):
        return True
    else:
        raise ValueError("Invalid email format.")

def is_unique(empID, phone_number, email):
    """Check if empID, phone_number, or email are unique."""
    for emp in employees:
        if emp['empID'] == empID:
            raise ValueError(f"Employee with employee number {empID} already exists.")
        if emp['phone_number'] == phone_number:
            raise ValueError(f"Phone number {phone_number} is already assigned to another employee.")
        if emp['email'] == email:
            raise ValueError(f"Email {email} is already in use.")
    return True

def add_employee():
    """Function to add a new employee to the contact book."""
    try:
        empID = input("Enter Employee ID: ")
        first_name = input("Enter First Name: ")
        last_name = input("Enter Last Name: ")
        phone_number = input("Enter Phone Number: ")
        email = input("Enter Email: ")
        address = input("Enter Address: ")

        # Validate inputs
        validate_name(first_name)
        validate_name(last_name)
        validate_phone_number(phone_number)
        validate_email(email)
        is_unique(empID, phone_number, email)

        # Add employee to the list
        employees.append({
            'empID': empID,
            'first_name': first_name,
            'last_name': last_name,
            'phone_number': phone_number,
            'email': email,
            'address': address
        })
        print("Employee added successfully!")

    except ValueError as ve:
        print(f"Error: {ve}")

def display_employees():
    """Function to display all employee contacts in a table format."""
    print("\nEmployee Contact List:")
    print(f"{'ID':<10}{'First Name':<15}{'Last Name':<15}{'Phone Number':<15}{'Email':<30}{'Address':<20}")
    print("="*105)
    for emp in employees:
        print(f"{emp['empID']:<10}{emp['first_name']:<15}{emp['last_name']:<15}{emp['phone_number']:<15}{emp['email']:<30}{emp['address']:<20}")
    print("="*105)

# Main loop
while True:
    print("\n1. Add Employee")
    print("2. Display Employees")
    print("3. Exit")
    choice = input("Enter your choice: ")

    if choice == '1':
        add_employee()
    elif choice == '2':
        display_employees()
    elif choice == '3':
        break
    else:
        print("Invalid choice! Please enter 1, 2, or 3.")
