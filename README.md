import os
import json

# File to save tasks
FILE_NAME = "todo_list.json"

# Load tasks from file
def load_tasks():
    if os.path.exists(FILE_NAME):
        with open(FILE_NAME, "r") as file:
            return json.load(file)
    return []

# Save tasks to file
def save_tasks(tasks):
    with open(FILE_NAME, "w") as file:
        json.dump(tasks, file, indent=4)

# Add a new task
def add_task(tasks):
    task = input("Enter the task: ")
    tasks.append({"task": task, "completed": False})
    print("Task added!")

# View all tasks
def view_tasks(tasks):
    if not tasks:
        print("No tasks found.")
        return

    for index, task in enumerate(tasks, start=1):
        status = "Done" if task["completed"] else "Not Done"
        print(f"{index}. {task['task']} - {status}")

# Update a task
def update_task(tasks):
    view_tasks(tasks)
    task_index = int(input("Enter the task number to update: ")) - 1

    if 0 <= task_index < len(tasks):
        task = tasks[task_index]
        new_task = input(f"Enter new task description (leave empty to keep '{task['task']}'): ")
        if new_task:
            task["task"] = new_task
        task["completed"] = input("Is the task completed? (yes/no): ").strip().lower() == "yes"
        print("Task updated!")
    else:
        print("Invalid task number.")

# Delete a task
def delete_task(tasks):
    view_tasks(tasks)
    task_index = int(input("Enter the task number to delete: ")) - 1

    if 0 <= task_index < len(tasks):
        tasks.pop(task_index)
        print("Task deleted!")
    else:
        print("Invalid task number.")

# Main function
def main():
    tasks = load_tasks()

    while True:
        print("\nTo-Do List Application")
        print("1. Add Task")
        print("2. View Tasks")
        print("3. Update Task")
        print("4. Delete Task")
        print("5. Exit")
        choice = input("Enter your choice: ").strip()

        if choice == "1":
            add_task(tasks)
        elif choice == "2":
            view_tasks(tasks)
        elif choice == "3":
            update_task(tasks)
        elif choice == "4":
            delete_task(tasks)
        elif choice == "5":
            save_tasks(tasks)
            print("Tasks saved. Exiting...")
            break
        else:
            print("Invalid choice. Please try again.")

if _name_ == "_main_":
    main()
