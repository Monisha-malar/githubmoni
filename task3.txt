class Contact:
    def __init__(self, name, phone, email, address):
        self.name = name
        self.phone = phone
        self.email = email
        self.address = address

class ContactManager:
    def __init__(self):
        self.contacts = []

    def add_contact(self):
        print("Add New Contact")
        name = input("Enter name: ").strip()
        phone = input("Enter phone number: ").strip()
        email = input("Enter email: ").strip()
        address = input("Enter address: ").strip()
        new_contact = Contact(name, phone, email, address)
        self.contacts.append(new_contact)
        print("Contact added successfully!\n")

    def view_contacts(self):
        if not self.contacts:
            print("No contacts found.\n")
            return
        print("Contact List:")
        for idx, contact in enumerate(self.contacts, start=1):
            print(f"{idx}. {contact.name} - {contact.phone}")
        print()

    def search_contact(self):
        query = input("Enter name or phone number to search: ").strip().lower()
        results = [contact for contact in self.contacts if query in contact.name.lower() or query in contact.phone]
        if results:
            print("Search Results:")
            for contact in results:
                print(f"Name: {contact.name}, Phone: {contact.phone}, Email: {contact.email}, Address: {contact.address}")
            print()
        else:
            print("No matching contacts found.\n")

    def update_contact(self):
        query = input("Enter the name of the contact to update: ").strip().lower()
        for contact in self.contacts:
            if contact.name.lower() == query:
                print("Leave a field blank to keep the current value.")
                contact.name = input(f"Enter new name ({contact.name}): ").strip() or contact.name
                contact.phone = input(f"Enter new phone number ({contact.phone}): ").strip() or contact.phone
                contact.email = input(f"Enter new email ({contact.email}): ").strip() or contact.email
                contact.address = input(f"Enter new address ({contact.address}): ").strip() or contact.address
                print("Contact updated successfully!\n")
                return
        print("Contact not found.\n")

    def delete_contact(self):
        query = input("Enter the name of the contact to delete: ").strip().lower()
        for contact in self.contacts:
            if contact.name.lower() == query:
                self.contacts.remove(contact)
                print("Contact deleted successfully!\n")
                return
        print("Contact not found.\n")

    def run(self):
        while True:
            print("Contact Manager")
            print("1. Add Contact")
            print("2. View Contact List")
            print("3. Search Contact")
            print("4. Update Contact")
            print("5. Delete Contact")
            print("6. Exit")
            choice = input("Enter your choice: ").strip()

            if choice == '1':
                self.add_contact()
            elif choice == '2':
                self.view_contacts()
            elif choice == '3':
                self.search_contact()
            elif choice == '4':
                self.update_contact()
            elif choice == '5':
                self.delete_contact()
            elif choice == '6':
                print("Exiting Contact Manager. Goodbye!")
                break
            else:
                print("Invalid choice. Please try again.\n")

if __name__ == "__main__":
    manager = ContactManager()
    manager.run()
