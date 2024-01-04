import tkinter as tk
import datetime

# Dictionary to store student information
students = {}

# Dictionary to store attendance records
attendance_records = {}

def add_student():
    student_id = input("Enter student ID: ")
    student_name = input("Enter student name: ")
    subject = input("Enter subject: ")

    students[student_id] = {'name': student_name, 'subject': subject}
    attendance_records[student_id] = {}

    print(f"\nStudent {student_name} with ID {student_id} registered successfully.")

def mark_attendance():
    student_id = input("Enter student ID: ")

    if student_id in students:
        date = datetime.date.today().strftime("%Y-%m-%d")
        
        if date not in attendance_records[student_id]:
            attendance_choice = input("Mark attendance (P for Present, A for Absent): ").upper()

            if attendance_choice == 'P':
                attendance_records[student_id][date] = 'Present'
                print(f"Attendance marked for {students[student_id]['name']} on {date}: Present")
            elif attendance_choice == 'A':
                attendance_records[student_id][date] = 'Absent'
                print(f"Attendance marked for {students[student_id]['name']} on {date}: Absent")
            else:
                print("Invalid choice. Please enter 'P' or 'A'.")
        else:
            print(f"Attendance for {students[student_id]['name']} on {date} already marked.")
    else:
        print("Student not found in records. Please register the student first.")

def view_students():
    print("\nRegistered Students:")
    for student_id, student_info in students.items():
        print(f"ID: {student_id}, Name: {student_info['name']}, Subject: {student_info['subject']}")

def view_attendance():
    student_id = input("Enter student ID to view attendance: ")

    if student_id in students:
        print("\nAttendance Records:")
        for date, status in attendance_records[student_id].items():
            print(f"{date}: {status}")
    else:
        print("Student not found in records. Please register the student first.")

def main_menu():
    while True:
        print("\nStudent Attendance System")
        print("1. Add Student")
        print("2. Mark Attendance")
        print("3. View Registered Students")
        print("4. View Attendance")
        print("5. Exit")

        choice = input("Enter your choice (1-5): ")

        if choice == '1':
            add_student()
        elif choice == '2':
            mark_attendance()
        elif choice == '3':
            view_students()
        elif choice == '4':
            view_attendance()
        elif choice == '5':
            print("Exiting the program. Goodbye!")
            break
        else:
            print("Invalid choice. Please enter a number between 1 and 5.")


def validate_login(username, password):
    # Replace this with your authentication logic
    return username == "admin" and password == "password"

def login():
    entered_username = username_entry.get()
    entered_password = password_entry.get()

    if validate_login(entered_username, entered_password):
        login_frame.pack_forget()
        show_terminal_page()
    else:
        print("registration is succsefully.")

def show_terminal_page():
    terminal_frame.pack(padx=20, pady=20)

    # Terminal-like content
    terminal_content = "Welcome, Admin!\n"
    terminal_content += "You are now on the terminal page."
    
    print(terminal_content)

# Main Tkinter window
root = tk.Tk()
root.title("Admin Login")

# Login Frame
login_frame = tk.Frame(root)
login_frame.pack(padx=20, pady=20)

username_label = tk.Label(login_frame, text="Username:")
username_label.grid(row=0, column=0, sticky="e")

username_entry = tk.Entry(login_frame)
username_entry.grid(row=0, column=1)

password_label = tk.Label(login_frame, text="Password:")
password_label.grid(row=1, column=0, sticky="e")

password_entry = tk.Entry(login_frame, show="*")
password_entry.grid(row=1, column=1)
