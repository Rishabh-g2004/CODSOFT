import os

TASKS_FILE = 'tasks.txt'

def load_tasks():
    """Load tasks from a file."""
    if os.path.exists(TASKS_FILE):
        with open(TASKS_FILE, 'r') as file:
            return [line.strip() for line in file.readlines()]
    return []

def save_tasks(task_list):
    """Save tasks to a file."""
    with open(TASKS_FILE, 'w') as file:
        for task in task_list:
            file.write(f"{task}\n")

def display_menu():
    """Display the menu options."""
    print("\nTo-Do List Menu:")
    print("1. Add Task")
    print("2. View Tasks")
    print("3. Remove Task")
    print("4. Save Tasks")
    print("5. Load Tasks")
    print("6. Exit")

def add_task(task_list):
    """Add a new task to the list."""
    task = input("Enter the task: ")
    task_list.append(task)
    print(f"Task '{task}' added.")

def view_tasks(task_list):
    """Display all tasks in the list."""
    if not task_list:
        print("Your to-do list is empty.")
    else:
        print("\nYour To-Do List:")
        for index, task in enumerate(task_list, start=1):
            print(f"{index}. {task}")

def remove_task(task_list):
    """Remove a task from the list."""
    view_tasks(task_list)
    if task_list:
        try:
            task_number = int(input("Enter the number of the task to remove: "))
            if 1 <= task_number <= len(task_list):
                removed_task = task_list.pop(task_number - 1)
                print(f"Task '{removed_task}' removed.")
            else:
                print("Invalid task number.")
        except ValueError:
            print("Please enter a valid number.")

def main():
    task_list = load_tasks()
    while True:
        display_menu()
        choice = input("Choose an option (1-6): ")
        if choice == '1':
            add_task(task_list)
        elif choice == '2':
            view_tasks(task_list)
        elif choice == '3':
            remove_task(task_list)
        elif choice == '4':
            save_tasks(task_list)
            print("Tasks saved.")
        elif choice == '5':
            task_list = load_tasks()
            print("Tasks loaded.")
        elif choice == '6':
            print("Exiting the to-do list application.")
            break
        else:
            print("Invalid choice. Please select a number between 1 and 6.")

if __name__ == "__main__":
    main()
