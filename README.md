#making of a simple calculator
def calculator():
     num1 = float(input("Enter the first number: "))
     num2 = float(input("Enter the second number: "))

     print("choose an operation:" )
     print("1. Addition")
     print("2. Subtraction")
     print("3. Multiplication")
     print("4. Division")

     choice = int(input("enter your choice(1/2/3/4):"))

     if choice == 1:
         result = num1 + num2
         print(f"{num1} + {num2} = {result}")
     elif choice ==2:
         result = num1 - num2
         print(f"{num1} - {num2} = {result}")
     elif choice == 3:
         result = num1*num2
         print(f"{num1} * {num2} = {result}")
     elif choice ==4:
         if num2 !=0:
             result = num1/num2
             print(f"{num1} / {num2} = {result}")
         else:
              print("error: Division by zero is not allowed.")
     else :
        print("error: Invalid choice. ")
calculator()
# CODSFT
#code for contact book

import json
import os

CONTACTS_FILE = "contacts.json"

def load_contacts():
    if not os.path.exists(CONTACTS_FILE):
        return []
    with open(CONTACTS_FILE, "r") as file:
        return json.load(file)

def save_contacts(contacts):
    with open(CONTACTS_FILE, "w") as file:
        json.dump(contacts, file, indent=4)

def add_contact():
    name = input("Enter name: ").strip()
    phone = input("Enter phone number: ").strip()
    email = input("Enter email address: ").strip()

    contacts = load_contacts()
    contacts.append({"name": name, "phone": phone, "email": email})
    save_contacts(contacts)
    print(f"\nContact '{name}' added successfully!\n")

def view_contacts():
    contacts = load_contacts()
    if not contacts:
        print("\nNo contacts found.\n")
        return
    print("\n--- Contact List ---")
    for idx, contact in enumerate(contacts, 1):
        print(f"{idx}. Name: {contact['name']}, Phone: {contact['phone']}, Email: {contact['email']}")
    print()

def search_contact():
    keyword = input("Enter name or phone/email to search: ").strip().lower()
    contacts = load_contacts()
    results = [c for c in contacts if keyword in c['name'].lower() or keyword in c['phone'] or keyword in c['email']]
    
    if results:
        print("\n--- Search Results ---")
        for contact in results:
            print(f"Name: {contact['name']}, Phone: {contact['phone']}, Email: {contact['email']}")
        print()
    else:
        print("\nNo matching contact found.\n")

def update_contact():
    name_to_update = input("Enter the name of the contact to update: ").strip()
    contacts = load_contacts()
    for contact in contacts:
        if contact['name'].lower() == name_to_update.lower():
            print("Leave blank to keep existing value.")
            new_name = input(f"New name [{contact['name']}]: ") or contact['name']
            new_phone = input(f"New phone [{contact['phone']}]: ") or contact['phone']
            new_email = input(f"New email [{contact['email']}]: ") or contact['email']
            
            contact['name'] = new_name
            contact['phone'] = new_phone
            contact['email'] = new_email

            save_contacts(contacts)
            print("\nContact updated successfully!\n")
            return
    print("\nContact not found.\n")

def delete_contact():
    name_to_delete = input("Enter the name of the contact to delete: ").strip()
    contacts = load_contacts()
    new_contacts = [c for c in contacts if c['name'].lower() != name_to_delete.lower()]
    
    if len(contacts) == len(new_contacts):
        print("\nContact not found.\n")
    else:
        save_contacts(new_contacts)
        print(f"\nContact '{name_to_delete}' deleted successfully.\n")

def main_menu():
    while True:
        print("==== Contact Book Menu ====")
        print("1. Add Contact")
        print("2. View Contacts")
        print("3. Search Contact")
        print("4. Update Contact")
        print("5. Delete Contact")
        print("6. Exit")
        choice = input("Enter your choice (1-6): ").strip()

        if choice == "1":
            add_contact()
        elif choice == "2":
            view_contacts()
        elif choice == "3":
            search_contact()
        elif choice == "4":
            update_contact()
        elif choice == "5":
            delete_contact()
        elif choice == "6":
            print("Exiting Contact Book. Goodbye!")
            break
        else:
            print("Invalid choice. Please enter a number between 1 and 6.\n")

if __name__ == "__main__":
    main_menu()
import json
import os

TODO_FILE = "todo_list.json"

def load_tasks():
    if os.path.exists(TODO_FILE):
        with open(TODO_FILE, "r") as f:
            return json.load(f)
    return []

def save_tasks(tasks):
    with open(TODO_FILE, "w") as f:
        json.dump(tasks, f, indent=2)

def list_tasks(tasks):
    if not tasks:
        print("Your to-do list is empty.")
    else:
        for i, task in enumerate(tasks, 1):
            status = "✓" if task['done'] else "✗"
            print(f"{i}. [{status}] {task['title']}")

def add_task(tasks):
    title = input("Enter the task title: ")
    tasks.append({"title": title, "done": False})
    print("Task added.")

def mark_task_done(tasks):
    list_tasks(tasks)
    try:
        index = int(input("Enter task number to mark as done: ")) - 1
        tasks[index]['done'] = True
        print("Task marked as done.")
    except (IndexError, ValueError):
        print("Invalid task number.")

def delete_task(tasks):
    list_tasks(tasks)
    try:
        index = int(input("Enter task number to delete: ")) - 1
        removed = tasks.pop(index)
        print(f"Task '{removed['title']}' deleted.")
    except (IndexError, ValueError):
        print("Invalid task number.")

def main():
    tasks = load_tasks()

    while True:
        print("\n==== TO-DO LIST ====")
        print("1. View Tasks")
        print("2. Add Task")
        print("3. Mark Task as Done")
        print("4. Delete Task")
        print("5. Exit")
        choice = input("Choose an option: ")

        if choice == "1":
            list_tasks(tasks)
        elif choice == "2":
            add_task(tasks)
        elif choice == "3":
            mark_task_done(tasks)
        elif choice == "4":
            delete_task(tasks)
        elif choice == "5":
            save_tasks(tasks)
            print("Goodbye!")
            break
        else:
            print("Invalid option.")

if __name__ == "__main__":
    main()




