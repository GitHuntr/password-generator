# NECESSARY MODULES

```python
# Import necessary libraries
from tkinter import *                   # Imports everything from the tkinter library
from tkinter import messagebox          # Import the messagebox module from tkinter
from random import randint, choice, shuffle  # Import specific functions from the random module
import pyperclip                        # Import the pyperclip library for clipboard operations
import json                             # Import the json module for working with JSON data
```

Here's a brief description of each import:

- `tkinter`: This is Python's standard GUI (Graphical User Interface) library. It allows you to create windows, buttons, labels, and more.
- `messagebox`: This is a submodule of tkinter used to display message boxes for showing messages or getting simple inputs.
- `random`: This module provides functions to generate random numbers, sequences, and more.
  - `randint`: Used to generate random integers.
  - `choice`: Used to choose a random element from a sequence.
  - `shuffle`: Used to shuffle a sequence in-place.
- `pyperclip`: This library allows you to easily copy and paste text to and from the clipboard.
- `json`: This module provides functions for encoding and decoding JSON data.


# searchPass()

```python
def searchPass():
    try:
        # Open the 'passwords.json' file for reading
        with open('passwords.json', 'r') as file:
            # Load the JSON data from the file into the 'data' variable
            data = json.load(file)
            
            # Get the website name from the 'website_field' Text widget
            website = website_field.get("1.0", END)[:-1]
            
            # Check if the website is in the loaded JSON data
            if website in data:
                # If the website is found, get the password and email associated with it
                password = data[website]["password"]
                email = data[website]["email"]
                
                # Show an information message box with the email and password
                messagebox.showinfo(title=website, message=f"Email: {email}\nPassword: {password}")
            else:
                # If the website is not found, show a warning message box
                warning = messagebox.showwarning(title="Warning", message=f"There is no password stored for {website} website")
    
    # Handle the case where the 'passwords.json' file is not found
    except FileNotFoundError:
        warning = messagebox.showwarning(title="Warning", message="No file found")
```

Here's a breakdown of what each part does:

1. The `try` block is used to catch exceptions that might occur during the execution of the code within it.

2. `with open('passwords.json', 'r') as file:`: This opens the 'passwords.json' file in read mode (`'r'`). The `with` statement ensures that the file is properly closed after its suite finishes.

3. `data = json.load(file)`: This loads the JSON data from the opened file into the `data` variable.

4. `website = website_field.get("1.0", END)[:-1]`: This gets the text from the `website_field` Text widget. `"1.0"` means "line 1, character 0", and `END` means the end of the text. `[:-1]` is used to remove the trailing newline character.

5. `if website in data:`: This checks if the `website` is a key in the `data` dictionary loaded from the JSON file.

6. If the `website` is found in the `data`:
   - `password = data[website]["password"]`: This gets the password associated with the `website` from the `data` dictionary.
   - `email = data[website]["email"]`: This gets the email associated with the `website` from the `data` dictionary.
   - `messagebox.showinfo(...)`: This displays an information message box showing the email and password associated with the `website`.

7. If the `website` is not found in the `data`:
   - `messagebox.showwarning(...)`: This displays a warning message box indicating that there is no password stored for the `website`.

8. The `except FileNotFoundError:` block catches the `FileNotFoundError` exception that might occur if the 'passwords.json' file is not found. It displays a warning message box indicating that no file was found.

This function is designed to search for a password in the 'passwords.json' file based on the website entered by the user in the `website_field`. If the website is found, it displays the associated email and password in an information message box. If the website is not found, it displays a warning message box. If the 'passwords.json' file is not found, it displays a warning message box indicating the absence of the file.

# generatePass()

```python
def generatePass():
    # Delete any old password from the password field
    passwordField.delete("1.0", END)

    # Generate a new password
    letters = ['a', 'b', 'c', 'd', 'e', 'f', 'g', 'h', 'i', 'j', 'k', 'l', 'm', 'n', 'o', 'p', 'q', 'r', 's', 't', 'u', 'v', 'w', 'x', 'y', 'z', 'A', 'B', 'C', 'D', 'E', 'F', 'G', 'H', 'I', 'J', 'K', 'L', 'M', 'N', 'O', 'P', 'Q', 'R', 'S', 'T', 'U', 'V', 'W', 'X', 'Y', 'Z']
    numbers = ['0', '1', '2', '3', '4', '5', '6', '7', '8', '9']
    symbols = ['!', '#', '$', '%', '&', '(', ')', '*', '+']

    # Create an empty list to store the characters of the password
    password_list = []

    # Add random letters to the password list (8 to 10 letters)
    password_list += [choice(letters) for _ in range(randint(8, 10))]

    # Add random symbols to the password list (5 to 6 symbols)
    password_list += [choice(symbols) for _ in range(randint(5, 6))]

    # Add random numbers to the password list (3 to 5 numbers)
    password_list += [choice(numbers) for _ in range(randint(3, 5))]

    # Shuffle the password list to mix the characters
    shuffle(password_list)

    # Join the characters in the password list to create the password
    password = ''.join(password_list)

    # Insert the generated password into the password field
    passwordField.insert(END, password)

    # Copy the password to the clipboard
    pyperclip.copy(password)
```

