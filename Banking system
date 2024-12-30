import random
import re
import sys

class BankingSystem:
    def __init__(self):
        self.users = {}

    def validate_name(self, name):
        return name.isalpha()

    def validate_dob(self, dob):
        pattern = r"\d{2}/\d{2}/\d{4}"
        return re.match(pattern, dob)

    def validate_city(self, city):
        return city.isalpha()

    def validate_password(self, password):
        pattern = r"^(?=.*[A-Za-z])(?=.*\d)(?=.*[@$!%*#?&])[A-Za-z\d@$!%*#?&]{8,}$"
        return re.match(pattern, password)

    def validate_contact(self, contact):
        return contact.isdigit() and len(contact) == 10

    def validate_email(self, email):
        pattern = r"^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$"
        return re.match(pattern, email)

    def create_account_number(self):
        return str(random.randint(1000000000, 9999999999))

    def add_user(self):
        print("\n--- Add User ---")
        name = input("Enter Name: ")
        if not self.validate_name(name):
            print("Invalid Name. Only alphabets are allowed.")
            return
        
        dob = input("Enter DOB (DD/MM/YYYY): ")
        if not self.validate_dob(dob):
            print("Invalid DOB format.")
            return

        city = input("Enter City: ")
        if not self.validate_city(city):
            print("Invalid City. Only alphabets are allowed.")
            return

        password = input("Enter Password (min 8 chars, incl. 1 letter, 1 digit, 1 special char): ")
        if not self.validate_password(password):
            print("Invalid Password.")
            return

        initial_balance = int(input("Enter Initial Balance (Minimum 2000): "))
        if initial_balance < 2000:
            print("Initial balance must be at least 2000.")
            return

        contact = input("Enter Contact Number (10 digits): ")
        if not self.validate_contact(contact):
            print("Invalid Contact Number.")
            return

        email = input("Enter Email ID: ")
        if not self.validate_email(email):
            print("Invalid Email ID.")
            return

        address = input("Enter Address: ")

        account_number = self.create_account_number()
        user = {
            "name": name,
            "dob": dob,
            "city": city,
            "password": password,
            "balance": initial_balance,
            "contact": contact,
            "email": email,
            "address": address,
            "active": True,
            "transactions": []
        }
        self.users[account_number] = user
        print(f"User added successfully! Account Number: {account_number}")

    def show_user(self):
        print("\n--- Show Users ---")
        if not self.users:
            print("No users found.")
            return
        for acc_no, user in self.users.items():
            print(f"\nAccount Number: {acc_no}")
            print(f"Name: {user['name']}")
            print(f"DOB: {user['dob']}")
            print(f"City: {user['city']}")
            print(f"Contact: {user['contact']}")
            print(f"Email: {user['email']}")
            print(f"Address: {user['address']}")
            print(f"Balance: {user['balance']}")
            print(f"Active: {user['active']}")

    def login(self):
        print("\n--- Login ---")
        acc_no = input("Enter Account Number: ")
        password = input("Enter Password: ")

        user = self.users.get(acc_no)
        if not user or user['password'] != password:
            print("Invalid Account Number or Password.")
            return

        if not user['active']:
            print("Account is deactivated.")
            return

        print(f"Welcome {user['name']}!")
        while True:
            print("\n1. Show Balance\n2. Show Transactions\n3. Credit Amount\n4. Debit Amount\n"
                  "5. Transfer Amount\n6. Activate/Deactivate Account\n7. Change Password\n"
                  "8. Update Profile\n9. Logout")
            choice = input("Enter choice: ")

            if choice == "1":
                print(f"Balance: {user['balance']}")
            elif choice == "2":
                print("Transactions: ", user['transactions'])
            elif choice == "3":
                amount = int(input("Enter amount to credit: "))
                user['balance'] += amount
                user['transactions'].append(f"Credited: {amount}")
                print("Amount credited successfully.")
            elif choice == "4":
                amount = int(input("Enter amount to debit: "))
                if amount > user['balance']:
                    print("Insufficient balance.")
                else:
                    user['balance'] -= amount
                    user['transactions'].append(f"Debited: {amount}")
                    print("Amount debited successfully.")
            elif choice == "5":
                target_acc = input("Enter target account number: ")
                target_user = self.users.get(target_acc)
                if not target_user:
                    print("Target account not found.")
                    continue
                amount = int(input("Enter amount to transfer: "))
                if amount > user['balance']:
                    print("Insufficient balance.")
                else:
                    user['balance'] -= amount
                    target_user['balance'] += amount
                    user['transactions'].append(f"Transferred: {amount} to {target_acc}")
                    target_user['transactions'].append(f"Received: {amount} from {acc_no}")
                    print("Amount transferred successfully.")
            elif choice == "6":
                user['active'] = not user['active']
                print("Account status toggled.")
            elif choice == "7":
                new_password = input("Enter new password: ")
                if not self.validate_password(new_password):
                    print("Invalid password.")
                else:
                    user['password'] = new_password
                    print("Password changed successfully.")
            elif choice == "8":
                user['name'] = input("Enter new name: ")
                user['city'] = input("Enter new city: ")
                user['contact'] = input("Enter new contact: ")
                user['email'] = input("Enter new email: ")
                user['address'] = input("Enter new address: ")
                print("Profile updated successfully.")
            elif choice == "9":
                print("Logged out.")
                break
            else:
                print("Invalid choice.")

    def exit(self):
        print("Exiting... Goodbye!")
        sys.exit()

def main():
    system = BankingSystem()
    while True:
        print("\n1. Add User\n2. Show Users\n3. Login\n4. Exit")
        choice = input("Enter choice: ")

        if choice == "1":
            system.add_user()
        elif choice == "2":
            system.show_user()
        elif choice == "3":
            system.login()
        elif choice == "4":
            system.exit()
        else:
            print("Invalid choice.")

if __name__ == "__main__":
    main()
