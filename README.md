import tkinter as tk
from tkinter import messagebox
import re

def check_password():
    password = password_entry.get()

    if password == "":
        messagebox.showwarning("Warning", "Please enter a password")
        return

    score = 0
    feedback = []

    # Length check
    if len(password) >= 8:
        score += 1
    else:
        feedback.append("Use at least 8 characters")

    # Uppercase check
    if re.search(r"[A-Z]", password):
        score += 1
    else:
        feedback.append("Add an uppercase letter")

    # Lowercase check
    if re.search(r"[a-z]", password):
        score += 1
    else:
        feedback.append("Add a lowercase letter")

    # Number check
    if re.search(r"[0-9]", password):
        score += 1
    else:
        feedback.append("Add a number")

    # Special character check
    if re.search(r"[^A-Za-z0-9]", password):
        score += 1
    else:
        feedback.append("Add a special character")

    # Display result
    if score <= 2:
        result = "Weak Password"
    elif score <= 4:
        result = "Medium Password"
    else:
        result = "Strong Password"

    result_label.config(text=result)

    if feedback:
        messagebox.showinfo(
            "Password Analysis",
            result + "\n\nSuggestions:\n" + "\n".join(feedback)
        )
    else:
        messagebox.showinfo(
            "Password Analysis",
            result + "\n\nYour password meets all basic requirements!"
        )


# Main window
root = tk.Tk()
root.title("Password Checker Analysis")
root.geometry("450x300")

title = tk.Label(
    root,
    text="Password Checker Analysis",
    font=("Arial", 18, "bold")
)
title.pack(pady=20)

tk.Label(root, text="Enter Password:").pack()

password_entry = tk.Entry(root, width=35, show="*")
password_entry.pack(pady=10)

check_button = tk.Button(
    root,
    text="Check Password",
    command=check_password
)
check_button.pack(pady=10)

result_label = tk.Label(
    root,
    text="",
    font=("Arial", 14, "bold")
)
result_label.pack(pady=20)

root.mainloop()