Here's what each part does:

1. `passwordField.delete("1.0", END)`: Clears any existing text in the `passwordField`, which is likely a tkinter Text widget used for displaying the generated password.

2. `letters`, `numbers`, and `symbols`: These are lists containing characters to be used in generating the password—letters, numbers, and symbols.

3. `password_list = []`: Creates an empty list to store the characters of the generated password.

4. `password_list += [choice(letters) for _ in range(randint(8, 10))]`: Adds 8 to 10 random letters to the `password_list`.

5. `password_list += [choice(symbols) for _ in range(randint(5, 6))]`: Adds 5 to 6 random symbols to the `password_list`.

6. `password_list += [choice(numbers) for _ in range(randint(3, 5))]`: Adds 3 to 5 random numbers to the `password_list`.

7. `shuffle(password_list)`: Shuffles the characters in `password_list` to mix them up.

8. `password = ''.join(password_list)`: Joins the characters in `password_list` into a single string to form the generated password.

9. `passwordField.insert(END, password)`: Inserts the generated password into the `passwordField`, likely displaying it to the user.

10. `pyperclip.copy(password)`: Copies the generated password to the clipboard, allowing the user to easily paste it elsewhere.

This function is designed to generate a random password with a mix of letters, numbers, and symbols, display it in a tkinter Text widget (`passwordField`), and copy it to the clipboard for easy use.


# savePass()


```python
def savePass():
    # Get the text from the website, email, and password fields
    website = website_field.get("1.0", END)
    email = emailField.get("1.0", END)
    password = passwordField.get("1.0", END)

    # Create a new dictionary with website as key and email/password as values
    new_data = {
        website[:-1]: {
            "email": email[:-1],       # Remove the trailing newline character
            "password": password[:-1]  # Remove the trailing newline character
        }
    }

    # Check if any of the fields are empty
    if len(website) == 1 or len(password) == 1:
        # Show a warning message if any field is empty
        warning = messagebox.showwarning(title="Warning", message="You left one or more fields empty!")
    else:
        # Ask for confirmation to save the details
        is_ok = messagebox.askokcancel(title=website, message=f"These are the details entered: \nEmail: {email}Password: {password} \nIs it ok to save?")

        if is_ok:
            try:
                with open('passwords.json', 'r') as file:
                    # Read existing data from the 'passwords.json' file
                    data = json.load(file)
                    # Update the data with the new entry
                    data.update(new_data)
            except FileNotFoundError:
                # If the file doesn't exist, use the new_data as the initial data
                data = new_data
            finally:
                with open('passwords.json', 'w') as file:
                    # Write the updated data back to the 'passwords.json' file
                    json.dump(data, file, indent=4)
                
                # Clear the website and password fields after saving
                website_field.delete("1.0", END)
                passwordField.delete("1.0", END)
```

Here's a breakdown of what each part does:

1. `website = website_field.get("1.0", END)`: Gets the text from the `website_field` Text widget, likely containing the website name.

2. `email = emailField.get("1.0", END)`: Gets the text from the `emailField` Text widget, likely containing the email.

3. `password = passwordField.get("1.0", END)`: Gets the text from the `passwordField` Text widget, likely containing the password.

4. `new_data`: Creates a new dictionary with the website as the key and a nested dictionary with email and password as values.

5. Checks if any of the fields are empty:
   - `if len(website) == 1 or len(password) == 1:`: This condition checks if the length of `website` or `password` is 1, which usually means they are empty.

6. If any field is empty, it shows a warning message:
   - `warning = messagebox.showwarning(...)`: Displays a warning message box if any field is empty.

7. If all fields are filled, it asks for confirmation to save the details:
   - `is_ok = messagebox.askokcancel(...)`: Displays a confirmation message box with the entered details.

8. If the user confirms to save (`is_ok` is `True`), it updates the JSON data:
   - It tries to open the 'passwords.json' file for reading.
   - If the file exists, it reads the existing data from the file using `json.load(file)`.
   - It updates the existing data with the new entry using `data.update(new_data)`.

9. If the 'passwords.json' file doesn't exist, it uses the `new_data` as the initial data.

10. Finally, it writes the updated data back to the 'passwords.json' file:
    - `json.dump(data, file, indent=4)`: Writes the updated `data` dictionary back to the file with an indentation of 4 spaces.

11. It then clears the `website_field` and `passwordField` after saving, likely preparing for the next entry.

