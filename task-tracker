# sql
import sqlite3

# ==============================
# Database Setup
# ==============================
conn = sqlite3.connect("task_tracker.db")
cursor = conn.cursor()

cursor.execute("""
CREATE TABLE IF NOT EXISTS tasks (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    title TEXT NOT NULL,
    status TEXT DEFAULT 'Pending'
)
""")
conn.commit()

# ==============================
# CRUD Functions
# ==============================
def add_task(title):
    cursor.execute("INSERT INTO tasks (title) VALUES (?)", (title,))
    conn.commit()
    print(f"✅ Task '{title}' added.")


def view_tasks():
    cursor.execute("SELECT * FROM tasks")
    tasks = cursor.fetchall()
    if not tasks:
        print("⚠️ No tasks found.")
    else:
        print("\nYour Tasks:")
        print("-" * 30)
        for task in tasks:
            print(f"[{task[0]}] {task[1]} - {task[2]}")
        print("-" * 30)


def update_task(task_id, status):
    cursor.execute("UPDATE tasks SET status = ? WHERE id = ?", (status, task_id))
    conn.commit()
    print(f"🔄 Task {task_id} updated to '{status}'.")


def delete_task(task_id):
    cursor.execute("DELETE FROM tasks WHERE id = ?", (task_id,))
    conn.commit()
    print(f"🗑️ Task {task_id} deleted.")


# ==============================
# CLI Menu
# ==============================
def main():
    while True:
        print("\n=== Task Tracker ===")
        print("1. Add Task")
        print("2. View Tasks")
        print("3. Mark Task as Completed")
        print("4. Delete Task")
        print("5. Exit")

        choice = input("Enter choice (1-5): ")

        if choice == "1":
            title = input("Enter task title: ")
            add_task(title)

        elif choice == "2":
            view_tasks()

        elif choice == "3":
            task_id = int(input("Enter task ID to mark completed: "))
            update_task(task_id, "Completed")

        elif choice == "4":
            task_id = int(input("Enter task ID to delete: "))
            delete_task(task_id)

        elif choice == "5":
            print("👋 Exiting... Goodbye!")
            break

        else:
            print("❌ Invalid choice. Please try again.")


if __name__ == "__main__":
    main()
