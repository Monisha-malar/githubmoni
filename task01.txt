import json

# Function to add a task
def add_task(tasks, title, description, priority):
    new_task = {
        "id": len(tasks) + 1,
        "title": title,
        "description": description,
        "priority": priority,
        "status": "Pending"
    }
    tasks.append(new_task)
    print("Task added successfully!")

# Function to view tasks
def view_tasks(tasks):
    if not tasks:
        print("No tasks available.")
        return
    print("\nID | Title           | Priority | Status    | Description")
    print("-" * 60)
    for task in tasks:
        print(f"{task['id']:>2} | {task['title'][:15]:<15} | {task['priority']:<8} | {task['status']:<9} | {task['description']}")

# Function to update a task
def update_task(tasks, task_id, status=None, priority=None):
    for task in tasks:
        if task["id"] == task_id:
            if status:
                task["status"] = status
            if priority:
                task["priority"] = priority
            print("Task updated successfully!")
            return
    print("Task not found.")

# Function to delete a task
def delete_task(tasks, task_id):
    initial_count = len(tasks)
    tasks[:] = [task for task in tasks if task["id"] != task_id]
    if len(tasks) < initial_count:
        print("Task deleted successfully!")
    else:
        print("Task not found.")

# Function to save tasks to a file
def save_tasks_to_file(tasks, filename="tasks.json"):
    with open(filename, "w") as f:
        json.dump(tasks, f)
    print("Tasks saved successfully!")

# Function to load tasks from a file
def load_tasks_from_file(filename="tasks.json"):
    try:
        with open(filename, "r") as f:
            return json.load(f)
    except FileNotFoundError:
        return []

# Main menu function
def main():
    tasks = load_tasks_from_file()
    while True:
        print("\nTo-Do List Menu")
        print("1. Add Task")
        print("2. View Tasks")
        print("3. Update Task")
        print("4. Delete Task")
        print("5. Save and Exit")
        choice = input("Choose an option: ")

        if choice == "1":
            title = input("Enter task title: ")
            description = input("Enter task description: ")
            priority = input("Enter task priority (High/Medium/Low): ")
            add_task(tasks, title, description, priority)
        elif choice == "2":
            view_tasks(tasks)
        elif choice == "3":
            try:
                task_id = int(input("Enter task ID to update: "))
                status = input("Enter new status (Pending/Completed) or press Enter to skip: ")
                priority = input("Enter new priority (High/Medium/Low) or press Enter to skip: ")
                update_task(tasks, task_id, status if status else None, priority if priority else None)
            except ValueError:
                print("Invalid input. Please enter a valid task ID.")
        elif choice == "4":
            try:
                task_id = int(input("Enter task ID to delete: "))
                delete_task(tasks, task_id)
            except ValueError:
                print("Invalid input. Please enter a valid task ID.")
        elif choice == "5":
            save_tasks_to_file(tasks)
            print("Goodbye!")
            break
        else:
            print("Invalid choice. Please try again.")

# Run the application
if __name__ == "__main__":
    main()
