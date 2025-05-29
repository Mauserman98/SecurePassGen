# SecurePassGen
A secure offline password generator with a simple GUI. Built using Python and tkinter, it uses the secrets module for strong password generation and stores the last 10 passwords in memory (not saved). Passwords are copied to clipboard automatically. No data is stored or sent online.




Source


    import secrets #import string and secrets module for secure random generation
    import pyperclip
    import tkinter as tk
    from tkinter import messagebox
    
    
    last_password = [] # List to store previously generated passwords, List is deleted once the program is closed.
    
    
    # This script generates a random password of a specified length and copies it to the clipboard.
    
    #define Password Generator Logic
    
    def generate_password():
        try:
            password_length = int(entry.get())
        
            if password_length < 8:
                print('Please use more than 8 characters.')
        
            else:
                characters = "abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789!@#$%^&*()_+-=[]{}|;:,.<>?/" #define characters used in password generation
                password = ''.join(secrets.choice(characters) for _ in range(password_length)) #generate password using secrets module for cryptographic security
                
                last_password.append(password)
                if len(last_password) > 10:
                    last_password.pop(0)
                
                # Copy the password to the clipboard automatically
                pyperclip.copy(password)
                
                messagebox.showinfo("Generated Password", f"Your password: {password}\n\nCopied to clipboard!")
        except ValueError:
            messagebox.showerror("Error", "Please enter a valid number for password length")
            
    
    def show_last_passwords(): # Function to display the last generated passwords
        if last_password:
            messagebox.showinfo("Last Generated Passwords", "\n---\n".join(last_password))
        else:
            messagebox.showinfo("Last Generated Passwords", "No passwords generated yet.")
    
    
    #add a gui
    root = tk.Tk()
    root.title("Random Password Generator")
    
    
    #gui menu
    label = tk.Label(root, text="Enter password length. More then 8 characters: \nPassword Generator uses secure random generation with secrets module. \nGenerated password will be copied to clipboard. \nLast 10 generated passwords will be stored in memory and deleted when the program is closed. \nYou can view them by clicking the button below. \nPlease use responsibly. Passwords are not 100% hackproof!")
    label.pack(pady=10)
    entry = tk.Entry(root)
    entry.pack(pady=10)
    
    
    # Button to generate password
    generate_button = tk.Button(root, text="Generate Password", command=generate_password)
    generate_button.pack(pady=20)
    
    # Button to view last generated passwords
    view_last_button = tk.Button(root, text="View Last Generated Passwords", command=show_last_passwords)
    view_last_button.pack(pady=10)

# Run the GUI
root.mainloop()