This function is designed to save the website, email, and password entered by the user into a JSON file named 'passwords.json'. Before saving, it checks if any field is empty and asks for confirmation from the user. If the file already exists, it updates the existing data with the new entry; otherwise, it creates a new file with the new entry.


# Creating the UI

```python
# Create the main window
window = Tk()
window.title("Password Manager")  # Set the title of the window
window.config(padx=20, pady=20)  # Add padding to the window

# Create a Canvas widget for the logo
c = Canvas(width=200, height=200)
logoimg = PhotoImage(file="logo.png")  # Load the logo image
c.create_image(60, 100, image=logoimg)  # Place the logo image on the canvas
c.grid(row=0, column=1)  # Grid placement of the canvas

# Labels and Text Entry for Website
website_label = Label(window, text="Website:")  # Create a label for website
website_label.grid(row=1, column=0)  # Grid placement of the website label

website_field = Text(window, height=1, width=20)  # Create a text entry for website
website_field.grid(row=1, column=1, sticky='w')  # Grid placement of the website text entry
website_field.focus()  # Set focus to the website text entry

# Labels and Text Entry for Email/Username
emailLabel = Label(window, text="Email/Username: ")  # Create a label for email
emailLabel.grid(row=2, column=0)  # Grid placement of the email label

emailField = Text(window, height=1, width=40)  # Create a text entry for email
emailField.insert(END, "upesddn@gmail.com")  # Insert a default email
emailField.grid(row=2, column=1)  # Grid placement of the email text entry

# Labels and Text Entry for Password
passwordLabel = Label(window, text="Password:")  # Create a label for password
passwordLabel.grid(row=3, column=0)  # Grid placement of the password label

passwordField = Text(window, height=1, width=20)  # Create a text entry for password
passwordField.grid(row=3, column=1, sticky="w")  # Grid placement of the password text entry

# Button to Generate Password
generate_button = Button(window, text="Generate Password", command=generatePass, height=1, width=20)
generate_button.grid(row=3, column=1, sticky="e")  # Grid placement of the generate password button

# Button to Add Password
add_button = Button(window, text="Add", command=savePass, height=1, width=45)  # Create a button to add password
add_button.grid(row=4, column=1)  # Grid placement of the add button

# Button to Search for Password
search_button = Button(window, text="Search", command=searchPass, height=1, width=20)  # Create a button to search for password
search_button.grid(row=1, column=1, sticky="e")  # Grid placement of the search button

window.mainloop()  # Start the main event loop for the window
```
Here's a basic explanation of the code:

1. **Creating the Window and Setting Up**:
   - The `Tk()` function creates the main window for the application.
   - `window.title("Password Manager")` sets the title of the window to "Password Manager".
   - `window.config(padx=20, pady=20)` adds padding of 20 pixels to the x and y directions inside the window.

2. **Adding the Logo**:
   - A `Canvas` widget named `c` is created with a width and height of 200 pixels.
   - The logo image (`logo.png`) is loaded using `PhotoImage`.
   - The logo image is placed on the canvas at coordinates (60, 100).
   - The canvas (`c`) is placed in the grid at row 0, column 1.

3. **Text Entries and Labels**:
   - `website_label` is a label with the text "Website:".
   - `website_field` is a text entry widget for the user to input the website.
     - It is placed in the grid at row 1, column 1.
     - The `sticky='w'` option means it will stick to the west (left) side of its cell.
     - `website_field.focus()` sets the focus to this field when the window opens.
   - `emailLabel` is a label with the text "Email/Username:".
   - `emailField` is a text entry widget for the user to input the email or username.
     - It has a default value of "upesddn@gmail.com" inserted into it.
     - It is placed in the grid at row 2, column 1.
   - `passwordLabel` is a label with the text "Password:".
   - `passwordField` is a text entry widget for the user to input the password.
     - It is placed in the grid at row 3, column 1.
     - The `sticky="w"` option means it will stick to the west (left) side of its cell.

4. **Buttons**:
   - `generate_button` is a button labeled "Generate Password" with the command `generatePass`.
     - It is placed in the grid at row 3, column 1, sticking to the east (right) side of its cell.
   - `add_button` is a button labeled "Add" with the command `savePass`.
     - It is placed in the grid at row 4, column 1.
   - `search_button` is a button labeled "Search" with the command `searchPass`.
     - It is placed in the grid at row 1, column 1, sticking to the east (right) side of its cell.

5. **Main Loop**:
   - `window.mainloop()` starts the Tkinter event loop, which listens for events (such as button clicks, window resizing, etc.) and responds to them.

In summary, this code creates a simple password manager GUI using Tkinter. It includes fields for the website, email/username, and password. Users can generate passwords, add new password entries, and search for existing passwords. The logo is displayed on the canvas at the top of the window.




