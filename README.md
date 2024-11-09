# Codsoft-Task-1
import os

# Define the file to store tasks
TASKS_FILE = "tasks.txt"

# Load tasks from the file
def load_tasks():
    tasks = []
    if os.path.exists(TASKS_FILE):
        with open(TASKS_FILE, 'r') as f:
            tasks = f.readlines()
    return tasks

# Save tasks to the file
def save_tasks(tasks):
    with open(TASKS_FILE, 'w') as f:
        f.writelines(tasks)

# Display the to-do list
def display_tasks(tasks):
    if not tasks:
        print("No tasks in the list.")
    else:
        for idx, task in enumerate(tasks, 1):
            task = task.strip()
            status = "✔" if task.endswith("[x]\n") else "✘"
            print(f"{idx}. {task[:-4]} {status}")

# Add a new task
def add_task(tasks, task):
    tasks.append(task + "\n")
    save_tasks(tasks)

# Delete a task
def delete_task(tasks, task_number):
    try:
        del tasks[task_number - 1]
        save_tasks(tasks)
    except IndexError:
        print("Task number is out of range.")

# Mark a task as completed
def mark_completed(tasks, task_number):
    try:
        task = tasks[task_number - 1].strip()
        if not task.endswith("[x]"):
            tasks[task_number - 1] = task + " [x]\n"
            save_tasks(tasks)
        else:
            print("Task is already completed.")
    except IndexError:
        print("Task number is out of range.")

# Main menu
def show_menu():
    print("\nTo-Do List:")
    print("1. View tasks")
    print("2. Add task")
    print("3. Delete task")
    print("4. Mark task as completed")
    print("5. Exit")

# Main function
def main():
    tasks = load_tasks()

    while True:
        show_menu()
        choice = input("Enter your choice: ")

        if choice == "1":
            display_tasks(tasks)
        elif choice == "2":
            new_task = input("Enter the task description: ")
            add_task(tasks, new_task)
        elif choice == "3":
            display_tasks(tasks)
            task_number = int(input("Enter task number to delete: "))
            delete_task(tasks, task_number)
        elif choice == "4":
            display_tasks(tasks)
            task_number = int(input("Enter task number to mark as completed: "))
            mark_completed(tasks, task_number)
        elif choice == "5":
            print("Goodbye!")
            break
        else:
            print("Invalid choice. Please try again.")

if __name__ == "__main__":
    main()
