import os

PHONEBOOK_FILE = "phonebook.txt"

def load_phonebook():
    phonebook = {}
    if os.path.exists(PHONEBOOK_FILE):
        with open(PHONEBOOK_FILE, 'r') as file:
            for line in file:
                name, number = line.strip().split(',')
                phonebook[name] = number
    return phonebook
def save_phonebook(phonebook):
    with open(PHONEBOOK_FILE, 'w') as file:
        for name, number in phonebook.items():
            file.write(f"{name},{number}\n")
def add_entry(phonebook):
    name = input("Enter the name: ").strip()
    if name in phonebook:
        print(f"{name} is already in the phone book.")
    else:
        number = input("Enter the phone number: ").strip()
        phonebook[name] = number
        print(f"Added {name} to the phone book.")
def delete_entry(phonebook):
    name = input("Enter the name to delete: ").strip()
    if name in phonebook:
        del phonebook[name]
        print(f"Deleted {name} from the phone book.")
    else:
        print(f"{name} was not found in the phone book.")
def change_number(phonebook):
    name = input("Enter the name to change the number for: ").strip()
    if name in phonebook:
        new_number = input(f"Enter the new phone number for {name}: ").strip()
        phonebook[name] = new_number
        print(f"Updated {name}'s phone number.")
    else:
        print(f"{name} was not found in the phone book.")
def display_phonebook(phonebook):
    if phonebook:
        print("\nPhone Book Entries:")
        for name, number in phonebook.items():
            print(f"{name}: {number}")
    else:
        print("\nPhone book is empty.")
def main_menu():
    phonebook = load_phonebook()

    while True:
        print("\nPhone Book Menu:")
        print("1. Enter new entry")
        print("2. Delete an existing one")
        print("3. Change phone number")
        print("4. Display the phone book")
        print("5. Exit")

        choice = input("Choose an option (1-5): ").strip()

        if choice == '1':
            add_entry(phonebook)
        elif choice == '2':
            delete_entry(phonebook)
        elif choice == '3':
            change_number(phonebook)
        elif choice == '4':
            display_phonebook(phonebook)
        elif choice == '5':
            save_phonebook(phonebook)
            print("Exiting the program. Phone book saved.")
            break
        else:
            print("Invalid option. Please choose a valid number from the menu.")
if __name__ == "__main__":
    main_menu()
